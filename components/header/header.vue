<template>
	<view class='header_con'>
		<slot></slot>
		<slot></slot>
		<slot></slot>
	</view>
</template>

<script>
	export default {
		name: 'Header',
		components: {},
		methods: {}
	}
</script>

<style scoped>
	.header_con {
		display: flex;
		align-items: center;
		position: fixed;
		top: 0;
		z-index: 99;
		background-color: var(--themeColor);
		width: 100vw;
		height: 100rpx;
		border-bottom-left-radius: 30rpx;
		border-bottom-right-radius: 30rpx;
	}
</style>
