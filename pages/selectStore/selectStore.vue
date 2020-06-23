<!-- 选择门店 -->
<template>
	<view class="content select-store">
		<view class="search">
			<view class="left" @click="viewStore">
				查看所有门店
				<text class="iconfont up" v-show="!showAllStore">&#xe637;</text>
				<text class="iconfont down" v-show="showAllStore">&#xe638;</text>
			</view>
			<view class="left">
				<input class="uni-input search-input" confirm-type="search" placeholder="搜索门店" />
			</view>
		</view>
		<view class="page-body">
			<view class="page-section page-section-gap">
				<map style="width: 100%; height: 100%;"
				 ref="map1"
				    id="storeMap"
					:show-location="true" 
					:show-compass="true" 
					:latitude="latitude" 
					:longitude="longitude"
					:markers="covers"
					@tap="tap"
					@markertap="markertap">
				</map>
			</view>
		</view>
		<!-- 最近门店信息 -->
		<view class="store-item" v-show="!showAllStore">
			<view class="name">
				{{storeList[current].name}}<text class="distance">{{storeList[current].distance}}</text>
			</view>
			<view class="address">
				{{storeList[current].address}}
			</view>
			<view class="uni-flex" style="margin-top: 30upx;">
				<view class="uni-flex-item grade" style="flex: 2;">
					<uni-rate  size="18" :value="storeList[current].rate"></uni-rate> <text>{{storeList[current].rate}}分</text>
				</view>
				<view class="uni-flex-item" style="flex: 1;" @click="openMap">
					<text class="iconfont">&#xe65f;</text> 到这里
				</view>
				<view class="uni-flex-item" style="flex: 1;">
					<text class="iconfont">&#xe600;</text> 联系门店
				</view>
			</view>
			<button type="primary" style="margin-top: 40upx;" @click="gotoMenu">进入菜单</button>
		</view>
		<!-- 回到手机自己定位点 -->
		<view class="back-origin" @click="backOrigin">
			<view class="box">
				<text class="iconfont">&#xe7d2;</text>
			</view>
		</view>
		<view class="store-list" v-show="showAllStore">
			<view class="box">
				<radio-group>
					<label class="uni-list-cell uni-list-cell-pd" v-for="(item, index) in storeList" :key="item.id">
						<view style="flex: 1;">
							<radio :value="item.id" :checked="index === current" />
						</view>
						<view style="flex: 4;">
						  <view class="uni-flex">
							  <view class="uni-flex-item" style="flex: 3;">
							     {{item.name}} <text class="status">营业中</text>
							     <view style="margin-top: 10upx; color: #999;">营业时间：{{item.businessHours}}</view>
							  </view>
							  <view class="uni-flex-item" style="flex: 1;">
							     {{item.distance}}
							  </view>
						  </view>
						</view>
					</label>
				</radio-group>
			</view>
			<button type="primary" style="margin: 40upx 0;">进入门店</button>
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
				}],
				current:0, // 当前门店
				storeList:[ // 所有门店的信息 ,默认按距离排好序
					{
						id:0,
						latitude: 22.535747337687695,
						longitude: 113.93247127532959,
						iconPath: '../../static/position.png',
						name:'科兴科学园店',
						address:'南山区粤海街道科兴科学园BG-13号铺',
						rate:'5.0',
						businessHours:'10:00~21:30'
					},
					{
						id:1,
						latitude: 22.524370661516432,
						longitude: 113.93500328063965,
						iconPath: '../../static/position.png',
						name:'皇廷广场店',
						address:'后海区粤海街道科兴科学园BG-14号铺',
						rate:'4.7',
						businessHours:'10:00~22:30'
					},
					{
						id:2,
						latitude:  22.529603256137566,
						longitude:  113.91826629638672,
						iconPath: '../../static/position.png',
						name:'龙华CO CO店',
						address:'龙华区华龙街道BG-13号铺',
						rate:'4.8',
						businessHours:'10:00~23:30'
					}
				],
			}
		},
		onLoad() {
			// 获取用户当前位置
			var _this = this;
			uni.getLocation({
				type: 'gcj02',
				success: function(res) {
					console.log(res.latitude,res.longitude)
					_this.latitude = res.latitude;
					_this.longitude = res.longitude;
					_this.covers[0].latitude = res.latitude;
					_this.covers[0].longitude = res.longitude;
					// 填入门店信息，计算距离
					_this.storeList.forEach(item=>{
						var obj = {
							id:item.id,
							latitude:item.latitude,
							longitude:item.longitude,
							iconPath:item.iconPath,
							width:20,
							height:20
						}
						var distance = _this.getDistance(_this.latitude,_this.longitude,item.latitude,item.longitude);
						item.distance = (distance/1000).toFixed(2)+'km';
						// 推入门店坐标
						_this.covers.push(obj)
					})
				}
			});
		},
		methods: {
			// 进入菜单
			gotoMenu(){
				uni.navigateTo({
					url:'../goods/goods?id=1'
				})
			},
			// 打开地图
			openMap(){
				var _this = this;
				wx.openLocation({
				  latitude:_this.latitude,
				  longitude:_this.longitude,
				  scale: 18,
				  name:_this.storeList[_this.current].name
			   })
			},
			// 点击标记点
			markertap(data){
				// console.log(obj)
				this.current = data.markerId;
			},
			// 查看门店
			viewStore(){
				this.showAllStore=!this.showAllStore;
			},
			// 点击地图的某个点
			tap(data){
				// console.log(data)
			},
			// 回到原点
			backOrigin(){
				var _this=this;
				var mapContext =  uni.createMapContext('storeMap', this);
				mapContext.moveToLocation();
			},
			// 计算距离
			getDistance(lat1, lng1, lat2, lng2) {
			  lat1 = lat1 || 0;
			  lng1 = lng1 || 0;
			  lat2 = lat2 || 0;
			  lng2 = lng2 || 0;
			
			  var rad1 = lat1 * Math.PI / 180.0;
			  var rad2 = lat2 * Math.PI / 180.0;
			  var a = rad1 - rad2;
			  var b = lng1 * Math.PI / 180.0 - lng2 * Math.PI / 180.0;
			  var r = 6378137;
			  var distance = r * 2 * Math.asin(Math.sqrt(Math.pow(Math.sin(a / 2), 2) + Math.cos(rad1) * Math.cos(rad2) * Math.pow(Math.sin(b / 2), 2)));
			  
			  return distance;
			}
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
	.back-origin {
		position: absolute;
		top: 50%;
		left: 30upx;
		width: auto;
	}
	.back-origin .box {
		height: 50upx;
		width: 50upx;
		background: #fff;
		box-shadow: 0 0 5px 1px rgba(0,0,0,0.2);
		text-align: center;
		border-radius: 8upx;
	}
	.back-origin text {
		font-size: 40upx;
		color: #333;
		font-weight: bold;
		line-height: 50upx;
	}
	.store-list {
		position: absolute;
		bottom: 0;
		height: 512upx;
		padding:40upx;
		background: #fff;
	}
	.store-list .box {
		height: 300upx;
		overflow: auto;
	}
	.store-list .box .uni-list-cell {
		padding: 20upx 0;
	}
	.store-list .box .uni-list-cell::after {
		height: 0;
	}
	.uni-flex-item {
		align-self: center;
	}
	.store-list .status {
		background: #1aad19;
		border-radius: 10upx;
		color: #fff;
		font-size: 24upx;
		padding: 4upx 8upx;
		margin-left: 16upx;
	}

</style>
