<template>
	<div id="app">
		<div class="left-menu">
			<el-tree :data="data" :props="defaultProps" @node-click="handleNodeClick" default-expand-all></el-tree>
			<div class="btn-wp">
				<el-button type="primary" plain class="anchors-btn" size="small" @click="addAnchorsClick">增加锚点</el-button>
				<el-button type="danger" plain size="small" class="yc-btn" @click="clearAnchorsClick">隐藏锚点</el-button>
			</div>
			
		</div>
		<div class="right-model">
			<iframe :src=url id="iframeView"></iframe>
		</div>
		<div class="parameter-view" v-show="parameterShow">
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
				</table>
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
							<th>字段名</th>
							<th>值</th>
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
		<div class="vedio-player" v-show="vedioShow">
			我是视频
		</div>
	</div>
</template>

<script>
	export default {
		name: 'App',
		data() {
			return {
				data: [
					{
						label:'安防监控',
						children:[
							{
								label:'A栋',
								children: [{
									label: '视频引导一体摄像机0',
									data:'83401c7c-2766-43ba-81c1-2500f235ea75^1256137_1489556',
									type:'af'
								},
								{
									label: '视频引导一体摄像机1',
									data:'83401c7c-2766-43ba-81c1-2500f235ea75^1256137_1489627',
									type:'af'
								},
								{
									label: '视频引导一体摄像机2',
									data:'83401c7c-2766-43ba-81c1-2500f235ea75^1256137_1489667',
									type:'af'
								},
								{
									label: '视频引导一体摄像机3',
									data:'83401c7c-2766-43ba-81c1-2500f235ea75^1256137_1489734',
									type:'af'
								}]
							},{
								label:'B栋'
							},{
								label:'C栋'
							}
						]
					},{
						label:'能耗管理',
						children:[
							{
								label:'A栋',
								children:[
									{
										label:'AHU-11F-01',
										data:'83401c7c-2766-43ba-81c1-2500f235ea75^1256129_1208913',
										type:'nh'
									},
									{
										label:'AHU-11F-02',
										data:'83401c7c-2766-43ba-81c1-2500f235ea75^1256137_1357560',
										type:'nh'
									}
								]
								
							},
							{
								label:'	B栋'
							},
							{
								label:'C栋'
							},
						]
					},
					{
						label:'设备管理',
						children:[
							{
								label:'A栋',
								children:[
									{
										label:'风机盘管',
										data:'83401c7c-2766-43ba-81c1-2500f235ea75^1256140_929124',
										type:'sb'
									},
									{
										label:'热回收新风机',
										data:'83401c7c-2766-43ba-81c1-2500f235ea75^1256129_1086843',
										type:'sb'
									},
									{
										label:'减压阀',
										data:'83401c7c-2766-43ba-81c1-2500f235ea75^1256129_1121538',
										type:'sb'
									},
									{
										label:'消火栓',
										data:'83401c7c-2766-43ba-81c1-2500f235ea75^1256129_1125076',
										type:'sb'
									}
								]
							},
							{
								label:'	B栋'
							},
							{
								label:'C栋'
							},
						]
					}
				],
				defaultProps: {
					children: 'children',
					label: 'label'
				},
				url:"/BIMComposer/index.html?projectId=32fcbf39-2282-4c3d-88fa-6f63da71f010&model=83401c7c-2766-43ba-81c1-2500f235ea75",
				parameterShow:false,
				equipmentShow:false,
				vedioShow:false,
				sbShow:false,
				selectElementID:''
			}
		},
		methods:{
			handleNodeClick(data) {
				if(data.data){
					if(data.type == 'af'){
						this.parameterShow = !this.parameterShow
						this.sbShow = false
						this.equipmentShow = false
						if(!this.parameterShow){
							this.vedioShow = false
						}
					}else if(data.type == 'nh'){
						this.equipmentShow = !this.equipmentShow
						this.sbShow = false
						this.parameterShow = false
					}else if(data.type == 'sb'){
						this.sbShow = !this.sbShow
						this.parameterShow = false
						this.equipmentShow = false
					}
					
					let iframeView = document.getElementById('iframeView')
					if(iframeView.contentWindow.BIMe){
						// console.log(iframeView.contentWindow.BIMe.control.BIMeUtility.getElementPosition(data.data))
						this.selectElementID = data.data
						iframeView.contentWindow.BIMe.control.BIMeZoom.zoomElementByElementId(data.data);
					}
				}
			},
			clearAnchorsClick(){
				
				let iframeView = document.getElementById('iframeView')
				iframeView.contentWindow.BIMe.control.BIMeUtility.clearAllAnchorpoint()
			},
			showVedioClick(){
				this.vedioShow = !this.vedioShow
				
			},
			addAnchorsClick(){
				if(this.selectElementID){
					let iframeView = document.getElementById('iframeView')
					let a = iframeView.contentWindow.BIMe.control.BIMeUtility.getElementPosition(this.selectElementID)
					let b = iframeView.contentWindow.BIMe.control.BIMeUtility.addAnchorPointByPosition(a,'./assets/point.svg')
					console.log(b)
					let newBtn = iframeView.contentWindow.document.getElementById(b.id)
					newBtn.addEventListener("click",function(e){
						//TODO
					},false)

					
				}else{
					this.$message.error('请选择构件');
				}
			}
		},
		mounted() {
			window.vm = this
		},
	}
</script>

<style>
.el-tree>div>div:nth-child(1){
	font-weight: bold
}
.vedio-player{
	width: 300px;
	height: 200px;
	background: #000;
	color: #fff;
	position: fixed;
	top: 50px;
	right: 0;
}
	.el-tree{
		max-height: 85%;
		overflow-y: auto;
	}
	#app {
		font-family: 'Avenir', Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
		color: #2c3e50;
		display: flex;
		height: 100%;
	}
	iframe{
		border: none
	}
	.left-menu {
		width: 300px;
		position: relative;
		border-right: 1px solid #ccc;
	}
	.left-menu .btn-wp{
		width: 100%;
		position: absolute;
		bottom: 50px;
		left: 50%;
		right: 50%;
		transform:translate(-50%,-50%);
	}
	.right-model {
		flex: 1;
	}
	.right-model iframe{
		width: 100%;
		height: 100%
	}
	table{
		border: 1px solid #ccc;
	}
	table th,td{
		text-align: center;
		width: 150px;
		height: 30px;
	}
	.parameter-view{
		background: #f1f1f1;
		position: fixed;
		left: 300px;
		top: 50px;
		border: 1px solid #ccc;
	}
	.table-wp{
		padding: 20px;
		
	}
	.equipment-view,.sb-view {
		background: #f1f1f1;
		position: fixed;
		left: 300px;
		top: 50px;
		border: 1px solid #ccc;
	}
	
	h1{
		line-height: 30px;
		width: 100%;
		background: rgb(226, 225, 225);
		color: rgb(80, 75, 75);
	}
</style>
