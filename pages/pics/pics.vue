<template>
	<view class="pics">
		<scroll-view scroll-y="true" class="left">
			<view :class="active===index?'active':''" 
			v-for="(item,index) in cate" 
			:key="item.cat_id"
			@click="leftClickHandle(index)"
			>{{item.cat_name}}</view>
		</scroll-view>
		<scroll-view scroll-y="true" class="right">
			<view class="item" v-for="item in cateChild" :key="item.cat_id">
				<image :src="item.cat_icon"></image>
				<text>{{item.name}}</text>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				cate:[],
				cateChild:[],
				active:0
			}
		},
		onLoad() {
			this.getPicsCate()
		},
		methods: {
			leftClickHandle(index){
				this.active = index
			},
			async getPicsCate(){
				const res = await this.$myRuquest({
					url:'/categories'
				})
				console.log(res)
				this.cate = res.data.message
				this.cateChild = res.data.message[this.active].children
				this.leftClickHandle()
				console.log(this.cateChild)
			}
		}
	}
</script>

<style lang="scss">
	page{
		height: 100%;
	}
	.pics{
		height: 100%;
		display: flex;
		.left{
			width: 200rpx;
			height: 100%;
			border-right: 1px solid #eee;
			view{
				height: 60px;
				line-height: 60px;
				border-top: 1px solid #eee;
				color: #333;
				text-align: center;
				font-size: 30rpx;
			}
			.active{
				background: #b50e03;
				color: #fff;
			}
		}
		.right{
			height: 100%;
			width: 520rpx;
			margin: 0 auto;
			.item{
				image{
				width: 520rpx;
				height: 520rpx;
				border-radius: 5px;
				}
			    text{
					font-size: 30rpx;
					line-height: 60rpx;
				}
			}
		}
	}
</style>
