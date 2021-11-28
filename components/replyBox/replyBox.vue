<template>
	<view :class="{common_reply_input:true,hidden:!isInput}">
		<textarea auto-height v-model="value" class="input_area" :placeholder="placeholder" cursor-spacing="20"
			:show-confirm-bar="false" adjust-position :fixed = "true" />
		<text class="iconfont icon-send" @click="submit"></text>
	</view>
</template>

<script>
	export default {
		props: {
			isInput: {
				default: false,
				required: true
			}
		},
		created() {
			getApp().placeholderWatch(this.updataPlaceholder)
			getApp().objIdWatch(this.clearValue)
		},
		data() {
			return {
				value: '',
				placeholder: ''
			}
		},

		methods: {
			updataPlaceholder(placeholder) {
				this.placeholder = placeholder
			},
			clearValue() {
				this.value = ''
			},
			submit() {
				// 设置一下防抖
				if (!this.value.trim()) {
					uni.showToast({
						title: '输入不能为空',
						icon: 'none',
						duration: 800
					})
					return
				}
				let globalData = getApp().globalData
				console.log(globalData)
				let {
					type,
					objId,
					placeholder,
					commonId
				} = globalData.inputBoxProps
				if (type === 3) {
					console.log('类型：', type)
					console.log('目标id：', objId)
					console.log('commonid：', commonId)
					console.log('placeholder', placeholder)
					console.log('内容:', this.value)
					this.value = ''
					this.$emit('refresh', type, commonId)
					globalData.isInput = false
					return
				}
				console.log('类型：', type)
				console.log('目标id：', objId)
				console.log('placeholder', placeholder)
				console.log('内容:', this.value)
				this.value = ''
				// 通知更新
				this.$emit('refresh', type)
				// 
				globalData.isInput = false
			},
		}
	}
</script>

<style>
	.common_reply_input {
		width: 100vw;
		border-top: 2rpx solid #ccc;
		border-bottom: 2rpx solid #ccc;
		box-sizing: border-box;
		background-color: #fff;
		padding: 20rpx 30rpx;
		position: fixed;
		bottom: 0;
		left: 0;
		z-index: 99;
	}

	.hidden {
		transform: translateY(100%);
	}

	.common_reply_input .iconfont {
		color: #75c82b;
		font-size: 56rpx;
		padding: 0 10rpx;
		position: absolute;
		bottom: 34rpx;
		right: 20rpx;
	}

	.input_area {
		border: 1px solid blue;
		width: 570rpx;
		height: 60rpx;
		max-height: 180rpx !important;
		padding: 20rpx;
		border: 2rpx solid #ccc;
		border-radius: 16rpx;

		font-size: 30rpx;

	}
</style>
