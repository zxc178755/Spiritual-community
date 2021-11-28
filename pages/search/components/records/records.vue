<template>
	<view class="records_con">
		<view class="title">
			搜索记录：<view class="fr clear_records" @click="clearRecords">
				清空
			</view>
		</view>
		<view class="group">
			<view v-for="(item,index) in recordList" :key="index" class="select_item" @click="tabSelector"
				:data-index="index">
				{{item}}
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			recordList: {
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
				console.log(this.recordList[index])
				// 把点击的搜索放在数组最前面
				this.$emit("tabRecord", index)
			},
			clearRecords() {
				console.log('清空搜索记录')
				this.$emit("clearRecords")
			}
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
		width: 714rpx;
		display: flex;
		flex-wrap: wrap;
	}

	.select_item {
		height: 56rpx;
		line-height: 56rpx;
		padding: 0 26rpx;
		margin-bottom: 22rpx;
		margin-right: 18rpx;
		background-color: #d7d7d7;
		color: #484848;
	}

	.select_item:active {
		background-color: #a5a5a5;
	}
</style>
