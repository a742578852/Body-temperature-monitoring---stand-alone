<template>
	<view class="id">
		<view class="div1">
			<image class="img" src="../../static/nick.png"></image>
			<text>张三</text>
			<view class="div2">
				<view class="div3">
					<image class="img" src="../../static/img/实时.png"></image>
					<text>实时数据</text>
				</view>
				<view class="div4">
					<image class="img" src="../../static/img/历史.png"></image>
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
				<picker @change="bindPickerChange" :value="index" :range="arrayCjpl" class="item2" style="width: 100%;">
					<view class="uni-input" style="width: 100%;">{{arrayCjpl[index]}} s</view>
				</picker>
				<u-icon name="arrow-right"></u-icon>
			</view>
			
			<view class="cu-form-group">
				<view class="title">温度校准:</view>
				<u-icon name="arrow-right"></u-icon>
			</view>
			<view class="cu-form-group">
				<view class="title">温度单位:</view>
				<picker @change="bindPickerChange1" :value="index1" :range="arrayWddw" class="" style="width: 100%;">
					<view class="uni-input" >{{arrayWddw[index1]}}</view>
				</picker>
				<u-icon name="arrow-right"></u-icon>
			</view>
			<view class="cu-form-group">
				<view class="title">体重单位:</view>
				<input  name="input" v-model="tzdw"></input>
			</view>
			<view class="cu-form-group">
				<view class="title">身高单位:</view>
				<input  name="input" v-model="sgdw"></input>
			</view>
			<view class="cu-form-group">
				<view class="title">日历转换:</view>
				<picker @change="bindPickerChange2" :value="index2" :range="arrayRl" class="" style="width: 100%;">
					<view class="uni-input" >{{arrayRl[index2]}}</view>
				</picker>
				<u-icon name="arrow-right"></u-icon>
			</view>
			<view class="cu-form-group">
				<view class="title">语言转换:</view>
				<picker @change="bindPickerChange3" :value="index3" :range="arrayYy" class="" style="width: 100%;">
					<view class="uni-input" >{{arrayYy[index3]}}</view>
				</picker>
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
				yyzh:'中文',
				index:0,
				index1:0,
				index2:0,
				index3:0,
				arrayCjpl:['500','600'],
				arrayWddw:['摄氏度','华氏度'],
				arrayRl:['阳历','阴历'],
				arrayYy:['中文','English']
			}
		},
		methods: {
			bindPickerChange(e) {
				console.log('picker发送选择改变，携带值为', e.target.value)
				this.index = e.target.value
			},
			bindPickerChange1(e) {
				console.log('picker发送选择改变，携带值为', e.target.value)
				this.index1 = e.target.value
			},
			bindPickerChange2(e) {
				console.log('picker发送选择改变，携带值为', e.target.value)
				this.index2 = e.target.value
			},
			bindPickerChange3(e) {
				console.log('picker发送选择改变，携带值为', e.target.value)
				this.index3 = e.target.value
			},
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
				.uni-input {
					margin-left: 300upx;
				}
			}
		}
	}
	
</style>
