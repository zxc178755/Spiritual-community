<template>
	<view class="robot_con">
		<image src="../../static/robot.svg" mode="widthFix" @click="toChat"></image>
		<view :class="{word_con:true , show_word:isShowWord}">
			{{word?word:'I am here !'}}
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				word: '来和我聊天呀？',
				isShowWord: false
			}
		},
		created() {
			// let 
			setTimeout(() => {
				this.isShowWord = true
			}, 1100)
		},
		methods: {
			toChat() {
				console.log('去聊天')
				uni.navigateTo({
					url: '../../pages/chat/chat'
				})
			}
		}
	}
</script>

<style scoped>
	.robot_con {
		width: 145rpx;
		height: 176rpx;
		position: relative;
	}

	.robot_con image {
		width: 160rpx;
		position: absolute;
		bottom: 10rpx;
		right: -160rpx;
		transform: rotate(-15deg);
		animation: showRobot 0.7s 0.3s forwards;
	}

	.word_con {
		line-height: 40rpx;
		max-width: 500rpx;
		min-width: 200rpx;
		padding: 16rpx 20rpx;
		position: absolute;
		top: -10rpx;
		left: 6rpx;
		transform: translateX(-100%);
		background-color: #fff;
		border-radius: 10rpx;
		text-align: center;
		box-shadow: -4rpx 4rpx 8rpx 0 #dfdfdf;
		white-space: nowrap;
		opacity: 0;
		transition: all 0.5s;
	}

	.robot_con .show_word {
		opacity: 1;
	}

	.word_con::after {
		content: "";
		position: absolute;
		top: 100%;
		right: 0;
		border: 20rpx solid transparent;
		border-right: 25rpx solid #fff;
		transform: translate(0%, -50%);
	}

	@keyframes showRobot {
		from {
			right: -160rpx;
		}

		to {
			right: -26rpx;
		}
	}
</style>
