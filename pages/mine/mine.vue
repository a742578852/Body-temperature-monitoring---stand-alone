<template>
	<view class="id">

		<view class="div1">
			<view>
				<u-popup v-model="calibration_show" mode='bottom'>
					<view>
						<view style="margin-top: 10rpx;width: 60%;margin-left:20%;">
							<u-button :ripple="true" type="primary" @click="calibrationGo('L1')">L1(左体表)通道</u-button>
						</view>
						<view style="margin-top: 10rpx;width: 60%;margin-left:20%;">
							<u-button :ripple="true" type="primary" @click="calibrationGo('L2')">L2(左腋下)通道</u-button>
						</view>
						<view style="margin-top: 10rpx;width: 60%;margin-left:20%;">
							<u-button :ripple="true" type="primary" @click="calibrationGo('R1')">R1(右体表)通道</u-button>
						</view>
						<view style="margin-top: 10rpx;width: 60%;margin-left:20%;">
							<u-button :ripple="true" type="primary" @click="calibrationGo('R2')">R2(右腋下)通道</u-button>
						</view>
						<view style="margin-top: 10rpx;width: 60%;margin-left:20%;">
							<u-button :ripple="true" type="success" @click="calibrationGo('all')">所有通道</u-button>
						</view>

					</view>
				</u-popup>
				<!--校准密码弹窗-->
				<u-popup v-model="password_show" mode='center' length = 'auto' border-radius="25">
					<view style="width: 600rpx;margin: 30rpx;">
						<u-input v-model="password" :type="type" :border="border" placeholder = '请输入密码' />
						
					</view>
					<view style="width: 400rpx;margin-left: 120rpx;margin-top: 40rpx;margin-bottom: 40rpx;">
						<u-button type="primary" shape="square" :ripple="true" @click="passwordVer()">确定</u-button>
					</view>
				</u-popup>
			</view>
			<view>
				<u-toast ref="uToast" />
			</view>
			<u-avatar class="img" :src="touxiang" @click="grzl"></u-avatar>
			<!-- <image class="img" :src="touxiang" @click="grzl"></image> -->
			<text>{{name}}</text>
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
			<!--电量-->
			<view class="cu-form-group">
				<view class="title" style="width: 290upx;">{{twj}}:</view>
				<input name="input" disabled="">{{dl}} %</input>
			</view>
			<view class="cu-form-group" @click="ghsb">
				<view class="title" style="padding-left: 33%;">+ {{ghsbb}}</view>
			</view>
		</view>
		<text style="margin-top: 30upx;">{{gdsz}}</text>
		<view class="div6">
			<!--采集频率-->
			<view class="cu-form-group">
				<view class="title">{{cjpl}}:</view>
				<picker @change="bindPickerChange" :value="index" :range="arrayCjpl" class="item2" style="width: 100%;">
					<view class="uni-input" style="width: 100%;">{{arrayCjpl[index]}} </view>
				</picker>
				<u-icon name="arrow-right"></u-icon>
			</view>

			<!--loding-->
			<view style="width: 60%;margin-left:30%;">

				<u-loading mode="flower" :show="loding_show" size='36'></u-loading>
			</view>
			<!--温度校准-->
			<view class="cu-form-group">
				<view class="title">{{wdxz}}:</view>
				<u-icon name="arrow-right" @click='calibration'></u-icon>
			</view>
			<view class="cu-form-group">
				<view class="title">{{wddw}}:</view>
				<picker @change="bindPickerChange1" :value="index1" :range="arrayWddw" class="" style="width: 100%;">
					<view class="uni-input">{{arrayWddw[index1]}}</view>
				</picker>
				<u-icon name="arrow-right"></u-icon>
			</view>
			<view class="cu-form-group">
				<view class="title">{{tzdw}}:</view>
				<picker @change="bindPickerChange4" :value="index4" :range="arrayTzdw" class="" style="width: 100%;">
					<view class="uni-input">{{arrayTzdw[index4]}}</view>
				</picker>
				<u-icon name="arrow-right"></u-icon>
			</view>
			<view class="cu-form-group">
				<view class="title">{{sgdww}}:</view>
				<input name="input" v-model="sgdw" disabled=""></input>
			</view>
			<view class="cu-form-group">
				<view class="title">{{rlzh}}:</view>
				<picker @change="bindPickerChange2" :value="index2" :range="arrayRl" class="" style="width: 100%;">
					<view class="uni-input">{{arrayRl[index2]}}</view>
				</picker>
				<u-icon name="arrow-right"></u-icon>
			</view>
			<view class="cu-form-group">
				<view class="title">{{yyzh}}:</view>
				<picker @change="bindPickerChange3" :value="index3" :range="arrayYy" class="" style="width: 100%;">
					<view class="uni-input">{{arrayYy[index3]}}</view>
				</picker>
				<u-icon name="arrow-right"></u-icon>
			</view>
		</view>
		<view class="" style="margin-top: 30upx; height: 60upx;" @click="abouts()">
			<text style="margin-top: 30upx; height: 60upx;">{{gywm}}</text>
		</view>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				name:'',
				type: 'text',
				border: true,
				password_show: false, //密码输入框弹窗
				loding_show: false,
				password: '', //密码
				calibration_show: false, //温度校准弹窗
				gywm: '关于我们',
				sgdww: '身高单位',
				wdxz: '温度校准',
				gdsz: '更多设置',
				sssj: '实时数据',
				lssj: '历史数据',
				wdsb: '我的设备',
				dl: '电量',
				twj: '体温计',
				ghsbb: '更换设备',
				touxiang: '',
				cjpl: '采集频率',
				wddw: '温度单位',
				tzdw: '体重单位',
				sgdw: 'cm',
				rlzh: '日历转换',
				yyzh: '语言转换',
				index: 0,
				index1: 0,
				index2: 0,
				index3: 0,
				index4: 0,
				arrayTzdw: ['千克', '磅'],
				arrayCjpl: ['10s', '50s','100s','500s','1000s','3000s'],//采集频率
				arrayWddw: ['摄氏度', '华氏度'],
				arrayRl: ['阳历', '农历'],
				arrayYy: ['中文', 'English'],
				nongLi: {},
				serviceId: '', //服务id
				ble_info: '' //deviceid

			}
		},
		methods: {
			//校准密码校验
			passwordVer(){
				if(this.password == 'DrCui'){
					this.password_show = false
					this.calibration_show = true
				}else{
					var toast_info = {
						'title': '密码校验失败',
						'type': 'success',
					}
					this.showToast(toast_info)
				}
				
				
			},
			//获取特征值
			getBLEDeviceCharacteristics(value) {
				console.log("进入特征");
				var _this = this
				setTimeout(() => {
					uni.getBLEDeviceCharacteristics({
						deviceId: _this.ble_info.deviceId,
						serviceId: _this.serviceId,
						success(res) {
							console.log(res);
							res.characteristics.forEach((item) => {
								console.log('获取所有char');
								if (item.uuid.indexOf('8653000C') != -1) {
									const buffer = new ArrayBuffer(2)
									const dataView = new DataView(buffer)
									dataView.setUint8(0, 0x02)
									dataView.setUint8(1, value)
									console.log(_this.deviceId + _this.serviceId + item.uuid);
									uni.writeBLECharacteristicValue({
										deviceId: _this.ble_info.deviceId,
										serviceId: _this.serviceId,
										characteristicId: item.uuid,
										value: buffer,
										success(res) {
											var toast_info = {
												'title': '设备校准成功',
												'type': 'success',
											}
											_this.showToast(toast_info)
											console.log(res);
										},
										fail(res) {
											var toast_info = {
												'title': '设备写入数据失败,请检查蓝牙连接',
												'type': 'warning',
											}
											_this.showToast(toast_info)
											console.log(res);
										}

									})

								}
							})
						},
						fail(res) {
							var toast_info = {
								'title': '蓝牙特征值获取失败,请检查蓝牙连接',
								'type': 'warning',
							}
							_this.showToast(toast_info)
							console.log(res);
						}
					})

				}, 1000)

			},
			//蓝牙连接提醒
			showToast(toast_info) {
				this.$refs.uToast.show({
					title: toast_info.title,
					type: toast_info.type,
					url: toast_info.url
				})
			},

			//温度校准
			calibration() {
				console.log('温度校准');
				//判断蓝牙有没有连接,没有连接提示弹窗
				var ble_link = uni.getStorageSync('ble_link');
				var ava = uni.getStorageSync('ava')
				if (ble_link.connected == false || ava.available == false) {
					var toast_info = {
						'title': '未检测到设备连接,请先连接设备',
						'type': 'warning',
					}
					this.showToast(toast_info)
				} else {
					//弹出密码校验层 
					this.password_show = true
				}

			},
			//校准
			calibrationGo(passageway) {

				this.loding_show = true
				var command
				if (passageway == 'L1') {
					command = '0x01'
				} else if (passageway == 'L2') {
					command = '0x02'
				} else if (passageway == 'R1') {
					command = '0x03'
				} else if (passageway == 'R2') {
					command = '0x04'
				} else if (passageway == 'all') {
					command = '0x05'
				}

				this.getBLEDeviceCharacteristics(command)
				this.loding_show = false
				this.calibration_show = false
			},
			//跳转关于页面
			abouts() {
				uni.navigateTo({
					url: '../about/about'
				})
			},
			bindPickerChange(e) {
				var _this = this
				console.log('picker发送选择改变，携带值为', e.target.value)
				this.index = e.target.value
				var frequency = this.arrayCjpl[this.index] //频率
				
				setTimeout(() => {
					uni.getBLEDeviceCharacteristics({
						deviceId: _this.ble_info.deviceId,
						serviceId: _this.serviceId,
						success(res) {
							console.log(res);
							res.characteristics.forEach((item) => {
								console.log('获取所有char');
								if (item.uuid.indexOf('8653000B') != -1) {
									const buffer = new ArrayBuffer(2)
									const dataView = new DataView(buffer)
									dataView.setUint8(0, 0x01)
									dataView.setUint8(1, 0x012c)
									console.log(_this.deviceId + _this.serviceId + item.uuid);
									uni.writeBLECharacteristicValue({
										deviceId: _this.ble_info.deviceId,
										serviceId: _this.serviceId,
										characteristicId: item.uuid,
										value: buffer,
										success(res) {
											var toast_info = {
												'title': '采集频率成功',
												'type': 'success',
											}
											_this.showToast(toast_info)
											console.log(res);
										},
										fail(res) {
											var toast_info = {
												'title': '设备写入数据失败,请检查蓝牙连接',
												'type': 'warning',
											}
											_this.showToast(toast_info)
											console.log(res);
										}
				
									})
				
								}
							})
						},
						fail(res) {
							var toast_info = {
								'title': '蓝牙特征值获取失败,请检查蓝牙连接',
								'type': 'warning',
							}
							_this.showToast(toast_info)
							console.log(res);
						}
					})
				
				}, 1000)
				
			},
			bindPickerChange1(e) {
				console.log('picker发送选择改变，携带值为', e.target.value)
				this.index1 = e.target.value
				if (this.index1 == 1) {
					uni.setStorageSync('wddw', '华氏度')
				} else {
					uni.setStorageSync('wddw', '摄氏度')
				}
			},
			bindPickerChange2(e) {
				console.log('picker发送选择改变，携带值为', e.target.value)
				this.index2 = e.target.value
				//把选择的阳历或阴历存入缓存 0：阳历，1：阴历
				uni.setStorageSync('rlzh', this.index2)
			},
			bindPickerChange3(e) {
				console.log('picker发送选择改变，携带值为', e.target.value)
				this.index3 = e.target.value
				//获取语言类型放在缓存
				uni.setStorageSync('indexYy', this.index3)
				if (e.target.value == 1) {
					this.arrayRl = ['Solar calendar', 'lunar calendar']
					this.arrayTzdw = ['kg', 'pound']
					this.arrayWddw = ['centigrade', 'Fahrenheit degree']
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
				} else {
					this.arrayRl = ['阳历', '农历']
					this.arrayWddw = ['摄氏度', '华氏度']
					this.arrayTzdw = ['千克', '磅']
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
				uni.setStorageSync('yyqh', e.target.value)
			},
			bindPickerChange4(e) {
				console.log('picker发送选择改变，携带值为', e.target.value)
				this.index4 = e.target.value

			},
			//更换设备
			ghsb() {
				uni.navigateTo({
					url: './bluetooth/bluetoothFind'
				})
			},
			//个人资料
			grzl() {
				uni.navigateTo({
					url: '../personal-data/personal-data'
				})
			},
			//实时数据
			shishi() {
				uni.switchTab({
					url: '../index/indexs'
				})
			},
			//历史数据
			lishi() {
				uni.navigateTo({
					url: '../history/history'
				})
			},




		},
		onLoad() {

		},
		onShow() {
			var _this = this
			this.touxiang = uni.getStorageSync('touxiang')
			var ble_link = uni.getStorageSync('ble_link')
			_this.name = uni.getStorageSync('name')
			//获取电量
			var history = uni.getStorageSync("historyData")
			 this.dl = history[0].electric
			
			uni.getStorage({
				key: 'link_ble_info',
				success: function(res) {
					_this.ble_info = res.data
				}
			})
			//判断蓝牙是否连接
			if (ble_link.connected == true) {
				//蓝牙已经连接,无需重复连接
				uni.openBluetoothAdapter({
					success() {
						//获取所有服务
						uni.getBLEDeviceServices({
							deviceId: _this.ble_info.deviceId,
							success(res) {
								_this.ble_services = res.services
								res.services.forEach((item) => {
									console.log("进入循环" + item.uuid);
									if (item.uuid.indexOf("8653000A") != -1) {
										_this.serviceId = item.uuid;

									}
								})

							}
						})
					}
				}, 1000)
			}


			//蓝牙连接状态监听
			uni.onBLEConnectionStateChange(function(res) {
				_this.blelink = res
				// 该方法回调中可以用于处理连接意外断开等异常情况
				console.log('蓝牙:' + res.deviceId + '连接状态:' + res.connected)
				uni.setStorageSync('ble_link', res);
			})

			//蓝牙开关状态监听
			uni.onBluetoothAdapterStateChange(function(res) {

				uni.setStorageSync('ava', res)

			})

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
			box-shadow: darkgrey 0px 0px 2px 2px;

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
			box-shadow: darkgrey 0px 0px 2px 2px;

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
			box-shadow: darkgrey 0px 0px 2px 2px;

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
