<template>
	<view class="essay_list">
		<navigator class="essay_item" v-for="(item) in essayList" :key="item.essayId"
			:url="`../../pages/essayDetail/essayDetail?id=${item.essayId}`">
			<view class="essay_title">
				{{item.title}}
			</view>
			<template v-if="item.imgSrc">
				<image :src="item.imgSrc" mode="widthFix"></image>
			</template>
			<view class="hot_common">
				<view class="hot_common_text">
					热评
				</view>
				<view class="content_area">
					<view class="content">
						<text class="user_name">{{item.commontor}}：</text>
						{{item.commont}}
					</view>

					<view class="like">
						<text class="iconfont icon-aixin"></text>
						<text>{{item.likeNum}}</text>
					</view>
				</view>
			</view>
		</navigator>
	</view>
</template>

<script>
	export default {
		props: {
			type: {
				default: 0,
				required: true
			},
			sortway: {
				default: 0
			}
		},
		data() {
			return {
				essayList: [{
					title: '时间总是不够用，怎么办？时间总是不够用，怎么办？时间总是不够用，怎么办？时间总是不够用，怎么办？时间总是不够用，怎么办？',
					// imgSrc: 'https://tse3-mm.cn.bing.net/th/id/OIP-C.bK7B4oEMB0zxctmPgoAFbwHaEK?w=306&h=180&c=7&r=0&o=5&pid=1.7',
					commontor: '匿名用户aa01',
					commont: '这是一段热评这是一段热评这是一段热评这是一段热评这是一段热评是一段热评是一段热评',
					likeNum: '100',
					essayId: 0
				}, {
					title: '时间总是不够用，怎么办？时间总是不够用，怎么办？时间总是不够用，怎么办？时间总是不够用，怎么办？时间总是不够用，怎么办？',
					imgSrc: 'https://tse2-mm.cn.bing.net/th/id/OIP-C.nW4Ig8K4Y3zKHHhKPwlTcgAAAA?w=262&h=180&c=7&r=0&o=5&dpr=1.1&pid=1.7',
					commontor: '匿名用户aa01',
					commont: '这是一段热评这是一段热评这是一段热评这是一段热评这是一段热评是一段热评是一段热评',
					likeNum: '100',
					essayId: 1
				}, {
					title: '时间总是不够用，怎么办？时间总是不够用，怎么办？时间总是不够用，怎么办？时间总是不够用，怎么办？时间总是不够用，怎么办？',
					imgSrc: 'https://tse2-mm.cn.bing.net/th/id/OIP-C.nW4Ig8K4Y3zKHHhKPwlTcgAAAA?w=262&h=180&c=7&r=0&o=5&dpr=1.1&pid=1.7',
					commontor: '匿名用户aa01',
					commont: '这是一段热评这是一段热评这是一段热评这是一段热评这是一段热评是一段热评是一段热评',
					likeNum: '100',
					essayId: 2
				}]
			}
		},
		created() {
			console.log(this.type, this.sortway)
			// 加载文章
		}
	}
</script>

<style scoped>
	.essay_item {
		margin-bottom: 20rpx;
		padding: 26rpx;
		background-color: #fff;
		box-shadow: 0 4rpx 4rpx 0 #ccc;
	}

	.essay_title {
		font-size: 32rpx;
		font-weight: bold;
		text-overflow: ellipsis;
		display: -webkit-box;
		-webkit-box-orient: vertical;
		-webkit-line-clamp: 2;
		overflow: hidden;
	}

	.essay_item image {
		max-height: 260rpx;
		border-radius: 8rpx;
		max-width: 680rpx;
		margin-top: 20rpx;
	}

	.hot_common {
		background-color: #f2f2f2;
		border-radius: 4rpx;
		padding: 10rpx;
		margin-top: 20rpx;
	}

	.hot_common_text {
		color: red;
	}

	.content_area {
		display: flex;
		padding: 10rpx 0;
	}

	.content {
		flex: 4;
		text-overflow: ellipsis;
		display: -webkit-box;
		-webkit-box-orient: vertical;
		-webkit-line-clamp: 2;
		overflow: hidden;
	}

	.user_name {
		color: #7f7f7f;
		padding-right: 6rpx;
	}

	.like {
		flex: 1;
		text-align: center;
		padding-top: 20rpx;
		color: #7f7f7f;
	}

	.like .iconfont {
		font-size: 40rpx;
		padding-right: 4rpx;
		position: relative;
		top: 3rpx;
	}
</style>
