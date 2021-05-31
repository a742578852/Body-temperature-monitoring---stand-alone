<template>
	<view class="id">
		<view class="div1">
			<u-avatar class="img" :src="touxiang" @click="grzl"></u-avatar>
			<!-- <image class="img" :src="touxiang" @click="grzl"></image> -->
			<text>张三</text>
			<view class="div2">
				<view class="div3" @click="shishi">
					<image class="img" src="../../static/shishi.png"></image>
					<text>{{sssj}}</text>
				</view>
				<view class="div4" @click="lishi">
					<image class="img" src="../../static/lishi.png"></image>
					<text>{{lssj}}</text>
				</view>
			</view>
		</view>
		<text style="margin-top: 30upx;">{{wdsb}}</text>
		<view class="div5">
			<view class="cu-form-group" >
				<view class="title" style="width: 290upx;">{{twj}}:</view>
				<input  name="input" disabled="">{{dl}}  100%</input>
			</view>
			<view class="cu-form-group" @click="ghsb">
				<view class="title" style="padding-left: 33%;">+ {{ghsbb}}</view>
			</view>
		</view>
		<text style="margin-top: 30upx;">{{gdsz}}</text>
		<view class="div6">
			<view class="cu-form-group">
				<view class="title">{{cjpl}}:</view>
				<picker @change="bindPickerChange" :value="index" :range="arrayCjpl" class="item2" style="width: 100%;">
					<view class="uni-input" style="width: 100%;">{{arrayCjpl[index]}} s</view>
				</picker>
				<u-icon name="arrow-right"></u-icon>
			</view>
			
			<view class="cu-form-group">
				<view class="title">{{wdxz}}:</view>
				<u-icon name="arrow-right"></u-icon>
			</view>
			<view class="cu-form-group">
				<view class="title">{{wddw}}:</view>
				<picker @change="bindPickerChange1" :value="index1" :range="arrayWddw" class="" style="width: 100%;">
					<view class="uni-input" >{{arrayWddw[index1]}}</view>
				</picker>
				<u-icon name="arrow-right"></u-icon>
			</view>
			<view class="cu-form-group">
				<view class="title">{{tzdw}}:</view>
				<picker @change="bindPickerChange4" :value="index4" :range="arrayTzdw" class="" style="width: 100%;">
					<view class="uni-input" >{{arrayTzdw[index4]}}</view>
				</picker>
				<u-icon name="arrow-right"></u-icon>
			</view>
			<view class="cu-form-group">
				<view class="title">{{sgdww}}:</view>
				<input  name="input" v-model="sgdw" disabled=""></input>
			</view>
			<view class="cu-form-group">
				<view class="title">{{rlzh}}:</view>
				<picker @change="bindPickerChange2" :value="index2" :range="arrayRl" class="" style="width: 100%;">
					<view class="uni-input" >{{arrayRl[index2]}}</view>
				</picker>
				<u-icon name="arrow-right"></u-icon>
			</view>
			<view class="cu-form-group">
				<view class="title">{{yyzh}}:</view>
				<picker @change="bindPickerChange3" :value="index3" :range="arrayYy" class="" style="width: 100%;">
					<view class="uni-input" >{{arrayYy[index3]}}</view>
				</picker>
				<u-icon name="arrow-right"></u-icon>
			</view>
		</view>
		<view class="" style="margin-top: 30upx; height: 60upx;" @click="abouts()">
			<text style="margin-top: 30upx; height: 60upx;" >{{gywm}}</text>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				gywm:'关于我们',
				sgdww:'身高单位',
				wdxz:'温度校准',
				gdsz:'更多设置',
				sssj:'实时数据',
				lssj:'历史数据',
				wdsb:'我的设备',
				dl:'电量',
				twj:'体温计',
				ghsbb:'更换设备',
				touxiang:'',
				cjpl:'采集频率',
				wddw:'温度单位',
				tzdw:'体重单位',
				sgdw:'cm',
				rlzh:'日历转换',
				yyzh:'语言转换',
				index:0,
				index1:0,
				index2:0,
				index3:0,
				index4:0,
				arrayTzdw:['千克','磅'],
				arrayCjpl:['500','600'],
				arrayWddw:['摄氏度','华氏度'],
				arrayRl:['阳历','农历'],
				arrayYy:['中文','English']
			}
		},
		methods: {
			abouts(){
				uni.navigateTo({
					url:'../about/about'
				})
			},
			bindPickerChange(e) {
				console.log('picker发送选择改变，携带值为', e.target.value)
				this.index = e.target.value
			},
			bindPickerChange1(e) {
				console.log('picker发送选择改变，携带值为', e.target.value)
				this.index1 = e.target.value
				if(this.index1==1){
					uni.setStorageSync('wddw','华氏度')
				}else{
					uni.setStorageSync('wddw','摄氏度')
				}
			},
			bindPickerChange2(e) {
				console.log('picker发送选择改变，携带值为', e.target.value)
				this.index2 = e.target.value
			},
			bindPickerChange3(e) {
				console.log('picker发送选择改变，携带值为', e.target.value)
				this.index3 = e.target.value
				uni.setStorageSync('indexYy',this.index3)
				if(e.target.value==1){
					this.arrayRl = ['Solar calendar','lunar calendar']
					this.arrayTzdw = ['kg','pound']
					this.arrayWddw = ['centigrade','Fahrenheit degree']
					this.gywm = 'About us'
					this.yyzh = 'Language conversion'
					this.rlzh = 'Calendar conversion'
					this.sgdww = 'Height unit'
					this.tzdw = 'Weight unit'
					this.wddw = 'Temperature unit'
					this.wdxz = 'Temperature calibration'
					this.cjpl = 'Acquisition frequency'
					this.gdsz = 'More settings'
					this.sssj = 'real-time data'
					this.lssj = 'historical data'
					this.wdsb = 'My device'
					this.twj = 'The thermometer'
					this.dl = 'Quantity of electricity'
					this.ghsbb = 'Replacement of equipment'
				}else{
					this.arrayRl = ['阳历','农历']
					this.arrayWddw = ['摄氏度','华氏度']
					this.arrayTzdw = ['千克','磅']
					this.gywm = '关于我们'
					this.yyzh = '语言转换'
					this.rlzh = '日历转换'
					this.sgdww = '身高单位'
					this.tzdw = '体重单位'
					this.wddw = '温度单位'
					this.wdxz = '温度校准'
					this.cjpl = '采集频率'
					this.gdsz = '更多设置'
					this.sssj = '实时数据'
					this.lssj = '历史数据'
					this.wdsb = '我的设备'
					this.twj = '体温计'
					this.dl = '电量'
					this.ghsbb = '更换设备'
				}
				uni.setStorageSync('yyqh',e.target.value)
			},
			bindPickerChange4(e) {
				console.log('picker发送选择改变，携带值为', e.target.value)
				this.index4 = e.target.value
			},
			ghsb(){
				uni.navigateTo({
					url:'./bluetooth/bluetoothFind'
				})
			},
			grzl(){
				uni.navigateTo({
					url:'../personal-data/personal-data'
				})
			},
			shishi(){
				uni.switchTab({
					url:'../index/indexs'
				})
			},
			lishi(){
				uni.navigateTo({
					url:'../history/history'
				})
			},
			
		},
		onLoad() {
			
		},
		onShow() {
			this.touxiang = uni.getStorageSync('touxiang')
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
				// input {
				// 	margin-left: 100upx;
				// }
				// .uni-input {
				// 	margin-left: 100upx;
				// }
			}
		}
	}
	
</style>
