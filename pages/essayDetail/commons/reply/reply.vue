<template>
	<view class="replys_con">
		<view class="reply_item clearfix" v-for="(item,index) in replyList" :key="item.respondentId">
			<view class="avator_con fl">
			</view>
			<view class="reply_info fr">
				<view class="name_and_time">
					<view class="name">
						{{item.respondentName}}<text class="reply">回复</text>{{item.beresponcedName}}
					</view>
					<view class="time">
						{{item.createTime[0]}} <text class="clock">{{item.createTime[1]}}</text>
					</view>
				</view>
				<view class="content_and_like clearfix">
					<view class="content fl">
						{{item.content}}
					</view>
					<view class="like fr" @click="tabLike(index)">
						<text :class="'iconfont '+(item.isLike?'icon-aixin1':'icon-aixin')"></text>
						{{item.likeNum}}
					</view>
				</view>
				<view class="reply_iner" @click="toReply(index)">
					<text class="iconfont icon-message1-copy"></text>
					回复
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			commonId: {
				required: true
			},
			isUpdate: {
				default: false,
				required: true
			}
		},
		watch: {
			commonId(e) {
				console.log('回复获取commonId', e)
				// 根据评论 Id 和用户名获取相关回复信息
			},
			isUpdate(e) {
				if (e) {
					this.refresh()
				}
			}
		},
		created() {
			console.log('回复获取commonId', this.commonId)
		},
		data() {
			return {
				replyList: [{
					respondentId: 1,
					respondentName: 'a001匿名用户',
					beresponcedName: '001匿名用户',
					createTime: ['2021-09-18', '11:30'],
					content: '生活就是猫吃鱼，狗吃肉，奥特曼打小怪兽！生活就是猫吃鱼，狗吃肉，奥特曼打小怪兽！',
					isLike: true,
					likeNum: 21
				}, {
					respondentId: 2,
					respondentName: 'a001匿名用户',
					beresponcedName: '001匿名用户',
					createTime: ['2021-09-18', '11:30'],
					content: '生活就是猫吃鱼，狗吃肉，奥特曼打小怪兽！生活就是猫吃鱼，狗吃肉，奥特曼打小怪兽！',
					isLike: true,
					likeNum: 20
				}, {
					respondentId: 3,
					respondentName: 'c001匿名用户',
					beresponcedName: '001匿名用户',
					createTime: ['2021-09-18', '11:30'],
					content: '生活就是猫吃鱼，狗吃肉，奥特曼打小怪兽！生活就是猫吃鱼，狗吃肉，奥特曼打小怪兽！',
					isLike: false,
					likeNum: 20
				}],
			}
		},
		methods: {
			toReply(index) {
				let placeholder = '回复' + this.replyList[index].respondentName,
					type = 3, // 回复-回复 ，需要回复的ID 和评论ID
					objId = this.replyList[index].respondentId
				let globalData = getApp().globalData
				let inputBoxProps = getApp().globalData.inputBoxProps
				inputBoxProps.placeholder = placeholder
				inputBoxProps.type = type
				inputBoxProps.objId = objId
				inputBoxProps.commonId = this.commonId
				globalData.isInput = true
			},
			refresh() {
				console.log('回复刷新1')
			},
			tabLike(index) {
				// 设置一下防抖
				let {
					respondentId,
					isLike
				} = this.replyList[index]
				if (isLike) {
					console.log('取消点赞')
					console.log('请求中')
					this.replyList[index].isLike = false
					this.replyList[index].likeNum--
				} else {
					console.log('点赞')
					console.log('请求中')
					this.replyList[index].isLike = true
					this.replyList[index].likeNum++
				}
			}
		},
	}
</script>

<style scoped>
	.reply_item {
		padding: 20rpx;
		padding-top: 0;
		background-color: #fff;
	}

	.avator_con {
		padding-top: 20rpx;
		width: 70rpx;
		height: 70rpx;
	}

	.reply_info {
		border-top: 2rpx solid #ccc;
		padding-top: 20rpx;
		margin-top: 10rpx;
		width: 610rpx;
	}

	.name_and_time .reply {
		font-weight: bold;
		padding: 0 20rpx;
		color: #5fa8d6;
	}

	.time {
		font-size: 24rpx;
		color: #7f7f7f;
	}

	.clock {
		padding: 0 20rpx;
	}

	.content_and_like {
		margin: 10rpx 0;
	}

	.content {
		width: 494rpx;
		color: #333333;
	}

	.like {
		color: #8a8a8a;
		height: 40rpx;
		line-height: 40rpx;
	}

	.like .iconfont {
		padding: 10rpx;
		font-size: 40rpx;
		position: relative;
		top: 3rpx;
	}

	.like .icon-aixin1 {
		color: red;
	}

	.reply_iner {
		color: #8a8a8a;
	}

	.reply_iner .iconfont {
		padding: 10rpx;
		font-size: 42rpx;
		position: relative;
		top: 3rpx;
	}
</style>
