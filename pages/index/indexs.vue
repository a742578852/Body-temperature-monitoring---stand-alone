<template>
	
		<view >
			<!--蓝色背景-->
			<view style="background-color: #4a5cd0;height: 500rpx;">
			<!--状态-->
			<view style="padding-top:150rpx ;">
				<view>状态</view>
				
			</view>
			</view>
		

		<!--蓝牙连接提醒-->
		<view>
			<u-toast ref="uToast" />
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
				serviceId: '',
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
				chartData:{
					categories:[],
					series:[],
				},
				historyData:[]
			}
		},
		methods: {
			//获取蓝牙特征值
			getBLEDeviceCharacteristics() {
				
				//16进制转成10进制
				function hex2int(hex) {
				    var len = hex.length, a = new Array(len), code;
				    for (var i = 0; i < len; i++) {
				        code = hex.charCodeAt(i);
				        if (48<=code && code < 58) {
				            code -= 48;
				        } else {
				            code = (code & 0xdf) - 65 + 10;
				        }
				        a[i] = code;
				    }
				     
				    return a.reduce(function(acc, c) {
				        acc = 16 * acc + c;
				        return acc;
				    }, 0);
				}
				
				//转码16进制
				function ab2hex(buffer) {
				  const hexArr = Array.prototype.map.call(
				    new Uint8Array(buffer),
				    function (bit) {
				      return ('00' + bit.toString(16)).slice(-2)
				    }
				  )
				  return hexArr.join('')
				}
				
				var _this = this
				console.log("进入获取蓝牙特征值");
				//获取蓝牙特征值
				setTimeout(() => {
					console.log('deviceid' + _this.ble_info
						.deviceId + 'serviceid' + _this.serviceId);
					uni.getBLEDeviceCharacteristics({
						deviceId: _this.ble_info.deviceId,
						serviceId: _this.serviceId,
						success(res) {
							console.log('获取蓝牙特征值');
							_this.ble_character =res.characteristics
							res.characteristics.forEach((item) => {
									console.log('uuid' +item.uuid);
									if (item.uuid.indexOf('8653000B') !=-1) {
										console.log('id是'+item.uuid);
										console.log(item.properties);
										_this.notifyBLECharacteristicValueChange(item.uuid)
										uni.onBLECharacteristicValueChange(function (res) {
										  console.log(`characteristic ${res.characteristicId} has changed, now is ${res.value}`)
										  console.log(ab2hex(res.value))
										
										  //数据解析
										  var linData = ab2hex(res.value)
										  //获取左腋下
										  var leftArmpit = hex2int(linData.substring(2,4))+'.'+(linData.substring(4,6))
										  //获取左体表
										  var leftBody = hex2int(linData.substring(6,8))+'.'+(linData.substring(8,10))
										//获取右腋下
										  var rightArmpit = hex2int(linData.substring(10,12))+'.'+(linData.substring(12,14))
										//获取右体表
										  var rightBody = hex2int(linData.substring(14,16))+'.'+(linData.substring(16,18))
										  //获取湿度
										  var humidity = hex2int(linData.substring(18,20))
										  //获取电量
										  var electric = hex2int(linData.substring(20,22))
										  //存入缓存
										  var date = new Date()
										  var data = {'leftArmpit':leftArmpit,'leftBody':leftBody,'rightArmpit':rightArmpit,
										  'rightBody':rightBody,'humidity':humidity,'electric':electric,
										  'date':date.getFullYear() + '-' + (date.getMonth() + 1) + '-' + date.getDate() + ' ' + date.getHours() + ':' + date.getMinutes() + ':' + date.getSeconds()}

										  var history = uni.getStorageSync("historyData") 
										  if(history == null || history == ''){
											  history = new Array()
										  }
										
										  history.push(data)
										  _this.historyData = history
											
										  uni.setStorageSync('historyData',_this.historyData)
										  
										})

									}
								})
						},
						fail(res) {
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
						const ble_link = uni.getStorageSync('ble_link')

						console.log('蓝牙连接信息' + ble_link.connected);
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
											setTimeout(() => {
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
														res.services.forEach((
															item) => {
															console
																.log(
																	"进入循环" +
																	item
																	.uuid
																	);
															if (item
																.uuid
																.indexOf(
																	"8653000A"
																	) !=
																-1) {
																_this
																	.serviceId =
																	item
																	.uuid;
																//进入特征
																_this
																	.getBLEDeviceCharacteristics()
															}
														})

													}
												})
											}, 3000)

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
				var toast_info = {
					'title': '蓝牙已断开,请重新连接',
					'type': 'sucess',
					'url': '/pages/mine/bluetooth/bluetoothFind'
				}
				if(res.connected == false){
					_this.showToast(toast_info)
				}
				
			
			})
			
			//特征值监听
			uni.onBLECharacteristicValueChange(function (characteristic) {
			  console.log('characteristic value comed:', ab2hex(characteristic.value))
			})
		},
		onLoad: function() {
			var _this = this
			uni.setStorageSync('ble_link', {
				'deviceId': '',
				'connected': false
			});
			
		}
	}
</script>

<style lang="scss">


</style>
