<template>
	<view class="home">

		<swiper indicator-dots autoplay circular>
			<swiper-item v-for="item in lunboList" :key="item.id">
				<image :src="item.img"></image>
			</swiper-item>
		</swiper>
		<!-- nav -->
		<view class="nav">
			<view class="nav-item" v-for="(item,index) in navList" :key="index" @click="goPage(item.path)">
				<view :class="item.icon"></view>
				<text>{{item.title}}</text>
			</view>
		</view>
		<view class="line"></view>
		<!--推荐商品 -->
		<view class="title">推荐商品</view>
		<view class="line"></view>
		<good-list :goodsList="goodsList"></good-list>
		<!-- <view class="goods">
			<view class="goods_item" v-for="item in goodsList" :key="item.id">
				<view class="img">
					<image :src="item.img_url"></image>
				</view>
				<view class="info">
					<span>¥{{item.sell_price}} <text>¥{{item.market_price}}</text></span>
					<view>{{item.title}}</view>
				</view>
			</view>

		</view>
 -->
	</view>
</template>

<script>
	import goodList from '../../components/goodList.vue'
	export default {
		components:{
			goodList
		},
		data() {
			return {
				lunboList: [],
				goodsList: [],
				navList:[
					{
						icon:'iconfont icon-ziyuan',
						title:'uni超市',
						path:'/pages/goods/goods'
					},
					{
						icon:'iconfont icon-guanyuwomen',
						title:'联系我们',
						path:'/pages/aboutUs/aboutUs'
					},
					{
						icon:'iconfont icon-tupian',
						title:'社区图片',
						path:'/pages/pics/pics'
					},
					{
						icon:'iconfont icon-shipin',
						title:'学习视频',
						path:'/pages/videos/videos'
					}
				],
				pageNum: 1,
			}
		},
		onLoad() {
			this.getLunbo();
			this.getGoods(this.pageNum)

		},
		methods: {
			async getLunbo() {
				const res = await this.$http({
					url: '/api/getlunbo'
				})
				this.lunboList = res.data.message
			},
			async getGoods(pageNum) {
				if (pageNum <= 2) {
					const res = await this.$http({
						url: '/api/getgoods?',
						data: {
							pageindex: pageNum
						}
					})
					this.goodsList.push(...res.data.message)
				}

			},
			goPage(path){
				uni.navigateTo({
					url:path
				})
			}
		}
	}
</script>

<style lang="scss">
	.home {
		swiper {
			width: 750rpx;
			height: 380rpx;

			image {
				width: 100%;
				height: 100%;
			}
		}

		.nav {
			padding-top: 20rpx;
			display: flex;
			width: 100%;
			justify-content: space-around;

			.nav-item {
				height: 212rpx;

				view {
					width: 110rpx;
					height: 110rpx;
					text-align: center;
					font-size: 60rpx;
					margin: 10rpx;
					background-color: #b50e03;
					border-radius: 50%;
					color: white;
					line-height: 110rpx;
				}

				text {
					display: inline-block;
					width: 100%;
					text-align: center;
					font-size: 28rpx;
				}
			}
		}

		.line {
			height: 6rpx;
			width: 100%;
			background-color: #eeeeee;
		}

		.title {
			padding: 20rpx;
			color: #b50e03;
			text-align: center;
			letter-spacing: 40rpx;
		}
	}
</style>
