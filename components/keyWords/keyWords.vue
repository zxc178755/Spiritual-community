<template>
	<view class="keywords_con">
		<view class="title" v-if="isHasTitle">
			{{kwtitle}} ：
		</view>
		<view :class="{group:true,colored:isColor }">
			<view v-for="(item,index) in keywordsList" :key="index" class="select_item" @click="tabSelector"
				:data-id="index">
				#{{item}}
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			kwtitle: {
				default: '话题',
				type: String
			},
			isHasTitle: {
				default: true,
				type: Boolean
			},
			keywordsList: {
				default: [],
				type: Array
			},
			isColor: {
				default: false
			}

		},
		data() {
			return {
				selectedIndex: 0
			}
		},
		methods: {
			tabSelector(e) {
				// console.log(e.target.dataset.index)
				let selectedID = e.target.dataset.id
				console.log(this.isColor ? '删除' : '添加', selectedID)
				this.$emit("tabWord", [this.isColor ? -1 : 1, selectedID])
			}
		}
	}
</script>

<style scoped>
	.keywords_con {
		width: 700rpx;
		margin: 0 auto;
	}

	.keywords_con .title {
		color: #000;
		font-size: 28rpx;
		padding: 14rpx 0;
	}

	.group {
		width: 720rpx;
		display: flex;
		flex-wrap: wrap;
	}

	.select_item {
		height: 56rpx;
		line-height: 56rpx;
		padding: 0 26rpx;
		margin-bottom: 22rpx;
		margin-right: 12rpx;
		color: #fff;
		background-color: #c6c6c6;
		color: white;
		border-radius: 60rpx;

	}

	.select_item:active {
		background-color: #5FA8D3;
	}

	.colored .select_item {
		background-color: #5FA8D3;
	}
</style>
