<template>
	<view>
		<view class="userInfo">
			<image :src="userInfo.portrait" mode=""></image>
			<text>{{userInfo.nickname}}</text>
		</view>
		<view class="pageTopBorder">
			<!-- 我的-用户 -->
			<view class="content" v-if="userInfo.role == 1">
			<!-- <view class="content"> -->
				<view class="item" @tap="goUserAttention">
					<view>
						<icon class="iconfont iconxingxing"></icon>
						<text>我的关注</text>
					</view>
					<icon class="iconfont iconxiangyou"></icon>
				</view>
				<button class="item" open-type='contact' session-from=''>
					<view>
						<icon class="iconfont iconbangzhu"></icon>
						<text>帮助与反馈</text>
					</view>
					<icon class="iconfont iconxiangyou"></icon>
				</button>
			</view>
			<!-- 我的-客户经理 -->
			<view class="content" v-if="userInfo.role == 2">
			<!-- <view class="content"> -->
				<view class="item" @tap="goUserVIP">
					<view>
						<icon class="iconfont iconhuiyuan"></icon>
						<text>我的会员</text>
					</view>
					<icon class="iconfont iconxiangyou"></icon>
				</view>
				<view class="item" @tap="goUserQualification">
					<view>
						<icon class="iconfont iconzizhi"></icon>
						<text>我的资质（认证）</text>
					</view>
					<icon class="iconfont iconxiangyou"></icon>
				</view>
				<button class="item" open-type='contact' session-from=''>
					<view>
						<icon class="iconfont iconbangzhu"></icon>
						<text>帮助与反馈</text>
					</view>
					<icon class="iconfont iconxiangyou"></icon>
				</button>
			</view>
		</view>
		<!-- <button open-type="getUserInfo" v-if="authorizationButton" id='getUserInfo' lang="zh_CN" @getuserinfo="wx_login"></button> -->
	</view>
</template>

<script>
	import User from "./user-model.js";
	const user = new User();
	export default {
		data() {
			return {
				authorizationButton: true,
				userInfo: {}
			};
		},
		onLoad() {
			const that = this
			that._onLoad()
		},
		methods: {
			_onLoad(callBack) {
				const that = this
				that.userInfo = that.$store.state.userInfo;
				// that.wx_login(() => {
				// 	that.getUserInfo(() => {
				// 		callBack && callBack();
				// 	})
				// })
			},
			goUserAttention() {
				user.navigate_to(`/pages/userAttention/userAttention`);
			},
			goUserVIP() {
				user.navigate_to(`/pages/userVIP/userVIP`);
			},
			goUserQualification() {
				user.navigate_to(`/pages/userQualification/userQualification`);
			},
		},
		// 下拉刷新
		onPullDownRefresh() {
			var that = this;
			that.page = 1;
			that._onLoad(() => {
				uni.stopPullDownRefresh();
			});
		},
		//上拉加载更多
		// onReachBottom() {
		//   var that = this;
		//   if (that.last_page == that.page) {
		//     return;
		//   }
		//   that.page += 1;
		//   that.get_product_list();
		// },
		// 分享
		onShareAppMessage() {
			// let shareData = {
			// 	title: '',
			// 	path: `pages/index/index`,
			// 	imageUrl: ''
			// }
			return user.onShareAppMessage({});
		}
	}
</script>

<style lang="less">
	@import url("../../static/css/variable.less");
	.userInfo {
		width: 750rpx;
		height: 285rpx;
		background-color: @themeColor_1;
		display: flex;
		align-items: center;
		justify-content: flex-end;
		flex-direction: column;
		image {
			width: 89rpx;
			height: 89rpx;
			border-radius: 89rpx;
		}
		text {
			font-size: @fontSize_1;
			font-weight: @mainFontWeight;
			color: #fff;
			padding: 20rpx 0;
		}
	}
	.content {
		width: 690rpx !important;;
		height: auto;
		padding: 30rpx;
		button {
			height: 90rpx;
		}
		.item {
			width: 100%;
			// height: 30rpx;
			padding: 30rpx 0;
			display: flex;
			align-items: center;
			justify-content: space-between;
			view {
				display: flex;
				align-items: center;
				justify-content: flex-start;
				font-size: @fontSize_1;
				color: @fontColor_1;
				.iconfont {
					margin-right: 20rpx;
					font-size: @fontSize_1;
					color: @themeColor_1;
				}
			}
			.iconfont {
				font-size: @fontSize_1;
				color: @fontSize_2;
			}
		}
	}
</style>
