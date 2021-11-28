<template>
	<view class="index_con">
		<Header>
			<Avator @tabAvator="tabAvator"></Avator>
			<Tabs @changeHeadTab="changeHeadTab"></Tabs>
			<Search></Search>
		</Header>
		<SideBar :isShow="isShow" @hiddenSideBar="hiddenSideBar" />
		<view :style="{
			paddingTop:'100rpx'}">
			<template v-if="isListenPage">
				<Listen />
			</template>
			<template v-else-if="isTalkPage">
				<Talk />
			</template>
			<template v-else>
				<Issue />
			</template>
		</view>
	</view>
</template>

<script>
	import Header from '../../components/header/header.vue'
	import Listen from './components/listen/listen.vue'
	import Issue from './components/issue/issue.vue'
	import Talk from './components/talk/talk.vue'
	import Tabs from '../../components/header/tabs/tabs.vue'
	import Avator from '../../components/header/avator/avator.vue'
	import Search from '../../components/header/search/search.vue'
	import SideBar from '../../components/sideBar/sideBar.vue'

	export default {
		components: {
			Header: Header,
			Listen: Listen,
			Issue: Issue,
			Talk: Talk,
			Tabs: Tabs,
			Avator: Avator,
			Search: Search,
			SideBar
		},
		data() {
			return {
				isListenPage: true,
				isTalkPage: false,
				isShow: false
			}
		},
		methods: {
			changeHeadTab(e) {
				if (e == 0) {
					this.isListenPage = true
					this.isTalkPage = false
				} else if (e == 1) {
					this.isListenPage = false
					this.isTalkPage = true
				} else {
					this.isListenPage = false
					this.isTalkPage = false
				}
			},
			tabAvator() {
				console.log('13213')
				this.isShow = true
			},
			hiddenSideBar() {
				this.isShow = false
			}
		}
	}
</script>

<style scoped>
	.index_con {
		background-color: #F2F2F2;
		width: 100vw;
		min-height: 100vh;
	}
</style>
