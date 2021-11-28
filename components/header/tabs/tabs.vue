<template>
	<view class='tabs_con' @click="handleTab">
		<view :class="{'tab_item':true , 'active':activeIndex == index}" v-for="(item,index) in tabList"
			:data-tabId='index' :key="index">
			<view class="text" :data-tabId='index'>
				{{item.text}}
				<view class="border_bottom"></view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'Tabs',
		data() {
			return {
				tabList: [{
					id: 1,
					text: '轻听'
				}, {
					id: 2,
					text: '轻诉'
				}, {
					id: 3,
					text: '发布'
				}],
				activeIndex: 0
			}
		},
		methods: {
			handleTab(e) {
				let tabId = e.target.dataset.tabid
				if (tabId === undefined) return
				this.activeIndex = tabId
				this.$emit("changeHeadTab", tabId)
			}
		}
	}
</script>

<style>
	.tabs_con {
		display: flex;
		align-items: center;
		color: #555555;
		font-size: 28rpx;
		width: 420rpx;
		border-right: 1px solid #a4d0fe;
		height: 80rpx;
		margin-top: 20rpx;
	}

	.tab_item {
		flex: 1;
		text-align: center;
		margin-right: 30rpx;
	}

	.tab_item:nth-child(3) {
		margin-right: 24rpx;
	}

	.tab_item .text {
		/* padding-bottom: 4rpx; */
		padding: 8rpx 15rpx;
	}

	.active .text {
		/* border-bottom: 6rpx solid #1B4965; */
		color: #1B4965;
		font-weight: 700;
		font-size: 32rpx;
	}
	.active .text .border_bottom{
		border-bottom: 6rpx solid #1B4965;
	}
	.border_bottom{
		width: 80%;
		margin: 0 auto;
		padding-top: 4rpx;
		border-bottom: 6rpx solid transparent;
	}
</style>
