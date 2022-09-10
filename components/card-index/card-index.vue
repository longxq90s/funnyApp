<template>
	<view >
		<view class="list-item flex-bt" >
			<view class="user-logo flex-v-center" >
				<image :src="item.userpic" mode=""></image>
				<view class="user-name">{{ item.username }}</view>
			</view>
			<view class="btn" @tap="toggleState">
				<view class="flex-center">
					<view v-if="item.isguanzhu" class="flex">
						<view  class="iconfont icon-select-bold"></view>
						<view>已关注</view> 
					</view>
					<view v-else class="flex">
						<view class="iconfont icon-add" />
						<view>关注</view> 
					</view>
				</view>
			</view>
		</view>
		<view class="list-item" @tap='openDetail'>
			{{item.title}}
		</view>
		<view class="list-item img-style ps-rel" @tap='openDetail'>
			<!-- 图片 -->
			<image lazy-load :src="item.titlePic" mode="widthFix" />
			<!-- 视频 -->
			<view class="index-play ps-abs ps-center" v-if="item.type === 'video'"><view class="iconfont icon-play"></view></view>
			<view class="index-play-info ps-abs ps-r-bottom" v-if="item.type === 'video'">20w次播放</view>
		</view>
		<view class="flex-bt btm-icon">
			<!-- 顶与踩 -->
			<view class="icon flex-bt" >
				<view class="flex icon-box" :class="item.infoNum.index === 1 ? 'active' : ''" @tap="upOrDown('ding')">
					<view class="iconfont icon-meh-filling"></view>
					<view>{{ item.infoNum.ding }}</view>
				</view>
				<view class="flex icon-box" :class="item.infoNum.index === 2 ? 'active' : ''" @tap="upOrDown('cai')" >
					<view class="iconfont icon-cry-filling"></view>
					<text>{{ item.infoNum.cai }}</text>
				</view>
			</view>
			<!-- 评论与分享 -->
			<view class="icon flex-bt">
				<view class="flex icon-box">
					<view class="iconfont icon-pinglun"></view>
					<text>{{ item.commentNum }}</text>
				</view>
				<view class="flex icon-box">
					<view class="iconfont icon-arrow-"></view>
					<text>{{ item.shareNum }}</text>
				</view>
			</view>
		</view>		
	</view>
</template>

<script>
export default {
	name: 'card-index',
	props:{
		item:Object,
		index:Number
	},
	onLoad(){
	},
	data() {
		return {};
	},
	methods:{
		toggleState(){
			this.item.isguanzhu = !this.item.isguanzhu
		},
		upOrDown(type){
			// console.log('this.item',this.item);
			// console.log(type);
			// 0:没有操作；1：顶；2：踩
			 switch(type){
				 case "ding":
					if(this.item.infoNum.index === 1){return;}
					this.item.infoNum.ding++
					if(this.item.infoNum.index === 2){
						this.item.infoNum.cai--
					}
					this.item.infoNum.index = 1
				 break;
				 case "cai":
					if(this.item.infoNum.index === 2){return;}
					this.item.infoNum.cai++
					if(this.item.infoNum.index === 1){
						this.item.infoNum.ding--
					}
					this.item.infoNum.index = 2
				 break;
			 }
		},
		openDetail(){
			console.log('进入详情页');
		}
	}
};
</script>

<style lang="scss" scoped>
	.list-item {
		padding: 10upx 15upx;
	}
	.user-logo {
		.user-name {
			margin-left: 10upx;
		}
		image {
			width: 80upx;
			height: 80upx;
			border-radius: 100%;
		}
	}
	.btn {
		background-color: #eee;
		// width: 100upx;
		padding:0 10upx;
		height: 60upx;
		line-height: 60upx;
		border-radius: 4upx;
	}
	.index-play > view{
		font-size: 150upx;
		color:#fff;
	}
	.index-play-info{
		background-color: rgba(51,51,51,.7);
		border-radius: 20upx;
		color:#fff;
		font-size: 25upx;
		padding: 0 12upx;
	}
	.index-list{
		border-bottom:1px solid #ccc;
	}
	.index-list > .btm-icon{
		padding:20upx 10upx;
		.icon{
			width: 160upx;
			color:#adadad;
		}
		.icon > .icon-box{
			height:100%;
			line-height: 100%;
		}	
		.active{
			color:aqua;
		}
	}
	.img-style{
		border-radius: 10upx;
		height:400upx;
	}
	.img-style > image{
		border-radius: 14upx;
		width:100%;
	}
	.active {
		color: orange;
	}
</style>
