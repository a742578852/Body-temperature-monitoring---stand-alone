<template>
	<view>
		<u-toast ref="uToast" />
		<view class="cu-form-group" @click="chooseImage">
			<view class="title">{{tx}}:</view>
			<image :src="imgUrl" style="width: 50upx;height: 50upx;margin-left: 280upx;"></image>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">{{xm}}:</view>
			<input name="input" v-model="name" maxlength="20"></input>
			<!-- <u-icon name="arrow-right"></u-icon> -->
		</view>
		<view class="cu-form-group">
			<view class="title">{{xb}}:</view>
			<picker @change="bindPickerChange" :value="index" :range="arraySex" class="" style="width: 100%;">
				<view class="uni-input" style="width: 100%;">{{arraySex[index]}}</view>
			</picker>
			<u-icon name="arrow-right"></u-icon>
		</view>
		<view class="cu-form-group">
			<view class="title">{{nl}}:</view>
			<input name="input" v-model="age" type="number"></input>
			<!-- <u-icon name="arrow-right"></u-icon> -->
		</view>
		<view class="cu-form-group">
			<view class="title">{{sg}}:</view>
			<input name="input" v-model="height" type="number">厘米</input>
			<!-- <u-icon name="arrow-right"></u-icon> -->
		</view>
		<view class="cu-form-group">
			<view class="title">{{tz}}:</view>
			<input name="input" v-model="weight" type="number">千克</input>
			<!-- <u-icon name="arrow-right"></u-icon> -->
		</view>
		<view class="cu-form-group">
			<view class="title">{{yw}}:</view>
			<input name="input" v-model="waist" type="number">厘米</input>
			<!-- <u-icon name="arrow-right"></u-icon> -->
		</view>
		<view class="cu-form-group">
			<view class="title">{{dh}}:</view>
			<input name="input" v-model="phone" type="number"></input>
			<!-- <u-icon name="arrow-right"></u-icon> -->
		</view>
		<view class="cu-form-group">
			<view class="title">{{yx}}:</view>
			<input name="input" v-model="mail" @blur="checkEmail(mail)"></input>
			<!-- <u-icon name="arrow-right"></u-icon> -->
		</view>
		<view class="cu-form-group">
			<view class="title">{{mz}}:</view>
			<input name="input" v-model="nation" type="text"></input>
			<!-- <u-icon name="arrow-right"></u-icon> -->
		</view>
		<view class="cu-form-group">
			<view class="title">{{zz}}:</view>
			<input name="input" v-model="address"></input>
			<!-- <u-icon name="arrow-right"></u-icon> -->
		</view>
		<view class="cu-form-group">
			<view class="title">{{lxr}}:</view>
			<input name="input" v-model="contacts"  type="text"></input>
			<!-- <u-icon name="arrow-right"></u-icon> -->
		</view>
		<view class="cu-form-group">
			<view class="title">{{lxrdh}}:</view>
			<input name="input" v-model="contactsphone"  type="number"></input>
			<!-- <u-icon name="arrow-right"></u-icon> -->
		</view>
		<view class="cu-form-group">
			<view class="title">{{gms}}:</view>
			<input name="input" v-model="allergy" ></input>
			<!-- <u-icon name="arrow-right"></u-icon> -->
		</view>
		<view class="cu-form-group">
			<view class="title">{{jbzd}}:</view>
			<input name="input" v-model="diagnosis" ></input>
			<!-- <u-icon name="arrow-right"></u-icon> -->
		</view>
		<!-- <button type="primary" @click='btn' :disabled="false">保存</button> -->
		<button type="default" @click="btn" style="background-color: #4a5cd0;"  >{{bc}}</button>
		<!-- <view style="text-align: center;height: 50upx;">
			<u-radio-group>
				<u-radio @change="radioChange" name='1'></u-radio>
			</u-radio-group>
			<text @click="yinsi">{{gz}}</text>
		</view> -->
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
				name: '',
				sex: '',
				age: '',
				height: '',
				weight: '',
				waist: '',
				phone: '',
				mail: '',
				nation: '',
				address: '',
				contacts: '',
				contactsphone: '',
				allergy: '',
				diagnosis: '',
				tx:'头像',
				xm:'姓名',
				xb:'性别',
				nl:'年龄',
				sg:'身高',
				tz:'体重',
				yw:'腰围',
				dh:'电话',
				yx:'邮箱',
				mz:'民族',
				zz:'住址',
				lxr:'联系人',
				lxrdh:'联系人电话',
				gms:'过敏史',
				jbzd:'疾病诊断',
				bc:'保存',
				gz:'服务协议及隐私政策告知'
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
				uni.setStorageSync('sexindex',e.target.value)
				this.index = e.target.value
			},
			//上传头像
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
			//隐私协议
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
				uni.setStorageSync("name",this.name)
				if(this.index==0){
					uni.setStorageSync('sex','男')
				}else if(this.index==1){
					uni.setStorageSync('sex','女')
				}else{
					uni.setStorageSync('sex','男')
				}
				uni.setStorageSync("age",this.age)
				uni.setStorageSync("height",this.height)
				uni.setStorageSync("weight",this.weight)
				uni.setStorageSync("waist",this.waist)
				uni.setStorageSync("phone",this.phone)
				uni.setStorageSync("mail",this.mail)
				uni.setStorageSync("nation",this.nation)
				uni.setStorageSync("address",this.address)
				uni.setStorageSync("contacts",this.contacts)
				uni.setStorageSync("contactsphone",this.contactsphone)
				uni.setStorageSync("allergy",this.allergy)
				uni.setStorageSync("diagnosis",this.diagnosis)
				uni.switchTab({
					url:'../mine/mine'
				})
			},
		},
		onLoad() {
			//获取头像地址
			this.imgUrl = uni.getStorageSync('touxiang')
		},
		onShow() {
			this.name = uni.getStorageSync('name')
			if(uni.getStorageSync('sexindex')==0){
				this.index = 0
			}else if(uni.getStorageSync('sexindex')==1){
				this.index = 1
			}
			this.age = uni.getStorageSync('age')
			this.height = uni.getStorageSync('height')
			this.weight = uni.getStorageSync('weight')
			this.waist = uni.getStorageSync('waist')
			this.phone = uni.getStorageSync('phone')
			this.mail = uni.getStorageSync('mail')
			this.nation = uni.getStorageSync('nation')
			this.address = uni.getStorageSync('address')
			this.contacts = uni.getStorageSync('contacts')
			this.contactsphone = uni.getStorageSync('contactsphone')
			this.allergy = uni.getStorageSync('allergy')
			this.diagnosis = uni.getStorageSync('diagnosis')
			//中英文切换
			var indexYy = uni.getStorageSync('indexYy')
			if(indexYy == 1){
				this.tx = 'head portrait'
				this.xm = 'name'
				this.xb = 'Gender'
				this.nl = 'age'
				this.sg = 'height'
				this.tz = 'weight'
				this.yw = 'the waist'
				this.dh = 'Telephone'
				this.yx = 'email'
				this.mz = 'nation'
				this.zz = 'address'
				this.lxr = 'contacts'
				this.lxrdh = 'Contact number'
				this.gms = 'Allergic history'
				this.jbzd = 'disease diagnosis'
				this.bc = 'save'
				this.gz = 'Service notification'
			}
		}
	}
</script>

<style>
	input {
		/* margin-left: 400upx; */
		/* float: right; */
	}

	.uni-input {
		/* margin-left: 400upx; */
	}
</style>
