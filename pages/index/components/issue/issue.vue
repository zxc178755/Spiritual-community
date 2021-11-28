<template>
	<view class="issue_con">
		<view v-if="!isIsuccess">
			<!-- 标题 -->
			<view class="title_con">
				<view class='label'>标题：</view><input class="title" type="text" v-model="titleValue" />
			</view>
			<!-- 已选关键字 -->
			<KeyWords :isHasTitle="false" :isColor="true" :keywordsList="hasSelectedList" @tabWord="tabWord" />
			<!-- 文章主体 -->
			<editor id="editor" class="body_content" :placeholder="placeholder" @ready="onEditorReady"
				placeholder="请输入正文..." cursor-spacing="30"></editor>

			<!-- 分区选择 -->
			<view class="distribute_con">
				<view class="distribute_title">分区选择</view>
				<view class="items" @click="changeDsitribute">
					<view v-for="(item,index) in distributeList" :key="index" :data-index="index"
						:class="{item:true , selected:distirbuteSelected===index}">
						<image :src="'../../../../static/distribute/'+item.icon" class="icon" :data-index="index">
						</image>
						<view class="text" :data-index="index">
							{{item.text}}
						</view>
					</view>
				</view>
			</view>
			<!-- 添加关键字 -->
			<view class="add_keywords_con">
				<view class="symbol fl">#</view>
				<input class="add_keywords fl" type="text" v-model="newKeywords" placeholder="添加标记话题" />
				<text class="fl iconfont icon-duigou" style="color:'#62b6cb'" @click="addKeyword"></text>
				<text class="fl iconfont icon-cuowuguanbiquxiao" style="color:'#d4237a'" @click="clearInput"></text>
				<image src="../../../../static/picture.png" class="choose_img fr" @click="addImg"></image>
			</view>
			<!-- 推荐关键字 -->
			<KeyWords :isHasTitle="true" :keywordsList="keywordsList" kwtitle="推荐话题" @tabWord="tabWord" />
			<!-- 发布或者保存 -->
			<view class="sumbit_buttons">
				<view class="button fr submit" @click="sumbit">
					确认发布
				</view>
				<view class="button fr save">
					保为草稿
				</view>
			</view>
		</view>
		<!-- 发布成功 -->
		<view class="issue_success" v-else>
			<view class="suc_buttons_con">
				<image src="../../../../static/issue_s.png"></image>
				<view class="suc_buttons">
					<view class="button suc_continue" @click="continueIssue">
						继续发布
					</view>
					<view class="button suc_detail" @click="toDetail">
						查看详情
					</view>
				</view>
				<view class="return_index">
					返回首页
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import KeyWords from '../../../../components/keyWords/keyWords.vue'
	export default {
		components: {
			KeyWords
		},
		data() {
			return {
				keywordsList: [],
				hasSelectedList: [],
				titleValue: '',
				distributeList: [{
					text: '校园生活',
					icon: 'school.png'
				}, {
					text: '个人成长',
					icon: 'growth.png'
				}, {
					text: '知识科普',
					icon: 'xing.png'
				}, {
					text: '人际交往',
					icon: 'jw.png'
				}],
				distirbuteSelected: 0,
				isIsuccess: false,
				newKeywords: ""
			}
		},
		created() {
			// 发送请求关键词
			this.keywordsList = ['苹果', '大西瓜', '榴莲', '巧克力', '瓜', '榴莲', '大西瓜', '大西瓜', '榴莲']
			this.hasSelectedList = ['西瓜', '牛奶']
		},
		methods: {
			// 分区选择
			changeDsitribute(e) {
				let index = e.target.dataset.index
				console.log()
				if ((typeof(index)).toLowerCase() === 'number') {
					this.distirbuteSelected = index
				}
			},
			// 富文本编辑器初始化
			onEditorReady() {
				this.createSelectorQuery().select('#editor').context((res) => {
					this.editorCtx = res.context
				}).exec()
			},
			// 清空内容 保留

			// 插入图片
			addImg() {
				let that = this
				uni.chooseImage({
					count: 1,
					success(e) {
						console.log(e.tempFilePaths[0])

						let src = e.tempFilePaths[0]

						that.editorCtx.insertImage({
							src,
							alt: '图片加载失败',
							width: '80%',
							extClass: 'rich_img'
						})
					}
				})
			},


			// 提交
			sumbit() {
				// this.isIsuccess = true
				// 获取首照片。
				// 获取标签
				// 获取标题
				// 获取分区
				this.editorCtx.getContents({
					success(e) {
						console.log('内容为:', e.html)
						uni.setStorageSync('essay1', e.html)
					}
				})
				this.isIsuccess = true
			},

			// 继续发布
			continueIssue() {
				this.isIsuccess = false
			},

			// 查看详情
			toDetail() {
				console.log('e')
				uni.navigateTo({
					url: '/pages/essayDetail/essayDetail'
				})
			},

			// 点击关键字
			tabWord([eventType, index]) {
				if (eventType === -1) {
					this.hasSelectedList.splice(index, 1)
				} else if (eventType === 1) {
					this.hasSelectedList.push(this.keywordsList[index])
				}
			},
			addKeyword() {
				if (!this.newKeywords.trim()) {
					uni.showToast({
						title: '内容不能为空',
						icon: 'none',
						duration: 800
					})
					return
				}
				this.hasSelectedList.push(this.newKeywords)
				this.newKeywords = ''
			},
			clearInput() {
				this.newKeywords = ''
			}
		}
	}
</script>

<style scoped>
	.issue_con {
		width: 700rpx;
		margin: 0 auto;
		padding-bottom: 100rpx;
	}

	.title_con {
		display: flex;
		height: 100rpx;
		align-items: center;
		background-color: #fff;
		box-shadow: 0 -40px 0 40px #fff;
		margin-bottom: 30rpx;
	}

	.label {
		font-size: 32rpx;
		font-weight: bold;
	}

	.title {
		font-size: 32rpx;
		width: 540rpx;
		padding: 10rpx 20rpx;
	}

	.body_content {
		min-height: 300rpx;
		padding: 20rpx 30rpx;
		background-color: #fff;
		box-shadow: 0px 0px 6rpx 1px rgba(170, 170, 170, 0.35);
		margin-top: 10rpx;
		border-radius: 10rpx;
		height: auto !important;
		font-size: 32rpx;
	}

	.rich_img {
		width: 90%;
		margin: 0 auto;
	}

	.distribute_con {
		background-color: #FFFF;
		border-radius: 8rpx;
		height: 208rpx;
		color: #555555;
		margin: 26rpx 0;
		padding: 8rpx;
		box-sizing: border-box;
	}

	.distribute_title {
		text-align: center;
	}

	.items {
		display: flex;
		align-items: center;
		padding: 8rpx 44rpx 0 44rpx;
	}

	.item {
		flex: 1;
		text-align: center;
		border-radius: 10rpx;
		padding: 6rpx 0;
		margin: 0 13rpx;
	}

	.items .selected {
		background-color: #a0d7fe;
	}

	.item .icon {
		border-radius: 50%;
		height: 90rpx;
		width: 90rpx;
		box-sizing: border-box;
		display: inline-block;
		text-align: center;
		line-height: 90rpx;
		background-color: #fff;
		border: 2rpx solid #ccc;
		padding: 10rpx;
	}

	.item .text {
		font-size: 24rpx;
		padding-top: 6rpx;
	}

	.add_keywords_con {
		height: 80rpx;
		border-radius: 8rpx;
		background-color: #fff;
		line-height: 80rpx;
		/* overflow: hidden; */
	}

	.symbol {
		font-size: 40rpx;
		font-weight: bold;
		color: #5fa8d3;
		padding-left: 24rpx;
		padding-right: 12rpx;
	}

	.add_keywords {
		border-radius: 30rpx;
		border: 1rpx solid #ccc;
		text-align: center;
		height: 60rpx;
		margin-top: 9rpx;
		width: 280rpx;
		line-height: 64rpx;
	}

	.add_keywords_con .iconfont {
		margin-left: 20rpx;
		padding: 0 10rpx;
		color: red;
		font-size: 50rpx;
	}

	.add_keywords_con .icon-duigou {
		color: #62b6cb;
	}

	.choose_img {
		width: 96rpx;
		box-sizing: border-box;
		height: 80rpx;
		padding: 10rpx;
		padding-left: 26rpx;
		margin-right: 16rpx;
		border-left: 1rpx solid #ccc;
	}

	.sumbit_buttons {
		position: fixed;
		bottom: 0;
		left: 0;
		width: 100vw;
		height: 100rpx;
		padding: 0 24rpx;
		box-sizing: border-box;
		border-top: 2rpx solid #ccc;
		z-index: 99;
		background-color: #f2f2f2;
	}

	.sumbit_buttons view {
		margin-top: 19rpx;
		height: 60rpx;
		width: 160rpx;
		border-radius: 10rpx;
		line-height: 60rpx;
		margin-left: 30rpx;
	}

	.save {
		background-color: #fff;
		border: 2rpx solid #ccc;
		color: #555555;
	}

	.submit {
		color: #fff;
		border: 2rpx solid #5fa8d3;
		background-color: #5fa8d3;
	}

	.issue_success {
		position: fixed;
		right: 0;
		top: 100rpx;
		left: 0;
		bottom: 0;
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.suc_buttons_con {
		width: 600rpx;
		margin: 0 auto;
	}

	.suc_buttons_con image {
		width: 100%;
		max-height: 512rpx;
	}

	.suc_buttons {
		display: flex;
		justify-content: space-around;
		align-items: center;
		padding: 20rpx 0;
	}

	.suc_buttons .button {
		width: 200rpx;
		height: 80rpx;
		text-align: center;
		line-height: 80rpx;
		border-radius: 8rpx;
	}

	.suc_continue {
		border: 2rpx solid #ccc;
	}

	.suc_continue:active {
		background-color: #dcdcdc;
	}

	.suc_detail {
		background-color: #5fa8d3;
		border: 2rpx solid #5fa8d3;
		color: #fff;
	}

	.return_index {
		text-align: center;
		color: #5fa8d3;
		margin-top: 16rpx;
		padding: 10rpx;
	}
</style>
