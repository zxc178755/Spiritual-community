<template>
	<view class="results_con">
		<view class="sortway_bar">
			<SortwayBar @changeSortway="changeSortway" />
		</view>
		<Essay />
	</view>
</template>

<script>
	import SortwayBar from '../../../../components/sortwayBar/sortwayBar.vue'
	import Essay from '../../../../components/essay/essay.vue'
	export default {
		components: {
			SortwayBar,
			Essay
		},
		data() {
			return {}
		},
		methods: {
			changeSortway(index) {
				console.log(index)
			}
		}
	}
</script>

<style>
	.results_con {
		padding-top: 20rpx;
	}
	.sortway_bar{
		display: flex;
		padding-left: 20rpx;
	}
</style>
