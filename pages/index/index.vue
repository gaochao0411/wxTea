<template>
	<view class="content">
		<!-- 头部--卡片 -->
		<view class="header">
			<view class="container">
				<navigator url="/page/home/home" hover-class="navigator-hover">
					<view class="user-info">
						<view class="container">
							<!-- 用户头像 -->
							<image :src="userImage" mode="" class="user-image"></image>
							<!-- 用户姓名 -->
							<view><text style="color:#fff;font-size: 30upx;">{{userName}} &gt;</text></view>
							<view><text style="color:#ccc;font-size: 20upx;">点击激活会员</text></view>
						</view>
					</view>
					<view class="QR-code">
						<view class="iconfont">&#xe632;</view>
					</view>
				</navigator>
			</view>
		</view>
		<!-- 会员--注册 -->
		<view class="member-register">
			<view class="container">
				<image src="../../static/member.png" mode="" class="member-img" ></image>
				<text>新会员注册，即得6元代金券</text>
				<text class="iconfont right" style="float: right;">&#xe70d;</text>
			</view>
		</view>
		<!-- 堂食-->
		<view class="order" id="hallFood">
			<view class="container uni-flex">
				<view class="uni-flex-item">
					<image src="../../static/hallFood.png" mode="" style="width: 200upx;height: 200upx;"></image>
				</view>
				<view class="uni-flex-item">
					<text class="title">堂食点单</text>
					<text class="desc">选一杯喜欢的茶吧</text>
				</view>
				<view class="uni-flex-item">
					<button type="mini">点 单</button>
				</view>
			</view>
		</view>
		<!-- 外卖-->
		<view class="order" id="takeoutFood">
			<view class="container uni-flex">
				<view class="uni-flex-item">
					<image src="../../static/takeoutFood.png" mode="" style="width: 200upx;height: 200upx;"></image>
				</view>
				<view class="uni-flex-item">
					<text class="title">外卖点单</text>
					<text class="desc">今日饮茶</text>
				</view>
				<view class="uni-flex-item">
					<button type="mini">外 卖</button>
				</view>
			</view>
		</view>
		<!-- 活动-->
		<view class="activity">
			<view class="container">
				<view class="image-container">
					<image src="../../static/activity1.png" mode=""></image>
				</view>
				<view class="image-container">
					<image src="../../static/activity2.png" mode=""></image>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				userName: '', //用户名称
				userImage:'', //用户图片
			}
		},
		onLoad() {
			// 获取用户信息
			var _this = this;
			wx.getUserInfo({
			  success: function(res) {
				  console.log(res)
			    _this.userName = res.userInfo.nickName;
			    _this.userImage = res.userInfo.avatarUrl;
			  }
			})
		},
		methods: {

		}
	}
</script>

<style>
	.container {
		padding: 0 30upx;
		position: relative;
	}
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}
	.user-info {
		height: 300upx;
		margin-top: 30upx;
		border:1px solid #ccc;
		border-radius: 20upx 20upx 0 0;
		background: #6d7170;
		padding: 30upx 30upx 0 30upx;
	}
	.QR-code {
		position: absolute;
		top: 80upx;
		right: 80upx;
		width: auto;
	}
	.QR-code .iconfont {
		color: #ccc;
		font-size: 100rpx;
	}
	.user-image {
		width: 80upx;
		height: 80upx;
		border-radius:50% ;
	}
	.user-info .container{
		border:1px solid #757978;
		border-bottom: 0;
		height: 100%;
		padding-top: 30upx;
		border-radius: 20upx 20upx 0 0;
	}
	.member-register {
		height: 60upx;
		background: #f9f9f9;
	}
	.member-register .container{
		line-height: 60upx;
	}
	.order .iconfont{
		font-size: 150upx;
	}
	.order .uni-flex-item{
		align-self:center;
		text-align: center;
		height: auto;
	}
	.order button{
		height: 70upx;
		line-height: 70upx;
		width: 140upx;
		font-size: 30upx;
	}
	.order .title {
		display: block;
	}
	.order .desc {
		font-size: 20upx;
		color: #999;
	}
	.activity .image-container {
		margin: 40upx 0;
		width: 100%;
		height: 320upx;
		border-radius: 20upx;
		overflow: hidden;
	}
	.activity image {
		width: 100%;
		border-radius: 20upx;
	}
	.member-img {
		width: 40upx;
		height: 40upx;
		margin-right:20upx; 
		vertical-align: middle;
		margin-top: -10upx;
	}
</style>
