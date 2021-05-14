<template>
	<view class="detailed">
		<swiper indicator-dots autoplay circular>
			<swiper-item v-for="item in imgList" :key="item.id">
				<image :src="item.src"></image>
			</swiper-item>
		</swiper>
		<view class="info">
			<span><text>¥{{info.sell_price}}</text> <text>¥{{info.market_price}}</text></span>
			<view>{{info.title}}</view>
		</view>
		<view class="line"></view>
		<view class="info">
			<view>货号：{{info.goods_no}}</view>
			<view>库存：{{info.stock_quantity}}</view>
		</view>
		<view class="line"></view>
		<view class="detailedInfo">
			<view class="title">详情介绍</view>
			<view class="content">
				<rich-text :nodes="desc.content"></rich-text>
			</view>

			<!-- <scroll-view class="content" v-html="desc.content" scroll-y></scroll-view> -->
		</view>
		<view class="nav">
			<uni-goods-nav :fill="true" :options="options" :buttonGroup="buttonGroup" @click="onClick" @buttonClick="buttonClick" />
		</view>
		
	</view>
</template>

<script>
	import uniGoodsNav from '@/components/uni-goods-nav/uni-goods-nav.vue'
	export default {
		components: {
			uniGoodsNav
		},
		data() {
			return {
				imgList: [],
				info: {},
				desc: {},
				options: [{
					icon: 'headphones',
					text: '客服'
				}, {
					icon: 'shop',
					text: '店铺',
					// info: 2,
					// infoBackgroundColor: '#007aff',
					// infoColor: "red"
				}, {
					icon: 'cart',
					text: '购物车',
					info: 2
				}],
				buttonGroup: [{
						text: '加入购物车',
						backgroundColor: '#ff0000',
						color: '#fff'
					},
					{
						text: '立即购买',
						backgroundColor: '#ffa200',
						color: '#fff'
					}
				]
			}
		},
		onLoad(option) {
			this.getDetailed(option.id)
		},
		methods: {
			async getDetailed(id) {
				const imgRes = await this.$http({
					url: '/api/getthumimages/' + id
				})
				this.imgList = imgRes.data.message;
				const infoRes = await this.$http({
					url: '/api/goods/getinfo/' + id
				})
				this.info = infoRes.data.message[0] || {}
				const descRes = await this.$http({
					url: '/api/goods/getdesc/' + id
				})
				this.desc = descRes.data.message[0] || []
			},
			onClick(e) {
				uni.showToast({
					title: `点击${e.content.text}`,
					icon: 'none'
				})
			},
			buttonClick(e) {
				console.log(e)
				e.index===0?this.options[2].info++:(this.options[2].info>0?this.options[2].info--:'')
			}

		}
	}
</script>

<style lang="scss">
	.detailed {
		swiper {
			width: 750rpx;
			height: 700rpx;

			image {
				width: 100%;
				height: 100%;
			}
		}

		.info {
			padding: 20rpx 30rpx;

			span {
				color: #b50e03;
				display: inline-block;
				padding: 12rpx 0 14rpx 30rpx;

				text:first-child {
					font-size: 42rpx;
				}

				text:last-child {
					color: #d5d5d5;
					font-size: 30rpx;
					text-decoration: line-through;
					margin-left: 20rpx;
				}
			}
		}

		.line {
			height: 8rpx;
			width: 100%;
			background-color: #eeeeee;
		}

		.detailedInfo {

			.title {
				height: 52rpx;
				line-height: 48rpx;
				border-bottom: 4rpx solid #eee;
				padding: 10rpx 30rpx;
			}

			.content {
				padding: 10rpx 30rpx;
				font-size: 28rpx;
				line-height: 50rpx;
				color: #333;
			}
		}
		.nav{
			width: 100%;
			background-color: white;
			position: fixed;
			bottom: 0;
		}
	}
</style>
