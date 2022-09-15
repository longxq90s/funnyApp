<template>
	<view class="body flex">
			<view class="left flex-h-center"><image :src="item.userLogo" mode="widthFix" /></view>
			<view class="right">
				<view class="flex-bt">
					<view class="tags">{{ item.age }} {{ item.sex === 0 ? '♀' : '♂' }}</view>
					<view class="add-focus flex-center">
						<view class="iconfont icon-add"></view>
						关注
					</view>
				</view>
				<view class="title">{{ item.title }}</view>
				<view class="flex-center"><image v-if="item.media.type === 'img'" :src="item.media.url" mode="widthFix"></image></view>
				<view class="flex-last bottom">
					<view class="share flex">
						<view class="iconfont icon-arrow-"></view>
						{{ item.info.share }}
					</view>
					<view class="commont flex">
						<view class="iconfont icon-pinglun"></view>
						{{ item.info.commit }}
					</view>
					<view class="collect flex">
						<view class="iconfont icon-xihuanfill"></view>
						{{ item.info.collects }}
					</view>
				</view>
			</view>
		
	</view>
</template>

<script>
export default {
	name: 'list',
	props:{
		item:Object,
		index:Number
	},
	data() {
		return {};
	}
};
</script>

<style lang="scss" scoped>
	.body {
		padding: 20upx;
		.left {
			width: 100upx;
		}
		.left image {
			width: 80upx;
		}
		.right {
			margin-left: 10upx;
			width: 100%;
			border-bottom:1px solid #ccc;
			.tags{
				background-color: #fede33;
				padding:0 10upx;
				border-radius: 20upx;
			}
			.add-focus{
				border:1px solid #ccc;
				border-radius: 10upx;
				padding:0 10upx;
				background-color: #ccc;
			}
			.title{
				margin:10upx 0;
			}
			.bottom{
				margin:10upx 0;
			}
		}
	}
</style>
