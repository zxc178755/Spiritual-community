<template>
	<view class="container">
		<view class="functional_area">
			<view class="left">
				<view class="test_fun" style="margin-bottom:20rpx;">
					<view class="title">测一测</view>
					<view class="fun_body">
						<image src="../../static/consult/test.png" :style="{
								width:'260rpx',
								height:'240rpx',
								display:'block',
								margin:'0 auto'
							}"></image>
						<view class="fun_text">
							心理压力测试
						</view>
					</view>
				</view>
				<view class="consult_fun" >
					<view class="title">想知道的都在这</view>
					<navigator class="fun_body" url="../consult/consult">
						<image src="../../static/consult/consult.png" :style="{
								width:'240rpx',
								height:'240rpx',
								display:'block',
								margin:'0 auto',
							}"></image>
						<view class="fun_text">
							咨询专区
						</view>
					</navigator>
				</view>
			</view>
			<view class="right">
				<view class="appoint_fun">
					<view class="title">心理预约</view>
					<view class="fun_body">
						<image src="../../static/consult/appoint.png" :style="{
								width:'300rpx',
								height:'360rpx',
								display:'block',
								margin:'0 auto',
							}"></image>
						<view class="fun_text" style="padding:34rpx 0;">
							进入预约
						</view>
					</view>
				</view>
				<image src="../../static/consult/hospital.png" class="hospital"></image>
			</view>
		</view>
	</view>
</template>

<script>
</script>

<style scoped>
	.functional_area {
		padding: 26rpx;
		background-color: var(--themeColor);
		border-bottom-left-radius: 30rpx;
		border-bottom-right-radius: 30rpx;
		display: flex;
		justify-content: space-between;
	}

	.left,
	.right {
		width: 340rpx;
		box-sizing: border-box;
	}

	.title {
		font-size: 32rpx;
		font-weight: bold;
		margin-bottom: 6rpx;
	}

	.fun_body {
		background-color: #fff;
		width: 100%;
		box-sizing: border-box;
		padding: 10rpx 34rpx;
		border-radius: 10rpx;
		box-shadow: 0 0 6rpx 0 #a8a8a8;
	}

	.fun_body:active {
		box-shadow: 0 0 10rpx 2rpx #55aaff;
	}

	.fun_text {
		font-size: 32rpx;
		font-weight: bold;
		text-align: center;
		padding: 6rpx 10rpx;
	}

	.hospital {
		display: block;
		width: 300rpx;
		height: 150rpx;
		padding-top: 58rpx;
		padding-left: 34rpx;
	}
</style>
