<template>
	<view class="at_bottom" v-if="isAtBottom">
		到底了~
	</view>
</template>

<script>
	export default {
		props: {
			isAtBottom: {
				default: false,
				required: true
			}
		}
	}
</script>

<style>
	.at_bottom {
		width: 100%;
		text-align: center;
		margin-top: 12rpx;
		font-size: 30rpx;
		color: #757575;
		padding-bottom: 12rpx;
	}
</style>
