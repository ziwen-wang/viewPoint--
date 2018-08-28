<template>
	<div id="app">
		<div class="left-menu">
			<el-tree :data="data" :props="defaultProps" @node-click="handleNodeClick" default-expand-all></el-tree>
			<el-button type="primary" plain class="anchors-btn" size="small" @click="addAnchorsClick">增加锚点</el-button>
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
									data:'83401c7c-2766-43ba-81c1-2500f235ea75^1256137_1489556'
								},
								{
									label: '视频引导一体摄像机1',
									data:'83401c7c-2766-43ba-81c1-2500f235ea75^1256137_1489627'
								},
								{
									label: '视频引导一体摄像机2',
									data:'83401c7c-2766-43ba-81c1-2500f235ea75^1256137_1489667'
								},
								{
									label: '视频引导一体摄像机3',
									data:'83401c7c-2766-43ba-81c1-2500f235ea75^1256137_1489734'
								}]
							},{
								label:'B栋'
							},{
								label:'C栋'
							}
						]
					},{
						label:'耗能管理',
						children:[
							{
								label:'A栋'
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
								label:'A栋'
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
				vedioShow:false,
				selectElementID:''
			}
		},
		methods:{
			handleNodeClick(data) {
				if(data.data){
					this.parameterShow = !this.parameterShow
					let iframeView = document.getElementById('iframeView')
					if(iframeView.contentWindow.BIMe){
						// console.log(iframeView.contentWindow.BIMe.control.BIMeUtility.getElementPosition(data.data))
						this.selectElementID = data.data
						iframeView.contentWindow.BIMe.control.BIMeZoom.zoomElementByElementId(data.data);
					}
				}
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
					
				}else{
					this.$message.error('请选择构件');
				}
			}
		}
	}
</script>

<style>
.vedio-player{
	width: 300px;
	height: 200px;
	background: #000;
	color: #fff;
	position: fixed;
	top: 50px;
	right: 0;
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
	.left-menu .anchors-btn{
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
	.parameter-view h1{
		line-height: 30px;
		width: 100%;
		background: rgb(226, 225, 225);
		color: rgb(80, 75, 75);
	}
</style>
