<template>
	<view class="" style="position: relative;">
		<swiper
			class="swiper"
			@change="swiperChange"
		>
			<swiper-item style="width: 100%;height: 360upx;">
				<view class="swiper-item" >
					<view class="swiper-item-view" v-for="(item, index) in swiperList" :key="index" @click="clickItem(item)" :class="{changeColor:index==0}">
						<image class="swiper-img" :src="item.img" ></image>
						<text >{{ item.text }}</text>
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
			color:''
		};
	},
	methods: {
		swiperChange(e) {
			this.swiperCurrent = e.detail.current;
		},

		clickItem(item) {
			this.$emit('clickItem', item);
		}
	}
};
</script>

<style>
	.changeColor {
		background-color: #ffcd93;
	}
.swiper {
	margin-top: 10px;
	width: 100%;
	height: 700upx;
	padding-top: 20upx;
}
.swiper-item {
	display: flex;
	flex-wrap: wrap;
}
.swiper-item-view {
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
	width: 25%;
	height: 170upx;
	
}
.swiper-img {
	width: 100upx;
	height: 100upx;
}

</style>
