  <template>
    <div>
        <div class="drag-box">
            <div class="node" id="node1"  @mouseover="showPannel1 = true" @mouseleave="showPannel1 = false">
                <img src="../../static/img/new/Reader.png" class="top-arrow" title="读取器">
                <div v-show="showPannel1" class="pannerlCss">
                    <Container :behaviour="'copy'" :group-name="'1'" :get-child-payload="getChildPayloadFirst">
                        <Draggable class="Prow" v-for="temp in toolBar.first" :key="temp.id">
                            <div class="Pleft">
                                <img :src=temp.img class="top-arrow">
                            </div> 
                            <div class="Pright">
                                <p>{{temp.text}}</p>
                            </div>
                        </Draggable>
                    </Container>
                </div>
            </div>
            <div class="node" id="node2" @mouseover="showPannel2 = true" @mouseleave="showPannel2 = false">
                <img src="../../static/img/new/processor.png" class="top-arrow" title="处理器">
                <div v-show="showPannel2" class="pannerlCss">
                    <div class="LRow" >
                        <Container class="Lf" :behaviour="'copy'" :group-name="'1'" :get-child-payload="getChildPayloadSecondL">
                            <Draggable class="Prow" v-for="temp in toolBar.second.left" :key="temp.id">
                                <div class="Pleft">
                                    <img :src=temp.img class="top-arrow">
                                </div> 
                                <div class="Pright">
                                    <p>{{temp.text}}</p>
                                </div>
                            </Draggable>
                        </Container>
                        <Container class="Lr" :behaviour="'copy'" :group-name="'1'" :get-child-payload="getChildPayloadSecondR">
                            <Draggable class="Prow" v-for="temp in toolBar.second.right" :key="temp.id">
                                <div class="Pleft">
                                    <img :src=temp.img class="top-arrow">
                                </div> 
                                <div class="Pright">
                                    <p>{{temp.text}}</p>
                                </div>
                            </Draggable>
                        </Container>
                    </div>
                </div>
            </div>
            <div class="node" id="node3" @mouseover="showPannel3 = true" @mouseleave="showPannel3 = false">
                <img src="../../static/img/new/Writer2.png" class="top-arrow" title="写入器">
                <div v-show="showPannel3" class="pannerlCss">

                    <Container :behaviour="'copy'" :group-name="'1'" :get-child-payload="getChildPayloadThird">
                        <Draggable class="Prow" v-for="temp in toolBar.third" :key="temp.id">
                            <div class="Pleft">
                                <img :src=temp.img class="top-arrow">
                            </div> 
                            <div class="Pright">
                                <p>{{temp.text}}</p>
                            </div>
                        </Draggable>
                    </Container>
                </div>
            </div>
            <div class="node" id="node4"  @mouseover="showPannel4 = true" @mouseleave="showPannel4 = false">
                <img src="../../static/img/new/service.png" class="top-arrow" title="服务">
                <div v-show="showPannel4" class="pannerlCss"> 
                   
                    <Container :behaviour="'copy'" :group-name="'1'" :get-child-payload="getChildPayloadFourth">
                        <Draggable class="Prow" v-for="temp in toolBar.fourth" :key="temp.id">
                            <div class="Pleft">
                                <img :src=temp.img class="top-arrow">
                            </div> 
                            <div class="Pright">
                                <p>{{temp.text}}</p>
                            </div>
                        </Draggable>
                    </Container>
                </div>
            </div>
            <div class="node" id="node5" @mouseover="showPannel5 = true" @mouseleave="showPannel5 = false">
                <img src="../../static/img/new/control.png" class="top-arrow" title="控制">
                <div v-show="showPannel5" class="pannerlCss"> 
                    <Container :behaviour="'copy'" :group-name="'1'" :get-child-payload="getChildPayloadFifth">
                        <Draggable class="Prow" v-for="temp in toolBar.fifth" :key="temp.id">
                            <div class="Pleft">
                                <img :src=temp.img class="top-arrow">
                            </div> 
                            <div class="Pright">
                                <p>{{temp.text}}</p>
                            </div>
                        </Draggable>
                    </Container>
                </div>
            </div>
        </div>
        <div id="diagramContainer" class="map">
            <Container :group-name="'1'" :get-child-payload="getChildPayload2" @drop="onDrop($event)" class="testArea">
                <div v-for="item in dropItems" :key="item.id" class="point" :id=item.id>
                    <div>
                        <img :src=item.img class="top-arrow">
                        <p>{{item.text}}</p>
                    </div>
                </div>
            </Container>

            <dl class="process-operation">
                <dd>
                    <span class="process-cancle first" @click="deleteSelected()">撤销</span>
                </dd>
                <dd><span class="process-checkIn" >检入</span></dd>
                <dd><span class="process-test" >仿真测试</span></dd>
                <dd><span class="process-save" @click="getAllConnection()" >保存设计</span></dd>
            </dl>
            <div class="releaseArea">
                <a class="process-release"></a>  
            </div>

            <div class="save" v-show="showRightPannel">
                <div class="operaDiv">
                    <p>编码</p>
                    <div>
                        <input class="input" placeholder="请输入编码" />
                    </div>
                </div>
                <div class="operaDiv">
                    <p>名称</p>
                    <div>
                        <input class="input" placeholder="请输入名称" />
                    </div>
                </div>
                <div class="operaDiv">
                    <p>描述</p>
                    <div>
                        <textarea class="textarea"> </textarea>
                    </div>
                </div>
                <div class="operaDiv">
                    <button class="btn btn-green"> 获取连接 </button>
                </div>
            </div>
        </div> 
    </div>
</template> 

<script>
    import $ from 'jquery'
    
    import { Container, Draggable } from "vue-smooth-dnd";
    import { applyDrag } from "../utils/tool";

    require('../assets/css/demo.css');
    require('../assets/css/jsplumb.css');

    const color = '#acd';
    var  position = {};

    document.onmouseup = mouseup ;

    function mouseup(ev){
        ev = ev || window.event;
        position = mousePosition(ev);
    }


    function mousePosition(ev){
        if(ev.pageX || ev.pageY){
            return {x:ev.pageX, y:ev.pageY};
        }
        return {
            x:ev.clientX + document.body.scrollLeft - document.body.clientLeft,
            y:ev.clientY + document.body.scrollTop  - document.body.clientTop
        };
    }

    export default {
        name: 'plumbComp',
        beforeCreate() {
            var _this = this;

            $.getJSON('../static/toolbar.json', function(json) {
                var res = json.toolbar;
                _this.toolBar = res;
            });
        },
        components: { Container, Draggable },
        data: function () {
            return {
                showPannel1: false,
                showPannel2: false,
                showPannel3: false,
                showPannel4: false,
                showPannel5: false,
                showRightPannel: false,
                instance: {},
                allInfos: [],
                //左侧工具栏数据结构
                toolBar: {
                    first: [],
                    second: {
                        left: [],
                        right: []
                    },
                    third: [],
                    fourth: [],
                    fifth: []
                },
                dropItems: [],
                //保存节点信息
                InitDatas: { 
                    point: [
                        {
                            id: "1",
                            text: "二进制文件阅读器",
                            img: "../../static/img/new/BinaryFileReader.png"
                        },
                        {
                            id: "2",
                            text: "excel读取器",
                            img: "../../static/img/new/excelReader.png"
                        }
                    ],
                    location: [
                        ['1', 360, 140],
                        ['2', 720, 340]
                    ],
                    line: [
                        ['1', '2']
                    ]
                }
            }
        },
        mounted(){
            jsPlumb.ready(() => {
                this.createFlow();
            });
        },
        methods: {
            onDrop: function(dropResult) {
                var _this = this;

                this.dropItems = applyDrag(this.dropItems, dropResult);

                this.InitDatas.point.push(_.last(this.dropItems));
                

                var nodes =  this.dropItems,
                    Lnode = _.last(nodes);

                //撤销节点用的
                this.allInfos.push(Lnode.id);

                // 获取鼠标位置赋值给要生成节点
                setTimeout(() => {
                    console.log('位置信息:', );
                    var tempArr = [];
                    tempArr[0] = Lnode.id;
                    tempArr[1] = position.x - 100;
                    tempArr[2] = position.y - 150;
                    this.InitDatas.location.push(tempArr);

                    $('#'+ Lnode.id).css('top', position.y - 100);
                    $('#'+ Lnode.id).css('left', position.x - 150);
                    var jspb = this.instance,
                        endpoint = {
                            isTarget:true,
                            isSource:true
                        },
                        pointId = Lnode.id;

                    jspb.draggable($('.point'));

                    jspb.addEndpoints(pointId, [{ anchor:"Left", enabled: true},
                        { anchor:"Right", enabled: true}], endpoint );

                    $('#'+ Lnode.id).click(function (e) {
                        $('.point').removeClass('selected');
                        $(e.target).parent().addClass('selected');
                        
                        _this.showRightPannel = !_this.showRightPannel;
                    });
                }, 20);

            },
            getChildPayloadFirst: function(index) {
                return this.toolBar.first[index];
            },
            getChildPayloadSecondL: function(index) {
                return this.toolBar.second.left[index];
            },
            getChildPayloadSecondR: function(index) {
                return this.toolBar.second.right[index];
            },
            getChildPayloadThird: function(index) {
                return this.toolBar.third[index];
            },
            getChildPayloadFourth: function(index) {
                return this.toolBar.fourth[index];
            },
            getChildPayloadFifth: function(index) {
                return this.toolBar.fifth[index];
            },
            getChildPayload2: function(index) {
                return this.dropItems[index];
            },
            createFlow() {
                var _this = this;

                this.instance = jsPlumb.getInstance({
                    Connector: 'Flowchart',
                    Endpoint: 'Dot',
                    EndpointStyle: { radius: 9, fill: color, stroke: 'red' },
                    EndpointHoverStyle: { fill: '#ec9f2e', stroke: '#acd' },
                    DragOptions: { cursor: 'pointer', zIndex: 5000 },
                    PaintStyle: { lineWidth: 5, stroke: '#445566' },
                    HoverPaintStyle: { stroke: '#ec9f2e', lineWidth: 4 },
                    ConnectionOverlays: [
                        ['Arrow', {
                            location: 0.9,
                            id: 'arrow',
                            length: 12,
                            foldback: 1,
                            paintStyle: {
                                lineWidth: 5,
                                stroke: '#2e6f9a',
                                fill: '#2e6f9a',
                            },
                            width: 12
                        }],
                        ['Label', { label: '链接说明', id: 'label' }],
                    ],
                    Container: 'points'
                });

                //初始化保存节点信息
                this.instance.batch(() => {
                    // declare some common values:
                    const arrowCommon = { foldback: 0.7, width: 12 };
                    // use three-arg spec to create two different arrows with the common values:
                    // const overlays = [
                    // ['Arrow', { location: 0.7 }, arrowCommon],
                    // ['Label', { label: '链接说明', id: 'label' }],
                    // ];
                    const InitDatas = this.InitDatas;
                    // init point
                    for (const point of InitDatas.point) {
                        $('#diagramContainer').append(
                            `<div id="${point.id}" class="point">
                                <img src="${point.img}" class="top-arrow">
                                <p>${point.text}</p>
                            </div>`

                        );
                        _this.instance.addEndpoint(point.id, {
                            uuid: `${point.id}-top`,
                            anchor: 'Left',
                            maxConnections: -1,
                            connectorStyle: { stroke: 'gray' },
                        }, {
                            isSource: true,
                            isTarget: true,
                            dragAllowedWhenFull: true,
                        });
                        _this.instance.addEndpoint(point.id, {
                            uuid: `${point.id}-bottom`,
                            anchor: 'Right',
                            maxConnections: -1,
                            connectorStyle: { stroke: 'green' },
                        }, {
                            isSource: true,
                            isTarget: true,
                            dragAllowedWhenFull: true,
                        });

                        
                        $('#'+ point.id).click(function (e) {
                            $('.point').removeClass('selected');

                            $(e.target).parent().addClass('selected');
                            
                            _this.showRightPannel = !_this.showRightPannel;
                        });
                    }

                    // init transition
                    for (const i of InitDatas.line) {
                        const uuid = [`${i[0]}-bottom`, `${i[1]}-top`];
                        _this.instance.connect({
                            uuids: uuid
                            // overlays,
                        });
                    }

                    // init location
                    for (const i of InitDatas.location) {
                        $(`#${i[0]}`).css('left', i[1]);
                        $(`#${i[0]}`).css('top', i[2]);
                    }

                    this.instance.draggable($('.point'));
                    
                });

                this.instance.bind("connection",function(info){
                    console.log('连接信息：', info);
                    //撤销连接用的
                    _this.allInfos.push(info.connection);

                    var tempArr1 = [];
                    tempArr1[0] = info.sourceId;
                    tempArr1[1] = info.targetId;
                    _this.InitDatas.line.push(tempArr1);
                });
            },
            getAllConnection() {
                var list = this.instance.getAllConnections();//获取所有的链接
                console.log('所有连接', list);
                //需要保存的节点信息
                console.log(this.InitDatas);
            },
            deleteSelected() {
                console.log(this.allInfos.length);
                if (this.allInfos.length === 0) {
                    this.$swal({
                        title: "WOOOOW!",
                        text: "没什么撤销的了",
                        icon: "warning",
                        button: "确定",
                    })
                    return;
                }
                
                var lInfo = _.last(this.allInfos);
                
                //是对象的话，则是撤销(删除)连接信息
                //否则删除的是节点信息
                if (_.isObject(lInfo)) {
                    this.instance.deleteConnection(lInfo);
                    //删除保存的连接线
                    this.InitDatas.line.pop();
                } else {
                    this.instance.remove(lInfo);

                    //删除节点和位置信息
                    this.InitDatas.point.pop();
                    this.InitDatas.location.pop();
                }

                this.allInfos.pop();
            }
        }
    }
</script> 
<style scope>

.testArea {
    height: 800px;
    width: 100%;
}

#diagramContainer {
    overflow-y: auto;
}

.map {
    height: 100%;
    width: 110%;
    background: #f7f7f7 url('../../static/img/process-bg.png') 0 0;
    overflow-x: visible;
    position: fixed;
    margin-left: -20px;
}
.item {
    height: 150px;
    width: 80px;
    border: 3px solid #ccc4c4;
    border-radius: 10px;
    position:absolute;
}

.save {
    margin-top: -40%;
    overflow-y: auto;
    right: 0px;
    width: 240px;
    height: 86%;
    background: #fff;
    position: fixed;
    font-size: 14px;
    z-index: 25;
}

.drag-box {
    width: 60px;
    background: white;
    top: 60px;
    z-index: 25;
}
.node:first-child {
    margin-top: 5px;
}
.node {
    margin-top: 20px;
    margin-left: 12px
}
.input:hover, .textarea:hover {
    background-color: #fff;
}

.input, .textarea {
    -moz-appearance: none;
    -webkit-appearance: none;
    -webkit-box-align: center;
    -ms-flex-align: center;
    align-items: center;
    border-color: #b5b5b5;
    border: 1px solid #34e661;
    border-radius: 3px;
    color: #363636;
    display: -webkit-inline-box;
    display: -ms-inline-flexbox;
    display: inline-flex;
    font-size: 12px;
    height: 32px;
    -webkit-box-pack: start;
    -ms-flex-pack: start;
    justify-content: flex-start;
    line-height: 24px;
    padding-left: 8px;
    padding-right: 8px;
    position: relative;
    vertical-align: top;
    box-shadow: inset 0 1px 2px hsla(0,0%,4%,.1);
    max-width: 100%;
    width: 180px;
}

.operaDiv:first-child {
    margin-top: 20%;
}
.operaDiv {
    margin-left: 25px;
    margin-top: 10%;
}

.process-operation {
    right: 70px;
}

.process-operation dd span.process-cancle {
    background: url('../../static/img/new/Shape-3.png') no-repeat 10px center;
}
.process-operation dd span.process-checkIn {
    background: url('../../static/img/new/Shape-2.png') no-repeat 10px center;
}
.process-operation dd span.process-test {
    background: url('../../static/img/new/test1.png') no-repeat 10px center;
}

.releaseArea {
    width: 36px;
    background: white;
    right: 20px;
    position: fixed;
    top: 115px;
}
.process-release {
    display:block;
    height: 36px;
    width: 19px;
    margin-left: 7px;
    background-image:url('../../static/img/new/release2.png');
    background-repeat: no-repeat;
    background-position:50% 50%;
}

.pannerlCss {
    margin-left: 52px;
    z-index: 80;
    position: fixed;
    width: 160px;
    background: white;
    margin-top: -45px;
}
.Pleft {
    margin-top: 5px;
    width: 10%;
    float: left;
}

.Pright {
    margin-left: 5%;
    width: 85%;
    float: left;
}
.Prow {
    width: 100%;
    height: 45px;
    line-height: 33px;
}
.Prow:hover {
    cursor: pointer;
    background: #f5f6fa;
}

.LRow {
    width: 320px;
    height: auto;
    min-height: 680px;
    line-height: 50px;
    background: white;
}

.Lf {
    width: 50%;
    float: left;
}
.Lr {
    width: 46%;
    margin-left: 10px;
    float: left;
}

.Lf {
    border-right: 1px solid gray;
}

.point{
    width: 180px;
    height: 85px;
    border: 2px solid #2e6f9a;
    border-radius: 8px;
    position: absolute;
    /* z-index: 25; */
}

.point img{
    display: block;
    margin: 0 auto;
}

.point.selected {
    border: 2px solid orange;
}

.Pright>p {
    margin-left: 10px;
}

</style>