<template>
	<view>
		<view class="cu-form-group">
			<view class="title">姓名:</view>
			<image src="../../static/nick.png" style="width: 50upx;height: 50upx;margin-left: 280upx;"></image>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">姓名:</view>
			<input  name="input" v-model="name"></input>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">性别:</view>
			<input  name="input" v-model="sex" ></input>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">年龄:</view>
			<input  name="input" v-model="age" ></input>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">身高:</view>
			<input  name="input" v-model="height" >cm</input>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">体重:</view>
			<input  name="input" v-model="weight" >kg</input>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">腰围:</view>
			<input  name="input" v-model="waist" >cm</input>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">电话:</view>
			<input  name="input" v-model="phone" ></input>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">邮件:</view>
			<input  name="input" v-model="mail" ></input>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">民族:</view>
			<input  name="input" v-model="nation" ></input>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">住址:</view>
			<input  name="input" v-model="address" ></input>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">联系人:</view>
			<input  name="input" v-model="contacts" style="margin-left: 370upx;"></input>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">联系人电话:</view>
			<input  name="input" v-model="contactsphone" style="margin-left: 310upx;"></input>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">过敏史:</view>
			<input  name="input" v-model="allergy" style="margin-left: 370upx;"></input>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">疾病诊断:</view>
			<input  name="input" v-model="diagnosis" style="margin-left: 370upx;"></input>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view>
			<u-radio-group  >
			<u-radio @change="radioChange" name='1'>服务协议及隐私政策告知</u-radio>
			</u-radio-group>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				name:'张三',
				sex:'男',
				age:'18',
				height:'180',
				weight:'70',
				waist:'70',
				phone:'15858888888',
				mail:'158322@qq.com',
				nation:'汉',
				address:'江苏',
				contacts:'李四',
				contactsphone:'15852288888',
				allergy:'无',
				diagnosis:'神经病'
			}
		},
		methods: {
			radioChange(e) {
				 console.log(e);
			},
			
		}
	}
</script>

<style>
	input {
		margin-left: 400upx;
	}
</style>
