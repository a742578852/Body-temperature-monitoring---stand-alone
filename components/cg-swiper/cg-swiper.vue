<template>
	<view class="" style="position: relative;">
		<swiper
			class="swiper"
			@change="swiperChange"
		>
			<swiper-item style="width: 100%;height: 360upx;">
				<view class="swiper-item" >
					<view class="swiper-item-view" v-for="(item, index) in swiperList" :key="index" @click="clickItem(item)" :class="{changeColor:index==0, changeColor1: index==current}">
						<image class="swiper-img" :src="item.img" ></image>
						<text style="font-weight: 800;font-size: 38upx;">{{ item.text }}</text>
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
			swiperCurrent: 0,
			color:'',
			current:0
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

<style>
	.changeColor {
		background-color: #fffcc9;
	}
	.changeColor1 {
		background-color: #aaffff;
	}
.swiper {
	margin-top: 10px;
	width: 100%;
	height: 1370upx;
	padding-top: 20upx;
}
.swiper-item {
	display: flex;
	flex-wrap: wrap;
}
.swiper-item-view {
	margin-bottom: 10upx;
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
	width: 33%;
	height: 220upx;
	
}
.swiper-img {
	width: 110upx;
	height: 120upx;
}

</style>
