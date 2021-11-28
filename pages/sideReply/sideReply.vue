<template>
	<view class="side_reply_con">
		<view class="replys">
			<view class="reply" v-for="(item,index) in replyList" :key="item.replyId">
				<view class="header clearfix">
					<view class="name_part fl">
						<text class="user">{{item.name}}</text><text class="reply_text">回复</text>你
					</view>
					<view class="time fr">
						{{item.time[0]}}<text>{{item.time[1]}}</text>
					</view>
				</view>
				<view class="content">
					{{item.content}}
				</view>
				<view class="tool">
					<text class="iconfont icon-message1-copy" @click.stop="toReply(item.replyId)"></text>回复
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				replyList: [{
					replyId: 1,
					name: "匿名用户aa101",
					time: ['2021-10-21', '21:20'],
					content: '生活就是猫吃鱼 ，狗吃肉 ，奥特曼打小怪兽！生活就是猫吃鱼 ，狗吃肉 ，奥特曼打小怪兽'
				}, {
					replyId: 2,
					name: "匿名用户aa101",
					time: ['2021-10-21', '21:20'],
					content: '生活就是猫吃鱼 ，狗吃肉 ，奥特曼打小怪兽！'
				}, {
					replyId: 3,
					name: "匿名用户aa101",
					time: ['2021-10-21', '21:20'],
					content: '生活就是猫吃鱼 ，狗吃肉 ，奥特曼打小怪兽！'
				}]
			}
		},
		methods: {
			toReply(e) {
				console.log(e)
			}
		}
	}
</script>

<style scoped>
	.side_reply_con {
		width: 100vw;
		min-height: 100vh;
		background-color: #f2f2f2;
	}

	.replys {
		width: 100%;
		padding-bottom: 20rpx;
	}

	.reply {
		display: flex;
		flex-direction: column;
		padding: 10rpx 30rpx;
		margin-bottom: 20rpx;
		box-shadow: 0 2rpx 6rpx 0 #ccc;
		background-color: #fff;
	}

	.header {
		height: 60rpx;
		line-height: 60rpx;
	}

	.header .user {
		font-weight: bold;
	}

	.reply_text {
		font-weight: bold;
		color: #65abd5;
		padding: 0 14rpx;
	}

	.time {
		font-size: 26rpx;
		color: #7f7f7f;
	}

	.tool {
		padding: 4rpx 20rpx;
		text-align: right;
		color: #7f7f7f;
	}

	.tool .iconfont {
		padding: 10rpx;
		font-size: 40rpx;
	}
</style>
