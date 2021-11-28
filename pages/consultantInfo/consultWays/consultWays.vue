<template>
	<view class="consult_ways">
		<view class="title">
			咨询方式
		</view>
		<view class="min_buttons clearfix">
			<view class="consult_by_phone fl">
				<text class="iconfont icon-yuyin_"></text>
				语音咨询
			</view>
			<view class="consult_by_phone fr">
				<text class="iconfont icon-shipin"></text>
				视频咨询
			</view>
		</view>
		<view class="big_buttons">
			<view class="consult_by_face">
				<text class="iconfont icon-huiyishi" :style="{fontWeight:'normal'}"></text>
				面对面咨询
			</view>
		</view>
		<view class="toConsult fr">
			立即咨询
		</view>
	</view>
</template>

<script>
</script>

<style scoped>
	.consult_ways {
		background-color: #b1ddfe;
		height: 400rpx;
		border-top-left-radius: 30rpx;
		border-top-right-radius: 30rpx;
		margin-top: 34rpx;
		padding: 20rpx 30rpx;
		color: #6baed6;
		font-weight: bold;
	}

	.title {
		text-align: center;
		font-size: 32rpx;
		font-weight: bold;
	}

	.iconfont {
		color: #3a9ced;
		font-size: 50rpx;
		padding-right: 20rpx;
	}

	.min_buttons {
		width: 600rpx;
		margin: 0 auto;
		margin-top: 20rpx;
	}


	.consult_by_phone {
		width: 280rpx;
		height: 100rpx;
		display: flex;
		align-items: center;
		justify-content: center;
		border: 2rpx solid #ccc;
		border-radius: 8rpx;
		background-color: #fff;
	}

	.big_buttons {
		width: 600rpx;
		margin: 0 auto;
		margin-top: 30rpx;
	}

	.consult_by_face {
		height: 100rpx;
		justify-content: center;
		display: flex;
		align-items: center;
		border: 2rpx solid #ccc;
		border-radius: 8rpx;
		background-color: #fff;
	}

	.toConsult {
		width: 240rpx;
		height: 70rpx;
		background-color: #20e3b2;
		border-radius: 30rpx;
		text-align: center;
		line-height: 70rpx;
		color: #fff;
		font-size: 32rpx;
		margin-top: 24rpx;
	}
</style>
