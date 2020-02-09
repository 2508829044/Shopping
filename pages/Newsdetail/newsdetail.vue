<template>
	<view class="newsdetail">
		<text>{{arr.author_name}}</text>
		<text>{{arr.updated_at}}</text>
		<text>{{arr.summary}}</text>
		<text v-html="arr.content">{{arr.content}}</text>
	</view>
</template>

<script>
	export default {
		data:function(){
			return {
				arr:''
			}
		},
		mounted() {
			this.arr = JSON.parse(localStorage.getItem('newsand'))
			console.log(this.arr)
		}
	}
</script>

<style scoped lang="less">
	.newsdetail{
		width:100%;
		overflow: hidden;
		text{
			text-align: center;
			margin:0px auto;
			display: block;
			font-weight: 600;
			font-family: 'Courier New', Courier, monospace;
			padding-top:10px;
		}
		image{
			width:100%;
		}
	}
	.newsdetail image:nth-last-child(2){width:100%;}
</style>
