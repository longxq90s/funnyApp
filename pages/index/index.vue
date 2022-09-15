<template>
	<view class="content">
		<view class="uni-tab-bar"> 
			<scroll-view scroll-x class="uni-swiper-tab" show-scrollbar>
				<block v-for="(tab, index) in tabBars" :key="tab.id">
					<view class="swiper-tab-list" :class="{ active: tabIndex == index }" @tap="toggleTab(index)">
						{{ tab.name }}
						<view class="swiper-tab-line"></view>
					</view>
				</block>
			</scroll-view>
		</view>
		<swiper-tab :newsList="newsList" :tabIndex="tabIndex" @tabChange='tabChange'></swiper-tab>
	</view>
</template>

<script>

import swiperTab from "@/components/swiperTab/swiperTab.vue"

export default {
	components: {
		swiperTab
	},
	data() {
		return {
			tabIndex: 0,
			tabBars: [
				{ name: '关注', id: '0' },
				{ name: '推荐', id: '1' },
				{ name: '体育', id: '2' },
				{ name: '热点', id: '3' },
				{ name: '财经', id: '4' },
				{ name: '新闻', id: '5' }
			],
			newsList: [
				{
					loadText:"上拉加载更多",
					list: [
						{
							userpic: '../../static/img/userpic/12.jpg',
							username: '张老板',
							isguanzhu: false,
							title: '没有标题 ',
							type: 'img',
							titlePic: '../../static/img/datapic/11.jpg',
							infoNum: {
								index: 1, //1表示已操作，0表示未操作
								ding: 300,
								cai: 100
							},
							commentNum: 200,
							shareNum: 199
						},
						{
							userpic: '../../static/img/userpic/12.jpg',
							username: 'li老板',
							isguanzhu: false,
							title: '有标题 ',
							type: 'video',
							titlePic: '../../static/img/datapic/11.jpg',
							infoNum: {
								index:2, //1表示已操作，0表示未操作
								ding: 11,
								cai: 23
							},
							commentNum: 10,
							shareNum: 10
						}
					]
				},
				{
					loadText:"上拉加载更多",
					list:[
						{
							userpic: '../../static/img/userpic/12.jpg',
							username: '张老板',
							isguanzhu: false,
							title: '没有标题 ',
							type: 'img',
							titlePic: '../../static/img/datapic/11.jpg',
							infoNum: {
								index: 1, //1表示已操作，0表示未操作
								ding: 300,
								cai: 100
							},
							commentNum: 200,
							shareNum: 199
						},
					]
				},
				{},
				{},
				{}
			],

		};
	},
	onLoad() {
		
	},
	onNavigationBarButtonTap(e){
		console.log('e',e.index);
		if(e.index === 1){
			uni.navigateTo({
				url:"/pages/addInput/addInput"
			})
		}
	},
	onNavigationBarSearchInputClicked() {
		uni.navigateTo({
			url:"/pages/search/search"
		})
	},
	methods: {
		toggleTab(index) {
			this.tabIndex = index;
		},
		tabChange(e){
			// console.log('detail',e.detail);
			this.tabIndex = e.detail.current
		}
	}
};
</script>

<style lang="scss" scoped>
.uni-swiper-tab {
	border-bottom: 1upx solid #eee;
}

.active {
	color: aqua;
}


</style>
