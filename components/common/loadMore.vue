<template>
	<!-- 上拉加载 -->
	<view class="load-more ">{{loadText}}</view>
</template>

<script>
	export default{
		props:{
			loadText:String
		}
	}
</script>

<style lang="scss" scoped>
	.load-more{
		text-align: center;
		color:#aaaaaa;
		padding:10upx;		
	}
</style>