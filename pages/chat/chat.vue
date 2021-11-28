<template>
	<view class="chat_page">
		<!-- 对话 -->
		<view class="chat_info ">
			<view v-for="(item,index) in chatList" :key="index"
				:class="item.charactor===0?'robot clearfix':'person clearfix'">
				<image class="avator" :src="item.charactor===0?'../../static/robot.svg':personAvator"></image>
				<view class="content_box">
					<text class="point"></text>
					<view class="content">
						{{item.content}}
					</view>
				</view>
			</view>
		</view>
		<!-- 底部输入框 -->
		<view class="chat_input" id="input">
			<textarea auto-height v-model="value" class="input_area" cursor-spacing="20" :show-confirm-bar="false" />
			<text class="tips button" @click="showTips">#</text>
			<view class="tips_con" v-if="isShowTips">
				<view class="tip_list" @click="chooseTip">
					<view class="tip" v-for="(item,index) in tipList" :key="index" :data-index="index">
						{{item}}
					</view>
				</view>
				<view class="tips_point"></view>
			</view>
			<text class="iconfont icon-send" @click="submit"></text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				personAvator: '../../static/avator.png',
				chatList: [{
					charactor: 0,
					content: '我是Light ，很高兴能为你服务！',
					time: ''
				}, {
					charactor: 1,
					content: '你好！讲个笑话吧',
					time: ''
				}, {
					charactor: 0,
					content: '有一天，一只狼把几十只样赶进了一个山洞 ，领头羊知道这样子不可能全跑掉，就跟狼说 ，你数一数我们有多少只羊，数对了，我们都不跑 ，数错了就让我们走。狼想了想，输错了到时候反悔也不亏。于是就数起来了。狼：”一只羊，两只羊，三只羊.....,ZZZ“。然后狼睡着了。',
					time: ''
				}, {
					charactor: 1,
					content: '哈哈',
					time: ''
				}],
				value: '',
				tipList: ['如何不挂科', '如何不掉头发'],
				isShowTips: false,
				scrollHeight: 800,

			}
		},
		created() {
			var that = this
			uni.getSystemInfo({
				success(e) {
					console.log(e.screenHeight)
					that.scrollHeight = e.screenHeight
				}
			})
			this.$nextTick(function() {
				uni.pageScrollTo({
					scrollTop: that.scrollHeight,
					duration: 100
				})
			})
		},
		methods: {
			submit() {
				if (!this.value.trim()) {
					uni.showToast({
						title: '请输入内容',
						duration: 500,
						icon: 'none'
					})
					return
				}
				this.personSay(this.value)
				this.value = ''
			},
			showTips() {
				this.isShowTips = !this.isShowTips
			},
			chooseTip(e) {
				this.isShowTips = false
				let content = this.tipList[e.target.dataset.index]
				// console.log(this.tipList[e.target.dataset.index])
				if (!content.trim()) {
					uni.showToast({
						title: '请输入内容',
						duration: 500,
						icon: 'none'
					})
					return
				}
				this.personSay(content)

			},
			personSay(content) {
				let scrollHeight = this.scrollHeight
				let say = {
					content,
					charactor: 1,
					time: ''
				};
				this.chatList.push(say)

				this.$nextTick(function() {
					uni.pageScrollTo({
						scrollTop: scrollHeight,
						duration: 100
					})
				})
			}
		}
	}
</script>

<style scoped>
	.chat_page {
		background-color: #f2f2f2;
		width: 100%;
		min-height: 100vh;
	}

	.chat_info {
		padding: 20rpx;
		padding-bottom: 140rpx;
	}

	.avator {
		height: 80rpx;
		width: 80rpx;
		border-radius: 50%;
	}

	.content_box {
		position: relative;
		z-index: 9;
		min-height: 80rpx;
		max-width: 480rpx;
		border: 2rpx solid #ccc;
		border-radius: 10rpx;
		margin-bottom: 16rpx;
	}

	.content {
		position: relative;
		top: 0;
		left: 0;
		z-index: 9;
		width: 100%;
		min-height: 80rpx;
		padding: 22rpx 10rpx;
		box-sizing: border-box;
		border-radius: 10rpx;
		font-size: 30rpx;
	}

	.robot .avator {
		float: left;
	}

	.robot .content_box {
		float: left;
		margin-left: 20rpx;
	}

	.person .content_box {
		float: right;
		margin-right: 20rpx;
	}

	.robot .content {
		background-color: #fff;
	}

	.person .content {
		background-color: #b8e3ff;
	}

	.robot .content_box .point {
		left: 0;
		background-color: #fff;
		transform: translateX(-50%) rotate(45deg);
	}

	.person .content_box .point {
		left: 100%;
		background-color: #b8e3ff;
		transform: translateX(-50%) rotate(45deg);
	}

	.person .avator {
		float: right;
	}

	.person .content_box {
		float: right;
	}

	.point {
		position: absolute;
		width: 20rpx;
		height: 20rpx;
		border: 1px solid #ccc;
		top: 20rpx;
	}

	/* 底部输入框 */
	.chat_input {
		width: 100vw;
		border-top: 2rpx solid #ccc;
		border-bottom: 2rpx solid #ccc;
		box-sizing: border-box;
		background-color: #fff;
		padding: 20rpx 30rpx;
		position: fixed;
		bottom: 0;
		left: 0;
		z-index: 99;
	}

	.tips {
		position: absolute;
		bottom: 30rpx;
		right: 180rpx;
		font-size: 38rpx;
		font-weight: 700;
		color: #fff;
		background-color: #639ef6;
		width: 56rpx;
		height: 56rpx;
		line-height: 56rpx;
		border-radius: 8rpx;
	}

	.tips_con {
		position: absolute;
		height: auto;
		top: -30rpx;
		transform: translateY(-100%);
		left: 28rpx;
		right: 28rpx;
		border: 2rpx solid #ccc;
		margin-bottom: 30rpx;
		border-radius: 8rpx;
	}

	.tip_list {
		width: 100%;
		position: relative;
		padding: 12rpx;
		z-index: 9;
		border-radius: 8rpx;
		box-sizing: border-box;
		background-color: #fff;
	}

	.tip {
		height: 40rpx;
		line-height: 40rpx;
		font-size: 28rpx;
		border: 2rpx solid #ccc;
		padding: 12rpx 14rpx;
		margin-bottom: 8rpx;
		border-radius: 8rpx;
		color: #333333;
	}

	.tip:active {
		background-color: #cae9ff;
	}

	.tips_point {
		position: absolute;
		bottom: 0;
		right: 176rpx;
		transform: translate(50%, 50%) rotate(45deg);
		width: 30rpx;
		height: 30rpx;
		background-color: #fff;
		border-bottom: 2rpx solid #ccc;
		border-right: 2rpx solid #ccc;
	}

	.chat_input .iconfont {
		color: #75c82b;
		font-size: 52rpx;
		padding: 6rpx 40rpx;
		position: absolute;
		bottom: 26rpx;
		text-align: center;
		border-radius: 34rpx;
		right: 20rpx;
		border: 1px solid #ccc;
	}

	.chat_input .iconfont:active {
		background-color: #f1f1f1;
	}

	.input_area {
		border: 1px solid blue;
		width: 428rpx;
		max-height: 180rpx !important;
		padding: 18rpx 14rpx;
		border: 2rpx solid #ccc;
		border-radius: 16rpx;
		font-size: 30rpx;
	}
</style>
