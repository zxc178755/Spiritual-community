<template>
	<view class="privacy_window" @click.stop="hidden">
		<view class="box">
			<view class="privicy_info" @click.stop="()=>{}">
				<view class="tile">
					用户隐私政策：
				</view>
				<view class="content">
					<rich-text :nodes="nodes"></rich-text>
				</view>
			</view>
			<view class="" :style="{width:'100%'}">
				<view class="Iknow button fr">
					我了解了
				</view>
			</view>

		</view>
	</view>
</template>

<script>
	import {
		text
	} from './privicy.js'
	export default {
		data() {
			return {
				nodes: text
			}
		},
		methods: {
			hidden() {
				this.$emit('hiddenPrivacy')
			}
		}
	}
</script>

<style scoped>
	.privacy_window {
		position: fixed;
		top: 0;
		left: 0;
		width: 100vw;
		height: 100vh;
		background-color: rgba(0, 0, 0, 0.1);
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.box {
		width: 600rpx;
		border: 2rpx solid #ccc;
		border-radius: 10rpx;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		background-color: #fff;
		padding: 30rpx;
	}

	.tile {
		font-size: 32rpx;
		color: #5fa8d3;
		font-weight: bold;
		margin-bottom: 20rpx;
	}

	.content {
		height: 700rpx;
		border: 2rpx solid #ccc;
		padding: 20rpx;
		overflow-y: scroll;
		border-radius: 10rpx;
	}

	.Iknow {
		width: 200rpx;
		height: 70rpx;
		line-height: 70rpx;
		color: #fff;
		background-color: #5fa8d3;
		font-size: 32rpx;
		font-weight: bold;
		border-radius: 10rpx;
		margin-top: 28rpx;
	}
</style>
