<template>
	<view class="home">
		<swiper indicator-dots circular autoplay='true'>
			<swiper-item v-for="item in swipers" :key="item.goods_id">
				<image :src="item.image_src"></image>
			</swiper-item>
		</swiper>
		<!-- 导航区域 -->
		<view class="nav">
			<view class="nav_item" v-for="(item,index) in navs" :key="index" @click="navItemClick(item.path)">
				<view :class="item.icon"></view>
				<text>{{item.title}}</text>
			</view>
		</view>
	  <!-- 推荐商品区 -->
	  <view class="hot_goods">
	  	<view class="tit">
	  		推荐商品
	  	</view>
		<goods-list :goods="goods"></goods-list>
	  </view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				swipers: [],
				goods:[],
				navs:[
					{
						icon:'iconfont icon-ziyuan',
						title:'黑马超市',
						path:'/pages/goods/goods'
					},
					{
						icon:'iconfont icon-guanyuwomen',
						title:'联系我们',
						path:'/pages/contact/contact'
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
				]
			}
		},
		onLoad() {
			this.getSwipers()
			this.getHotGoods()
		},
		methods: {
			//获取轮播图的数据
			async getSwipers() {
				// console.log("获取轮博")
				// uni.request({
				// 	url:'https://api-hmugo-web.itheima.net/api/public/v1/home/swiperdata',
				// 	success:res=>{
				// 		console.log(res)
				// 		if(res.data.meta.status  !== 200){
				// 			return uni.showTabBar({
				// 				title:'获取数据失败'
				// 			})
				// 		}
				// 		this.swipers = res.data.message
				// 	}
				// })
				const res = await this.$myRuquest({
					url: '/home/swiperdata'
				})
				this.swipers = res.data.message
			},
			//获取热门商品列表数据
			async getHotGoods(){
				const res = await this.$myRuquest({
					url:'/goods/search'
				})
				console.log(res)
				this.goods = res.data.message.goods
			},
			//导航点击的处理函数
			navItemClick(url){
				uni.navigateTo({
					url
				})
			}
		}
	}
</script>

<style lang="scss">
	.home{
		swiper{
			width: 750rpx;
			height: 380rpx;
			image{
				width: 100%;
				height: 100%;
			}
		}
		.nav{
			display: flex;
			.nav_item{
				width: 25%;
				text-align: center;
				view{
					width: 120rpx;
					height: 120rpx;
					background-color: #b50e03;
					border-radius: 60rpx;
					margin: 10px auto;
					line-height: 120rpx;
					color: #fff;
					font-size: 50rpx;
				}
				.icon-tupian{
					font-size: 45rpx;
				}
				text{
					font-size: 30rpx;
				}
			}
		}
		.hot_goods{
			background: #eee;
			overflow: hidden;
			margin-top: 10px;
			.tit{
				height: 50px;
				line-height: 50px;
				color: #b50e03;
				background-color: #fff;
				text-align: center;
				letter-spacing: 20px;
				margin: 7px 0;
			}
		
		}
	}
</style>
