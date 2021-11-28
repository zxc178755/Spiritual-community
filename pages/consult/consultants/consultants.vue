<template>
	<view class="consultants">
		<navigator class="consultant" v-for="(item) in consultantList" :key="item.id"
			url="../../pages/consultantInfo/consultantInfo">
			<image :src="item.avator"></image>
			<view class="info">
				<view class="name">
					{{item.name}}
				</view>
				<view class="position">
					{{item.position}}
				</view>
				<view class="good_at">
					<text class="good_at_text">擅长：</text>
					<text class="good_at_item" v-for="(arritem,index) in item.goodAt" :key="index">{{arritem}}</text>
				</view>
			</view>
			<text class="iconfont icon-arrow1"></text>
		</navigator>
	</view>
</template>

<script>
	export default {
		props: {
			sortway: {
				default: 0
			},
			type: {
				default: '学习'
			},
			city: {
				default: '广州'
			}
		},
		data() {
			return {
				consultantList: [{
					id: 1,
					avator: '../../../static/avator.png',
					name: '咨询师名称',
					position: '高级心理咨询师',
					goodAt: ['个人成长', '职场心理']
				}, {
					id: 2,
					avator: '../../../static/avator.png',
					name: '咨询师名称',
					position: '高级心理咨询师',
					goodAt: ['个人成长', '职场心理']
				}, {
					id: 1,
					avator: '../../../static/avator.png',
					name: '咨询师名称',
					position: '高级心理咨询师',
					goodAt: ['个人成长', '职场心理']
				}, {
					id: 1,
					avator: '../../../static/avator.png',
					name: '咨询师名称',
					position: '高级心理咨询师',
					goodAt: ['个人成长', '职场心理']
				}, {
					id: 1,
					avator: '../../../static/avator.png',
					name: '咨询师名称',
					position: '高级心理咨询师',
					goodAt: ['个人成长', '职场心理']
				}, {
					id: 1,
					avator: '../../../static/avator.png',
					name: '咨询师名称',
					position: '高级心理咨询师',
					goodAt: ['个人成长', '职场心理']
				}, ]
			}
		}
	}
</script>

<style>
	.consultants {
		padding: 60rpx;
		padding-top: 10rpx;
	}

	.consultant {
		border: 2rpx solid #ccc;
		border-radius: 14rpx;
		background-color: #fff;
		box-shadow: 0 0 4rpx 0 #ccc;
		display: flex;
		align-items: center;
		width: 600rpx;
		height: 160rpx;
		padding: 20rpx;
		padding-right: 10rpx;
		margin-bottom: 20rpx;
	}

	.consultant image {
		width: 130rpx;
		height: 130rpx;
		border-radius: 50%;
		margin-right: 20rpx;
	}

	.info {
		width: 420rpx;
		display: flex;
		flex-direction: column;
		justify-content: space-around;
		font-size: 28rpx;
	}

	.name {
		font-size: 32rpx;
	}

	.position {
		color: #5fa8d3;
		padding: 10rpx 0;
	}

	.good_at_text {
		color: #5fa8d3;
	}

	.good_at_item {
		padding-right: 10rpx;
	}

	.iconfont {
		font-size: 38rpx;
	}
</style>
