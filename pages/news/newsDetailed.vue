<template>
	<view class="detailed">
		<view class="detailedItem" v-for="(item,index) in detailedList" :key="index">
			<h4 class="title">{{item.title}}</h4>
			<view class="info">
				<text class="time">发表时间：{{item.add_time.substring(0,item.add_time.indexOf('T'))}}</text><text class="click">浏览：{{item.click}}</text>
			</view>
			<view class="content" v-html="item.content"></view>
			
		</view>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				detailedList: []
			}
		},
		onLoad(option) {
		
			this.getDetailed(option.id)
		},
		methods: {
			async getDetailed(id) {
				const res = await this.$http({
					url: '/api/getnew/' + id
				})
				this.detailedList=res.data.message;
				console.log('this.detailedList',this.detailedList)
			}
		}
	}
</script>

<style lang="scss">
	.detailedItem{
		padding: 20rpx 30rpx;
		.info{
			display: flex;
			justify-content: space-between;
			font-size: 30rpx;
		}
		.content{
			text-indent: 64rpx;
		
		}
		
	}
	
</style>
