<template>
	<view class="content">
		<view class="header">
			<view class="container">
				<navigator url="/page/home/home" hover-class="navigator-hover">
					<view class="user-info">
						<!-- 用户头像 -->
						<image :src="userImage" mode="" class="user-image"></image>
						<!-- 用户姓名 -->
						<view><text>{{userName}}</text></view>
						<view><text>点击激活会员</text></view>
					</view>
				</navigator>
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
	}
	.user-image {
		width: 80upx;
		height: 80upx;
		border-radius:50% ;
	}

</style>
