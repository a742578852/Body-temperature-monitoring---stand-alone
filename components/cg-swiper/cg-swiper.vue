<template>
	<view class="" style="position: relative;">
		<swiper
			class="swiper"
			@change="swiperChange"
		>
			<swiper-item style="width: 100%;height: 360upx;">
				<view class="swiper-item" >
					<view class="swiper-item-view" v-for="(item, index) in swiperList" :key="index" @click="clickItem(item)" >
						<image class="swiper-img" :src="item.img" :class="{changeColor1: index==current}"></image>
						<text class="text" style="" :class="{changeColor:index==8 || index == 7 || index == 0}">{{ item.text }}</text>
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
	
	.swiper-img {
		width: 120upx;
		height: 120upx;
		border: 1upx solid #cfcfcf;
		border-radius: 20upx;
		// background-color: #ffffff;
		padding: 20upx;
	}
	.text {
		// font-weight: 800;
		font-size: 38upx;
	}
	.changeColor {
		/* background-color: #fffcc9; */
		font-size: 32upx;
	}
}
.changeColor1 {
		background-color: #4a5cd0;
	}
.swiper-img {
	width: 110upx;
	height: 120upx;
}

</style>
