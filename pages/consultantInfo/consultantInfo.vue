<template>
	<view class="consultant_info container">
		<!-- 顶部 -->
		<view class="top_part">
			<image src="../../static/avator.png"></image>
			<view class="name_occupation">
				咨询师名字
				<view class="occupation">
					高级心理咨询师
				</view>
			</view>
			<view class="private_letter">
				<text class="iconfont icon-sixin"></text>
				私信
			</view>
		</view>
		<!-- 资质认证 -->
		<view class="qualifications_con">
			<view class="title">
				<text class="iconfont icon-yinzhangrenzheng"></text>
				资质认证
			</view>
			<view class="info_card">
				<view class="hadwork">
					从业时间：8年
				</view>
				<view class="occupation_certification">
					职业认证：
					<view class="occupations">
						<view class="item" v-for="(item,index) in occupationList" :key="index">
							{{item}}
						</view>
					</view>
				</view>
			</view>
		</view>
		<!-- 擅长方向 -->
		<view class="good_at_con">
			<view class="title">
				<text class="iconfont icon-techang" :style="{color:'#ff7b58'}"></text>
				擅长方向
			</view>
			<view class="info_card">
				<view class="item" v-for="(item,index) in goodAtList" :key="index">
					<view class="main_tile" :style="{backgroundColor:colorList[index%5]}">
						{{item.summary}}
					</view>
					<view class="detail">
						{{item.detail}}
					</view>
				</view>
			</view>
		</view>
		<!-- 咨询对象 -->
		<view class="consult_obj">
			<view class="title">
				<text class="iconfont icon-duixiang" :style="{color:'#7ea701'}"></text>
				咨询对象
			</view>
			<view class="info_card">
				青少年，中年人，学生，留学生，情侣，夫妻，孕妇，成年人
			</view>
		</view>
		<ConsultWays :consultantDId="1" />
	</view>
</template>

<script>
	import ConsultWays from './consultWays/consultWays.vue'
	export default {
		components: {
			ConsultWays
		},
		data() {
			return {
				colorList: ['#5fa8d3', '#f08e83', '#ebadef', '#cfe07d', '#64bdba'],
				goodAtList: [{
					summary: '个人成长',
					detail: '个人体验，自我探索'
				}, {
					summary: '婚姻家庭',
					detail: '产后抑郁,家庭创伤,婚姻关系 '
				}, {
					summary: '职场心理',
					detail: '工作压力大,职业倦怠，办公室恋情'
				}, ],
				occupationList: ['国家二级心理咨询师', 'CPS注册系统助力咨询师', 'WMECA国际完形治疗师']
			}
		}
	}
</script>

<style>
	.top_part {
		display: flex;
		align-items: center;
		background-color: #fff;
		border: 2rpx solid #ccc;
		border-top: 0;
		border-bottom-left-radius: 30rpx;
		border-bottom-right-radius: 30rpx;
		padding: 30rpx 34rpx;
	}

	.top_part image {
		width: 140rpx;
		height: 140rpx;
		border-radius: 50%;
		display: block;
		margin-right: 20rpx;
	}

	.name_occupation {
		width: 320rpx;
		margin-right: 20rpx;
		font-size: 32rpx;
		font-weight: bold;
	}

	.occupation {
		font-weight: normal;
		font-size: 28rpx;
		margin-top: 10rpx;
		color: #71b2d8;
	}

	.private_letter {
		border: 2rpx solid #ccc;
		border-radius: 10rpx;
		width: 180rpx;
		height: 80rpx;
		line-height: 80rpx;
		text-align: center;
	}

	.private_letter .iconfont {
		color: #437dff;
		font-size: 38rpx;
		position: relative;
		top: 2rpx;
		padding-right: 20rpx;
	}

	/* 资质认证等 */
	.qualifications_con,
	.good_at_con,
	.consult_obj {
		margin: 0 auto;
		padding: 0 34rpx;
		margin-top: 30rpx;
	}

	.title .iconfont {
		color: #1677ff;
		font-size: 50rpx;
		margin-right: 10rpx;
	}

	.info_card {
		border-radius: 8rpx;
		margin: 0 auto;
		background-color: #fff;
		margin-top: 4rpx;
		padding: 20rpx;
		box-shadow: 0 0 4rpx 0 #ccc;
	}

	.occupation_certification {
		margin-top: 8rpx;
	}

	.occupations {
		border: 2rpx solid var(--themeColor);
		border-radius: 10rpx;
		padding: 10rpx 0;
		margin-top: 6rpx;
	}

	.occupations .item {
		height: 50rpx;
		line-height: 50rpx;
		text-align: center;

	}

	.good_at_con .item {
		display: flex;
		margin-bottom: 20rpx;
	}

	.good_at_con .item:last-child {
		margin-bottom: 0;
	}

	.main_tile {
		width: 160rpx;
		height: 60rpx;
		text-align: center;
		line-height: 60rpx;
		color: #fff;
		background-color: #5fa8d3;
		border-radius: 30rpx;
		margin-right: 16rpx
	}

	.detail {
		width: 476rpx;
		padding: 10rpx 0;
	}
</style>
