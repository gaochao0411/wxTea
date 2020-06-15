<template>
	<view class="content interagl-mall">
		<view class="header">
			<view class="container">
				<view class="user-info">
					<view>
						<text class="iconfont icon-money">&#xe602;</text>
					</view>
					<view style="color:#fff;font-size: 40upx; padding: 20upx 0;">
						有茶币：
						<text style="color: #fff100;">{{money}}</text>
					</view>
					<navigator url="/pages/home/home" hover-class="navigator-hover">
						<text class="underline">兑换记录</text>
					</navigator>
				</view>
				<view class="QR-code">
					<view class="iconfont">&#xe632;</view>
				</view>
			</view>
		</view>
		<view class="main">
			<uni-segmented-control :current="current" :values="items" @clickItem="onClickItem" style-type="button" active-color="#999"></uni-segmented-control>
			<view class="content">
				<view v-show="current === 0">
					<view class="card-item" v-for="item in cardData" :key="item.id">
						<view class="container">
							<view class='title'>
								<text>{{item.title}}</text>
								<view class="right">
									<text class="money">{{item.money}}</text>
									有茶币
								</view>
							</view>
							<view class='requirement'>
								<text>{{item.requirement}}</text>
								<button class="right my-button" type="mini">兑换</button>
							</view>
							<!-- 查看说明 -->
							<uni-collapse accordion="true">
							    <uni-collapse-item title="点击查看说明">
							        <view style="padding: 30rpx;" v-html="item.description">
							            <!-- {{item.description}} -->
							        </view>
							    </uni-collapse-item>
							</uni-collapse>
						</view>
					</view>
				</view>
				<view v-show="current === 1">
					<view class="goods-item" v-for="item in goodsData" :key="item.id">
						<view class="container">
							<view class="uni-flex" style="margin-bottom: 40upx;">
								<view class='uni-flex-item' style="flex:2">
									<image :src="item.images" mode=""></image>
								</view>
								<view class='uni-flex-item desc' style="flex:3">
									<view class="title">{{item.title}}</view>
									<view class="uni-flex">
										<view class='uni-flex-item' >
											<text class="money">{{item.money}}</text>
											有茶币
										</view>
										<view class='uni-flex-item clearfix'>
										    <button class="my-button right" type="mini">兑换</button>
										</view>
									</view>
								</view>
							</view>
							<!-- 查看说明 -->
							<uni-collapse accordion="true">
							    <uni-collapse-item title="点击查看说明">
							        <view style="padding: 30rpx;" v-html="item.description">
							            <!-- {{item.description}} -->
							        </view>
							    </uni-collapse-item>
							</uni-collapse>
						</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import uniSegmentedControl from "@/components/uni-segmented-control/uni-segmented-control.vue"
	export default {
		components: {uniSegmentedControl},
		data() {
			return {
				money: '34', //有茶币
				items: ['卡券','周边商品'],
				current: 0,
				cardData:[ // 卡券数据
					{
						id:1,
						title:'鲜果茶系列兑换券',
						money:'266',
						requirement:'无使用门槛',
						description:'1、可使用该兑换券兑换任意的鲜果茶系列 \<br/\> 2、有效期2个月'
					},
					{
						id:2,
						title:'小程序免配送费',
						money:'88',
						requirement:'无使用门槛',
						description:'1、可使用该兑换券免配送费 \<br/\> 2、有效期2个月'
					},
					{
						id:3,
						title:'满49减8元券',
						money:'266',
						requirement:'无使用门槛',
						description:'1、可使用该兑换券兑换任意的商品 \<br/\> 2、有效期2个月'
					}
				],
				goodsData:[
					{
						id:1,
						images:'../../static/goods1.jpg',
						title:'限量卡牌券',
						money:'288',
						description:'1、可使用该兑换券兑换卡牌 \<br/\> 2、有效期2个月'
					},
				],
			}
		},
		onLoad() {
			
		},
		methods: {
			onClickItem(e) {
				if (this.current !== e.currentIndex) {
					this.current = e.currentIndex;
				}
			}
		}
	}
</script>

<style scoped>
	.user-info .icon-money {
		font-size: 60upx;
		color: #fff100 ;
	}
	.underline {
		color: #999;
		text-decoration: underline;
	}
	.card-item {
		padding: 30upx 30upx;
		color: #9b9b9b;
	}
	.card-item .container{
		padding: 30upx;
		box-shadow: 0px 0px 3px 0px rgba(0,0,0,0.2);
	}
	.card-item .title>text {
		font-size: 34upx;
		color: #333;
		font-weight: bold;
	}
	.card-item .title .right {
		margin-top: 10upx;
	}
	.card-item .money {
		color: #fff100;
		float: left;
		font-size: 34upx;
		margin-top: -6upx;
		font-weight: normal;
	}
	.card-item text ,.card-item view {
		color: #999;
	}
	.card-item .requirement {
		margin-top: 30upx;
		height: 96upx;
		line-height: 80upx;

	}
	/* 修正样式 */
	.interagl-mall /deep/.uni-collapse-cell {
		border-bottom:0 ;
		background: #f1f1f1;
	}
	.goods-item {
		padding: 30upx 30upx;
		color: #9b9b9b;
	}
	.goods-item .container{
		padding: 30upx;
		box-shadow: 0px 0px 3px 0px rgba(0,0,0,0.2);
	}
	.goods-item .uni-flex-item image{
		width: 180upx;
		height: 200upx;
	}
	.goods-item .uni-flex-item .title{
		font-size: 34upx;
		color: #333;
		font-weight: bold;
		margin-bottom: 60upx;
	}
	.goods-item .money {
		font-size: 48upx;
		margin-right: 10upx;
		color: #fff100;
	}
</style>
