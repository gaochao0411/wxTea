<template>
	<view class="content goods">
		<view class=" header">
			<text style="color: #007AFF;">[切换]</text>
			<text class="name">{{name}}</text>
			<text style="font-size: 20upx;">{{status}}</text>
			<view class="right" style="margin-top: 30upx;">
				<text class="iconfont">&#xe600;</text> 联系门店
			</view>
		</view>
		<view class="goods-list">
			<scroll-view class="nav-left" scroll-y :style="'height:'+height+'px'">
				<view class="nav-left-item" @click="categoryClickMain(item,index)" :key="index" :class="index==categoryActive?'active':''"
				 v-for="(item,index) in categoryList">
					{{item.name}}
				</view>
			</scroll-view>
			<scroll-view class="nav-right" scroll-y :scroll-top="scrollTop" @scroll="scroll" :style="'height:'+height+'px'"
			 scroll-with-animation>
				<view class="uni-list">
					<view class="uni-list-cell" :id="index===0?'first':''" hover-class="uni-list-cell-hover" v-for="(item,index) in subCategoryList"
					 :key="index">
						<view class="uni-media-list">
							<view class="uni-media-list-logo">
								<image :src="item.logo"></image>
							</view>
							<view class="uni-media-list-body">
								<view class="uni-media-list-text-top">{{item.name}}</view>
								<view class="uni-media-list-text-bottom uni-ellipsis">{{item.intro}}</view>
								<view class="select-type">
									<text>￥{{item.price}} </text>
									<button type="primary" class="my-button" @click="selectSpecific(index)">选规格</button>
								</view>
							</view>
						</view>
					</view>
				</view>
			</scroll-view>
		</view>
		<!-- 购物车 -->
		<view class="shop-cart">
			<view class="cart">
				<view class="container" v-bind:class="{active:isActive}" @click="open">
					<text class="iconfont">&#xe601;</text>
				</view>
				<view class="badge" v-if="isActive">{{shopCartList.length}}</view>
			</view>
			<button type="button" class="right" v-bind:class="{active:isActive}" >去下单</button>
			
		</view>
		<uni-popup  ref="middlePopup"  type="middle" animation="true"  maskClick="true" class="specific-list">
			<view class="container">
				<image :src="currentCategory.logo"></image>
				<view class="specfic">
					<text>规格:</text>
					<view class="paramas-list">
						<text class="active">{{currentCategory.name}}</text>
					</view>
					<text>冰量:</text>
					<view class="paramas-list">
						<text class="active">正常冰</text>
						<text>少冰</text>
						<text>去冰</text>
					</view>
					<text>甜度:</text>
					<view class="paramas-list">
						<text class="active">正常糖</text>
						<text>少糖</text>
						<text>3分糖</text>
					</view>
				</view>
				<view class="footer">
					<text>{{currentCategory.intro}}</text>
					<view style="margin-top: 10upx; ">
						<text>￥{{currentCategory.price}} </text>
						<text class="right iconfont" >&#xe601;</text>
					</view>
				</view>
			</view>
		</uni-popup>
		<uni-popup  ref="bottomPopup"  type="bottom" animation="true"  maskClick="true" class="cart-list">
			<view class="title">
				<view class="right"><text class="iconfont">&#xe61e;</text>清空购物车</view>
			</view>
		    <view class="content">
				
			</view>
		</uni-popup>
	</view>
</template>

<script>
	import uniPopup from '@/components/uni-popup/uni-popup.vue'
	export default {
		components: {
			uniPopup
		},
		computed: {
			isActive(){
				return this.shopCartList.length>0
			}
		},
		data() {
			return {
				storeId: '',
				name: '科兴科学园店',
				status: '营业中',
				tel: '0755-1265269',
				categoryList: [{
						value: 1,
						name: '应季限定系列',
						subCategoryList: [{
								id: 11,
								logo: '../../static/category1.jpg',
								name: '应季限定系列1',
								price: '23',
								intro: '浓郁奶香，爽滑口感，清爽的果味'
							},
							{
								id: 12,
								logo: '../../static/category2.jpg',
								name: '应季限定系列2',
								price: '26',
								intro: '浓郁奶香，爽滑口感，清爽的果味'
							}
						]
					},
					{
						value: 2,
						name: '有料方杯鲜果茶',
						subCategoryList: [{
								id: 21,
								logo: '../../static/category1.jpg',
								name: '有料方杯鲜果茶1',
								price: '23',
								intro: '浓郁奶香，爽滑口感，清爽的果味'
							},
							{
								id: 22,
								logo: '../../static/category2.jpg',
								name: '有料方杯鲜果茶2',
								price: '26',
								intro: '浓郁奶香，爽滑口感，清爽的果味'
							}
						]
					},
					{
						value: 3,
						name: '大块鲜果爆爆冰系列',
						subCategoryList: [{
								id: 31,
								logo: '../../static/category1.jpg',
								name: '大块鲜果爆爆冰系列1',
								price: '23',
								intro: '浓郁奶香，爽滑口感，清爽的果味'
							},
							{
								id: 32,
								logo: '../../static/category2.jpg',
								name: '大块鲜果爆爆冰系列2',
								price: '26',
								intro: '浓郁奶香，爽滑口感，清爽的果味'
							}
						]
					},
					{
						value: 4,
						name: '芝士奶盖茶冰系列',
						subCategoryList: [{
								id: 41,
								logo: '../../static/category1.jpg',
								name: '芝士奶盖茶冰系列1',
								price: '23',
								intro: '浓郁奶香，爽滑口感，清爽的果味'
							},
							{
								id: 42,
								logo: '../../static/category2.jpg',
								name: '芝士奶盖茶冰系列2',
								price: '26',
								intro: '浓郁奶香，爽滑口感，清爽的果味'
							}
						]
					},
				],
				subCategoryList: [], // 子系列的产品列表
				currentCategory:{}, // 当前产品
				height: 0,
				categoryActive: 0,
				scrollTop: 0,
				scrollHeight: 0,
				shopCartList:[],	
				show:true
			}
		},
		onLoad(option) {
			var _this = this;
			// 获取当前url的参数,根据门店id获取信息
			this.storeId = JSON.parse(decodeURIComponent(option.id));
			// 设置高度
			this.height = uni.getSystemInfoSync().windowHeight-100;
			this.subCategoryList = this.categoryList[0].subCategoryList;
		},
		methods: {
			// 选规格
			selectSpecific(index){
				this.currentCategory = JSON.parse(JSON.stringify(this.subCategoryList[index]));
				this.$refs.middlePopup.open();
			},
			// 打开购物车
			open() {
				this.$refs.bottomPopup.open()
			},
			categoryClickMain(categroy, index) {
				this.categoryActive = index;
				this.subCategoryList = categroy.subCategoryList;
				this.scrollTop = -this.scrollHeight * index;
			},
		}
	}
</script>

<style scoped>
	.goods .header {
		position: absolute;
		top: 0;
		height: 100upx;
		line-height: 100upx;
		background: #fff;
		padding: 0 30upx;
		box-shadow: 0 0 3px 0 rgba(0, 0, 0, 0.2);
		z-index: 5;
	}

	.header .name {
		color: #000;
		font-size: 30upx;
		font-weight: bold;
		margin: 0 20upx;
	}

	/* 商品列表样式 */
	.goods-list {
		display: flex;
		padding: 100upx 0;
		box-sizing: border-box;
	}

	.nav {
		display: flex;
		width: 100%;
	}

	.nav-left {
		width: 30%;
		background: #f7f8f9;
	}

	.nav-left view {
		font-size: 24upx;
	}

	.nav-left-item {
		height: 150upx;
		font-size: 30upx;
		display: flex;
		align-items: center;
		justify-content: center;
		padding: 0 30upx;
	}

	.nav-right {
		width: 70%;
	}

	.nav-right-item {
		width: 28%;
		height: 220upx;
		float: left;
		text-align: center;
		padding: 11upx;
		font-size: 28upx;
	}

	.nav-right-item image {
		width: 100upx;
		height: 100upx;
	}

	.active {
		color: #007AFF;
		background: #fff;
	}

	.uni-media-list-logo {
		height: 180upx;
		width: 135upx;
	}

	.uni-media-list-body {
		height: 180upx;
	}

	.my-button {
		position: absolute;
		right: 0;
		height: 60rpx;
		font-size: 12px;
		line-height: 60rpx;
	}

	.select-type {
		display: flex;
		align-items: center;
		width: 100%;
		position: relative;
		height: 60upx;
	}
	.shop-cart {
		z-index: 100;
		height: 100upx;
		box-shadow: 0 0 3px 0 rgba(0, 0, 0, 0.2);
		position: absolute;
		background: #fff;
		bottom: 0;
		width: 100%;
	}
	.shop-cart button {
		height: 100upx;
		border-radius: 0;
		width: 200upx;
		background: #ccc;
		color: #fff;
	}
	.shop-cart button.active {
		background: #09BB07;
	}
	.shop-cart .cart {
		float: left;
		position: relative;
		height: 120upx;
		width: 120upx;
		border-radius: 50%;
		line-height: 50upx;
		background: #fff;
		text-align: center;
		top: -28upx;
		left:40upx;
	}
	.shop-cart .cart .container.active {
		background: #09BB07;
	}
	.shop-cart .cart .container {
		background: #ccc;
		border-radius: 50%;
		height: 100upx;
		width: 100upx;
		display: inline-block;
		margin: 10upx;
	}
	.shop-cart .cart .badge {
		position: absolute;
		top: 0;
		right: 0;
		height: 40upx;
		width: 40upx;
		background: #e50000;
		color: #fff;
		border-radius: 50%;
	}
	.shop-cart .iconfont {
		font-size: 48upx;
		float: left;
		margin: 12upx 0 0 -6upx;
	}
	/* 购物车列表 */
	.cart-list {
		
	}
	.cart-list .title {
		height: 60upx;
		background: #ccc;
	}
	.cart-list .title .right {
		margin-top: 8upx;
		padding: 0 15upx;
	}
	.cart-list .content{
		height: 300upx;
		overflow: auto;
		width: 100%;
		background: #fff;
		margin-bottom: 100upx;
	}
	/* 选规格 */
	.specific-list .container{
		background: #fff;
		width: 80%;
		height: auto;
		left: 50%;
		margin-left: -40%;
		top: 100upx;
		padding: 0;
		border-radius: 12upx;
	}
	.specific-list image {
		width: 100%;
	}
	.specific-list .specfic {
		padding: 0 30upx;
	}
	.specific-list .paramas-list {
		display: flex;
		align-items: flex-start;
		margin: 10upx 0;
	}
	.specific-list .paramas-list text{
		margin-right: 20upx;
		padding: 8upx 10upx;
		border: 1px solid #ccc;
		color: #ccc;
		font-size: 24upx;
		border-radius: 8upx;
	}
	.specific-list .paramas-list text.active{
		border: 1px solid #007AFF;
		color: #007AFF;
	}
	.specific-list .footer {
		box-shadow: 0 0 3px 0 rgba(0, 0, 0, 0.2);
		padding: 20upx 30upx;
		margin-top: 20upx;
	}
	.specific-list .footer .iconfont {
		background: #007AFF;
		border-radius: 50%;
		font-size: 32upx;
		color: #fff;
		width: 50upx;
		height: 50upx;
		text-align: center;
	}
</style>
