<template>
	<view class='search_con' @click="toSearch">
		<icon type="search" size="38rpx" class="icon" color='#5FA8D3' :style="{
			position:'absolute',
			top:'14rpx',
			left:'20rpx',
		}"></icon>
	</view>

</template>

<script>
	export default {
		name: 'Search',
		methods: {
			toSearch() {
				console.log('toSearch')
				uni.navigateTo({
					url: '/pages/search/search',
					fail(e) {
						console.log(e)
					}
				})
			}
		}
	}
</script>

<style scoped>
	.search_con {
		position: relative;
		width: 160rpx;
		height: 60rpx;
		background-color: #fff;
		border-radius: 56rpx;
		margin-left: 20rpx;
	}

	.search_con:active {
		background-color: #f3f3f3;
	}
</style>
