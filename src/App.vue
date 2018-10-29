<template>
  <div id="app">
    <div class="left-menu">
      <el-tree :data="data" :props="defaultProps" @node-click="handleNodeClick" default-expand-all></el-tree>
      <div class="btn-wp">
        <el-button type="primary" plain class="anchors-btn" size="small" @click="addAllAnchorsClick">显示全部锚点</el-button>
        <el-button type="danger" plain size="small" class="yc-btn" @click="clearAnchorsClick">隐藏锚点</el-button>
      </div>
    </div>
    <div class="right-model">
      <iframe :src=url id="iframeView"></iframe>
    </div>
    <div class="parameter-view" v-show="parameterShow" style="max-width:400px;">
      <h1>参数列表</h1>
      <div class="table-wp">
        <!-- <table border="1" cellspacing="0">
  						<thead>
  							<tr>
  								<th>字段名</th>
  								<th>值</th>
  							</tr>
  						</thead>
  						<tbody>
  							<tr>
  								<td>编号</td>
  								<td>A1F01</td>
  							</tr>
  							<tr>
  								<td>名称</td>
  								<td>视频引导一体摄像机</td>
  							</tr>
  							<tr>
  								<td>运行状态</td>
  								<td>正常</td>
  							</tr>
  							<tr>
  								<td>监控画面</td>
  								<td @click="showVedioClick" style="cursor: pointer;" id="showVedioBtn">查看</td>
  							</tr>
  						</tbody>
  					</table> -->
        <el-tabs v-model="activeName">
          <el-tab-pane label="监控" name="first">
            <video src="./VID_20180829_091706.mp4" style="width:100%;height:100%;" autoplay muted loop></video>
          </el-tab-pane>
          <el-tab-pane label="参数" name="second">
            <table border="1" cellspacing="0">
              <thead>
                <tr>
                  <th>字段名</th>
                  <th>值</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td>名称</td>
                  <td>A栋1F配电室监控</td>
                </tr>
                <tr>
                  <td>IP地址</td>
                  <td>192.168.1.1</td>
                </tr>
                <tr>
                  <td>生产厂家</td>
                  <td>大华</td>
                </tr>
                <tr>
                  <td>规格型号</td>
                  <td @click="showVedioClick">DH-DSS-H500</td>
                </tr>
                <tr>
                  <td>其他</td>
                  <td @click="showVedioClick">1080P综合管理</td>
                </tr>
              </tbody>
            </table>
          </el-tab-pane>
        </el-tabs>
      </div>
    </div>
    <div class="sb-view" v-show="sbShow">
      <h1>参数列表</h1>
      <div class="table-wp">
        <table border="1" cellspacing="0">
          <thead>
            <tr>
              <th>字段名</th>
              <th>值</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>电压</td>
              <td>380.00V</td>
            </tr>
            <tr>
              <td>极数</td>
              <td>3</td>
            </tr>
            <tr>
              <td>负荷分类</td>
              <td>制冷</td>
            </tr>
            <tr>
              <td>风量</td>
              <td>1020.0000m³/h</td>
            </tr>
            <tr>
              <td>名义载荷</td>
              <td>94.00V</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
    <div class="equipment-view" v-show="equipmentShow">
      <h1>参数列表</h1>
      <div class="table-wp">
        <table border="1" cellspacing="0">
          <thead>
            <tr>
              <th>设备名称</th>
              <th>AHU-11F-01</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>设备品牌</td>
              <td>Honeywe</td>
            </tr>
            <tr>
              <td>规格型号</td>
              <td>GMV-H160WL/A</td>
            </tr>
            <tr>
              <td>运行状态</td>
              <td>启动</td>
            </tr>
            <tr>
              <td>风机频率</td>
              <td>50Hz</td>
            </tr>
            <tr>
              <td>送风温度</td>
              <td>30°C</td>
            </tr>
            <tr>
              <td>回风湿度</td>
              <td>97%RH</td>
            </tr>
            <tr>
              <td>室内PM2.5</td>
              <td>33</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
    <div class="echarts-view" v-if="chartsShow">
      <div id="gauge"></div>
      <div id="bar"></div>
      <div id="line"></div>
    </div>
    <!-- <div class="vedio-player" v-show="vedioShow">
  				
  			</div> -->
  </div>
</template>

<script>
  export default {
    name: "App",
    data() {
      return {
        activeName: "first",
        arr: [{
            id: "83401c7c-2766-43ba-81c1-2500f235ea75^1256137_1489556",
            type: "af"
          },
          {
            id: "83401c7c-2766-43ba-81c1-2500f235ea75^1256137_1489627",
            type: "af"
          },
          {
            id: "83401c7c-2766-43ba-81c1-2500f235ea75^1256137_1489667",
            type: "af"
          },
          {
            id: "83401c7c-2766-43ba-81c1-2500f235ea75^1256137_1489734",
            type: "af"
          },
          {
            id: "83401c7c-2766-43ba-81c1-2500f235ea75^1256129_1208913",
            type: "nh"
          },
          {
            id: "83401c7c-2766-43ba-81c1-2500f235ea75^1256137_1357560",
            type: "nh"
          },
          {
            id: "83401c7c-2766-43ba-81c1-2500f235ea75^1256140_929124",
            type: "sb"
          },
          {
            id: "83401c7c-2766-43ba-81c1-2500f235ea75^1256129_1086843",
            type: "sb"
          },
          {
            id: "83401c7c-2766-43ba-81c1-2500f235ea75^1256129_1121538",
            type: "sb"
          },
          {
            id: "83401c7c-2766-43ba-81c1-2500f235ea75^1256129_1125076",
            type: "sb"
          }
        ],
        data: [{
            label: "安防监控",
            children: [{
                label: "A栋",
                children: [{
                    label: "视频引导一体摄像机0",
                    data: "83401c7c-2766-43ba-81c1-2500f235ea75^1256137_1489556",
                    type: "af"
                  },
                  {
                    label: "视频引导一体摄像机1",
                    data: "83401c7c-2766-43ba-81c1-2500f235ea75^1256137_1489627",
                    type: "af"
                  },
                  {
                    label: "视频引导一体摄像机2",
                    data: "83401c7c-2766-43ba-81c1-2500f235ea75^1256137_1489667",
                    type: "af"
                  },
                  {
                    label: "视频引导一体摄像机3",
                    data: "83401c7c-2766-43ba-81c1-2500f235ea75^1256137_1489734",
                    type: "af"
                  }
                ]
              },
              {
                label: "B栋"
              },
              {
                label: "C栋"
              }
            ]
          },
          {
            label: "设备管理",
            children: [{
                label: "A栋",
                children: [{
                    label: "AHU-11F-01",
                    data: "83401c7c-2766-43ba-81c1-2500f235ea75^1256129_1208913",
                    type: "nh"
                  },
                  {
                    label: "AHU-11F-02",
                    data: "83401c7c-2766-43ba-81c1-2500f235ea75^1256137_1357560",
                    type: "nh"
                  },
                  {
                    label: "风机盘管",
                    data: "83401c7c-2766-43ba-81c1-2500f235ea75^1256140_929124",
                    type: "sb"
                  },
                  {
                    label: "热回收新风机",
                    data: "83401c7c-2766-43ba-81c1-2500f235ea75^1256129_1086843",
                    type: "sb"
                  },
                  {
                    label: "减压阀",
                    data: "83401c7c-2766-43ba-81c1-2500f235ea75^1256129_1121538",
                    type: "sb"
                  },
                  {
                    label: "消火栓",
                    data: "83401c7c-2766-43ba-81c1-2500f235ea75^1256129_1125076",
                    type: "sb"
                  }
                ]
              },
              {
                label: "	B栋"
              },
              {
                label: "C栋"
              }
            ]
          },
          {
            label: "能耗管理",
            type: "echart"
          }
        ],
        defaultProps: {
          children: "children",
          label: "label"
        },
        
        url: "/BIMComposer/index.html?projectId=9d24fa8e-25e9-4812-12d4-ea5354042eb3&model=731419a7-13ea-43f0-b115-96157e2f83dd",
        parameterShow: false,
        equipmentShow: false,
        vedioShow: false,
        sbShow: false,
        selectElementID: "",
        chartsShow: false,
        selectType: ""
      };
    },
    methods: {
      handleNodeClick(data) {
        if (data.data) {
          if (data.type == "af") {
            if (data.data == this.selectElementID) {
              this.parameterShow = !this.parameterShow;
            } else {
              this.parameterShow = true;
            }
            this.sbShow = false;
            this.equipmentShow = false;
            this.chartsShow = false;
            if (!this.parameterShow) {
              this.vedioShow = false;
            }
          } else if (data.type == "nh") {
            if (data.data == this.selectElementID) {
              this.equipmentShow = !this.equipmentShow;
            } else {
              this.equipmentShow = true;
            }
            this.sbShow = false;
            this.parameterShow = false;
            this.chartsShow = false;
          } else if (data.type == "sb") {
            if (data.data == this.selectElementID) {
              this.sbShow = !this.sbShow;
            } else {
              this.sbShow = true;
            }
            this.parameterShow = false;
            this.equipmentShow = false;
            this.chartsShow = false;
          }
          let iframeView = document.getElementById("iframeView");
          if (iframeView.contentWindow.BIMe) {
            // console.log(iframeView.contentWindow.BIMe.control.BIMeUtility.getElementPosition(data.data))
            iframeView.contentWindow.BIMe.control.BIMeZoom.zoomElementByElementId(
              data.data
            );
          }
          this.selectElementID = data.data;
          this.selectType = data.type;
        }
        if (data.type == "echart") {
          this.chartsShow = !this.chartsShow;
          if (this.chartsShow) {
            this.parameterShow = false;
            this.equipmentShow = false;
            this.sbShow = false;
            this.$nextTick(function() {
              var conversion = function(value) {
                if (value >= 10000 && value < 10000000) {
                  value = value / 10000 + "万";
                } else if (value >= 10000000) {
                  value = value / 10000000 + "千万";
                }
                return value;
              }
              var getDateStr = function(addDayCount) {
                var dateArray = new Array();
                for (var i = addDayCount; i > 0; i--) {
                  var dd = new Date();
                  dd.setDate(dd.getDate() - i);
                  var y = dd.getFullYear();
                  var m = dd.getMonth() + 1;
                  var d = dd.getDate();
                  dateArray.push(m + "-" + d); //y +"-"+ m +"-"+ d
                }
                return dateArray;
              }
              var myChart = this.$echarts.init(document.getElementById('line'));
              var option = {
                title: {
                  text: '七日耗电量',
                  left: 'center'
                },
                xAxis: {
                  type: 'category',
                  data: getDateStr(7)
                },
                yAxis: {
                  name: '单位：kw/h',
                  type: 'value',
                  axisLabel: {
                    formatter: function(value, index) {
                      return conversion(value);
                    }
                  }
                  /*axisLabel: {
                  	formatter: '{value} kW/h'
                  }*/
                },
                series: [{
                  name: '七日耗电量',
                  data: [9220, 7942, 10054, 7755, 6557, 6508, 8447],
                  type: 'line',
                  itemStyle: {
                    normal: {
                      color: 'rgb(236, 192, 59)',
                      lineStyle: {
                        color: "rgb(236, 192, 59)",
                        width: 3
                      },
                    }
                  }
                }]
              };
              myChart.setOption(option);
              var myChart1 = this.$echarts.init(document.getElementById('bar'));
              var option1 = {
                title: {
                  text: '当日各专业耗电量',
                  left: 'center'
                },
                tooltip: {
                  trigger: 'axis',
                  axisPointer: {
                    type: 'shadow'
                  }
                },
                xAxis: {
                  type: 'value',
                  boundaryGap: [0, 0.01],
                  axisLabel: {
                    formatter: function(value, index) {
                      return conversion(value);
                    }
                  }
                  /*axisLabel: {
                  	formatter: '{value} kW/h'
                  },*/
                },
                yAxis: {
                  name: '单位：kw/h',
                  nameLocation: 'start',
                  type: 'category',
                  inverse: true,
                  data: ['其他', '空调', '排水', '照明']
                },
                series: [{
                    type: 'bar',
                    barWidth: 30,
                    data: [5601, 6441, 8451, 7601],
                    itemStyle: {
                      normal: {
                        color: function(params) {
                          var colorList = ['rgb(181, 73, 66)', 'rgb(97, 195, 101)', 'rgb(42,170,227)', 'rgb(239, 227, 122)'];
                          return colorList[params.dataIndex];
                        }
                      },
                      emphasis: {
                        shadowBlur: 10,
                        shadowOffsetX: 0,
                        shadowColor: 'rgba(0, 0, 0, 0.5)'
                      }
                    }
                  },
                ]
              };
              myChart1.setOption(option1);
              var myChart2 = this.$echarts.init(document.getElementById('gauge'));
              var option2 = {
                title: {
                  text: '当日用电量',
                  left: 'center'
                },
                tooltip: {
                  formatter: "{a}：{c} kw/h"
                },
                series: [{
                  name: '用电量',
                  type: 'gauge',
                  z: 3,
                  min: 0,
                  max: 50000,
                  axisLine: { // 坐标轴线
                    lineStyle: { // 属性lineStyle控制线条样式
                      width: 10,
                      color: [
                        [0.2, '#91c7ae'],
                        [0.8, 'rgb(206, 192, 75)'],
                        [1, '#c23531']
                      ]
                    }
                  },
                  axisTick: { // 坐标轴小标记
                    length: 15, // 属性length控制线长
                    lineStyle: { // 属性lineStyle控制线条样式
                      color: 'auto'
                    }
                  },
                  splitLine: { // 分隔线
                    length: 20, // 属性length控制线长
                    lineStyle: { // 属性lineStyle（详见lineStyle）控制线条样式
                      color: 'auto'
                    }
                  },
                  axisLabel: {
                    backgroundColor: 'auto',
                    borderRadius: 2,
                    color: '#eee',
                    padding: 3,
                    textShadowBlur: 2,
                    textShadowOffsetX: 1,
                    textShadowOffsetY: 1,
                    textShadowColor: '#222',
                    formatter: function(value, index) {
                      return conversion(value);
                    }
                  },
                  detail: {
                    formatter: function(value) {
                      if (value >= 10000 && value < 10000000) {
                        value = value / 10000;
                        value = value.toFixed(1) + "万";
                      } else if (value >= 10000000) {
                        value = value / 10000000;
                        value = value.toFixed(1) + "千万";
                      }
                      return value;
                    },
                    fontWeight: 'bolder',
                    borderRadius: 3,
                    backgroundColor: '#444',
                    borderColor: '#aaa',
                    shadowBlur: 5,
                    shadowColor: '#333',
                    shadowOffsetX: 0,
                    shadowOffsetY: 3,
                    borderWidth: 2,
                    textBorderColor: '#000',
                    textBorderWidth: 2,
                    textShadowBlur: 2,
                    textShadowColor: '#fff',
                    textShadowOffsetX: 0,
                    textShadowOffsetY: 0,
                    fontFamily: 'Arial',
                    width: 60,
                    fontSize: 16,
                    color: '#eee',
                    rich: {}
                  },
                  data: [{
                    value: 28094,
                    name: 'kw/h'
                  }]
                }]
              };
              myChart2.setOption(option2, true);
            });
          }
        }
      },
      clearAnchorsClick() {
        let iframeView = document.getElementById("iframeView");
        iframeView.contentWindow.BIMe.control.BIMeUtility.clearAllAnchorpoint();
      },
      showVedioClick() {
        this.vedioShow = !this.vedioShow;
      },
      addAllAnchorsClick() {
        let iframeView = document.getElementById("iframeView");
        this.arr.forEach(element => {
          let a = iframeView.contentWindow.BIMe.control.BIMeUtility.getElementPosition(
            element.id
          );
          let b = iframeView.contentWindow.BIMe.control.BIMeUtility.addAnchorPointByPosition(
            a,
            "./assets/point.svg", {
              elementid: element.id,
              type: element.type
            }
          );
          let newBtn = iframeView.contentWindow.document.getElementById(b.id);
          newBtn.addEventListener(
            "click",
            function(e) {
              let iframeView = document.getElementById("iframeView");
              if (iframeView.contentWindow.BIMe) {
                iframeView.contentWindow.BIMe.control.BIMeZoom.zoomElementByElementId(
                  b.data.elementid
                );
                if (b.data.type == "af") {
                  vm.parameterShow = !vm.parameterShow;
                  vm.sbShow = false;
                  vm.equipmentShow = false;
                  vm.chartsShow = false;
                  if (!vm.parameterShow) {
                    vm.vedioShow = false;
                  }
                } else if (b.data.type == "nh") {
                  vm.equipmentShow = !vm.equipmentShow;
                  vm.sbShow = false;
                  vm.parameterShow = false;
                  vm.chartsShow = false;
                } else if (b.data.type == "sb") {
                  vm.sbShow = !vm.sbShow;
                  vm.parameterShow = false;
                  vm.equipmentShow = false;
                  vm.chartsShow = false;
                }
              }
            },
            false
          );
        });
      },
      addAnchorsClick() {
        if (this.selectElementID) {
          let iframeView = document.getElementById("iframeView");
          let a = iframeView.contentWindow.BIMe.control.BIMeUtility.getElementPosition(
            this.selectElementID
          );
          let b = iframeView.contentWindow.BIMe.control.BIMeUtility.addAnchorPointByPosition(
            a,
            "./assets/point.svg", {
              elementid: this.selectElementID,
              type: this.selectType
            }
          );
          let newBtn = iframeView.contentWindow.document.getElementById(b.id);
          newBtn.addEventListener(
            "click",
            function(e) {
              let iframeView = document.getElementById("iframeView");
              if (iframeView.contentWindow.BIMe) {
                iframeView.contentWindow.BIMe.control.BIMeZoom.zoomElementByElementId(
                  b.data.elementid
                );
                if (b.data.type == "af") {
                  vm.parameterShow = !vm.parameterShow;
                  vm.sbShow = false;
                  vm.equipmentShow = false;
                  vm.chartsShow = false;
                  if (!vm.parameterShow) {
                    vm.vedioShow = false;
                  }
                } else if (b.data.type == "nh") {
                  vm.equipmentShow = !vm.equipmentShow;
                  vm.sbShow = false;
                  vm.parameterShow = false;
                  vm.chartsShow = false;
                } else if (b.data.type == "sb") {
                  vm.sbShow = !vm.sbShow;
                  vm.parameterShow = false;
                  vm.equipmentShow = false;
                  vm.chartsShow = false;
                }
              }
            },
            false
          );
        } else {
          this.$message.error("请选择构件");
        }
      }
    },
    mounted() {
      window.vm = this;
    }
  };
</script>

<style>
  .echarts-view {
    width: calc(100% - 300px);
    position: absolute;
    bottom: 35px;
    left: 300px;
    height: 300px;
    background: rgba(132, 171, 185, 0.53);
    padding-top: 10px;
    border-top: 1px solid #ccc;
    display: flex;
    flex-direction: row;
    align-items: center;
  }
  .echarts-view>div {
    flex: 1;
    height: 100%;
  }
  section {
    color: #fff;
    width: 200px;
  }
  .el-tree>div>div:nth-child(1) {
    font-weight: bold;
  }
  .vedio-player {
    width: 300px;
    height: 200px;
    background: #000;
    color: #fff;
    position: fixed;
    top: 50px;
    right: 0;
  }
  .el-tree {
    max-height: 85%;
    overflow-y: auto;
  }
  #app {
    font-family: "Avenir", Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    display: flex;
    height: 100%;
    overflow: hidden;
  }
  iframe {
    border: none;
  }
  .left-menu {
    width: 300px;
    position: relative;
    border-right: 1px solid #ccc;
  }
  .left-menu .btn-wp {
    width: 100%;
    position: absolute;
    bottom: 50px;
    left: 50%;
    right: 50%;
    transform: translate(-50%, -50%);
  }
  .right-model {
    flex: 1;
  }
  .right-model iframe {
    width: 100%;
    height: 100%;
  }
  table {
    border: 1px solid #ccc;
  }
  table th,
  td {
    text-align: center;
    width: 150px;
    height: 30px;
  }
  .parameter-view {
    background: #f1f1f1;
    position: fixed;
    left: 300px;
    top: 50px;
    border: 1px solid #ccc;
  }
  .table-wp {
    padding: 20px;
  }
  .equipment-view,
  .sb-view {
    background: #f1f1f1;
    position: fixed;
    left: 300px;
    top: 50px;
    border: 1px solid #ccc;
  }
  h1 {
    line-height: 30px;
    width: 100%;
    background: rgb(226, 225, 225);
    color: rgb(80, 75, 75);
  }
</style>
