<template>
	<view class="" style="position: relative;">
		<swiper
			class="swiper"
			@change="swiperChange"
		>
			<swiper-item style="width: 100%;height: 360upx;">
				<view class="swiper-item" >
					<view class="swiper-item-view" v-for="(item, index) in swiperList" :key="index" v-if="index < 20" @click="clickItem(item)">
						<image class="swiper-img" :src="item.img" ></image>
						<text>{{ item.text }}</text>
					</view>
				</view>
			</swiper-item>
			<!-- <block v-if="swiperList.length > 20">
				<swiper-item style="width: 100%;height: 360upx;">
					<view class="swiper-item">
						<view class="swiper-item-view" v-for="(item, index) in swiperList" :key="index" v-if="index > 19 && index < 30" @click="clickItem(item.item)">
							<image class="swiper-img" :src="item.img"></image>
							<text>{{ item.text }}</text>
						</view>
					</view>
				</swiper-item>
			</block> -->
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
			swiperCurrent: 0
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
