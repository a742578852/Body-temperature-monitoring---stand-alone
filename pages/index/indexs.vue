<template>
	
		<view id="main">
			<!--蓝色背景-->
			<view style="background-color: #4a5cd0;height: 700rpx;">
			<!--状态-->
			<view style="width: 75%; padding-top:30rpx;display: flex;justify-content: space-between;margin-left: 12%;">
				<view style="color: #FFFFFF;font-size: 30rpx;">状态: {{motion_state}}</view>
				<view style="color: #FFFFFF;font-size: 30rpx;">湿度: {{shidu}}</view>
			</view>
			<!--四个温度显示-->
			<view>
					<view style="display: flex;">
						<view style="margin-left: 37rpx; margin-top: 30rpx; background-color: #7885dc;height: 190rpx;width: 320rpx;border-radius: 50rpx 0 0 0;">
							<view style="margin-left: 30rpx;margin-top: 20rpx; color: #FFFFFF;">左体表(°C)</view>
							<view style="margin-top:50rpx;margin-left: 150rpx;color: #FFFFFF;font-size: 60rpx;">{{leftBody}}</view>
						</view>
						<view style="margin-left: 37rpx; margin-top: 30rpx; background-color: #7885dc;height: 190rpx;width: 320rpx;border-radius: 0 50rpx 0 0;">
							<view style="margin-left: 30rpx;margin-top: 20rpx; color: #FFFFFF;">右体表(°C)</view>
							<view style="margin-top:50rpx;margin-left: 150rpx;color: #FFFFFF;font-size: 60rpx;">{{rightBody}}</view>
						</view>
					</view>
				<view style="display: flex;">
					<view style="margin-left: 37rpx; margin-top: 30rpx; background-color: #7885dc;height: 190rpx;width: 320rpx;border-radius: 0 0 0 50rpx;">
						<view style="margin-left: 30rpx;margin-top: 20rpx; color: #FFFFFF;">左腋下(°C)</view>
						<view style="margin-top:50rpx;margin-left: 150rpx;color: #FFFFFF;font-size: 60rpx;">{{leftArmpit}}</view>
					</view>
					<view style="margin-left: 37rpx; margin-top: 30rpx; background-color: #7885dc;height: 190rpx;width: 320rpx;border-radius: 0 0 50rpx 0;">
						<view style="margin-left: 30rpx;margin-top: 20rpx; color: #FFFFFF;">右体表(°C)</view>
						<view style="margin-top:50rpx;margin-left: 150rpx;color: #FFFFFF;font-size: 60rpx;">{{rightArmpit}}</view>
					</view>
				</view>
			</view>
			<!--温差-->
			<view style="display: flex;">
				<view>
					<view style="color: #FFFFFF;margin-top: 20rpx;margin-left: 100rpx;">体表温差(°C)</view>
					<view style="color: #FFFFFF;margin-top: 20rpx;margin-left: 100rpx;font-size: 60rpx;">{{bodyDisparity}}</view>
				</view>
				<view>
					<view style="color: #FFFFFF;margin-top: 20rpx;margin-left: 240rpx;">腋下温差(°C)</view>
					<view style="color: #FFFFFF;margin-top: 20rpx;margin-left: 240rpx;font-size: 60rpx;">{{armpitDisparity}}</view>
				</view>
			</view>
			
			</view>
		

		<!--蓝牙连接提醒-->
		<view>
			<u-toast ref="uToast" />
		</view>
		<view class="topTj">
			<view class="wdtj" @click="dianji">温度</view>
			<view class="wctj" @click="dianjis">温差</view>
		</view>
		<view class="tj" v-if="state">
			<view class="charts-box">
			  <qiun-data-charts
			    type="demotype"
			    :chartData="chartData"
			    :loadingType="5"
			    :errorShow="false"
			    :inScrollView="true"
			    background="none"
			    :ontouch="true"
			  />
			</view>
		</view>
		
		<view class="tj" v-if="state1">
			<view class="charts-box">
			  <qiun-data-charts
			    type="demotype"
			    :chartData="chartData1"
			    :loadingType="5"
			    :errorShow="false"
			    :inScrollView="true"
			    background="none"
			    :ontouch="true"
			  />
			</view>
		</view>
		
		
		<!--返回监控按钮-->
		<view >
			<u-button @click="resType" shape="circle" size="medium"  :ripple="true" style="background-color:#4a5cd0 ;color: #FFFFFF;width: 80%;margin-left: 10%;">结束监控</u-button>
		</view>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				shidu:'',
				state:true,
				state1:false,
				leftBody:'',//左体表
				leftArmpit:'',//左腋下
				rightArmpit:'',//右腋下
				rightBody:'',//右体表
				bodyDisparity:'',//体表温差
				
				armpitDisparity:'',//腋下温差
				
				motion_state:'',
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
					series:[
						{
							"name": "左腋下",
							"data": []
						},
						{
							"name": "右腋下",
							"data": []
						},
						{
							"name": "左体表",
							"data": []
						},
						{
							"name": "右体表",
							"data": []
						},
					],
				},
				chartData1:{
					categories:[],
					series:[
						{
							"name": "腋下温差",
							"data": []
						},
						{
							"name": "体表温差",
							"data": []
						},
					],
				},
				historyData:[]
			}
		},
		methods: {
			dianji(){
				this.state = true
				this.state1 = false
			},
			dianjis(){
				this.state = false
				this.state1 = true
			},
			resType(){
				uni.navigateTo({
					url:'./index'
				})
			},
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
										  'rightBody':rightBody,'humidity':humidity,'electric':electric,'motion_state':_this.motion_state,
										  'date':date.getFullYear() + '-' + (date.getMonth() + 1) + '-' + date.getDate() + ' ' + date.getHours() + ':' + date.getMinutes() + ':' + date.getSeconds()}

										  var history = uni.getStorageSync("historyData") 
										  if(history == null || history == ''){
											  history = new Array()
										  }
										console.log(history);
										  history.unshift(data)
										  _this.historyData = history
										  _this.chartData.series[0].data=[]
										  _this.chartData.series[1].data=[]
										  _this.chartData.series[2].data=[]
										  _this.chartData.series[3].data=[]
										  _this.chartData.categories = []
										  
										  _this.chartData1.series[0].data=[]
										  _this.chartData1.series[1].data=[]
										  _this.chartData1.categories = []
										  //往统计图中放数据
										  for(var i = 0;i<5;i++){
											  _this.chartData.categories.push('')
											  _this.chartData.series[0].data.push(_this.historyData[i].leftArmpit)  
											  _this.chartData.series[1].data.push(_this.historyData[i].leftBody)
											  _this.chartData.series[2].data.push(_this.historyData[i].rightArmpit)
											  _this.chartData.series[3].data.push(_this.historyData[i].rightBody)
											  //温差数组
											  _this.chartData1.categories.push('')
											  _this.chartData1.series[0].data.push(Math.abs((_this.historyData[i].leftArmpit - _this.historyData[i].rightArmpit).toString().substring(0,5)))
											  _this.chartData1.series[1].data.push(Math.abs((_this.historyData[i].leftBody - _this.historyData[i].rightBody).toString().substring(0,5)))
										  }
											//左体表温度
											_this.leftBody = _this.historyData[0].leftBody
											//右体表温度
											_this.rightBody = _this.historyData[0].rightBody
											//左腋下温度
											_this.leftArmpit = _this.historyData[0].leftArmpit
											//右腋下温度
											_this.rightArmpit = _this.historyData[0].rightArmpit
											//体表温差
										  _this.bodyDisparity = Math.abs((_this.historyData[0].leftBody - _this.historyData[0].rightBody).toString().substring(0,5))
											//腋下温差
										  _this.armpitDisparity = Math.abs((_this.historyData[0].leftArmpit - _this.historyData[0].rightArmpit).toString().substring(0,5))
										  _this.shidu = _this.historyData[0].humidity

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
		},
		onShow() {
			var _this = this
			_this.wddw = uni.getStorageSync('wddw')
			_this.motion_state = uni.getStorageSync('motionState')
			
						
			
console.log('546464545');
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
											_this.ble_services =res.services
										
											res.services.forEach((item) => {
												console.log("进入循环" +item.uuid);
												if (item.uuid.indexOf("8653000A") !=-1) {
													_this.serviceId =item.uuid;
													//进入特征
													_this.getBLEDeviceCharacteristics()
												}
											})
											
										}
									})
									}
									}, 1000)

								
					
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
													deviceId: _this.ble_info.deviceId,
													fail(res) {
														console.log(res);
													},
													success(res) {
														console.log(res);
														_this.ble_services =res.services
														res.services.forEach((item) => {
															console.log("进入循环" +item.uuid);
															if (item.uuid.indexOf("8653000A") !=-1) {
																_this.serviceId =item.uuid;
																//进入特征
																_this.getBLEDeviceCharacteristics()
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
	#main {
		.tj {
			width: 100%;
			height: 650upx;
			/* 请根据需求修改图表容器尺寸，如果父容器没有高度图表则会显示异常 */
			.charts-box{
			  width: 100%;
			  height:300px;
			}
		}
		.topTj {
			margin-top: 20upx;
			margin-left: 30%;
			width: 40%;
			height: 60upx;
			display: flex;
			justify-content: space-between;
			.wdtj {
				text-align: center;
				height: 45upx;
				width: 85upx;
				border: 1upx solid #55aaff;
				border-radius: 20upx;
				background-color: #55aaff;
			}
			.wctj {
				text-align: center;
				height: 45upx;
				width: 85upx;
				border: 1upx solid #55aaff;
				border-radius: 20upx;
				background-color: #55aaff;
			}
		}
	}
.wrap {
		padding: 24rpx;
	}

	.u-row {
		margin: 40rpx 0;
	}

	.demo-layout {
		height: 80rpx;
		border-radius: 8rpx;
	}

	.bg-purple {
		background: #d3dce6;
	}

	.bg-purple-light {
		background: #e5e9f2;
	}

	.bg-purple-dark {
		background: #99a9bf;
	}
</style>

</style>
