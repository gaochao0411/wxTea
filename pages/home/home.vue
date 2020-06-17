<template>
	<view class="content home">
		<view class="header">
			<!-- 背景图 -->
			<view class="bg-color"></view>
			<!-- 用户头像 -->
			<image :src="userImage" mode="" class="user-image"></image>
			<!-- 用户姓名 -->
			<view class="user-name"><text >{{userName}}</text></view>
		</view>
		<!-- 资产 -->
		<view class="wealth">
			<view class="wealth-item">
				<text>茶多分</text>
				<text class="money">336</text>
			</view>
			<view class="wealth-item">
				<text>有茶币</text>
				<text class="money">36</text>
			</view>
		</view>
		<!-- 列表 -->
		<view class="list-container">
			<uni-list>
			    <uni-list-item thumb="../../static/icon-card.png" title="我的卡包" rightText="0张优惠券"></uni-list-item>
			    <uni-list-item thumb="../../static/icon-member.png" title="会员权益" rightText="当前组别 黄金会员"></uni-list-item>
			    <uni-list-item thumb="../../static/icon-adress.png" title="我的收货地址" rightText="历史收货地址"></uni-list-item>
			    <uni-list-item thumb="../../static/icon-edit.png" title="会员信息" ></uni-list-item>
				<uni-list-item thumb="../../static/icon-gift.png" title="礼品" rightText="礼品商城"></uni-list-item>
				<uni-list-item thumb="../../static/icon-service.png" title="客服" rightText="立即咨询"></uni-list-item>
			</uni-list>
		</view>
	</view>
</template>

<script>
	import uniList from "@/components/uni-list/uni-list.vue"
	import uniListItem from "@/components/uni-list-item/uni-list-item.vue"
	export default {
	    components: {uniList,uniListItem},
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
	.header {
		height: 300upx;
		overflow: hidden;
		position: relative;
	}
	.header .user-image{
		width: 160upx;
		height: 160upx;
		border-radius: 50%;
		position: absolute;
		z-index: 20;
		left: 50%;
		margin-left: -80upx;
		bottom: 50upx;
	}
	.header .user-name{
		color: #999;
		font-size: 30upx;
		position: absolute;
		z-index: 20;
		left: 0;
		bottom: 0;
		width: 100%;
		text-align: center;
	}
	.header .bg-color{
		background-color: #6d7170;
		width: 1000upx;
		height: 1000upx;
		border-radius: 50%;
		position: absolute;
		bottom: 85upx;
		left: 50%;
		margin-left: -500upx;
		z-index: 10;
	}
	.wealth {
		display: flex;
		padding: 20upx 30upx;
	}
	.wealth .wealth-item {
		flex: 1;
		text-align: center;
	}
	.wealth .wealth-item .money{
		display: block;
		color: #fdad00;
	}
</style>
