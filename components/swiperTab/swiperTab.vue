<template>
	<view>
		<swiper class="swiper-box" :style="{ height: swiperHeight + 'px' }" :current="tabIndex" @change="tabChange">
			<swiper-item v-for="(items, index) in newsList" :key="index">
				<scroll-view scroll-y class="list " @scrolltolower="loadMore(index)">
					<template >
						<!-- 图文列表 -->
						<block v-for="(item, idx) in items.list" :key="idx">
							<card-index :item="item" style="margin:15upx 0 " @toggleState="toggleState"></card-index>
						</block>
						<!-- 上拉加载更多 -->
						<load-more :loadText="items.loadText"></load-more>
					</template>
					<template >
						<image src="../../static/img/nothing.png" mode=""></image>
					</template>
				</scroll-view>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
import cardIndex from '@/components/card-index/card-index.vue';

import loadMore from '@/components/common/load-more.vue'

export default {
	name: 'swiperTab',
	components:{
		cardIndex,
		loadMore
	},
	props:{
		newsList:Array,
		tabIndex:Number
	},
	onLoad(){
		console.log('newslist',newsList);
		uni.getSystemInfo({
			success:(res)=>{
				let wHeight = res.windowHeight - uni.upx2px(100)
				this.swiperHeight = wHeight
			}
		})
	},
	data() {
		return {
			swiperHeight:800,//动态swiper高度
		};
	},
	methods:{
		tabChange(e){
			// console.log('e',e);
			this.$emit('tabChange',e)
		},
		// 上拉加载更多
		loadMore(index){
			if(this.newsList[index].loadText !== '上拉加载更多'){return };
			this.newsList[index].loadText = '上拉加载更多';
			
			this.newsList[index].loadText = '加载中...';
			this.newsList[index].loadText = '没有更多数据！';
		},
	}
};
</script>

<style lang="scss" scoped>
	.swiper-tab-list {
		color: #969696;
		font-weight: bold;
	}
	.uni-tab-bar .active {
		color: #343434;
		.swiper-tab-line {
			color: #feef4d;
			border-top: 6upx solid #feef4d;
			border-bottom: 6upx solide #feef4d;
			width: 70upx;
			height: 4upx;
			margin: auto;
			margin-top: -20upx;
			border-radius: 30upx;
		}
	}
	
</style>
