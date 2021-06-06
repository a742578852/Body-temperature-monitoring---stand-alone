<template>
	<view>
		<cg-swiper :swiperList="swiperList" @clickItem="clickItem"></cg-swiper>
		<u-input v-model="value" maxlength='40' type="textarea" border height="200" placeholder='备注:' />
		<view class="start" @click="back">
			<text>确认</text>
		</view>
		<!--蓝牙连接提醒-->
		
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
				ble_info:'',//蓝牙连接信息
				index: '',
				value: '',
				swiperList: [{
						index: 0,
						text: '早上醒来',
						img: '../../static/zaoshangxinglai.png'
					},
					{
						index: 1,
						text: '便后',
						img: '../../static/bianhou.png'
					},
					{
						index: 2,
						text: '口苦',
						img: '../../static/kouku.png'
					},
					{
						index: 3,
						text: '跑',
						img: '../../static/pao.png'
					},
					{
						index: 4,
						text: '走',
						img: '../../static/zou.png'
					},
					{
						index: 5,
						text: '卧',
						img: '../../static/wo.png'
					},
					{
						index: 6,
						text: '坐',
						img: '../../static/zuo.png'
					},
					{
						index: 7,
						text: '上肢运动',
						img: '../../static/shangzhiyundong.png'
					},
					{
						index: 8,
						text: '上下肢运动',
						img: '../../static/shangxiazhiyundong.png'
					},
					{
						index: 9,
						text: '讲',
						img: '../../static/jiang.png'
					},
					{
						index: 10,
						text: '写',
						img: '../../static/xie.png'
					},
					{
						index: 11,
						text: '听,看',
						img: '../../static/tingkan.png'
					},
					{
						index: 12,
						text: '吃',
						img: '../../static/chi.png'
					},
					{
						index: 13,
						text: '疲劳',
						img: '../../static/pilao.png'
					},
					{
						index: 14,
						text: '忧愁',
						img: '../../static/youchou.png'
					},
					{
						index: 15,
						text: '喜悦',
						img: '../../static/xingfen.png'
					}

				]
			}
		},
		methods: {
			
			clickItem(item) {
				this.index = item.text
			},
			back() {
				uni.setStorageSync('motionState', this.index)
				uni.setStorageSync('remarks',this.value)
				uni.switchTab({
					url: './indexs'
				})
			}

		},
		
	}
</script>

<style>
	.start {
		width: 80%;
		margin-left: 10%;
		margin-top: 30upx;
		margin-bottom: 30upx;
		height: 80upx;
		border: 1upx solid #000000;
		border-radius: 30upx;
		text-align: center;
		line-height: 80upx;
		background-color: #8aecff;
		color: #1606ff;
	}
</style>
