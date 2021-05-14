<template>
	<view class="goodsWrap">
		<good-list :goodsList="goodsList"></good-list>
		<text class="tip" v-if="flag">----我到底了----</text>
	</view>
</template>

<script>
	import goodList from '../../components/goodList.vue'
	export default {
		components: {
			goodList
		},
		data() {
			return {
				goodsList: [],
				pageNum: 1,
				flag:false
			}
		},
		onLoad() {
			this.getGoods(this.pageNum)

		},
		onReachBottom() {
			this.getGoods(this.pageNum += 1)
		},
		onPullDownRefresh(){
			this.goodsList=[]
			this.flag=false
			setTimeout(()=>{
				this.getGoods(1,()=>{
					uni.stopPullDownRefresh()
				});
			},1500)
			
		},
		methods: {

			async getGoods(pageNum,callback) {
				if (pageNum <= 2) {
					const res = await this.$http({
						url: '/api/getgoods?',
						data: {
							pageindex: pageNum
						}
					})
					this.goodsList.push(...res.data.message)
					callback && callback()
				}else{
					this.flag=true
				}

			}

		}
	}
</script>

<style lang="scss">
	.goodsWrap{
		background-color: #eee;
		.tip{
			color: #C8C7CC;
			font-size: 20rpx;
			width: 100%;
			display: inline-block;
			text-align: center;
		}
	}
</style>
