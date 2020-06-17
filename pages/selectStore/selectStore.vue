<!-- 选择门店 -->
<template>
	<view class="content select-store">
		<view class="search">
			<view class="left">
				查看所有门店
				<text class="iconfont up" v-show="showAllStore">&#xe637;</text>
				<text class="iconfont down" v-show="!showAllStore">&#xe638;</text>
			</view>
			<view class="left">
				<input class="uni-input search-input" confirm-type="search" placeholder="搜索门店" />
			</view>
		</view>
		<view class="page-body">
			<view class="page-section page-section-gap">
				<map style="width: 100%; height: 100%;" 
					:show-location="true" 
					:show-compass="true" 
					:latitude="latitude" 
					:longitude="longitude"
					:markers="covers">
				</map>
			</view>
		</view>
		<!-- 最近门店信息 -->
		<view class="store-item">
			<view class="name">
				科兴科学园店 <text class="distance">3.35km</text>
			</view>
			<view class="address">
				南山区粤海街道科兴科学园BG-13号铺
			</view>
			<view class="uni-flex" style="margin-top: 30upx;">
				<view class="uni-flex-item grade" style="flex: 2;">
					<uni-rate  size="18" value="5.0"></uni-rate> <text>5.0分</text>
				</view>
				<view class="uni-flex-item" style="flex: 1;">
					<text class="iconfont">&#xe65f;</text> 到这里
				</view>
				<view class="uni-flex-item" style="flex: 1;">
					<text class="iconfont">&#xe600;</text> 联系门店
				</view>
			</view>
			<button type="primary" style="margin-top: 40upx;">进入菜单</button>
		</view>
	</view>
</template>

<script>
	import uniRate from '@/components/uni-rate/uni-rate.vue'
	export default {
		components: {uniRate},
		data() {
			return {
				showAllStore:false, // 是否展示所有门店
				latitude: 39.909,
				longitude: 116.39742,
				covers: [{
					latitude: 39.909,
					longitude: 116.39742,
				}]
			}
		},
		onLoad() {
			// 获取用户当前位置
			var _this = this;
			uni.getLocation({
				type: 'wgs84',
				success: function(res) {
					console.log('当前位置的经度：' + res.longitude);
					console.log('当前位置的纬度：' + res.latitude);
					_this.latitude = res.latitude;
					_this.longitude = res.longitude;
					_this.covers[0].latitude = res.latitude;
					_this.covers[0].longitude = res.longitude;
				}
			});
		},
		methods: {

		}
	}
</script>

<style>
	page {
		height: 100%;
	}

	view.select-store,.page-body,.page-section{
		height: 100%;
	}

	.select-store {
		position: relative;
	}

	.select-store .search {
		position: absolute;
		top: 0;
		left: 0;
		height: 90upx;
		line-height: 90upx;
		z-index: 20;
		background: #fff;
		padding: 0 30upx;
	}
	.search view {
		line-height: 90upx;
	}
	.search-input {
		height: auto;
		line-height: auto;
		border:1px solid #ccc;
		border-radius: 10upx;
		padding: 8upx 25upx;
		margin: 12upx 0 0 30upx;
		width: 400upx;
	}
	.store-item {
		position: absolute;
		bottom: 0;
		height: 360upx;
		padding:40upx;
		background: #fff;
	}
	.store-item .name {
		height: auto;
		text-align: center;
		font-size: 32upx;
		position: relative;
	}
	.store-item .name .distance {
		font-size: 24upx;
		color: #666;
		position: absolute;
		right: 0;
	}
	.store-item .address {
		font-size: 20upx;
		color: #999;
		text-align: center;
	}
	.grade uni-rate {
		display: inline-block;
	}
</style>
