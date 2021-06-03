<template>
	<view class="id">
		<view class="tj">
			<qiun-data-charts type="line" :chartData="chartData" />
		</view>
		<view class="btn">
			<u-button type="primary" @click='show2 = true'>{{dcsj}}</u-button>
			<u-button type="primary" @click='show1 = true'>{{qksj}}</u-button>
		</view>

		<u-modal v-model="show1" :content="content" :mask-close-able="true" @confirm="confirm"></u-modal>
		<u-calendar v-model="show2" mode="range" @change="change"></u-calendar>
		<view class="table">
			<scroll-view scroll-x="true" class="scroll">
				<view class="table1">
					<view class="table-item">{{xh}}</view>
					<view class="table-item">{{xm}}</view>
					<view class="table-item">{{sj}}</view>
					<view class="table-item">{{wd}}</view>
					<view class="table-item">{{wc}}</view>
				</view>
				<view class="table-data" v-for="(item,index) in dataList">
					<view class="table-data-item">{{index+1}}</view>
					<view class="table-data-item">{{item.name}}</view>
					<view class="table-data-item">{{item.time}}</view>
					<view class="table-data-item">{{item.temp}}</view>
					<view class="table-data-item">{{item.wc}}</view>
				</view>

			</scroll-view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				show1: false,
				show2: false,
				dcsj: '导出数据',
				qksj: '清空数据',
				content: '确认清空数据吗?',
				xh: '序号',
				xm: '姓名',
				sj: '时间',
				wd: '温度',
				wc: '温差',
				n: '左腋下',
				chartData: {
					categories: ["300", "400", "500", "600", "700", "800"],
					series: [{
						name: '左腋下',
						data: [35, 36, 31, 33, 13, 34]
					}, {
						name: "左体表",
						data: [18, 25, 21, 27, 6, 28]
					}, {
						name: "右腋下",
						data: [14, 27, 21, 24, 6, 28]
					}, {
						name: "右体表",
						data: [16, 22, 26, 28, 6, 28]
					}]
				},
				dataList: [{
						'name': '张三',
						'time': '2021-5-22',
						'temp': '36.7-333-333-333',
						'wc': '1.2'
					},
					{
						'name': '张三',
						'time': '2021-5-22',
						'temp': '36.7-333-333-333',
						'wc': '1.2'
					},
					{
						'name': '张三',
						'time': '2021-5-22',
						'temp': '36.7-333-333-333',
						'wc': '1.2'
					},
					{
						'name': '张三',
						'time': '2021-5-22',
						'temp': '36.7-333-333-333',
						'wc': '1.2'
					},
					{
						'name': '张三',
						'time': '2021-5-22',
						'temp': '36.7-333-333-333',
						'wc': '1.2'
					},
					{
						'name': '张三',
						'time': '2021-5-22',
						'temp': '36.7-333-333-333',
						'wc': '1.2'
					},
					{
						'name': '张三',
						'time': '2021-5-22',
						'temp': '36.7-333-333-333',
						'wc': '1.2'
					}

				]

			}
		},
		methods: {
			confirm() {
				//清空数据js

				this.show1 = false
			},
			change(e) {
				//判断是否在时间区间内
				var JudgeTime= function (planStartTime,planStopTime,dataTime)
				{
				//将计划开始时间转成以秒为单位：
				var startTime = new Array();
				startTime = planStartTime.split('-');
				planStartTime = Date.UTC(parseInt(startTime[0]), parseInt(startTime[1]), parseInt(startTime[2]));
				//将计划结束时间转成以秒为单位：
				
				var stopTime = new Array();
				stopTime = planStopTime .split('-');
				planStopTime = Date.UTC(parseInt(stopTime[0]), parseInt(stopTime[1]), parseInt(stopTime[2]));
				//将当前系统时间转化成以秒为单位：
				//获取当前时间
				var nowDate = new Date(dataTime);
				//当前年
				var nowYear = nowDate.getFullYear();
				//当前月，记得要加1
				var nowMonth = (nowDate.getMonth() + 1);
				//当前日
				var nowDay = nowDate.getDate();
				var nowTime = Date.UTC(nowYear,nowMonth,nowDay);
				//判断：如果当前系统时间大于等于开始时间以及小于等于结束时间则登记成功
				if (nowTime >= planStartTime && nowTime <= planStopTime) {
				return true;
				} else {
				return false;
				}
				}
				
				var name = uni.getStorageSync('name')
				var sex = uni.getStorageSync('sex')
				var age = uni.getStorageSync('age')
				//获取历史数据
				var historyData = uni.getStorageSync("historyData")
				var headerData = [
					{
							content: '姓名',
							color: 'blue',
							type: 'text',
							width: '200px',
							height: '25px',
							fontSize: '16px'
						},
					{
							content: '性别',
							color: 'blue',
							type: 'text',
							width: '200px',
							height: '25px',
							fontSize: '16px'
						},
					{
							content: '年龄',
							color: 'blue',
							type: 'text',
							width: '200px',
							height: '25px',
							fontSize: '16px'
						},
					{
						content: '左腋下',
						color: 'blue',
						type: 'text',
						width: '200px',
						height: '25px',
						fontSize: '16px'
					},
					{
						content: '左体表',
						color: 'blue',
						type: 'text',
						width: '200px',
						height: '25px',
						fontSize: '16px'
					},
					{
						content: '右腋下',
						color: 'blue',
						type: 'text',
						width: '200px',
						height: '25px',
						fontSize: '16px'
					},
					{
						content: '右体表',
						color: 'blue',
						type: 'text',
						width: '200px',
						height: '25px',
						fontSize: '16px'
					},
					{
						content: '湿度',
						color: 'blue',
						type: 'text',
						width: '200px',
						height: '25px',
						fontSize: '16px'
					},
					{
						content: '体表温差',
						color: 'blue',
						type: 'text',
						width: '300px',
						height: '25px',
						fontSize: '16px'
					},
					{
						content: '腋下温差',
						color: 'blue',
						type: 'text',
						width: '300px',
						height: '25px',
						fontSize: '16px'
					},
					{
						content: '运动状态',
						color: 'blue',
						type: 'text',
						width: '300px',
						height: '25px',
						fontSize: '16px'
					},
					{
						content: '采集时间',
						color: 'blue',
						type: 'text',
						width: '400px',
						height: '25px',
						fontSize: '16px'
					},
				]
			
				var dataList = new Array()
				var data = new Array()
				if (historyData != null && historyData != '') {
					
					for (var i = 0; i < historyData.length; i++) {
						if(JudgeTime(e.startDate,e.endDate,historyData[i].date)){
							data = [
								{
										content: name,
										color: 'blue',
										type: 'text',
										width: '200px',
										height: '25px',
										fontSize: '16px'
									
									},
								{
										content: sex,
										color: 'blue',
										type: 'text',
										width: '200px',
										height: '25px',
										fontSize: '16px'
									
									},
								{
										content: age,
										color: 'blue',
										type: 'text',
										width: '200px',
										height: '25px',
										fontSize: '16px'
									
									},
								{
									content: historyData[i].leftArmpit,
									color: 'blue',
									type: 'text',
									width: '200px',
									height: '25px',
									fontSize: '16px'
								
								},
								{
									content: historyData[i].leftBody,
									color: 'blue',
									type: 'text',
									width: '200px',
									height: '25px',
									fontSize: '16px'
									
								},
								{
									content: historyData[i].rightArmpit,
									color: 'blue',
									type: 'text',
									width: '200px',
									height: '25px',
									fontSize: '16px'
									
								},
								{
									content: historyData[i].rightBody,
									color: 'blue',
									type: 'text',
									width: '200px',
									height: '25px',
									fontSize: '16px'
									
								},
								//{'conent':historyData[i].humidity,'color':'color',type: 'text',width: '200px',height: '25px',fontSize: '16px',colspan: 2,rowspan:2},
								{
									content: historyData[i].electric,
									color: 'blue',
									type: 'text',
									width: '200px',
									height: '25px',
									fontSize: '16px'
								
								},
								{
									content: historyData[i].bodyDisparity,
									color: 'blue',
									type: 'text',
									width: '300px',
									height: '25px',
									fontSize: '16px'
								
								},
								{
									content: historyData[i].armpitDisparity,
									color: 'blue',
									type: 'text',
									width: '300px',
									height: '25px',
									fontSize: '16px'
								
								},
								{
									content: historyData[i].motion_state,
									color: 'blue',
									type: 'text',
									width: '400px',
									height: '25px',
									fontSize: '16px'
									
								},
								{
									content: historyData[i].date,
									color: 'blue',
									type: 'text',
									width: '400px',
									height: '25px',
									fontSize: '16px'
									
								},
							]
							dataList.unshift(data)
						}						
					}
					
				}
				dataList.unshift(headerData)
	

				let doExport = require('@/js_sdk/LZN-exportExcel/exportExcel.js');
				doExport(name, dataList, function(res) {
				
				})
			}
		},
		onShow() {
			var indexYy = uni.getStorageSync('indexYy')
			if (indexYy == 1) {
				this.dcsj = 'Export data'
				this.qksj = 'wipe data'
				this.content = 'Are you sure to clear the data?'
				this.xh = 'Serial number'
				this.xm = 'name'
				this.sj = 'time'
				this.wd = 'temperature'
				this.wc = 'Temperature difference'
				this.chartData = {
					categories: ["300", "400", "500", "600", "700", "800"],
					series: [{
						name: 'Left armpit',
						data: [35, 36, 31, 33, 13, 34]
					}, {
						name: "Left body surface",
						data: [18, 25, 21, 27, 6, 28]
					}, {
						name: "Right armpit",
						data: [14, 27, 21, 24, 6, 28]
					}, {
						name: "Right body surface",
						data: [16, 22, 26, 28, 6, 28]
					}]
				}
			}
		}
	}
</script>

<style lang="scss">
	.id {
		display: flex;
		justify-content: center;
		flex-direction: column;
		align-items: center;

		.tj {
			display: flex;
			// flex-direction: column;
			align-items: center;
			margin-top: 30upx;
			width: 700upx;
			height: 500upx;
			border: 1upx solid #3F536E;
			border-radius: 30upx;
			box-shadow: darkgrey 0px 0px 2px 2px;
		}

		.btn {
			margin-top: 20upx;
			width: 70%;
			display: flex;
			justify-content: space-between;
		}

		.table {
			margin-top: 30upx;
			width: 100%;

			// height: 500upx;
			.scroll {
				width: 100%;

				.table1 {
					width: 100%;
					margin-bottom: 20upx;
					display: flex;
					justify-content: space-between;
				}

				.table-data {
					width: 100%;
					display: flex;

					.table-data-item {
						border: 1upx solid #7cc0c1;
						width: 30%;
						text-align: center;
					}
				}
			}
		}
	}
</style>
