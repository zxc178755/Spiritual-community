<template>
	<view class="container">
		<view class="screen_bar">
			<SortwayBar />
			<SortwayBar title="类别" :screenwayList="['类别类别类别1','类别2']" />
			<SortwayBar title="城市" :screenwayList="['城市1','城市2']" />
		</view>
		<Consultants />
	</view>
</template>

<script>
	import SortwayBar from '../../components/sortwayBar/sortwayBar.vue'
	import Consultants from './consultants/consultants.vue'
	export default {
		components: {
			SortwayBar,
			Consultants
		}
	}
</script>

<style>
	.screen_bar {
		padding: 0 40rpx;
		display: flex;
		align-items: center;
		justify-content: space-between;
		margin-bottom: 10rpx;
	}
</style>
