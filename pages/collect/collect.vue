<template>
	<view class="collect_con">
		<Essay />
	</view>
</template>

<script>
	import Essay from '../../components/essay/essay.vue'
	export default {
		components: {
			Essay
		},
		data() {
			return {
				collectList: []
			}
		},
		created() {
			console.log('请求收藏数据')
		}
	}
</script>

<style>
	.collect_con{
		width: 100vw;
		min-height: 100vh;
		background-color: #f2f2f2;
		padding: 20rpx 0;
	}
</style>
