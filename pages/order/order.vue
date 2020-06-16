<template>
	<view class="content order">
		<view style="padding: 20upx 30upx 0; ">
			<button type="default" class="my-button" style="float: right;">申请发票</button>
		</view>
		
		<!-- 当前订单 -->
		<view class="current-order">
			<view class="title-bar">
				当前订单
			</view>
			<view style="padding: 0 30upx;">还没订单，请去查看订单</view>
		</view>
		<!-- 已完成订单 -->
		<view class="completed-order">
			<view class="title-bar">
				已完成订单
			</view>
			<uni-card :title="item.shopName"  :extra="item.status"  class="order-item" v-for="item in completedOrder" :key="item.id">
			    <view class="date">{{item.date}}</view>
				<view class="uni-flex">
					<view class="uni-flex-item" >
						<text>{{item.goodsName}}</text>
					</view>
					<view class="uni-flex-item" style="text-align: right; margin-top: 20upx;">
						<button type="default" class="my-button" style="margin-right: 20upx;">再来一单</button>
						<button type="default" class="my-button">评价</button>
					</view>
				</view>
			</uni-card>
		</view>
		
	</view>
</template>

<script>
	import uniCard from '@/components/uni-card/uni-card.vue'
	export default {
	    components: {uniCard},
		data() {
			return {
				completedOrder:[
					{ 
						id:1,
						shopName:'福永益田假日店',
						status:'买家已签收',
						date:'2020-05-18 15:08:02',
						goodsName:'珍珠奶茶,共2杯'
					}
				]
		    }
		},
	}
</script>

<style scoped>
	.title-bar {
		background: #eee;
		height: 80upx;
		line-height: 80upx;
		font-size: 28upx;
		color: #999;
		padding: 0 30upx ;
		margin: 20upx 0;
	}
	.order view {
		color: #999;
	}
	.order-item .uni-flex-item {
		align-self: center;
	}
</style>
