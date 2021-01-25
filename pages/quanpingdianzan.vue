<template>
	<view>
		<view class="ripple" :style="rippleStyle">
			<image class="img" src="https://6e69-niew6-1302638010.tcb.qcloud.la/%E6%B0%94%E6%B3%A1/%E7%82%B9%E8%B5%9E.png?sign=2afe8d0bd68867e56c7df3e35c3db555&t=1604483361"></image>
		</view>
		<view class="container" @touchstart="containerTap">点击屏幕任意位置查看效果</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				rippleStyle: ''
			};
		},
		methods: {
			containerTap(res) {
				var that = this
				var x = res.touches[0].pageX;
				var y = res.touches[0].pageY + 85;
				this.rippleStyle = ''
				setTimeout(function() {
					that.rippleStyle = 'top:' + y + 'px;left:' + x +
						'px;-webkit-animation: ripple 0.4s linear;animation:ripple 0.4s linear;'
				}, 200)
			}
		}
	}
</script>

<style lang="scss">
	page {
		height: 100%;
		background-color: #999999;
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


	@-webkit-keyframes ripple {
		100% {
			-webkit-transform: scale(3);
			transform: scale(3);
			background-color: transparent;
		}
	}
</style>
