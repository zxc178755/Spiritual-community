<template>
	<view class="shelter" catchtouchmove="()=>{return}" v-if="isShow" @click="hiddenSideBar">
		<view :class="{sideBar_con:true,show_sidebar:isShow}" @click.stop="tabSideBar">
			<view class="avator_con">
				<image :src="userInfo.avator" mode=""></image>
				<view class="user_name">{{userInfo.userName}}</view>
			</view>
			<view class="column_list">
				<navigator class="item clearfix" v-for="(item,index) in columList" :key="index"
					:url="'../../pages/'+item.navi">
					<text :class="'fl '+'iconfont '+item.icon"></text>
					<view class="fr text">
						{{item.text}}
					</view>
				</navigator>
			</view>
			<image src="../../static/side.png" :style="{
				width:'100%',
				height:'331rpx',
				padding:'0rpx 20rpx',
				'box-sizing':'border-box'
			}"></image>
			<view class="login_out button" :data-actionId='3'>
				{{isLogin?'退出登陆':'登陆'}}
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			isShow: {
				default: false,
				required: true
			}
		},
		data() {
			return {
				isLogin: false,
				userInfo: {
					avator: '../../static/avator.png',
					userName: '用户857857857857857857',
				},
				columList: [{
					icon: 'icon-message1-copy',
					text: '回复',
					navi: 'sideReply/sideReply'
				}, {
					icon: 'icon-shoucang',
					text: '我的收藏',
					navi: 'collect/collect'
				}, {
					icon: 'icon-zixun',
					text: '咨询',
					navi: 'sideConsult/sideConsult'
				}, {
					icon: 'icon-group',
					text: '关于我们',
					navi: 'aboutUs/aboutUs'
				}],
			}
		},
		methods: {
			hiddenSideBar() {
				this.$emit("hiddenSideBar")
				console.log('hidden')
			},
			tabSideBar(e) {
				console.log(e)
				let actionId = e.target.dataset.actionid
				console.log(e.target.dataset.actionid)
				if (actionId === 3 && this.isLogin === false) {
					uni.navigateTo({
						url: '../../pages/login/login'
					})
				}
			}
		}
	}
</script>

<style scoped>
	.shelter {
		height: 100vh;
		width: 100vw;
		position: fixed;
		top: 0;
		z-index: 999;
		left: 0;
		background-color: rgba(0, 0, 0, 0.6);

	}

	.sideBar_con {
		height: 100vh;
		width: 340rpx;
		position: absolute;
		top: 0;
		left: 0rpx;
		transform: translateX(-90%);
		box-sizing: border-box;
		border-top-right-radius: 10rpx;
		background-color: #fff;
	}

	.shelter .show_sidebar {
		animation: show 0.3s 0s forwards linear;
	}

	@keyframes show {
		from {
			transform: translateX(-90%);
		}

		to {
			transform: translateX(-0%);
		}
	}

	.avator_con {
		padding: 20rpx 34rpx;
		height: 154rpx;
		background-color: #B1DDFE;
		border-top-right-radius: 10rpx;
	}

	.avator_con image {
		width: 100rpx;
		height: 100rpx;
		border-radius: 50%;
	}

	.user_name {
		padding: 10rpx 0;
		font-weight: bold;
		width: 95%;
		text-overflow: ellipsis;
		overflow: hidden;
		white-space: nowrap;
	}


	.column_list {
		padding: 1.75vh 34rpx;
	}

	.item {
		border: 2rpx solid #ccc;
		padding: 14rpx 16rpx;
		border-radius: 8rpx;
		height: 62rpx;
		line-height: 62rpx;
		margin-bottom: 16rpx;
	}

	.item:active {
		background-color: #f5f5f5;
	}

	.item .iconfont {
		font-size: 56rpx;
		color: #48b5f4;
		position: relative;
	}

	.item .text {
		width: 158rpx;
		text-align: center;
		padding-right: 12rpx;
	}

	.login_out {
		position: absolute;
		bottom: 1.8vh;
		left: 30rpx;
		width: 280rpx;
		height: 80rpx;
		color: #fff;
		line-height: 80rpx;
		background-color: #5fa8d3;
		border-radius: 8rpx;
	}
</style>
