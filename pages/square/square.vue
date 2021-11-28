<template>
	<view class="square_con">
		<!-- 分类区 -->
		<view class="distribute_con">
			<view class="items" @click="changeDsitribute">
				<view v-for="(item,index) in distributeList" :key="index" :data-index="index"
					:class="{item:true , selected:distirbuteSelected===index}">
					<image class="icon" :src="'../../static/distribute/'+item.icon" :data-index="index"></image>
					<view class="text" :data-index="index">
						{{item.text}}
					</view>
				</view>
			</view>
		</view>
		<!-- 筛选区 -->
		<view class="sort_bar">
			<SortwayBar @changeSortway="changeSortway" />
		</view>
		<view class="essays_con">
			<Essay :type='type' :sortway='sortway' />
		</view>
	</view>
</template>

<script>
	import Essay from './essay/essay.vue'
	import SortwayBar from '../../components/sortwayBar/sortwayBar.vue'
	export default {
		components: {
			Essay,
			SortwayBar
		},
		data() {
			return {
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
				type: 0,
				sortway: 0

			}
		},
		methods: {
			changeDsitribute(e) {
				let index = e.target.dataset.index
				console.log(index)
				if ((typeof(index)).toLowerCase() === 'number') {
					this.type = index
					this.distirbuteSelected = index
				}
			},
			changeSortway(e) {
				console.log(e)
			}
		}
	}
</script>

<style scoped>
	.square_con {
		width: 100vw;
		min-height: 100vh;
		padding-bottom: 20rpx;
		background-color: #f2f2f2;
	}

	.distribute_con {
		height: 208rpx;
		box-sizing: border-box;
		padding: 20rpx;
		margin-bottom: 10rpx;
	}

	.items {
		display: flex;
		align-items: center;
		justify-content: space-around;
	}

	.item {
		text-align: center;
		border-radius: 10rpx;
		padding: 6rpx 0;
		width: 140rpx;
	}

	.items .selected {
		background-color: #cae9ff;
	}

	.item .icon {
		border-radius: 50%;
		height: 120rpx;
		width: 120rpx;
		box-sizing: border-box;
		display: inline-block;
		text-align: center;
		line-height: 120rpx;
		background-color: #fff;
		border: 1px solid #ccc;
		padding: 20rpx;
	}

	.item .text {
		font-size: 28rpx;
		padding-top: 6rpx;
	}

	.essays_con {
		width: 100vw;
	}

	.sort_bar {
		margin-top: 10rpx;
		height: 80rpx;
		background-color: #fff;
		padding: 20rpx;
		box-sizing: border-box;
		border-bottom: 1rpx solid #ccc;
		background-color: #fff;
		display: flex;
		align-items: center;

	}
</style>
