<template>
	<view class="pics">
		<scroll-view scroll-y="true" class="sideMenu">
			<view @click="getIndex(index,item.id)" :class="active===index?'active':''" v-for="(item,index) in sideMenuList" :key="item.id">{{item.title}}</view>
		</scroll-view>
		<scroll-view scroll-y="true" class="rightData">
			<view v-if="rightDataList.length===0">暂无数据</view>
			<view v-else v-for="(item,index) in rightDataList" :key=index>
				<image @click="previewImg(item.img_url)" :src="item.img_url" ></image>
				<view>
					<h5>{{item.title}}</h5>
					<text>{{item.zhaiyao}}</text>
				</view>
			</view>
			
		</scroll-view>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				sideMenuList: [],
				rightDataList: [],
				active: 0
			}
		},
		onLoad() {
			this.getSideMenu()
			
		},
		methods: {
			async getSideMenu() {
				const res = await this.$http({
					url: "/api/getimgcategory"
				})
				this.sideMenuList = res.data.message
				this.getIndex(0,this.sideMenuList[0].id)

			},
			async getIndex(index,id){
				this.active=index;
				const res = await this.$http({
					url:'/api/getimages/'+id
				})
				this.rightDataList =res.data.message
				console.log('res',res)
			},
			previewImg(current){
				const imgList = this.rightDataList.map(item=>{
					return item.img_url
				})
				uni.previewImage({
					current:current,
					urls:imgList
				})
			}
		}
	}
</script>

<style lang="scss">
	page {
		height: 100%
	}

	.pics {
		height: 100%;
		width: 100%;

		.sideMenu {
			float: left;
			width: 200rpx;
			height: 100%;
			border-right: 2rpx solid #eeeeee;

			.active {
				color: white;
				background-color: $shop-primary;
			}

			view {
				width: 100%;
				line-height: 120rpx;
				height: 120rpx;
				text-align: center;
				border-bottom: 2rpx solid #eeeeee;

			}
		}
		.rightData{
			display: inline-block;
			height: 100%;
			float: right;
			width: 518rpx;
			padding: 0 15rpx;
			text{
				font-size: 24rpx;
			}
		}
	}
</style>
