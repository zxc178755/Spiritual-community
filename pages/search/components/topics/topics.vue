<template>
	<view class="records_con">
		<view class="title">
			热门话题 ：
		</view>
		<view class="group">
			<view v-for="(item,index) in hotTopicList" :key="index" class="select_item" @click="tabSelector"
				:data-index="index">
				<text>{{index+1}}.</text>{{item}}
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			hotTopicList: {
				default: [],
				type: Array
			},
		},
		data() {
			return {
				selectedIndex: 0
			}
		},
		methods: {
			tabSelector(e) {
				// console.log(e.target.dataset.index)
				let index = e.target.dataset.index
				console.log(this.hotTopicList[index])
				this.$emit("tabTopic", index)
				// 把点击的放入搜索记录 ，同时放入输入框 ，然后自动搜索
			},
		}
	}
</script>

<style scoped>
	.records_con {
		width: 700rpx;
		margin: 0 auto;
		padding-top: 20rpx;
	}

	.records_con .title {
		color: #000;
		font-weight: bold;
		font-size: 32rpx;
		margin: 24rpx 0;
	}

	.clear_records {
		font-size: 28rpx;
		font-weight: normal;
		color: #555555;
		padding: 0 8rpx;
	}

	.group {
		padding: 0 20rpx;
	}

	.select_item {
		padding: 8rpx 0;
		width: 640rpx;
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;
	}

	.select_item text {
		font-size: 30rpx;
		padding-right: 10rpx;
	}

	.select_item:active {
		background-color: #c3c3c3;
	}
</style>
