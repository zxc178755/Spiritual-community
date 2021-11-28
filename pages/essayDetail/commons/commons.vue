<template>
	<view class="commons_con">
		<view class="common_and_reply" v-for="(item,index) in commonList" :key="item.commonId">
			<view class="common_item clearfix">
				<view class="avator_con fl">
					<image :src="item.avator" class="avator"></image>
				</view>
				<view class="common_info fr">
					<view class="name_and_time">
						<view class="name">
							{{item.Commentator}}
						</view>
						<view class="time">
							{{item.time[0]}} <text class="clock">{{item.time[1]}}</text>
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
			<Reply :commonId='item.commonId' :isUpdate="upDataId === item.commonId" />
		</view>
		<!-- 评论输入框 -->
		<ReplyBox @refresh="refresh" :isInput="isInput"  />
	</view>
</template>
<script>
	import Reply from './reply/reply.vue'
	import ReplyBox from '../../../components/replyBox/replyBox.vue'
	export default {
		components: {
			Reply,
			ReplyBox
		},
		props: {
			essayId: {
				required: true
			},
		},
		created() {
			console.log('11112', this.essayId)
			getApp().isInputWatch(this.switchInput)
		},
		watch: {
			// 监听，因为一开始是的 essayId 是 undefined。 或者是空字符
			essayId(e) {
				console.log('watchessatID', e)
				// 请求数据
			},
		},
		data() {
			return {
				commonList: [{
					commonId: 1,
					avator: '../../../static/avator.png',
					Commentator: '匿名用户aa001',
					time: ['2021-09-18', '11:30'],
					content: '生活就是猫吃鱼，狗吃肉，奥特曼打小怪兽！生活就是猫吃鱼，狗吃肉，奥特曼打小怪兽！',
					isLike: false,
					likeNum: 20
				}, {
					commonId: 2,
					avator: '../../../static/avator.png',
					Commentator: '匿名用户bb001',
					time: ['2021-11-18', '01:30'],
					content: '生活就是猫吃鱼，狗吃肉，',
					isLike: true,
					likeNum: 3
				}, {
					commonId: 3,
					avator: '../../../static/avator.png',
					Commentator: '匿名用户cc003',
					time: ['2021-02-18', '03:30'],
					content: '生活就是猫吃鱼，奥特曼打小怪兽！',
					isLike: true,
					likeNum: 0
				}, {
					commonId: 4,
					avator: '../../../static/avator.png',
					Commentator: '匿名用户dd004',
					time: ['2020-10-18', '08:30'],
					content: '，狗吃肉，奥特曼打小怪兽！',
					isLike: false,
					likeNum: 3030
				}, ],
				isInput: false,
				upDataId: -1
			}
		},
		methods: {
			toReply(index) {
				let placeholder = '回复' + this.commonList[index].Commentator,
					type = 2, // 回复评论 ，只需要 评论Id。
					objId = this.commonList[index].commonId

				let globalData = getApp().globalData
				let inputBoxProps = getApp().globalData.inputBoxProps
				inputBoxProps.placeholder = placeholder
				inputBoxProps.type = type
				inputBoxProps.objId = objId
				globalData.isInput = true

			},
			refresh(type, upDataId) {
				if (type === 3) {
					console.log('刷新回复')
					this.upDataId = upDataId
				} else
					console.log('刷新评论')
			},
			switchInput(e) {
				this.isInput = e
			},
			tabLike(index) {
				let {
					commonId,
					isLike
				} = this.commonList[index]
				if (isLike) {
					console.log('取消点赞')
					console.log('请求中')
					this.commonList[index].isLike = false
					this.commonList[index].likeNum--
				} else {
					console.log('点赞')
					console.log('请求中')
					this.commonList[index].isLike = true
					this.commonList[index].likeNum++
				}
			}
		},

	}
</script>

<style scoped>
	.commons_con {
		padding-bottom: 20rpx;
	}

	.common_item {
		padding: 20rpx;
		padding-bottom: 0rpx;
		background-color: #fff;
		margin-top: 6rpx;
	}

	.avator_con {
		width: 70rpx;
		height: 70rpx;
	}

	.avator {
		width: 70rpx;
		height: 70rpx;
		border-radius: 50%;
	}

	.common_info {
		width: 610rpx;
	}

	.name_and_time {}

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
