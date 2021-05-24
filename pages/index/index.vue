<template>
	<view >
		<cg-swiper :swiperList="swiperList" @clickItem="clickItem"></cg-swiper>
		<u-input v-model="value" maxlength='40' type="textarea" border height="100"  placeholder='备注:'/>
		<view class="start" @click="back">
			<text >返回检测</text>
		</view>
	</view>
</template>

<script>
	import cgSwiper from '@/components/cg-swiper/cg-swiper.vue';
	export default {
		components: {
			cgSwiper,
		},
		data() {
			return {
				index:'',
				value:'',
				swiperList: [
					{
						index:0,
						text: '早上醒来',
						img: '../../static/img/早上醒来.png'
					},
					{
						index:1,
						text: '便后',
						img: '../../static/img/便后.png'
					},
					{
						index:2,
						text: '口苦',
						img: '../../static/img/口苦.png'
					},
					{
						index:3,
						text: '跑',
						img: '../../static/img/跑.png'
					},
					{
						index:4,
						text: '走',
						img: '../../static/img/走.png'
					},
					{
						index:5,
						text: '卧',
						img: '../../static/img/卧.png'
					},
					{
						index:6,
						text: '坐',
						img: '../../static/img/坐.png'
					},
					{
						index:7,
						text: '上肢运动',
						img: '../../static/img/上肢运动.png'
					},
					{
						index:8,
						text: '上下肢运动',
						img: '../../static/img/上下肢运动.png'
					},
					{
						index:9,
						text: '讲',
						img: '../../static/img/讲.png'
					},
					{
						index:10,
						text: '写',
						img: '../../static/img/写.png'
					},
					{
						index:11,
						text: '听,看',
						img: '../../static/img/听看.png'
					},
					{
						index:12,
						text: '吃',
						img: '../../static/img/吃.png'
					},
					{
						index:13,
						text: '疲劳',
						img: '../../static/img/疲劳.png'
					},
					{
						index:14,
						text: '忧愁',
						img: '../../static/img/忧愁.png'
					},
					{
						index:15,
						text: '喜悦',
						img: '../../static/img/兴奋.png'
					}
					
				]
			}
		},
		methods: {
			clickItem(item) {
				this.index = item.index
			},
			back(){
				uni.setStorageSync('index',this.index)
				uni.navigateTo({
					url:'./indexs'
				})
			}
			
		}
	}
</script>

<style>
	.start {
		width: 200upx;
		margin-left: 36%;
		margin-top: 50upx;
		height: 200upx;
		border: 1upx solid #000000;
		border-radius: 100upx;
		text-align: center;
		line-height: 200upx;
		background-color: #ff0000;
		color: #007AFF;
	}
</style>
