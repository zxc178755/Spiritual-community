<template>
	<view class="essay_cards">
		<navigator class="card" v-for="(item,index) in essayList" :key="index"
			:url="`../../pages/essayDetail/essayDetail?id=${index}`">
			<view class="left_part">
				<view class="content">
					{{item.content}}
				</view>
				<view class="common_num">
					<text class="icon iconfont icon-message1-copy"></text>{{item.commonNum}}
				</view>
			</view>
			<image :src="item.ImgUrl" class="right_part"></image>
		</navigator>
		<AtBottom :isAtBottom="true" />
	</view>
</template>

<script>
	import AtBottom from '../atBottom/atBottom.vue'
	export default {
		components: {
			AtBottom
		},
		props: {
			type: {
				required: true,
				default: 0
			}
		},

		data() {
			return {
				essayList: [{
					content: '第一条文本的内容 ，这里只有一行',
					ImgUrl: 'https://tse2-mm.cn.bing.net/th/id/OIP-C.nW4Ig8K4Y3zKHHhKPwlTcgAAAA?w=262&h=180&c=7&r=0&o=5&dpr=1.1&pid=1.7',
					url: '',
					commonNum: 12
				}, {
					content: '文本的内容 ，这里有2行，文本的内容文本的内容 ',
					ImgUrl: 'https://tse3-mm.cn.bing.net/th/id/OIP-C.TSbuVrbu8Rn60eewBQvrGAHaEo?w=289&h=180&c=7&r=0&o=5&dpr=1.1&pid=1.7',
					url: '',
					commonNum: 20
				}, {
					content: '文本的内容 ，这里有2行，文本的内容文本的内容文本的内容',
					ImgUrl: 'https://tse3-mm.cn.bing.net/th/id/OIP-C.L04yP1_pCdFq1SuVfUhpkgHaDt?w=318&h=175&c=7&r=0&o=5&dpr=1.1&pid=1.7',
					url: '',
					commonNum: 13
				}],
				isAtBottom: false
			}
		}
	}
</script>

<style>
	.essay_cards {
		width: 640rpx;
		margin: 0 auto;
		margin-top: 10rpx;
		padding-bottom: 14rpx;
	}

	.card {
		height: 212rpxs;
		display: flex;
		margin-bottom: 30rpx;
		background-color: #ffffff;
		padding: 26rpx 14rpx;
		border-radius: 10rpx;
		box-shadow: 4rpx 4rpx 6rpx 0 rgba(170, 170, 170, 0.5);
	}

	.card .left_part {
		width: 372rpx;
	}

	.content {
		font-size: 30rpx;
		padding-right: 10rpx;
		color: #333333;
		font-weight: bold;
		text-overflow: ellipsis;
		display: -webkit-box;
		-webkit-box-orient: vertical;
		-webkit-line-clamp: 2;
		overflow: hidden;
	}

	.card .right_part {
		/* position: relative; */
		width: 240rpx;
		height: 160rpx;
		display: block;
		border-radius: 8rpx;
	}

	.common_num {
		margin-top: 40rpx;
		font-size: 26rpx;
		color: #555555;
		height: 40rpx;
		line-height: 40rpx;
	}

	.icon {
		padding: 0 8rpx;
		color: #000;
		font-size: 40rpx;
		position: relative;
		top: 2rpx;
	}
</style>
