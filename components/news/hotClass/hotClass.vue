<template>
	<view class="topic-nav">
		<view class="flex-bt ">
			<view>热门分类</view>
			<view class="flex-center" @tap="getMoreClass">
				更多
				<view class="iconfont icon-arrow-right"></view>
			</view>
		</view>
		<view class="flex-center">
			<block v-for="(item) in themes" :key="item.id">
				<view class="flex-center">{{item.name}}</view>
			</block>
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			themes:Array,
		},
		data(){
			return {}
		},
		methods:{
			getMoreClass(){
				// console.log('更多分类');
				uni.navigateTo({
					url:"/pages/moreClass/moreClass"
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.topic-nav{
		border-bottom: 1upx solid #EEEEEE;
		border-top: 1upx solid #EEEEEE;
		padding: 20upx;
	}
	.topic-nav>view:first-child{
		margin-bottom: 10upx;
	}
	.topic-nav>view:first-child view{
		color: #9E9E9E;
	}
	.topic-nav>view:first-child>view:first-child{
		color: #333333;
		font-size: 32upx;
	}
	.topic-nav>view:last-child>view{
		flex: 1;
		background: #dddddd;
		color: #9E9E9E;
		border-radius: 10upx;
		margin: 0 10upx;
	}
</style>