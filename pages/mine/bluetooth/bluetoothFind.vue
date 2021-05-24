<template>
	<view>
		<!--文字-->
		<view>
			<view style="text-align: center;margin-top: 40upx;">
				<text style="font-size: 50upx;">{{search}}</text>
			</view>
			<view style="text-align: center;margin-top: 20upx;">
				<text style="">{{remind}}</text>
			</view>
		</view>
		<!--波浪特效-->
		<div class="container">
			<div class="wave ripple danger">
				<div class="circle"></div>
				<div class="circle"></div>
				<div class="circle"></div>
				<div class="content">
					<i class="fa fa-bell"></i>
				</div>
			</div>
			<view style="position: relative ;top:-400upx;right: -180upx;">
				<image src="../../../static/tiwenji.png" style="width: 120upx;height: 270upx;"></image>
			</view>

		</div>

		<!--设备列表-->
		<view style="margin-bottom: 60rpx;margin-left: 25rpx;margin-right: 25rpx;">
			<view v-for="(item,i) in bleList" style="width: 100%;height: 160rpx;background-color: #DDDDDD;border-radius: 25rpx;">
				<view style="text-align: center;margin-top: 30rpx;color: #000000;font-size: 60rpx;padding-top: 36rpx;">
				{{item.name}}
				</view>
			</view>
		</view>

		<!--按钮-->
		<view>
			<u-button  @click="bluetoothIsOpen()" shape="circle" size="default" style="color: #F37B1D;width: 500upx;margin-bottom: 50rpx;">
				{{binding}}
			</u-button>
		</view>

		<!--提醒弹出框-->
		<view>
			<div>
				<u-popup v-model="popubShow" mode="bottom" height="auto" border-radius="15">
					<view style="text-align: center;font-size: 35upx;margin-top: 30upx;">{{remindeon}}</view>
					<view style="font-size: 32upx;margin-top: 30upx;color: #8799A3;text-align: center;">
						{{remindeon_one}}
					</view>
					<view style="margin-top: 30upx;">
						<button @click="popubShow = false">{{bu_cancel}}</button>
						<button @click="cancel()">{{bu_set}}</button>
					</view>
				</u-popup>
			</div>
		</view>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				search: '',
				binding: '',
				remind: '',
				remindeon: '',
				remindeon_one: '',
				bu_cancel: '',
				bu_set: '',
				popubShow: false,
				bleList:[],//蓝牙设备列表
			}
		},
		methods: {


			//跳转到手机设置页
			cancel() {
				var main = plus.android.runtimeMainActivity();
				var Intent = plus.android.importClass("android.content.Intent");
				var mIntent = new Intent('android.settings.SETTINGS');
				main.startActivity(mIntent);
			},
			//蓝牙搜索 
			startBluetoothDeviceDiscovery() {
				//在页面显示的时候判断是都已经初始化完成蓝牙适配器若成功，则开始查找设备
				let self = this;
				setTimeout(function() {
					
						console.log("开始搜寻智能设备");
						uni.startBluetoothDevicesDiscovery({
							success: res => {
								self.onBluetoothDeviceFound();
							},
							fail: res => {
								console.log("查找设备失败!");
								uni.showToast({
									icon: "none",
									title: "查找设备失败！",
									duration: 3000
								})
							}
						});
					
				}, 300);
			},
			/**
			 * 停止搜索蓝牙设备 
			 */
			stopBluetoothDevicesDiscovery() {
				uni.stopBluetoothDevicesDiscovery({
					success: e => {
						console.log('停止搜索蓝牙设备:' + e.errMsg);
					},
					fail: e => {
						console.log('停止搜索蓝牙设备失败，错误码：' + e.errCode);
					}
				});
			},
			/**
			 * 发现外围设备
			 */
			onBluetoothDeviceFound() {
				console.log("监听寻找新设备");
				// this.getBluetoothDevices();
				uni.onBluetoothDeviceFound(devices => {
					console.log('开始监听寻找到新设备的事件');
					this.getBluetoothDevices();
				});
			},
			/**
			 * 获取在蓝牙模块生效期间所有已发现的蓝牙设备。包括已经和本机处于连接状态的设备。
			 */
			getBluetoothDevices() {
				var _this = this
				console.log("获取蓝牙设备");
				uni.getBluetoothDevices({
					success: res => {
						console.log('获取蓝牙设备成功:' + res.errMsg);
						console.log(res)
						_this.bleList = res.devices
						console.log('数据是是'+_this.bleList.get(0).name);
					}
				});
			},
			//连接蓝牙设备
			

		},

		onShow() {
			var _this = this
		

			//判断中英文
			this.search = "正在搜索";
			this.binding = "暂不绑定"
			this.remind = "请将体温计贴近手机"
			this.remindeon = "请开启蓝牙服务"
			this.remindeon_one = "开启后即可搜索和连接设备"
			this.bu_cancel = "取消"
			this.bu_set = "去设置"

			//蓝牙设置

			//蓝牙搜索
			uni.openBluetoothAdapter({
				success() {

					//蓝牙初始化成功,开始搜索
					_this.startBluetoothDeviceDiscovery()

				},
				fail() {
					//蓝牙初始化失败,弹窗提示打开蓝牙
					_this.popubShow = true
				}

			})
		//蓝牙状态监听
		uni.onBluetoothAdapterStateChange(function(res) {
			if (res.available == true) {
				_this.popubShow = false
			} else {
				_this.popubShow = true
			}
		})

		},

	}
</script>


<style>
	body {
		margin: 0;
	}

	.container {
		position: relative;
		top: 80upx;
		left: 20%;
		width: 40%;
		height: 40%;
	}

	.spliter {
		width: 100%;
		height: 20px;
	}

	/************以下为具体实现************/

	.wave {
		position: relative;
		width: 200px;
		height: 200px;
		text-align: center;
		line-height: 100px;
		font-size: 28px;
	}

	.wave .circle {
		position: absolute;
		border-radius: 50%;
		opacity: 0;

	}

	/* 波纹效果 */
	.wave.ripple .circle {
		width: calc(100% - 6px);
		/* 减去边框的大小 */
		height: calc(100% - 6px);
		/* 减去边框的大小 */
		border: 2px solid #2986ff;
	}

	.wave.ripple .circle:first-child {
		animation: circle-opacity 2s infinite;
	}

	.wave.ripple .circle:nth-child(2) {
		animation: circle-opacity 2s infinite;
		animation-delay: .3s;
	}

	.wave.ripple .circle:nth-child(3) {
		animation: circle-opacity 2s infinite;
		animation-delay: .6s;
	}

	.wave.ripple.danger {
		color: blule;
	}

	.wave.ripple.danger .circle {
		border-color: blule;
	}

	.wave.ripple.warning {
		color: orange;
	}

	.wave.ripple.warning .circle {
		border-color: orange;
	}

	/* 波动效果 */
	.wave.solid .circle {
		width: 100%;
		height: 100%;
		background: #fff;
	}

	.wave.solid .circle:first-child {
		animation: circle-opacity 2s infinite;
	}

	.wave.solid.danger {
		color: red;
	}

	.wave.solid.danger .circle {
		background: red;
	}

	.wave.solid.warning {
		color: orange;
	}

	.wave.solid.warning .circle {
		background: orange;
	}

	@keyframes circle-opacity {
		from {
			opacity: 1;
			transform: scale(0);
		}

		to {
			opacity: 0;
			transform: scale(1);
		}
	}
</style>
