<template>
	<view class="" style="position: relative;">
		<swiper
			class="swiper"
			@change="swiperChange"
		>
			<swiper-item style="width: 100%;height: 360upx;">
				<view class="swiper-item" >
					<view class="swiper-item-view" v-for="(item, index) in swiperList" :key="index" @click="clickItem(item)" :class="{changeColor1: index==current,changeColor:index==8}">
						<image class="swiper-img" :src="item.img" ></image>
						<text class="text" style="" :class="{changeColor:index==8}">{{ item.text }}</text>
					</view>
				</view>
			</swiper-item>
		</swiper>
		</view>
	</view>
</template>

<script>
export default {
	name: 'cg-swiper',
	props: {
		// 滑动块视图容器
		swiperList: {
			type: Array,
			default: function() {
				return [];
			}
		},
		
	},
	data() {
		return {
			swiperCurrent: '',
			color:'',
			current:'100'
		};
	},
	methods: {
		swiperChange(e) {
			this.swiperCurrent = e.detail.current;
		},

		clickItem(item) {
			this.current = item.index
			this.$emit('clickItem', item);
		}
	}
};
</script>

<style lang="scss">
	
	
.swiper {
	margin-top: 10px;
	width: 100%;
	height: 1000upx;
	padding-top: 20upx;
}
.swiper-item {
	display: flex;
	flex-wrap: wrap;
}
.swiper-item-view {
	margin: 5upx;
	margin-bottom: 10upx;
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
	width: 23.8%;
	height: 220upx;
	border: 1upx solid #000000;
	border-radius: 10upx;
	background-color: #e0ffff;
	.text {
		font-weight: 800;
		font-size: 38upx;
	}
	.changeColor {
		/* background-color: #fffcc9; */
		font-size: 30upx;
	}
}
.changeColor1 {
		background-color: #ff0000;
	}
.swiper-img {
	width: 110upx;
	height: 120upx;
}

</style>
