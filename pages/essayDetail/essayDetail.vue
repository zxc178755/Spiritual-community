<template>
	<view class="essay_detail_con">
		<!-- 标题 -->
		<view class="essay_title">
			我是标题！一个有内涵的标题！
		</view>
		<!-- 关键字 -->
		<KeyWords :keywordsList="keywordsList" :isHasTitle="false" :isColor="true" />
		<!-- 文章主体 -->
		<view class="body_content">
			<rich-text :nodes="nodes"></rich-text>
		</view>
		<!-- 工具bar -->
		<view class="tools_bar">
			<view class="tool" @click="toCommon">
				<text class="iconfont icon-message1-copy"></text>
				评论
			</view>
			<view class="tool" @click="tabStore">
				<text :class="'iconfont '+(isStore?'icon-shoucang1':'icon-shoucang-copy')"></text>
				收藏
			</view>
		</view>
		<!-- 评论 -->
		<view class="sort_bar_con">
			<view class="reply_title">
				评论列表
			</view>
			<SortwayBar @changeSortway="changeSortway" />
		</view>
		<!-- 评论 -->
		<Commons :essayId="essayId" :_isInput="isInput"></Commons>
		<!-- 是否在底部 -->
		<AtBottm :isAtBottom="true" />
	</view>
</template>
<script>
	import HTMLParser from '../../utils/html-parser.js'
	import KeyWords from '../../components/keyWords/keyWords.vue'
	import SortwayBar from '../../components/sortwayBar/sortwayBar.vue'
	import Commons from './commons/commons.vue'
	import AtBottm from '../../components/atBottom/atBottom.vue'

	export default {
		components: {
			KeyWords,
			SortwayBar,
			Commons,
			AtBottm
		},
		data() {
			return {
				nodes: '',
				keywordsList: ['代码', '头发', '选择'],
				stop: false,
				isStore: false
			}
		},

		onLoad(e) {
			this.nodes = HTMLParser(uni.getStorageSync('essay1'))
			console.log(e.id)
			if (!e.id) {
				console.log('文章ID出错')
				return
			}
			this.essayId = e.id
			console.log('文章Id是', e.id)
			// API for essayDetail 。

			// 考虑是否要在文章请求回来后再调用请求，请求评论数据。
		},
		methods: {
			changeSortway(e) {
				console.log(e)
			},
			toCommon(data) {
				// 设置一下防抖
				let globalData = getApp().globalData
				let inputBoxProps = getApp().globalData.inputBoxProps
				inputBoxProps.placeholder = '评论文章...'
				inputBoxProps.type = 1
				inputBoxProps.objId = this.essayId
				globalData.isInput = true
			},
			tabStore() {
				// 设置一下防抖
				this.isStore = !this.isStore
			},
		},
		onPageScroll() {
			if (this.stop) {
				setTimeout(() => {
					this.stop = false
				}, 200)
				return
			}
			this.stop = true
			getApp().globalData.isInput = false
		},
	}
</script>

<style scoped>
	.essay_detail_con {
		width: 100vw;
		background-color: #f2f2f2;
	}

	.essay_title {
		font-size: 32rpx;
		font-weight: bold;
		background-color: #fff;
		width: 100vw;
		box-sizing: border-box;
		padding: 24rpx 30rpx;
		margin-bottom: 20rpx;
	}

	.body_content {
		width: 700rpx;
		margin: 0 auto;
		box-sizing: border-box;
		min-height: 300rpx;
		padding: 20rpx 30rpx;
		font-size: 32rpx;
	}

	.rich_img {
		width: 90%;
		margin: 0 auto;
	}

	.sort_bar_con {
		height: 80rpx;
		padding: 20rpx;
		padding-left: 20rpx;
		background-color: #fff;
		box-sizing: border-box;
		display: flex;
		justify-content: space-between;
		align-items: center;
		border-top: 2rpx solid #ccc;
		border-bottom: 2rpx solid #ccc;
		margin-bottom: 20rpx;
	}

	.reply_title {
		color: #4d4d4d;
	}

	.tools_bar {
		display: flex;
		align-items: center;
		border-top: 2rpx dotted #ccc;
		margin-top: 10rpx;
		padding: 4rpx 0;
	}

	.tool {
		padding: 10rpx;
		margin-left: 30rpx;
	}

	.tool .iconfont {
		font-size: 40rpx;
		position: relative;
		top: 3rpx;
		padding-right: 6rpx;
	}

	.icon-shoucang1 {
		color: #599ec6;
		font-weight: bold;
	}

	.icon-message1-copy {
		font-size: 50rpx;
		font-weight: bold;
	}
</style>
