<template>
	<view class="goods">
		<view class="goods_item" v-for="item in goodsList" :key="item.id" @click="goDetailed(item.id)">
			<view class="img">
				<image :src="item.img_url"></image>
			</view>
			<view class="info">
				<span>¥{{item.sell_price}} <text>¥{{item.market_price}}</text></span>
				<view>{{item.title}}</view>
			</view>
		</view>
	
	</view>
</template>

<script>
	export default{
		props:{
			goodsList:{
				type:Array
			}
		},
		methods:{
			goDetailed(id){
				uni.navigateTo({
					url:"/pages/goods/goodsDetailed?id="+id
				})
			}
		}
	}
</script>

<style lang="scss">
	.goods {
		display: flex;
		padding: 10rpx;
		padding-left: 0;
		flex-wrap: wrap;
		background-color: #eeeeee;
	
		.goods_item {
			width: 354rpx;
			height: 576rpx;
			background-color: white;
			margin-bottom: 16rpx;
			margin-left: 12rpx;
	
			.img {
				width: 100%;
				height: 60%;
	
				image {
					margin: 10% 10%;
					width: 80%;
					height: 80%
				}
			}
	
			.info {
	
				span {
					color: #b50e03;
					display: inline-block;
					padding: 12rpx 0 14rpx 30rpx;
	
					text {
						color: #d5d5d5;
						font-size: 24rpx;
						text-decoration: line-through;
						margin-left: 20rpx;
					}
				}
	
				view {
					padding-left: 30rpx;
					font-size: 32rpx;
					display: -webkit-box;
					-webkit-box-orient: vertical;
					-webkit-line-clamp: 3;
					overflow: hidden;
				}
			}
	
	
		}
	}
</style>
