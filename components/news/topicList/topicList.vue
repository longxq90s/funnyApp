<template>
	<view class="topic-list flex animated fadeInLeft fast" @tap="getDetail">
		<image :src="item.titlepic" mode="widthFix" lazy-load></image>
		<view class="flex-sa" style="flex-direction: column;">
			<view>#{{item.title}}#</view>
			<view>{{item.desc}}</view>
			<view>动态 {{item.totalnum}} 今日 {{item.todaynum}}</view>
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			item:Object,
			index:Number
		},
		data(){},
		methods:{
			getDetail(){
				uni.navigateTo({
					url:"/pages/themeDetail/themeDetail"
				})
			}
		}
	}
</script>

<style scoped>
.topic-list{
	padding: 20upx 0;
	border-bottom: 1upx solid #EEEEEE;
}
.topic-list image{
	width: 150upx;
	height: 150upx;
	border-radius:10upx;
	margin-right: 20upx;
}
.topic-list>view>view{
	color: #A4A4A4;
}
.topic-list>view>view:first-child{
	color: #333333;
	font-size: 32upx;
}
</style>
