<template>
	<view class="container">
		<view class="login_bag">
			<image src="../../static/consult/hospital.png" mode="widthFix"></image>
		</view>
		<view class="login_box">
			<!-- 			<view class="welcome">
				Welcome
			</view> -->
			<view class="name item">
				<view class="label">
					用户名
				</view><input @focus="nameInputFocus" @blur="nameInputBlur" type="text" v-model="userName"
					placeholder="请输入姓名" :style="{
						borderColor:nameInputBorderColor
					}" />
				<view class="alert">
					{{nameAlert}}
				</view>
			</view>
			<view class="id item">
				<view class="label">
					学号
				</view><input @focus="idInputFocus" @blur="idInputBlur" type="text" v-model="userId" placeholder="请输入学号"
					:style="{
						borderColor:idInputBorderColor
					}" />
				<view class="alert">
					{{idAlert}}
				</view>
			</view>
			<view class="submit button" @click="submit">
				登陆
			</view>
		</view>
		<view class="clause_rule">登陆后代表您同意 <text class="clause" @click="openPrivacyClause">《隐私保护条款》</text>
		</view>
		<Privacy @hiddenPrivacy="hiddenPrivacy" v-if="isShowPrivacyClause" />
	</view>
</template>

<script>
	import Privacy from '../../components/privacy/privacy.vue'
	export default {
		components: {
			Privacy
		},
		data() {
			return {
				userName: '',
				userId: '',
				isShowPrivacyClause: false,
				nameInputBorderColor: '#f7f7f7',
				idInputBorderColor: '#f7f7f7',
				nameAlert: '',
				idAlert: ''
			}
		},
		methods: {
			submit() {
				if (!this.userName.trim() || !this.userId.trim()) {
					this.idInputBlur()
					this.nameInputBlur()
					return
				}
			},
			openPrivacyClause() {
				this.isShowPrivacyClause = true
			},
			hiddenPrivacy() {
				this.isShowPrivacyClause = false
			},
			nameInputFocus() {
				this.nameInputBorderColor = '#5fa8d3'
			},
			nameInputBlur() {
				if (!this.userName.trim()) {
					this.nameInputBorderColor = "#f15f5f"
					this.nameAlert = "姓名不能为空"
				} else {
					this.nameInputBorderColor = "#f7f7f7"
					this.nameAlert = ""
				}
			},
			idInputFocus() {
				this.idInputBorderColor = '#5fa8d3'
			},
			idInputBlur() {
				if (!this.userId.trim()) {
					this.idInputBorderColor = "#f15f5f"
					this.idAlert = "学号不能为空"
				} else {
					this.idInputBorderColor = "#f7f7f7"
					this.idAlert = ""
				}
			}
		}

	}
</script>

<style scoped>
	.login_bag {
		height: 30vh;
		background-color: var(--themeColor);
		display: flex;
		align-items: center;
		justify-content: center;
		box-shadow: 0 3rpx 10rpx var(--themeColor);
	}

	.login_bag image {
		width: 60%;
		display: block;
	}

	.login_box {
		width: 640rpx;
		height: 600rpx;
		background: linear-gradient(transparent 1%, #fff 16%, #fff);
		box-shadow: 0 4rpx 6rpx 0 #bfbfbf;
		padding: 30rpx;
		padding-top: 160rpx;
		box-sizing: border-box;
		border-radius: 8rpx;
		margin: 0 auto;
		transform: translateY(-15%);
		font-size: 32rpx;
	}

	.item {
		display: flex;
		height: 100rpx;
		margin: 0 auto;
		justify-content: center;
		margin-bottom: 40rpx;
		position: relative;
	}

	.label {
		width: 110rpx;
		height: 78rpx;
		line-height: 78rpx;
		text-align: justify;
		margin-right: 20rpx;
	}

	.label::after {
		display: inline-block;
		width: 100%;
		content: "";
	}

	input {
		width: 340rpx;
		height: 70rpx;
		line-height: 70rpx;
		padding: 4rpx 20rpx;
		border-radius: 8rpx;
		background-color: #f7f7f7;
		border: 2rpx solid #f7f7f7;
	}

	.alert {
		position: absolute;
		width: 380rpx;
		right: 36rpx;
		height: 30rpx;
		font-size: 24rpx;
		bottom: -16rpx;
		color: #f15f5f;
	}


	.submit {
		width: 300rpx;
		height: 80rpx;
		line-height: 80rpx;
		color: #fff;
		font-size: 34rpx;
		font-weight: bold;
		background-color: #5fa8d3;
		border-radius: 10rpx;
		margin: 30rpx auto;
	}

	.clause_rule {
		width: 80%;
		transform: translateY(-60rpx);
		text-align: center;
		margin: 0 auto;
	}

	.clause {
		color: #5fa8d3;
		padding: 0 10rpx;
	}

	/* 	.welcome{
		font-size: 40rpx;
		text-align: center;
		color: #1e72cc;
		font-weight: bolder;
		padding:30rpx 0;
	} */
</style>
