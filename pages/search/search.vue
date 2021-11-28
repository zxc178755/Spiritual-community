<template>
	<view class="p_search_con">
		<Header>
			<view class="search_box">
				<view class="search">
					<input type="text" focus="true" @focus="focus" @confirm="confirmSearch" @input="searchInput"
						v-model="value" />
					<icon type="search" size="38rpx" class="icon" color='#5FA8D3' :style="{
					position:'absolute',
					top:'12rpx',
					left:'20rpx',
				}"></icon>
					<icon @click="clearValue" type="clear" size="34rpx" class="icon" color='#9a9a9a' v-if="value.trim()"
						:style="{
						position:'absolute',
						top:'2rpx',
						right:'12rpx',
						padding:'10rpx'
					}"></icon>
				</view>
				<view class="cancel" v-if="isSearch" @click="cancel">
					取消
				</view>
			</view>
		</Header>
		<view :style="{
			paddingTop:'100rpx'}">
			<template v-if="isSearch">
				<view>
					<Records :recordList="recordList" @clearRecords="clearRecords" @tabRecord="tabRecord" />
					<Topics :hotTopicList="hotTopicList" @tabTopic="tabTopic" />
				</view>
			</template>
			<template v-else>
				<Result />
			</template>
		</view>
	</view>
</template>

<script>
	import Header from '../../components/header/header.vue'
	import Records from './components/records/records.vue'
	import Topics from './components/topics/topics.vue'
	import Result from './components/result/result.vue'
	export default {
		name: 'SearchPage',
		components: {
			Header,
			Records,
			Result,
			Topics
		},
		data() {
			return {
				isSearch: true,
				value: '',
				searchRecords: [],
				recordList: ['西瓜', '牛奶', '方便面', '耳机', '耳机', '一起嗑瓜子？'],
				hotTopicList: ['热点1', '热2', '热3', '热4', '热点5', '热点6']
			}
		},
		methods: {
			searchInput(e) {
				// console.log(e)
				// let value = this.value
				// console.log(value)
				return
			},
			confirmSearch() {
				console.log('搜索')

				uni.showLoading({
					title: '搜索中'
				});
				var that = this
				setTimeout(function() {
					that.isSearch = false
					uni.hideLoading();

				}, 2000);

			},
			focus() {
				this.isSearch = true
			},
			cancel() {
				this.value = '';
				this.isSearch = false
			},
			clearValue() {
				this.value = '';
			},
			tabRecord(index) {
				this.value = this.recordList[index]
				this.confirmSearch()
				this.recordList.splice(index, 1)
				this.recordList.unshift(this.value)
				// this.recordList[index] = this.recordList[0]
				// this.recordList[0] = this.value
			},

			clearRecords() {
				this.recordList = []
			},
			tabTopic(index) {
				this.value = this.hotTopicList[index]
				this.confirmSearch()
				this.recordList.unshift(this.value)
			}
		}
	}
</script>

<style scoped>
	.p_search_con {
		width: 100vw;
		min-height: 100vh;
		background-color: #F2F2F2;
	}

	.search_box {
		display: flex;
		width: 95vw;
		margin: 0 auto;
		justify-content: space-around;
	}

	.search {
		position: relative;
		width: 560rpx;
		height: 60rpx;
		background-color: #fff;
		border-radius: 56rpx;
		transition: all 3s;
	}

	.search input {
		position: absolute;
		top: 0;
		left: 10rpx;
		bottom: 0;
		right: 60rpx;
		height: 60rpx;
		line-height: 60rpx;
		padding: 0 20rpx 0 70rpx;
		font-size: 28rpx;
	}

	.cancel {
		color: #888888;
		line-height: 60rpx;
		width: 80rpx;
		/* text-align: center; */
		/* border: 1px solid red; */
	}
</style>
