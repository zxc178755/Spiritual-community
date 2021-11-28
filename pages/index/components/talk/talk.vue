<template>
	<view class="talk_con">
		<view class="talk_list">
			<view class="talk_card" v-for="(item,index) in talksList" :key='index' :style="{
			backgroundColor:colorList[index%4],
		}">
				<view class="content">
					{{item.content}}
				</view>
				<view class="time">
					{{item.time}}
				</view>
			</view>
		</view>

		<view class="movable_area" v-if="!isShowWriteBoard&&isready">
			<movable-area :style=" {width:'100vw',height:maxHeight}">
				<movable-view @touchend="touchEnd" @click="showWriteBoard" class="write_talk_con" :x="x" :y="y"
					direction="all">
					<image src="../../../../static/write.png" :style="{
						width:'70rpx',
						height:'70rpx',
						display:'block'
					}"></image>
				</movable-view>
			</movable-area>
		</view>
		<view catchtouchmove="()=>{return}" class="wirte_board" v-else>
			<view class="write_box">
				<textarea cursor-spacing="30" class="write_area" v-model="publishValue" placeholder="说说你的心事吧!"
					:show-confirm-bar="false" :maxlength="100">
				</textarea>
				<view class="buttons clearfix">
					<view class="button publish fr" @click="publish">发布</view>
					<view class="button cancel fr" @click="cancel">取消</view>
				</view>
			</view>
		</view>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				talksList: [{
					content: '我刚认识他的时候 ，他很帅气 ，他很努力 ，说要给我们一个美好的未来。我相信他。但是他是一个程序员 ，渐渐的 ，它秃顶了，我... ',
					time: '2021-10-09'
				}, {
					content: '她很善良 ，很通情达理，也很好看 。她喜欢吃我做的饭，她说，心疼你穷，去外面吃太贵了。',
					time: '2021-11-19'
				}, {
					content: '生活就是猫吃鱼，狗吃肉，奥特曼打小怪兽 。',
					time: '2021-01-22'
				}, {
					content: '记得那是一个晴朗的夏天 ，柠檬味的可乐 ，想起，还能打个隔 。是夏天的味道',
					time: '2021-12-29'
				}, ],
				colorList: ['#cae9ff', '#bee9e8', '#62b6cb', '#ffff80'],
				y: '',
				x: '',
				SystemW: '',
				SystemH: '',
				isShowWriteBoard: false,
				publishValue: '',
				maxHeight: '677px',
				isready: false
			}
		},
		created() {
			var that = this
			uni.getSystemInfoAsync({
				success(e) {
					that.SystemH = e.windowHeight
					that.SystemW = e.windowWidth
					that.maxHeight = e.windowHeight - 50 + 'px'
					that.x = e.windowWidth - 40
					that.y = e.windowHeight - 280
					that.isready = true
				},
			})


		},
		methods: {
			touchEnd(e) {
				// console.log('结束')
				console.log(e)
				this.x = e.changedTouches[0].clientX < this.SystemW / 2 ? 0 : this.SystemW
				this.y = e.changedTouches[0].clientY - 72.5
			},
			showWriteBoard() {
				this.isShowWriteBoard = true
			},
			cancel() {
				this.isShowWriteBoard = false
			},
			publish() {
				// console.log(this.publishValue)
				let value = this.publishValue
				if (!value.trim()) {
					console.log('不能为空')
					uni.showToast({
						title: '内容不能为空',
						icon: "none",
						duration: 1000
					})
					return
				}
				console.log(value.length)
				// 请求成功后的操作
				uni.showLoading({
					title: '发送中...'
				})

				this.talksList.unshift({
					content: value,
					time: '2021-01-20'
				})
				setTimeout(() => {
					uni.hideLoading()
					this.isShowWriteBoard = false
					this.publishValue = ''
					// 得重新加载请求
				}, 1200)

			},
		}
	}
</script>

<style scoped>
	.talk_con {
		width: 100vw;
	}

	.talk_list {
		width: 640rpx;
		margin: 0 auto;
		/* border: 1px solid red; */
		margin-top: 60rpx;
		padding-bottom: 40rpx;
	}

	.talk_card {
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		/* background-color: #cae9ff; */
		border-radius: 10rpx;
		margin-bottom: 40rpx;
		padding: 30rpx;
		color: #1B4965;
		min-height: 140rpx;
		box-shadow: 8rpx 8rpx 12rpx 0 #b3b3b3;
	}

	.time {
		margin-top: 16rpx;
		text-align: right;
	}

	.movable_area {
		position: fixed;
		top: 0;
		left: 0;
		z-index: 10;
		width: 100vw;
		padding-top: 100rpx;
	}

	.write_talk_con {
		width: 70rpx;
		height: 70rpx;
		padding: 13rpx;
		background-color: #b1ddfe;
		border-radius: 50%;
		text-align: center;
		line-height: 90rpx;
	}

	.wirte_board {
		position: fixed;
		top: 0rpx;
		left: 0;
		width: 100vw;
		height: 100vh;
		z-index: 99;
		background-color: rgba(239, 239, 239, 0.4);
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.write_box {
		width: 660rpx;
		height: 490rpx;
		border-radius: 8rpx;
		border: 2rpx solid #ccc;
		padding: 30rpx;
		box-sizing: border-box;
		background-color: #fff;
	}

	.write_area {
		border: 2rpx solid #ccc;
		border-radius: 8rpx;
		width: 600rpx;
		height: 340rpx;
		padding: 10rpx;
		box-sizing: border-box;
		font-size: 30rpx;
		line-height: 40rpx;
		color: #595959;
	}

	.buttons {
		padding-top: 27rpx;
	}

	.button {
		width: 140rpx;
		height: 60rpx;
		line-height: 60rpx;
		font-size: 28rpx;
		margin-left: 28rpx;
		border-radius: 6rpx;
	}

	.cancel {
		background-color: #d7d7d7;
		color: #555555;
	}

	.publish {
		background-color: #5fa8d3;
		color: #fff;
	}
</style>
