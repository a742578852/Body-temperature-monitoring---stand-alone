<template>
	<view>
		<view class="" style="display: flex;align-items: center;justify-content: center;flex-direction: column;font-size: 50upx;">
			<image src="../../static/logo.png" style="width: 150upx;height: 150upx;"></image>
			<text>对称平衡</text>
		</view>
		<view class="" style="margin-top: 150upx;">
		<view class="cu-form-group" >
			<view class="title">版本:</view>
			<input  name="input" disabled>1.0.0</input>
		</view>
		<!-- <view class="cu-form-group">
			<view class="title">版权:</view>
			<input  name="input" disabled>所有者</input>
		</view> -->
		<view class="cu-form-group" @click="serve">
			<view class="title">服务协议:</view>
			<u-icon name="arrow-right" disabled></u-icon>
		</view>
		<view class="cu-form-group" @click="yinsi">
			<view class="title">隐私协议:</view>
			<u-icon name="arrow-right" disabled></u-icon>
		</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			//服务协议
			serve(){
				uni.navigateTo({
					url:'./server'
				})
			},
			//隐私协议
			yinsi(){
				uni.navigateTo({
					url:'./privacy'
				})
			}
		}
	}
</script>

<style>
	.cu-form-group {
		margin-bottom: 20upx
	}
</style>
