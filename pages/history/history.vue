<template>
	<view class="id">
		<view class="tj">
			<qiun-data-charts type="line" :chartData="chartData" />
		</view>
		<view class="btn">
			<u-button type="primary" @click='show2 = true'>导出数据</u-button>
			<u-button type="primary" @click='show1 = true'>清空数据</u-button>
		</view>
		
		<u-modal v-model="show1" content="确认清空数据吗？" :mask-close-able="true" @confirm="confirm"></u-modal>
		<u-calendar v-model="show2" mode="range" @change="change" ></u-calendar>
		<view class="table">
			<scroll-view scroll-x="true" class="scroll">
				<view class="table1">
					<view class="table-item" >序号</view>
					<view class="table-item" >姓名</view>
					<view class="table-item" >时间</view>
					<view class="table-item" >温度</view>
					<view class="table-item" >温差</view>
				</view>
					<view class="table-data"  v-for="(item,index) in dataList" >
						<view class="table-data-item" >{{index+1}}</view>
						<view class="table-data-item" >{{item.name}}</view>
						<view class="table-data-item">{{item.time}}</view>
						<view class="table-data-item" >{{item.temp}}</view>
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
				show1:false,
				show2:false,
				chartData:{
					
				  categories: ["300", "400", "500", "600", "700", "800"],
				  series: [{
				    name: "左腋下",
				    data: [35, 36, 31, 33, 13, 34]
				  }, {
				    name: "左体表",
				    data: [18, 25, 21, 27, 6, 28]
				  },{
				    name: "右腋下",
				    data: [14, 27, 21, 24, 6, 28]
				  },{
				    name: "右体表",
				    data: [16, 22, 26, 28, 6, 28]
				  }
				  ]
				},
				dataList:
					[
						{'name':'张三','time':'2021-5-22','temp':'36.7-333-333-333','wc':'1.2'},
						{'name':'张三','time':'2021-5-22','temp':'36.7-333-333-333','wc':'1.2'},
						{'name':'张三','time':'2021-5-22','temp':'36.7-333-333-333','wc':'1.2'},
						{'name':'张三','time':'2021-5-22','temp':'36.7-333-333-333','wc':'1.2'},
						{'name':'张三','time':'2021-5-22','temp':'36.7-333-333-333','wc':'1.2'},
						{'name':'张三','time':'2021-5-22','temp':'36.7-333-333-333','wc':'1.2'},
						{'name':'张三','time':'2021-5-22','temp':'36.7-333-333-333','wc':'1.2'}
						
					]
				
			}
		},
		methods: {
			confirm(){
				//清空数据js
				
				this.show1 = false
			},
			change(e) {
				console.log(e);
				
				
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
			box-shadow: darkgrey 0px 0px 2px 2px ;
		}
		.btn {
			margin-top: 20upx;
			width: 70%;
			display: flex;
			justify-content: space-between;
		}
		.table {
			margin-top: 30upx;
			width: 700upx;
			height: 500upx;
			.table1 {
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
</style>
