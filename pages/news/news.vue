<template>
	<scroll-view class="news" scroll-y>
		<view class="newsItem" v-for="(item,index) in newsList" :key="index" @click=goDetailed(item.id)>
			<view class="picLeft">
				<image :src="item.img_url"></image>
			</view>
			<view class="right">
				<view>{{item.title}}</view>
				<text>发表时间：{{item.add_time.substring(0,item.add_time.indexOf('T'))}}</text> <text>浏览：{{item.click}}</text>
			</view>
		</view>
		
	</scroll-view>
</template>

<script>
	export default{
		data(){
			return{
				newsList:[]
			}
		},
		onLoad(){
			this.getNews()
		},
		methods:{
			async getNews(){
				const res = await this.$http({
					url:'/api/getnewslist'
				})
				this.newsList=res.data.message
				console.log('res',res)
			},
			goDetailed(id){
				uni.navigateTo({
					url:"/pages/news/newsDetailed?id="+id
				})
			}
		}
	}
</script>

<style lang="scss">
	page{
		height: 100%;
	}
	.news{
		height:100%;
		.newsItem{
			height:200rpx;
			border-bottom: 2rpx solid $shop-primary;
			.picLeft{
				width: 200rpx;
				height:150rpx;
				padding:26rpx 15rpx;
				display: inline-block;
				float: left;
				image{
					width: 100%;
					height:100%
				}
			}
			.right{
				width:510rpx;
				display: inline-block;
				font-size: 32rpx;
				padding: 12rpx 10rpx 12rpx 0;
				text{
					display: inline-block;
					font-size: 24rpx;
					line-height: 30rpx;
				}
			}
		}
	}
</style>
