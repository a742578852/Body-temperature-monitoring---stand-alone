<template>
	<view>
		<u-toast ref="uToast" />
		<view class="cu-form-group" @click="chooseImage">
			<view class="title">头像:</view>
			<image :src="imgUrl" style="width: 50upx;height: 50upx;margin-left: 280upx;"></image>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">姓名:</view>
			<input name="input" v-model="name" maxlength="20"></input>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">性别:</view>
			<picker @change="bindPickerChange" :value="index" :range="arraySex" class="" style="width: 100%;">
				<view class="uni-input" style="width: 100%;">{{arraySex[index]}}</view>
			</picker>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">年龄:</view>
			<input name="input" v-model="age" type="number"></input>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">身高:</view>
			<input name="input" v-model="height" type="number">cm</input>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">体重:</view>
			<input name="input" v-model="weight" type="number">kg</input>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">腰围:</view>
			<input name="input" v-model="waist" type="number">cm</input>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">电话:</view>
			<input name="input" v-model="phone" type="number"></input>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">邮箱:</view>
			<input name="input" v-model="mail" @blur="checkEmail(mail)"></input>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">民族:</view>
			<input name="input" v-model="nation" type="text"></input>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">住址:</view>
			<input name="input" v-model="address"></input>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">联系人:</view>
			<input name="input" v-model="contacts" style="margin-left: 370upx;" type="text"></input>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">联系人电话:</view>
			<input name="input" v-model="contactsphone" style="margin-left: 310upx;" type="number"></input>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">过敏史:</view>
			<input name="input" v-model="allergy" style="margin-left: 370upx;"></input>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">疾病诊断:</view>
			<input name="input" v-model="diagnosis" style="margin-left: 370upx;"></input>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<!-- <button type="primary" @click='btn' :disabled="false">保存</button> -->
		<button type="default" @click="btn" style="background-color: #FBBD08;"  :disabled="isTrue">保存</button>
		<view style="text-align: center;height: 50upx;">
			<u-radio-group>
				<u-radio @change="radioChange" name='1'></u-radio>
			</u-radio-group>
			<text @click="yinsi">服务协议及隐私政策告知</text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				index: 0,
				imgUrl: '',
				isTrue:true,
				arraySex: ['男', '女'],
				name: '张三',
				sex: '男',
				age: '18',
				height: '180',
				weight: '70',
				waist: '70',
				phone: '15858888888',
				mail: '158322@qq.com',
				nation: '汉',
				address: '江苏',
				contacts: '李四',
				contactsphone: '15852288888',
				allergy: '无',
				diagnosis: '神经病'
			}
		},
		methods: {
			radioChange(e) {
				if(e==1){
					this.isTrue = false
				}
			},
			bindPickerChange(e) {
				console.log('picker发送选择改变，携带值为', e.target.value)
				this.index = e.target.value
			},
			chooseImage() {
				uni.chooseImage({
					count: 1,
					success: res => {
						this.imgUrl = res.tempFilePaths[0]
						console.log(this.imgUrl);
						uni.setStorageSync('touxiang', this.imgUrl)
					}
				})
			},
			showToast() {
				this.$refs.uToast.show({
					title: '邮箱格式错误'
				})
			},
			yinsi(){
				uni.navigateTo({
					url:'../about/privacy'
				})
			},
			//判断邮箱
			checkEmail(str) {
				var re = /^[A-Za-z\d]+([-_.][A-Za-z\d]+)*@([A-Za-z\d]+[-.])+[A-Za-z\d]{2,4}$/;
				if (!re.test(str)) {
					this.showToast()
					this.mail = ''
				} 
			},
			btn(){
				console.log('000');
				uni.switchTab({
					url:'../mine/mine'
				})
			},
		},
		onLoad() {
			this.imgUrl = uni.getStorageSync('touxiang')
		}
	}
</script>

<style>
	input {
		margin-left: 400upx;
	}

	.uni-input {
		margin-left: 400upx;
	}
</style>
