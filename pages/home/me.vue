<template>
	<view>
		<!-- <view class="head comm-center">
			<image src="/static/img/user/avatar.jpg"></image>
			<view class="name">兽人加鲁鲁</view>
			<view class="remarks"> 每天都要笑一笑！</view>
		</view> -->
		<view class="head comm-center">
			<open-data class="avatar" type="userAvatarUrl" default-avatar="http://image.xiangchengshu.com/images/heads/ia_600000017.png"></open-data>
			<open-data class="nickname" type="userNickName"></open-data>
			<view class="remarks"> 每天都要笑一笑！</view>
		</view>
		<!-- <view class="home-menu">
			<view class="row comm-center">
				<view>￥0</view>
				<view>余额</view>
			</view>
			<view class="row edge comm-center">
				<view>0</view>
				<view>积分</view>
			</view>
			<view class="row comm-center">
				<view>Lv.1</view>
				<view>等级</view>
			</view>
		</view> -->
		<view class="list-menu">
			<!-- <view class="row" v-for="(item,index) in listMenu" :key="index" @click="listMenuClick(index)">
				<image :src="item.icon" mode="aspectFill"></image>
				<text>{{item.name}}</text>
				<u-icon name="arrow-right" color="#B6B6B6"></u-icon>
			</view> -->

			<view class="cell" v-for="(item,index) in listMenu" :key="index" @click="listMenuClick(index)">
				<view class="left-icon comm-center">
					<image :src="item.icon"></image>
				</view>
				<view class="txt">{{item.name}}</view>
				<view class="right-icon comm-center">
					<!-- <image src="/static/img/tabbar/guanzhuactive.png"></image> -->
				</view>
			</view>
			<!-- <view class="cell" @click="listMenuClick">
				<view class="left-icon comm-center">
					<image src="/static/img/tabbar/homeactive.png"></image>
				</view>
				<view class="txt">浏览记录</view>
				<view class="right-icon comm-center">
					<image src="/static/other/youjiantou.png"></image>
				</view>
			</view> -->
			<!-- <view class="cell">
				<view class="left-icon comm-center">
					<image src="/static/other/10.png"></image>
				</view>
				<view class="txt">我的便便</view>
				<view class="right-icon comm-center">
					<image src="/static/other/youjiantou.png"></image>
				</view>
			</view> -->
			<!-- <view class="cell">
				<view class="left-icon comm-center">
					<image src="/static/other/1.png"></image>
				</view>
				<view class="txt">我的帅气</view>
				<view class="right-icon comm-center">
					<image src="/static/other/youjiantou.png"></image>
				</view>
			</view> -->
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				listMenu: [{
						name: '我的收藏',
						icon: '/static/img/tabbar/guanzhuactive.png',
						url: '/pages/quanpingdianzan'
					},
					{
						name: '浏览记录',
						icon: '/static/img/tabbar/homeactive.png',
						url: '/pages/quanpingdianzan'
					}
				]
			}
		},
		methods: {
			//列表菜单点击
			listMenuClick(index) {
				//alert(this.listMenu[index].url)
				uni.navigateTo({
					url: this.listMenu[index].url
				})
			}
		}
	}
</script>

<style lang="scss">
	page {
		background-color: #f8f8f8;
	}

	.head {
		height: 370rpx;
		flex-direction: column;
		background-color: #ffff0a;
		color: #800080;

		image {
			width: 150rpx;
			height: 150rpx;
			border: 5rpx solid #FFFFFF;
			border-radius: 100%;
		}

		.name {
			padding-top: 30rpx;
			font-size: 30rpx;
		}

		.remarks {
			padding-top: 15rpx;
			font-size: 24rpx;
		}

		.avatar {
			height: 120rpx;
			width: 120rpx;
			background-size: 100%;
			border: 5rpx solid #FFFFFF;
			border-radius: 50%;
			overflow: hidden;
		}

		.nickname {
			color: #000000;
			padding-top: 10rpx;
			font-size: 30rpx;
			font-family: KaiTi;
		}
	}

	.avatar_box {
		position: fixed;
		display: flex;
		justify-content: center;
		align-items: center;
		flex-direction: column;
		//top: 80rpx;
		left: 275rpx;
		width: 200rpx;
		height: 400rpx;

		.avatar {
			height: 120rpx;
			width: 120rpx;
			background-size: 100%;
			border: 5rpx solid #FFFFFF;
			border-radius: 50%;
			overflow: hidden;
		}

		.nickname {
			color: #FFFFFF;
			padding-top: 10rpx;
			font-size: 34rpx;
			font-family: KaiTi;
		}

	}

	.home-menu {
		display: flex;
		justify-content: space-around;
		align-items: center;
		margin: 20rpx 0;
		height: 180rpx;
		border-radius: 5rpx;
		background-color: #FFFFFF;

		.row {
			width: 30%;
			font-size: 28rpx;
			font-weight: bold;
			flex-direction: column;

			view {
				line-height: 50rpx;
			}
		}

		.edge {
			border-left: 5rpx solid #f1f1f1;
			border-right: 5rpx solid #f1f1f1;
		}
	}

	.list-menu {
		background-color: #FFFFFF;

		.cell {
			display: flex;
			justify-content: space-between;
			align-items: center;
			height: 100rpx;
			border-top: 5rpx solid #f8f8f8;

			.left-icon {
				width: 15%;

				image {
					width: 40rpx;
					height: 40rpx;
				}
			}

			.txt {
				width: 80%;
				font-size: 26rpx;
			}

			.right-icon {
				width: 10%;

				image {
					width: 30rpx;
					height: 30rpx;
				}
			}
		}
	}
</style>
