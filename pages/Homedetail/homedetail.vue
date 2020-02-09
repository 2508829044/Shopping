<template>
	<view>
		<view class="uni-padding-wrap">   <!-- swiper区域 -->
		           <view class="page-section swiper">
		               <view class="page-section-spacing">
		                   <swiper class="swiper" :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration" >      
							<swiper-item v-for="item in obje.coverurl" :key='item.index'>
							<view> <image :src="item"></image></view>
							</swiper-item>								  
		                   </swiper>
		               </view>
		           </view>
		</view>
		<view class="shoppingtitle"> <!-- 商品title区域 -->
			<text>{{obje.title}}</text>
			<view>￥{{obje.price}}</view>
		</view>
		
		<view class="bottom-button">  <!-- 底部button -->
			<view style="width:50%;height:60px;background-color: rgb(239,194,15);text-align: center;line-height: 60px;color: rgb(255,255,255);font-size:16px;" @click="join()">加入购物车</view>
			<view style="width:50%;height:60px;background-color:red;text-align: center;line-height: 60px;color: rgb(255,255,255);font-size:16px;">立即购买</view>
		</view>
		
		<view class="switch">  <!-- 多选切换框区域 -->
			<view v-for="(item,index) in title" :key='item.index' :class="{active:index==ins}" @click="active(item,index)">
				<text>{{item.name}}</text>
			</view>
		</view>
		
		<view v-for="item in obje.content" :key="item.index" class="introduce">   <!-- 商品介绍区域 -->
			<image :src="item"></image>
		</view>
		
		<view class="commodity" v-show="num">  <!-- 商品选择框 -->
			<view style="position: relative;right:-355px;top:7px;z-index:999;">x</view>
			<view class="commoditytwo">
				<image :src="obje.cover" style="width:100px;height:100px;"></image>
				<view class="commodityone">
					<text>{{obje.title}}</text>
					<view>￥{{obje.price}}</view>
					<view style="padding-top:15px;font-size:14px;color: black;padding-left:3px;">已选: 3瓶顺丰包邮 360...</view>
				</view>
			</view>
			<view class="number">
				<text>数量:</text>
				<view>
					<uni-number-box @change="bindChange"></uni-number-box>
				</view>
			</view>
			<view class="style">
				<text style="font-size:14px;">规格:</text>
				<view>默认</view>
			</view>
		</view>
		
		<view :class="{rgb : num}"></view>  <!-- rgba颜色层 -->
			
		
	</view>
</template>

<script>
import uniNumberBox from '@/components/uni-number-box/uni-number-box.vue'
	export default {
		data:function(){
			return {
				background: ['color1', 'color2', 'color3'],
				indicatorDots: true,
				autoplay: true,
				interval: 2000,
				duration: 500,
				obje:'',
				title:[
					{name:'商品介绍'},
					{name:'规格参数'},
					{name:'包装清单'},
					{name:'售后服务'},
				],
				ins:0,
				num:false,
				age:''
			}
		},
		components:{
		  	uniNumberBox
		},
		mounted(){
			this.homeshopping()
			
		},
		methods:{
			homeshopping:function(){
				var arr = new Array()
				arr = JSON.parse(localStorage.getItem('home'))
				 if(arr.index == this.$store.state.homedata[arr.id].id){
					this.obje = JSON.parse(localStorage.getItem('home'))
					console.log(this.obje)
				  }else{
					  console.log('商品id不一致')
				  }
			},
			active:function(item,index){
				this.ins = index
			},
			join:function(){
				uni.showToast({
				    title: '亲我在购物车等着您哦!',
				    duration: 2000
				});
				this.obje['age'] = this.age //把用户点击的商品数量存储到此商品信息中
				localStorage.setItem('shopping',JSON.stringify(this.obje))  //购物车数据备用
			},
			bindChange:function(e){ //获取到用户点击的商品数量
				this.age = e
				console.log(e)
			}
		}
	}
</script>

<style scoped lang="less">
	*{margin:0px;padding:0px;}
	.rgb{
		width:100%;
		height:100%;
		position: fixed;
		bottom:0px;
		left:0px;
		background-color: rgba(0,0,0,0.5);
		overflow: hidden;
	}
	page{background-color: rgb(248,248,248);}
	.page-section swiper{display: block;height:300px;}
	.swiper{
		image{
			width:100%;
			height:300px;
		}
	}
	.shoppingtitle{
		width:100%;
		background-color: rgb(255,255,255);
		text{
			padding-top:15px;
			padding-bottom:15px;
			font-size:17px;
			display: -webkit-box;
			-webkit-box-orient: vertical;
			padding-left:5px;
			-webkit-line-clamp:2;
			overflow: hidden;
		}
		view{
			color: red;
			font-size:16px;
			font-weight: 600;
			padding-left:3px;
		}
	}
	.bottom-button{
		width:100%;
		position:fixed;
		bottom:0px;
		left:0px;
		display:flex;
		z-index:999;
	}
	.switch{
		width:100%;
		height:60px;
		display:flex;
		justify-content: space-around;
		line-height:40px;
		font-size:15.7px;
		background-color: rgb(255,255,255);
		text{
			width:20px;
			height:50px;
			padding-bottom:20px;
			padding-left:15.5px;
			padding-right:15.5px;
		}
	}
	.active {
		text{
		   color: red;
		   border-bottom:1px solid red;
		}
	}
	.introduce{
		image{
			width:100%;
			height:320px;
		}
	}
	.commodity{
		width:100%;
		height:400px;
		background-color: rgb(255,255,255);
		position: fixed;
		bottom:0px;
		left:0px;
		z-index:99;
		.commoditytwo{
			display: flex;
			justify-content: space-around;
		}
		image{
			width:150px;
			height:130px;
			padding-top:16px;
		}
		text{
			font-size:14px;
			padding-top:16px;
			display: -webkit-box;
			display: -webkit-box;
			-webkit-box-orient: vertical;
			padding-left:5px;
			-webkit-line-clamp:2;
			overflow: hidden;
		}
		.commodityone{
			width:60%;
			view{
				color: red;
				font-size:14px;
				padding-left:3px;
				padding-top:15px;
			}
		}
	}
	.number{
		display:flex;
		justify-content: space-between;
		/* height:100px; */
		width:98%;
		margin:20px auto;
	}
	.style{
		width:98%;
		text{
			display: block;
			padding-bottom:10px;
		}
		view{
			background-color: red;
			width:44px;
			height:25px;
			font-size:14px;
			line-height:25px;
			color: rgb(255,255,255);
			text-align: center;
		}		
	}
</style>
