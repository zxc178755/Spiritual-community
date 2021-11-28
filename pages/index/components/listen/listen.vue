<template>
	<view class="listen_con">
		<!-- 轮播图 -->
		<view class="swiper_con">
			<swiper class="swiper" :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000"
				:style="{height:'260rpx'}" :circular="true" indicator-active-color="#b1ddfe" indicator-color="#fff">
				<swiper-item v-for="(item,index) in swiperData" :key="index">
					<view class="swiper-item">
						<image :src="item.ImgUrl" :data-index="index"></image>
					</view>
				</swiper-item>
			</swiper>
			<view class="swiper_underNavigator">
				<view class="text">
					{{swiperText}}
				</view>
				<text class="iconfont icon-arrow1"></text>
			</view>
		</view>
		<!-- 机器人 -->
		<Robot class="robot_position" />
		<!-- 分组 -->
		<Group />
	</view>
</template>

<script>
	import Group from './group/group.vue'
	import Robot from '../../../../components/robot/robot.vue'
	export default {
		components: {
			Group,
			Robot
		},
		data() {
			return {
				swiperData: [{
					ImgUrl: 'https://tse2-mm.cn.bing.net/th/id/OIP-C.nW4Ig8K4Y3zKHHhKPwlTcgAAAA?w=262&h=180&c=7&r=0&o=5&dpr=1.1&pid=1.7',
					url: ''
				}, {
					ImgUrl: 'https://tse3-mm.cn.bing.net/th/id/OIP-C.TSbuVrbu8Rn60eewBQvrGAHaEo?w=289&h=180&c=7&r=0&o=5&dpr=1.1&pid=1.7',
					url: ''
				}, {
					ImgUrl: 'https://tse3-mm.cn.bing.net/th/id/OIP-C.L04yP1_pCdFq1SuVfUhpkgHaDt?w=318&h=175&c=7&r=0&o=5&dpr=1.1&pid=1.7',
					url: ''
				}],
				swiperText: '关注孩子心理成长活动火热来袭！'
			}
		}
	}
</script>

<style scoped>
	.swiper_con {
		width: 600rpx;
		margin: 40rpx auto;
		border: 1rpx solid #ccc;
		padding: 10rpx 4rpx;
		border-radius: 10rpx;
	}

	.swiper-item {
		width: 100%;
		height: 100%;
		border-radius: 10rpx;
		overflow: hidden;
	}

	.swiper-item image {
		display: block;
		width: 100%;
		height: 100%;
	}

	.swiper_underNavigator {
		padding: 24rpx 10rpx 10rpx 10rpx;
		height: 70rpx;
		box-sizing: border-box;
		height: ;
		display: flex;
		align-items: center;
		justify-content: space-between;
	}

	.swiper_underNavigator .text {
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;
		width: 500rpx;
	}

	.robot_position {
		position: absolute;
		top: 530rpx;
		right: 0;
	}
</style>
