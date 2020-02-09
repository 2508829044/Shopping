<template>
	<view>
		<text>
			<!-- <view style="position: absolute;top:0px;left:0px;width:100px;height:30px;border:1px solid red;z-index:9999;text-align: center;">您好</view> -->
			 <view class="uni-padding-wrap">   <!-- swiper区域 -->
			            <view class="page-section swiper">
			                <view class="page-section-spacing">
			                    <swiper class="swiper" :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration" >      
									   <swiper-item v-for="item in swiper" :key='item.index'>
									      <view> <image :src="item.img"></image></view>
									   </swiper-item>								  
			                    </swiper>
			                </view>
			            </view>
			 </view>
			 <view style="display: flex;justify-content: center;color:rgb(199,26,82);"><text class="text">为你推荐</text></view>
			 <view class="shopping">
				 <view v-for="(time,index) in arr" :key='time.index' class="shoppingdetail" @click="logan(time,index)">
					 <view class="shoppinglist">
						 <image :src="time.cover"></image>
						<text>{{time.title}}</text>
						<view style="padding-top:30px;color: red;font-weight: 500;padding-left:5px;">￥{{time.price}}</view>
					 </view>
				 </view>
			 </view>		
		</text>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				  background: ['color1', 'color2', 'color3'],
				  indicatorDots: true,
				  autoplay: true,
				  interval: 2000,
				  duration: 500,
				  arr:''		
			}
		},
		mounted(){
		/* uni.chooseLocation({
		    success: function (res) {
		        console.log('位置名称：' + res.name);
		        console.log('详细地址：' + res.address);
		        console.log('纬度：' + res.latitude);
		        console.log('经度：' + res.longitude);
		    }
		});	 */
		},
		computed:{
			swiper:function(){
				return this.$store.state.swiper //从vuex把模拟数据给拿出来
			}
		},
		onLoad() {
			this.arr = this.$store.state.homedata
			console.log(this.arr)
		},
		methods: {
			logan:function(item,index){  //点击那个就把那个商品信息存储到本地
				var indexone = index
				if(indexone == index){
					this.arr[index]['index']=index  //把他的索引存储到data里面
					localStorage.setItem('home',JSON.stringify(this.arr[index]))
					uni.navigateTo({
						url:'../Homedetail/homedetail'  //成功存储商品信息以后跳转详情页
					})
				}else{
					console.log("这都能出错")
				}
			}
		}
	}
</script>

<style scoped lang="less">
	page{background-color: rgb(249,249,249);}
	.text{font-family:"Arial","Microsoft YaHei",sans-serif;padding-top:10px;font-weight: 600;}
	.uni-swiper{display: block;height:175px;}
	.swiper{
		image{
			width:100%;
			height:170px;
		}
	}
	.shopping{
		width:100%;
		display: flex;
		justify-content:space-between;
		flex-wrap: wrap;
		.shoppingdetail{
			.shoppinglist{
				width:180px;
				height:250px;
				margin-top:10px;
				background-color: rgb(255,255,255);
				border:1px solid rgb(255,255,255);
				border-radius:8px;
				image{
					width:100%;
					height:150px;
				}
				text{
					font-size:15.8px;
					display: -webkit-box;
					-webkit-box-orient: vertical;
					padding-left:5px;
					-webkit-line-clamp:2;
					overflow: hidden;
					font-family:"Arial","Microsoft YaHei","SimHei","SimSun",sans-serif;
				}
			}
			
		}
	}
</style>
