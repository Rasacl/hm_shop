<template>
	<view class="goods-list">
		<goods-list :goods="goods"></goods-list>
		<view class="isOver" v-if="flag">
			-----我是有底线的-----
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				goods:[],
				pagenum:"1",
				flag:false,
				total:4
			}
		},
		onLoad() {
		this.getHotGoods()	
		},
		onReachBottom() {
			// console.log(this.goods.length)
			// console.log(this.total)
			// console.log(this.pagenum)
			if(this.goods.length === this.total){
				this.flag = true
				return
			}
		    // console.log('触底了')
			this.pagenum++
			this.getHotGoods()
		},
		onPullDownRefresh() {
		// console.log('下拉刷新拉')	
		this.pagenum = '1'
		this.goods = []
		this.flag = false
		setTimeout(()=>{
			this.getHotGoods(()=>{
				uni.stopPullDownRefresh()
			})
		},1000)
		},
		methods: {
			async getHotGoods(callback){
				const res = await this.$myRuquest({
					url:'/goods/search',
					data:{
						pagenum:this.pagenum
					}
				})
				// console.log(res)
				this.goods = [...this.goods,...res.data.message.goods]
				this.total = res.data.message.total
				callback && callback()
			},
		}
	}
</script>

<style lang="scss">
	.goods-list{
		background-color: #eee;
		.isOver{
			width: 100%;
			height: 50px;
			line-height: 50px;
			text-align: center;
			// background: #fff;
			font-size: 28rpx;
		}
	}
</style>
