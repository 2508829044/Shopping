<template>
	<view>
		<view v-for="(item,index) in obje" :key='item.index' class="head" @click="click(item,index)">
			<view class="imgtwo">
				<image :src="item.cover" style="margin-top:20px;"></image>
				<text style="font-size:17px;padding-left:5px;padding-top:20px;">{{item.title}}</text>
			</view>
			<text style="font-family: Arial, Helvetica, sans-serif;">{{item.column_name}} &nbsp &nbsp{{item.created_at}}</text>
			<view class="imgtwo" style="margin-top:10px;">
				<image :src="item.author_avatar" style="margin-top:10px;"></image>
				<text style="font-size:17px;padding-left:5px;">{{item.summary}}</text>
			</view>
			<text style="font-family: Arial, Helvetica, sans-serif;">{{item.author_name}} &nbsp &nbsp{{item.updated_at}}</text>
		</view>		
	</view>
</template>
<script>
	export default {
		data:function(){
			return {
				obje:''
			}
		},
		mounted(){
			this.logan()
		},
		methods:{
			logan:function(){
				uni.request({
					method:'GET',
					url:'https://unidemo.dcloud.net.cn/api/news',
					success: (res) =>{
						if(res.statusCode == 200){
							this.obje=res.data
						 console.log(res.data)	
						}else{
							console.log(Error)
						}
					}
				})
			},
			click:function(item,index){
				var index = index
				localStorage.setItem('newsand',JSON.stringify(this.obje[index]))
				uni.navigateTo({
					url:'../Newsdetail/newsdetail',
				})
				console.log(index)
			}
		}
	}
</script>

<style scoped lang="less">
*{margin:0px;padding:0px;}
	.head{
		width:97%;
		margin:0px auto;
		text{
			font-size:16px;
			width:70%;
			padding-top:11px;
			flex-wrap: nowrap;
			font-weight: 400;
			font-family: Arial, Helvetica, sans-serif;
		}
		image{
			width:150px;
			height:100px;
			margin-top:10px;
			border:1px solid rgb(255,255,255);
			border-radius:8px;
		}
		.imgtwo{
			display:flex;
			justify-content: center;
		}
	}
</style>
