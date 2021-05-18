<template>
	<view >
		<cg-swiper :swiperList="swiperList" @clickItem="clickItem"></cg-swiper>
		<view style="width: 50%;margin-left: 25%;margin-bottom: 20upx;">
			<image src="../../static/logo.png" style="height: 400upx;border-radius: 200upx;"></image>
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
				swiperList: [
					{
						index:0,
						text: '卧',
						img: '../../static/logo.png'
					},
					{
						index:1,
						text: '坐',
						img: '../../static/logo.png'
					},
					{
						index:2,
						text: '走',
						img: '../../static/logo.png'
					},
					{
						index:3,
						text: '跑',
						img: '../../static/logo.png'
					},
					{
						index:4,
						text: '上肢运动',
						img: '../../static/logo.png'
					},
					{
						index:5,
						text: '上下肢运动',
						img: '../../static/logo.png'
					},
					{
						index:6,
						text: '吃',
						img: '../../static/logo.png'
					},
					{
						index:7,
						text: '写',
						img: '../../static/logo.png'
					},
					{
						index:8,
						text: '跑',
						img: '../../static/logo.png'
					},
					{
						index:9,
						text: '早上醒来',
						img: '../../static/logo.png'
					},
					{
						index:10,
						text: '忧愁',
						img: '../../static/logo.png'
					},
					{
						index:11,
						text: '口苦',
						img: '../../static/logo.png'
					},
					{
						index:12,
						text: '喜悦',
						img: '../../static/logo.png'
					},
					{
						index:13,
						text: '疲劳',
						img: '../../static/logo.png'
					},
					{
						index:14,
						text: '听,看',
						img: '../../static/logo.png'
					},
					{
						index:15,
						text: '便后',
						img: '../../static/logo.png'
					}
					
				]
			}
		},
		methods: {
			clickItem(item) {
				console.log(item.index);
			}
		}
	}
</script>

<style>

</style>
