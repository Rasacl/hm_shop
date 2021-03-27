<template>
	<view class="goos_list">
		<view class="goods_item" v-for="item in goods" :key="item.goods_id">
			<image :src="item.goods_small_logo"></image>
			<view class="price">
				<text>¥{{item.goods_price}}</text>
				<text>¥2499</text>
			</view>
			<view class="name">
				{{item.goods_name}}
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props:['goods'],
		name:"goods-list",
		data() {
			return {
				
			};
		}
	}
</script>

<style lang="scss">
	.goos_list{
		padding: 0 6px;
		display: flex;
		flex-wrap:wrap;
		justify-content: space-between;
		.goods_item{
			margin: 10rpx 0;
			background: #fff;
			width: 355rpx;
			padding: 15rpx;
			box-sizing: border-box;
			image{
				display: block;
				width: 80%;
				height: 150px;
				margin: 0 auto;
			}
			.price{
				color: #b50e03;
				font-size: 36rpx;
				margin: 15rpx 0 10rpx 0;
				text:nth-child(2){
					color: #ccc;
					font-size: 28rpx;
					margin-left: 17rpx;
					text-decoration: line-through;
				}
			}
			.name{
				font-size: 28rpx;
				line-height: 30rpx;
				padding-bottom: 15rpx;
				padding-top: 10rpx;
			}
		}
	}
</style>
