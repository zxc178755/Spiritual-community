<template>
	<view class="group_con">
		<view class="title">
			大暖炉
		</view>
		<view class="group">
			<view v-for="(item,index) in selectGroup" :key="index"
				:class="{ select_item:true,selected:selectedIndex===index}" @click="changeSelect" :data-id="index">
				{{item.text}}
			</view>
		</view>
		<Essay :type="selectedIndex"></Essay>
	</view>
</template>

<script>
	import Essay from '../../../../../components/essay/essay.vue'
	export default {
		components: {
			Essay
		},
		data() {
			return {
				selectGroup: [{
						text: '全部'
					},
					{
						text: '精选'
					},
					{
						text: '心理科普'
					},
					{
						text: '人际关系'
					},
					{
						text: '家庭关系'
					},
					{
						text: '校园学习'
					}
				],
				selectedIndex: 0
			}
		},
		methods: {
			changeSelect(e) {
				let selectedIndex = e.target.dataset.id
				this.selectedIndex = selectedIndex
			}
		}
	}
</script>

<style scoped>
	.group_con {
		width: 640rpx;
		margin: 0 auto;
		margin-top: 160rpx;
	}

	.group_con .title {
		color: #5FA8D3;
		font-weight: bold;
		font-size: 34rpx;
		padding: 10rpx 0;
		height: ;
	}

	.group {
		width: 670rpx;
		display: flex;
		flex-wrap: wrap;
		margin-bottom: 20rpx;
	}

	.select_item {
		height: 40rpx;
		line-height: 40rpx;
		padding: 2rpx 21rpx;
		margin-top: 22rpx;
		color: #555555;
	}

	.selected {
		background-color: #5FA8D3;
		color: white;
		border-radius: 60rpx;
	}
</style>
