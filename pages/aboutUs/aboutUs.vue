<template>
	<view class="contact">
		<image src="http://www.itcast.cn/2018czydz/images/gywmban.jpg"></image>
		<text @click="callPhone">联系我们 ：400-618-9990 (点击拨打)</text>
		<view class="line"></view>
		<text>公司地址 ：北京市海淀区东北旺尚东数字谷B区3号楼</text>
		<view class="line"></view>
		<map  :longitude="longitude" :latitude="latitude" :markers="marker"></map>

	</view>
</template>

<script>
	export default{
		data(){
			return {
				longitude:116.295796,
				latitude:40.04953,
				marker:[{
					"longitude":116.295796,
					"latitude":40.04953,
					"iconPath":'../../static/img/hmlogo.png',
					"width":20,
					"height":20,
				}]
			}
		},
		methods:{
			callPhone(){
				uni.makePhoneCall({
					phoneNumber:'400-618-9990'
				})
			}
		}
	}
</script>

<style lang="scss">
	.contact {
		image {
			width: 100%;
			height: 320rpx
		}
		text{
			display: inline-block;
			font-size: 30rpx;
			line-height:80rpx;
			padding: 0 20rpx;
		}
		.line {
			height: 2rpx;
			width: 100%;
			margin: 0 16rpx;
			background-color: #eeeeee;
		}
		map{
			width: 100%;
			height:750rpx
		}
	}
</style>
