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
			
			<view>
				
			</view>
			
			<!--按钮-->
			<view>
				<u-button shape="circle" size="default" style="color: #F37B1D;width: 500upx;">{{binding}}</u-button>
			</view>
			
			<!--提醒弹出框-->
			<view>
					<u-popup v-model="popubShow" mode = "bottom" height = "auto" border-radius = "15">
						<view style="text-align: center;font-size: 35upx;margin-top: 30upx;">{{remindeon}}</view>
						<view style="font-size: 32upx;margin-top: 30upx;color: #8799A3;text-align: center;">{{remindeon_one}}</view>
						<view style="margin-top: 30upx;">
							<button @click="popubShow = false">{{bu_cancel}}</button>
							<button >{{bu_set}}</button>
						</view>
					</u-popup>
					
				</view>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				search:'',
				binding:'',
				remind:'',
				remindeon:'',
				remindeon_one:'',
				bu_cancel:'',
				bu_set:'',
				popubShow:false
			}
		},
		methods: {
			cancel(){
				
			},
			//判断蓝牙是否打开
			bluetoothIsOpen(){
				//蓝牙搜索
				uni.openBluetoothAdapter({
					complete(res) {
						console.log(res.errCode)
						//蓝牙未打开 提示用户打开
						if(res.errCode == 10001){
							this.popubShow = true
						}
					
					},
					
				})
			}
		},
		onShow() {
			//判断中英文
			this.search = "正在搜索";
			this.binding = "暂不绑定"
			this.remind = "请将体温计贴近手机"
			this.remindeon = "请开启蓝牙服务"
			this.remindeon_one = "开启后即可搜索和连接设备"
			this.bu_cancel = "取消"
			this.bu_set = "去设置"
			
			this.bluetoothIsOpen()
		}
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
			    width: calc(100% - 6px); /* 减去边框的大小 */
	    		height: calc(100% - 6px);/* 减去边框的大小 */
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
			.wave.solid .circle{
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
	 
			.wave.solid.danger .circle{
				background: red;
			}
			
			.wave.solid.warning {
				color: orange;
			}
	 
			.wave.solid.warning .circle{
				background: orange;
			}
	 
			@keyframes circle-opacity{
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
