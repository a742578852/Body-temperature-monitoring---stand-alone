<template>
	<view class="id">
		<view class="info">
			<view class="" style="display: flex;align-items: center;">
				当前状态：<image :src="imgUrl" style="width: 80upx;height: 80upx;margin-right: 10upx;"></image>
			</view>
			<view class="">采集时间：{{cjsj}}</view>
		</view>

		<view class="tj">
			<qiun-data-charts type="line" :chartData="chartData1" />
		</view>
		<view class="" style="display: flex;justify-content: space-between;width: 70%;">
			<view class=""><text style="">湿度：{{sd}}</text></view>
			<view class=""><text style="">单位：{{wddw}}</text></view>

		</view>

		<!--蓝牙连接提醒-->
		<view>
			<u-toast ref="uToast" />
		</view>

		<view class="temp">
			<!-- <view class="div5" >
				<view class="div1">
					<view class="div7">
						<text style="color: red;">---</text>
						<text >左体表</text>
					</view>
					<view class="div8">
						<text>36.5</text>
					</view>
				</view>
				<view class="div2">
					<view class="div9">
						<text style="color: blue;">---</text>
						<text >右体表</text>
					</view>
					<view class="div10">
						<text>36.6</text>
					</view>
				</view>
			</view>
			<view class="div6">
				<view class="div3">
					<view class="div11">
						<text style="color: green;">---</text>
						<text >左腋下</text>
					</view>
					<view class="div12">
						<text>36.7</text>
					</view>
				</view>
				<view class="div4">
					<view class="div13">
						<text style="color: pink;">---</text>
						<text >右腋下</text>
					</view>
					<view class="div14">
						<text>36.8</text>
					</view>
				</view>
			</view> -->
			<qiun-data-charts type="line" :chartData="chartData2" />
		</view>
		<view class="btn">
			<view class="start" @click="xzms">
				<text>选择模式</text>
			</view>
		</view>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				serviceId:'',
				ble_info: '', //连接的蓝牙设备信息
				ble_services: '', //蓝牙设备服务信息
				ble_character: '', //蓝牙设备特征值
				blelink: {
					'deviceId': '',
					'connected': false
				}, //蓝牙设备连接状态
				index: '',
				imgUrl: '',
				cjsj: '',
				wddw: '摄氏度',
				sd: '59',
				chartData1: {

					categories: ["", "", "", "", "", "", "", "", "", "", ""],
					series: [{
						name: "左腋下",
						data: [35, 36, 31, 33, 13, 34, 35, 36, 31, 33, 13, 34]
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
				chartData2: {

					categories: ["300", "400", "500", "600", "700", "800"],
					series: [{
						name: "腋下温差",
						data: [2.2, 1.3, 1.1, 1.8, 1.3, 2.4]
					}, {
						name: "体表温差",
						data: [1.1, 1.5, 1.3, 1.4, 1.6, 0.8]
					}]
				}
			}
		},
		methods: {
			
			//获取蓝牙特征值
			getBLEDeviceCharacteristics(){
				var _this = this
				console.log("进入获取蓝牙特征值");
				//获取蓝牙特征值
				setTimeout(() => {
					console.log('deviceid'+ _this.ble_info
							.deviceId+'serviceid'+_this.serviceId);
					uni.getBLEDeviceCharacteristics({
						deviceId: _this.ble_info
							.deviceId,
						serviceId: _this
							.serviceId,
						success(res) {
							console.log(
								'获取蓝牙特征值');
							_this
								.ble_character =
								res
								.characteristics
							res.characteristics
								.forEach((
									item
								) => {
									console
										.log(
											'uuid' +
											item
											.uuid
										);
									if (item
										.uuid
										.indexOf(
											'8653000B'
										) !=
										-1
									) {
										_this
											.notifyBLECharacteristicValueChange(
												item
												.uuid
											)
				
									}
								})
						},fail(res) {
							console.log(res);
						}
					})
				
				
				}, 1000)
				
			},
			
			//数据异步上传
			notifyBLECharacteristicValueChange(characteristicId) {
				var _this = this
				uni.notifyBLECharacteristicValueChange({
					state: true, //启用notify功能
					deviceId: _this.ble_info.deviceId,
					serviceId: _this.serviceId,
					characteristicId: characteristicId,
					success(res) {
						
						console.log(res);
					},
					fail(res) {
						console.log(res);
					}
				})
			},
			//蓝牙连接提醒
			showToast(toast_info) {
				this.$refs.uToast.show({
					title: toast_info.title,
					type: toast_info.type,
					url: toast_info.url
				})
			},
			xzms() {
				uni.navigateTo({
					url: './index'
				})
			},

		},
		onShow() {
			var _this = this
			this.wddw = uni.getStorageSync('wddw')
			this.index = uni.getStorageSync('index')
			//判断首页状态图标
			if (this.index == 0) {
				this.imgUrl = '../../static/zaoshangxinglai.png'
			} else if (this.index == 1) {
				this.imgUrl = '../../static/bianhou.png'
			} else if (this.index == 2) {
				this.imgUrl = '../../static/kouku.png'
			} else if (this.index == 3) {
				this.imgUrl = '../../static/pao.png'
			} else if (this.index == 4) {
				this.imgUrl = '../../static/zou.png'
			} else if (this.index == 5) {
				this.imgUrl = '../../static/wo.png'
			} else if (this.index == 6) {
				this.imgUrl = '../../static/zuo.png'
			} else if (this.index == 7) {
				this.imgUrl = '../../static/shangzhiyundong.png'
			} else if (this.index == 8) {
				this.imgUrl = '../../static/shangxiazhiyundong.png'
			} else if (this.index == 9) {
				this.imgUrl = '../../static/jiang.png'
			} else if (this.index == 10) {
				this.imgUrl = '../../static/xie.png'
			} else if (this.index == 11) {
				this.imgUrl = '../../static/tingkan.png'
			} else if (this.index == 12) {
				this.imgUrl = '../../static/chi.png'
			} else if (this.index == 13) {
				this.imgUrl = '../../static/pilao.png'
			} else if (this.index == 14) {
				this.imgUrl = '../../static/youchou.png'
			} else if (this.index == 15) {
				this.imgUrl = '../../static/xingfen.png'
			}



			//数据上报
			//蓝牙连接操作
			//判断蓝牙有无连接设备
			//读取缓存数据
			uni.getStorage({
				key: 'link_ble_info',
				success: function(res) {
					//判断是否是初次连接
					if (res.data == null || res.data == '') {
						var toast_info = {
							'title': '请先连接蓝牙',
							'type': 'sucess',
							'url': '/pages/mine/bluetooth/bluetoothFind'
						}
						_this.showToast(toast_info)
					} else {
						_this.ble_info = res.data
						console.log('蓝牙连接信息');
						//console.log('蓝牙连接状态'+_this.blelink);

						//判断是否已连接
						//if (_this.blelink.connected == false) {
						//蓝牙未连接,根据id直接连接
						const ble_link =  uni.getStorageSync('ble_link')
												
								console.log('蓝牙连接信息'+ble_link.connected); 
								if (ble_link.connected == true) {
									//蓝牙已经连接,无需重复连接
									uni.openBluetoothAdapter({
										success() {
											//获取所有服务
											uni.getBLEDeviceServices({
												deviceId: _this
													.ble_info
													.deviceId,
												success(res) {
													_this
														.ble_services =
														res
														.services
												}
											})

											//获取蓝牙特征值
											setTimeout(() => {
												uni.getBLEDeviceCharacteristics({
													deviceId: res.data
														.deviceId,
													serviceId: _this
														.ble_services
														.serviceId,
													success(res) {
														console.log(
															'获取蓝牙特征值');
														_this
															.ble_character =
															res
															.characteristics
														res.characteristics
															.forEach((
																item
															) => {
																console
																	.log(
																		'uuid' +
																		item
																		.uuid
																	);
																if (item
																	.uuid
																	.indexOf(
																		'8653000B'
																	) !=
																	-1
																) {
																	_this
																		.notifyBLECharacteristicValueChange(
																			item
																			.uuid
																		)

																}
															})
													}
												})


											}, 1000)

										}
									})

									//蓝牙未连接,重新连接
								} else {
								
									uni.openBluetoothAdapter({
										success() {
											uni.createBLEConnection({
												deviceId: _this.ble_info.deviceId,
												timeout: 6000,
												fail(res) {
													console.log(res);

													var toast_info = {
														'title': '蓝牙连接失败,请重新选择设备',
														'type': 'sucess',
														'url': '/pages/mine/bluetooth/bluetoothFind'
													}
													_this.showToast(toast_info)
												},
												success() {
													//获取所有服务
													setTimeout(()=>{
														uni.getBLEDeviceServices({
															deviceId: _this
																.ble_info
																.deviceId,
																fail(res) {
																	console.log(res);
																},
															success(res) {
																console.log(res);
																_this
																	.ble_services =
																	res
																	.services
																		res.services.forEach((item)=>{
																			console.log("进入循环"+item.uuid);
																					if(item.uuid.indexOf("8653000A")!=-1){
																						_this.serviceId = item.uuid;
																						//进入特征
																						_this.getBLEDeviceCharacteristics()
																					}
																				})
																	
															}
														})
													},3000) 
													
												}
											})
											

										}
									})

								}
							
					


						//}

					}
				}

			})



			//蓝牙连接状态监听
			uni.onBLEConnectionStateChange(function(res) {
				_this.blelink = res
				// 该方法回调中可以用于处理连接意外断开等异常情况
				console.log('蓝牙:' + res.deviceId + '连接状态:' + res.connected)
				uni.setStorageSync('ble_link', res); 
			})
		},
		onLoad: function() {
			var _this = this
			
			uni.setStorageSync('ble_link', {
				
				
					'deviceId': '',
					'connected': false
				});
			var date = new Date()
			var year = date.getFullYear()
			var month = date.getMonth() + 1
			var day = date.getDate()
			if (month < 10) {
				month = '0' + month
			}
			var day = date.getDate()
			if (day < 10) {
				day = '0' + day
			}
			this.cjsj = year + '-' + month + '-' + day


		}
	}
</script>

<style lang="scss">
	.id {
		display: flex;
		justify-content: center;
		flex-direction: column;
		align-items: center;

		.info {
			display: flex;
			justify-content: center;
			// flex-direction: column;
			align-items: center;
		}

		.tj {
			display: flex;
			// flex-direction: column;
			align-items: center;
			margin-top: 10upx;
			width: 700upx;
			height: 500upx;
			border: 1upx solid #3F536E;
			border-radius: 30upx;
			box-shadow: darkgrey 0px 0px 2px 2px;
		}

		.temp {
			// display: flex;
			// justify-content: center;
			// align-items: center;
			margin-top: 20upx;
			width: 700upx;
			height: 400upx;
			border: 1upx solid #3F536E;
			border-radius: 30upx;
			box-shadow: darkgrey 0px 0px 2px 2px;

			.div5 {
				display: flex;
				// justify-content: space-between;
				width: 700upx;
				height: 200upx;
				border-bottom: 1upx solid darkgrey;

				.div1 {
					display: flex;
					flex-direction: column;
					justify-content: center;
					align-items: center;
					width: 350upx;
					height: 200upx;
					border-right: 1upx solid darkgrey;

					.div7,
					.div8 {
						font-size: 50upx;
					}
				}

				.div2 {
					display: flex;
					flex-direction: column;
					justify-content: center;
					align-items: center;
					width: 350upx;
					height: 200upx;

					.div9,
					.div10 {
						font-size: 50upx;
					}

				}
			}

			.div6 {
				display: flex;
				// justify-content: space-between;
				width: 700upx;
				height: 200upx;

				// border: 1upx solid #007AFF;
				.div3 {
					display: flex;
					flex-direction: column;
					justify-content: center;
					align-items: center;
					width: 350upx;
					height: 200upx;
					border-right: 1upx solid darkgrey;

					.div11,
					.div12 {
						font-size: 50upx;
					}
				}

				.div4 {
					display: flex;
					flex-direction: column;
					justify-content: center;
					align-items: center;
					width: 350upx;
					height: 200upx;

					.div13,
					.div14 {
						font-size: 50upx;
					}
				}
			}

		}

		.start {
			width: 200upx;
			margin-top: 30upx;
			height: 200upx;
			border: 1upx solid #000000;
			border-radius: 100upx;
			text-align: center;
			line-height: 200upx;
			background-color: #ff466e;
			color: #ffffff;
		}
	}
</style>
