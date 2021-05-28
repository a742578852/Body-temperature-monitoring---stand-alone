<template>
	<view >
		<cg-swiper :swiperList="swiperList" @clickItem="clickItem"></cg-swiper>
		<u-input  v-model="value" maxlength='40' type="textarea" border height="100" :auto-height='autoheight'  :placeholder='placeholder'/>
		<view class="starts">
			<view class="start" @click="back">
				<text>{{fhjc}}</text>
			</view>
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
				autoheight:true,
				placeholder:'备注:',
				fhjc:'返回检测',
				index:'',
				value:'',
				swiperList: [
					{
						index:0,
						text: '早上醒来',
						img: '../../static/zaoshangxinglai.png'
					},
					{
						index:1,
						text: '便后',
						img: '../../static/bianhou.png'
					},
					{
						index:2,
						text: '口苦',
						img: '../../static/kouku.png'
					},
					{
						index:3,
						text: '跑',
						img: '../../static/pao.png'
					},
					{
						index:4,
						text: '走',
						img: '../../static/zou.png'
					},
					{
						index:5,
						text: '卧',
						img: '../../static/wo.png'
					},
					{
						index:6,
						text: '坐',
						img: '../../static/zuo.png'
					},
					{
						index:7,
						text: '上肢运动',
						img: '../../static/shangzhiyundong.png'
					},
					{
						index:8,
						text: '上下肢运动',
						img: '../../static/shangxiazhiyundong.png'
					},
					{
						index:9,
						text: '讲',
						img: '../../static/jiang.png'
					},
					{
						index:10,
						text: '写',
						img: '../../static/xie.png'
					},
					{
						index:11,
						text: '听,看',
						img: '../../static/tingkan.png'
					},
					{
						index:12,
						text: '吃',
						img: '../../static/chi.png'
					},
					{
						index:13,
						text: '疲劳',
						img: '../../static/pilao.png'
					},
					{
						index:14,
						text: '忧愁',
						img: '../../static/youchou.png'
					},
					{
						index:15,
						text: '喜悦',
						img: '../../static/xingfen.png'
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
				uni.switchTab({
					url:'./indexs'
				})
			}
		},
		onShow() {
			var indexYy = uni.getStorageSync('indexYy')
			if(indexYy == 1){
				this.placeholder = 'remarks:'
				this.fhjc = 'Return detection'
				this.swiperList = [
					{
						index:0,
						text: 'get up',
						img: '../../static/zaoshangxinglai.png'
					},
					{
						index:1,
						text: 'After defecation',
						img: '../../static/bianhou.png'
					},
					{
						index:2,
						text: 'Bitter mouth',
						img: '../../static/kouku.png'
					},
					{
						index:3,
						text: 'run',
						img: '../../static/pao.png'
					},
					{
						index:4,
						text: 'go',
						img: '../../static/zou.png'
					},
					{
						index:5,
						text: 'Lie down',
						img: '../../static/wo.png'
					},
					{
						index:6,
						text: 'sit',
						img: '../../static/zuo.png'
					},
					{
						index:7,
						text: 'Upper limb movement',
						img: '../../static/shangzhiyundong.png'
					},
					{
						index:8,
						text: 'Whole body exercise',
						img: '../../static/shangxiazhiyundong.png'
					},
					{
						index:9,
						text: 'speak',
						img: '../../static/jiang.png'
					},
					{
						index:10,
						text: 'write',
						img: '../../static/xie.png'
					},
					{
						index:11,
						text: 'Listen, look',
						img: '../../static/tingkan.png'
					},
					{
						index:12,
						text: 'eat',
						img: '../../static/chi.png'
					},
					{
						index:13,
						text: 'fatigue',
						img: '../../static/pilao.png'
					},
					{
						index:14,
						text: 'Sorrow',
						img: '../../static/youchou.png'
					},
					{
						index:15,
						text: 'Joy',
						img: '../../static/xingfen.png'
					}
					
				]
			}
		}
	}
</script>

<style lang="scss">
	.starts {
		display: flex;
		flex-direction: column;
		align-items: center;
		// justify-content: space-between;
		.start {
			width: 210upx;
			margin-top: 30upx;
			height: 210upx;
			border: 1upx solid #000000;
			 border-radius: 100upx; 
			text-align: center;
			line-height: 210upx;
			background-color: #ff0000;
			color: #ffffff;
		}
	}
</style>
