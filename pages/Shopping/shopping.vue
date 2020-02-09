<template>
	<view>
		<view class="Allelection">
		<checkbox value="删除选中商品" >删除选中商品</checkbox>
		</view>
		<view v-for="time in arr" :key='time.index' class="shoppinginformation">
			<checkbox ></checkbox>
			<image :src="time.cover" style="border: none;"></image>
			<view class="active">
				<text>{{time.title}}</text>
				<view class="activeone">
					<view>￥{{time.price}}</view>
					<uni-number-box @change="bindChange" style="height:30px;" :value="time.age"></uni-number-box>
				</view>
			</view>
		</view>
		<view class="bottomnav">
		<checkbox  @click="logan">全选</checkbox>	
		</view>
	</view>
</template>

<script>
import uniNumberBox from '@/components/uni-number-box/uni-number-box.vue'	
	export default {
		data:function(){
			return {
				bloore:true,
				arr:[]
			}
		},
		components:{
			uniNumberBox
		},
		mounted(){
		this.arr.push(JSON.parse(localStorage.getItem('shopping')))
		},
		methods:{
			bindChange:function(e){
				console.log(e)
			},
			logan:function(){
				this.arr[0].deletect = this.bloore
				console.log(this.arr[0].deletect)
			}
		}
	}
</script>

<style scoped lang="less">
	checkbox{
		padding-left:10px;
	}
	.Allelection{
		width:100%;
		height:60px;
		background-color:red;
		checkbox{
			line-height:60px;
			font-size:16px;
			color: rgb(255,255,255);
		}
	}
	.shoppinginformation{
		width:100%;
		height:100px;
		display: flex;
		border-bottom:1px solid rgb(240,240,240);
		image{
			width:100px;
			height:100px;
		}
		checkbox{
			line-height:100px;
		}
		text{
			width:60%;
			font-size:14px;
		}
	}
	.active{
		width:60%;
		text{
			display: -webkit-box;
			-webkit-box-orient: vertical;
			padding-left:5px;
			-webkit-line-clamp:2;
			overflow: hidden;
			padding-top:10px;
		}
		view{
			color: red;
			font-size:14px;
			padding-top:5px;
		}
		.activeone{
			display: flex;
			justify-content: space-between;
			
		}
	}
	.bottomnav{
		width:100%;
		background-color:red;
		height:60px;
		position: fixed;
		bottom:51px;
		left:0px;
		checkbox{
			line-height:60px;
			font-size:16px;
			color: rgb(255,255,255);
		}
	}
</style>
