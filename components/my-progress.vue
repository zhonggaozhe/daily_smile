<template>
	<view class="progress-box">
		<view class="progress-box-sgin" v-bind:style="{width:getSginWid}">
			<view :animation="animationData" class="progress-box-sgin-n" v-bind:style="{background:contentBacColor}">
				<text v-bind:style="{color:contentColor}">{{content}}</text>
			</view>
		</view>
		<view class="progress-box-w" v-bind:style="[{background:progressColor,width:getWid}]">
			 <view class="progress-box-w-w" v-bind:style="{background:progressBckColor}" :animation="animationData" >
				 <view class="progress-box-w-n" v-bind:style="{background:progressColor}"></view>
			 </view>
		</view>
		
	</view>
</template>

<script>
	export default {
		created: function() {
			var animation = uni.createAnimation({
				duration: this.time,
				timingFunction: this.type,
			})
			this.animation = animation
			this.cpMobile()
			setTimeout(function() {
				animation.translate(this.mobilePx).step()
				this.animationData = animation.export()
			}.bind(this), 100)
		},
		props:{
			nowD:{},
			sumD:{},
			content:'',
			contentColor:{
				type: String,
				default: 'rgba(3,144,252,1)'
			},
			contentBacColor:{
				type: String,
				default: '#F4F4F4'
			},
			time:{
				type: Number,
				default: 1000
			},
			progressBckColor:{
				type: String,
				default: 'rgba(184, 224, 255,1)'
			},
			progressColor:{
				type: String,
				default: '#FFFFFF'
			},
			wid:{
				type: Number,
				default: 280
			},
			type:{
				type: String,
				default: "ease"
			}
		},
		computed:{
			getWid(){
				return this.wid.toString()+"px"
			},
			getSginWid(){
				return (this.wid+40).toString()+"px"
			}
		},
		data() {
			return {
				animationData: {},
				mobilePx:0,
			};
		},
		methods: {
			cpMobile(){
				this.mobilePx=this.nowD/this.sumD*this.wid
			}
		}
	}
</script>

<style >
	
	.progress-box {
		display: flex;
		margin: auto auto;
		flex-direction: column;
	}
	
	.progress-box-sgin{
		height: 80rpx;
		margin: auto auto;
		
	}
	.progress-box-sgin-n{
		text-align: center;
		position: relative;
		width: 120rpx;
		height: 60rpx;
		border-radius: 50rpx;
		box-shadow:0px 3px 6px rgba(3,144,252,1);
	}
	.progress-box-sgin-n>text{
		width:8px;
		height:20px;
		font-size:15px;
		font-family:SFProText-Semibold;
		line-height:20px;
		opacity:1;
	}
	
	.progress-box-sgin-n:after{
		position: absolute;
		left: 0rpx;
		right: 0;
		top: 60rpx;
		content: '';
		width: 0;
		height: 0;
		margin: auto auto;
		border: 16rpx solid #F4F4F4;
		border-color: #F4F4F4 transparent  transparent transparent;
	}
	.progress-box-w {
		overflow:hidden;
		margin: auto auto;
		border-radius: 10rpx;
		background-color:  #FFFFFF;
	}
	.progress-box-w-w{
		border-radius: 10rpx;
		width: 100%;
		height: 20rpx;
	}
	.progress-box-w-n{
		height: 20rpx;
		background-color:  #FFFFFF;
		width: 20rpx;
		border-radius: 50%;
	}
</style>
