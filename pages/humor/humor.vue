<template>
	<view>
		<!-- 刷新页面后的顶部提示框 -->
		<view class="tips" :class="{ 'tips-ani': tipShow }">为您更新了10条最新数据</view>
		<view class="ripple" :style="rippleStyle">
			<image class="img" src="https://6e69-niew6-1302638010.tcb.qcloud.la/%E6%B0%94%E6%B3%A1/%E7%82%B9%E8%B5%9E.png?sign=2afe8d0bd68867e56c7df3e35c3db555&t=1604483361"></image>
		</view>
		<!--
		<uni-clientdb ref="udb" v-slot:default="{data, loading, error, options}" :options="formData" :collection="collection"
		 :field="field" @load="load">
		 -->
		<!-- 基于 uni-list 的页面布局 -->
		<uni-list>
			<!-- to 属性携带参数跳转详情页面，当前只为参考 -->
			<uni-list-item direction="column" v-for="item in dataList" :key="item.id">
				<!-- 通过header插槽定义列表的标题 -->
				<template v-slot:header>
					<!-- <image src="item.userInfo.headUrl"></image> -->
					<view class="uni-title">{{item.title}}</view>
				</template>
				<!-- 通过body插槽定义列表内容显示 -->
				<template v-slot:body>
					<view class="uni-list-box">
						<view class="uni-content">
							<view class="uni-title-sub uni-ellipsis-2" v-html="item.content">
								 
							</view>
							<view class="uni-note">{{item.userInfo.userName}} - {{item.dateTime}}</view>
						</view>
					</view>
				</template>
				<!-- 同步footer插槽定义列表底部的显示效果 -->
				<template v-slot:footer>
					<view class="uni-footer">
						<text class="uni-footer-text">评论</text>
						<text class="uni-footer-text" @touchstart="onClickZan">点赞</text>
						<text class="uni-footer-text">分享</text>
					</view>
				</template>
			</uni-list-item>
		</uni-list>
		<!-- 通过 loadMore 组件实现上拉加载效果，如需自定义显示内容，可参考：https://ext.dcloud.net.cn/plugin?id=29 -->
		<!-- <uni-load-more v-if="loading || options.status === 'noMore' " :status="options.status" /> -->
		<!-- </uni-clientdb> -->
	</view>
</template>

<script>
	import $U from '@/common/js/util.js';
	import $H from '@/common/js/request.js';
	import $C from '@/common/js/config.js';

	export default {
		components: {},
		data() {
			return {
				loading: false,
				page: 1,
				options: {
					status: 'noMore'
				},
				formData: {
					status: 'loading' // 加载状态
				},
				dataList: [],
				tipShow: false, // 是否显示顶部提示框
				rippleStyle: ''
			};
		},
		onLoad() {
			this.getPageData()
		},
		methods: {
			/**
			 * 下拉刷新回调函数
			 */
			onPullDownRefresh() {
				this.page--;
				this.tipShow = true;
				this.formData.status = 'more';
				console.info("下拉刷新回调函数");
				this.getPageData();
				// this.$refs.udb.loadData({
				// 	clear: true
				// }, () => {
				// 	this.tipShow = false
				// 	uni.stopPullDownRefresh()
				// })
			},
			/**
			 * 上拉加载回调函数
			 */
			onReachBottom() {
				console.info("上拉加载回调函数")
				// this.$refs.udb.loadMore()
				this.page++;
				uni.showNavigationBarLoading();
				this.getPageData()
			},
			load(data, ended) {
				console.log(data)
				console.log(ended)
				if (ended) {
					this.formData.status = 'noMore'
				}

			},
			getPageData() {
				console.info("当前查询第" + this.page + " 页")
				$H.get('/getXdData?pageNum='+this.page).then(res => {
					// alert(1)
					// console.info(" 数据:" + res.data);
					if(this.page == 1){
						this.dataList = [];
					}
					this.dataList = this.dataList.concat(res.data);
					uni.hideNavigationBarLoading();
				});
			},
			onClickZan(res) {
				var that = this;
				// var x = 100;
				// var y = 100 + 85;
				var x = res.touches[0].pageX;
				var y = res.touches[0].pageY + 85;
				
				//alert("x="+x)
				this.rippleStyle = ''
				setTimeout(function() {
					//alert(4444)
					that.rippleStyle = 'top:' + y + 'px;left:' + x +
						'px;-webkit-animation: ripple 0.4s linear;animation:ripple 0.4s linear;'
				}, 200)
			}
		}
	};
</script>

<style lang="scss">
	@import '@/common/uni-ui.scss';

	page {
		display: flex;
		flex-direction: column;
		box-sizing: border-box;
		background-color: #efeff4;
		min-height: 60%;
		height: auto;
	}

	.tips {
		color: #67c23a;
		font-size: 14px;
		line-height: 40px;
		text-align: center;
		background-color: #f0f9eb;
		height: 0;
		opacity: 0;
		transform: translateY(-100%);
		transition: all 0.3s;
	}

	.tips-ani {
		transform: translateY(0);
		height: 40px;
		opacity: 1;
	}

	.content {
		width: 100%;
		display: flex;
	}

	.list-picture {
		width: 100%;
		height: 145px;
	}

	.thumb-image {
		width: 100%;
		height: 100%;
	}

	.ellipsis {
		display: flex;
		overflow: hidden;
	}

	.uni-ellipsis-1 {
		overflow: hidden;
		white-space: nowrap;
		text-overflow: ellipsis;
	}

	.uni-ellipsis-2 {
		overflow: hidden;
		text-overflow: ellipsis;
		display: -webkit-box;
		//-webkit-line-clamp: 2;
		-webkit-box-orient: vertical;
	}
	
	// 点赞动画
	.ripple {
		height: 50rpx;
		width: 50rpx;
		margin-top: -90px;
		position: absolute;
		-webkit-transform: scale(0);
		overflow: hidden;
		z-index: 1;
	}
	
	.img {
		z-index: 2;
		width: 50rpx;
		height: 50rpx;
	}
	
	.container {
		display: flex;
		justify-content: center;
		padding-top: 100rpx;
		font-size: 30rpx;
		width: 100vw;
		height: 100vh;
		overflow: hidden;
	}
	
	@-webkit-keyframes ripple {
		100% {
			-webkit-transform: scale(2);
			transform: scale(2);
			background-color: transparent;
		}
	}
</style>
