<template>
	<view class="id">
		<view class="div1">
			<image class="img" src="../../static/nick.png"></image>
			<text>张三</text>
			<view class="div2">
				<view class="div3">
					<image class="img" src="../../static/nick.png"></image>
					<text>实时数据</text>
				</view>
				<view class="div4">
					<image class="img" src="../../static/nick.png"></image>
					<text>历史数据</text>
				</view>
			</view>
		</view>
		<text style="margin-top: 30upx;">我的设备</text>
		<view class="div5">
			<view class="cu-form-group" >
				<view class="title">一号体温计:</view>
				<input  name="input" >电量 100%</input>
			</view>
			<view class="cu-form-group" >
				<view class="title" style="padding-left: 35%;">+ 更换设备</view>
			</view>
		</view>
		<text style="margin-top: 30upx;">更多设置</text>
		<view class="div6">
			<view class="cu-form-group">
				<view class="title">采集频率:</view>
				<input  name="input" v-model="cjpl">s</input>
				<u-icon name="arrow-right"></u-icon>
			</view>
			<view class="cu-form-group">
				<view class="title">温度校准:</view>
				<u-icon name="arrow-right"></u-icon>
			</view>
			<view class="cu-form-group">
				<view class="title">温度单位:</view>
				<input  name="input" v-model="wddw"></input>
				<u-icon name="arrow-right"></u-icon>
			</view>
			<view class="cu-form-group">
				<view class="title">体重单位:</view>
				<input  name="input" v-model="tzdw"></input>
				<u-icon name="arrow-right"></u-icon>
			</view>
			<view class="cu-form-group">
				<view class="title">身高单位:</view>
				<input  name="input" v-model="sgdw"></input>
				<u-icon name="arrow-right"></u-icon>
			</view>
			<view class="cu-form-group">
				<view class="title">日历转换:</view>
				<input  name="input" v-model="rlzh"></input>
				<u-icon name="arrow-right"></u-icon>
			</view>
			<view class="cu-form-group">
				<view class="title">语言转换:</view>
				<input  name="input" v-model="yyzh"></input>
				<u-icon name="arrow-right"></u-icon>
			</view>
		</view>
		<text style="margin-top: 30upx; height: 60upx;">关于我们</text>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				cjpl:'500',
				wddw:'摄氏度',
				tzdw:'kg',
				sgdw:'cm',
				rlzh:'阳历',
				yyzh:'中文'
			}
		},
		methods: {
			
		}
	}
</script>

<style lang="scss">
	.id {
		display: flex;
		justify-content: center;
		flex-direction: column;
		align-items: center;
		.div1 {
			display: flex;
			flex-direction: column;
			align-items: center;
			margin-top: 50upx;
			width: 700upx;
			height: 400upx;
			border: 1upx solid #3F536E;
			border-radius: 30upx;
			box-shadow: darkgrey 0px 0px 2px 2px ;
			.img {
				margin-top: 50upx;
				width: 100upx;
				height: 100upx;
			}
			.div2 {
				width: 80%;
				display: flex;
				justify-content: space-between;
				.div3 {
					display: flex;
					flex-direction: column;
				}
				.div4 {
					display: flex;
					flex-direction: column;
				}
			}
		}
		.div5 {
			margin-top: 20upx;
			width: 700upx;
			height: 220upx;
			border: 1upx solid #3F536E;
			border-radius: 30upx;
			box-shadow: darkgrey 0px 0px 2px 2px ;
			.cu-form-group {
				width: 680upx;
				margin-left: 10upx;
				margin-top: 5upx;
				border-radius: 30upx;
			}
		}
		.div6 {
			margin-top: 20upx;
			width: 700upx;
			height: 750upx;
			border: 1upx solid #3F536E;
			border-radius: 30upx;
			box-shadow: darkgrey 0px 0px 2px 2px ;
			.cu-form-group {
				width: 680upx;
				margin-left: 10upx;
				margin-top: 5upx;
				border-radius: 30upx;
				input {
					margin-left: 300upx;
				}
			}
		}
	}
	
</style>
