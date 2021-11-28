<template>
	<view class='avator_con' @click="ClikcAvator">
		<image src="../../../static/avator.png" class="avator"></image>
	</view>
</template>

<script>
	export default {
		name: 'Avator',
		methods: {
			ClikcAvator() {
				this.$emit("tabAvator")
				// 检查登陆什么的
			}
		}
	}
</script>

<style>
	.avator_con {
		width: 70rpx;
		height: 70rpx;
		margin: 0 12rpx 0 24rpx;
		padding: 10rpx 10rpx 0 10rpx;
	}

	.avator {
		display: block;
		width: 100%;
		height: 100%;
		border-radius: 50%;
	}
</style>
