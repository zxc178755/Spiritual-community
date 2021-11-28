<template>
	<view class="sort_con" @click="showSorts">
		<view class="sort_title">
			{{choosed}}
			<text :class="{rotate: isshowSorts===true , iconfont:true , 'icon-arrow1':true}"></text>
		</view>
		<view class="sorts" v-if="isshowSorts">
			<view class="sort_item" v-for="(item,index) in screenwayList" :key="index" :data-id="index">
				{{item}}
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			screenwayList: {
				default: ['综合排序', '顺序排序', '逆序排序'],
			},
			title: {
				default: '综合排序'
			}
		},
		data() {
			return {
				isshowSorts: false,
				choosed: '',
			}
		},
		created() {
			this.choosed = this.title
		},
		methods: {
			showSorts(e) {
				this.isshowSorts = !this.isshowSorts
				let id = e.target.dataset.id
				if (id === undefined) return;
				console.log(id)

				this.choosed = this.screenwayList[id]
				this.$emit("changeSortway", id)
			},
		}
	}
</script>

<style scoped>
	.sort_con {
		background-color: transparent;
		height: 80rpx;
		position: relative;
		margin: 0 10rpx;
	}

	.sort_title {
		margin: 0 auto;
		height: 80rpx;
		line-height: 80rpx;
		color: #4d4d4d;
		text-align: center;
	}

	.sort_title .iconfont {
		margin-left: 30rpx;
		position: relative;
		top: 2rpx;
		display: inline-block;
		transition: all 0.2s;
		transform: rotate(90deg);
	}

	.sort_title .rotate {
		transform: rotate(-90deg);
	}

	.sorts {
		position: absolute;
		top: 100%;
		left: 50%;
		transform: translateX(-50%);
		background-color: #f8f8f8;
		box-shadow: 0 4rpx 6rpx 0 #ccc;
		z-index: 88;
	}

	.sort_item {
		height: 40rpx;
		white-space: nowrap;
		min-width: 180rpx;
		line-height: 40rpx;
		/* text-align: center; */
		padding: 10rpx;
		color: #6d6d6d;
	}

	.sort_item:hover,
	.sort_item:active {
		background-color: #eaeaea;
	}
</style>
