<template>
	<view>
		<newsNavBar :tabBars="tabBars" :selectedIndex="selectedIndex" @toggleSelect="toggleSelect"></newsNavBar>
		<swiper class="swiper-box" :style="{ height: swiperHeight + 'px' }" :current="tabIndex" @change="tabChange">
			<!-- 关注 -->
			<swiper-item>
				<scroll-view scroll-y class="list " @scrolltolower="loadMore()">
					<block v-for="(item, index) in guanzhu.list" :key="index"><list :item="item" :index="index"></list></block>
					<load-more :loadText="guanzhu.loadtext"></load-more>
				</scroll-view>
			</swiper-item>
			<!-- 话题 -->
			<swiper-item>
				<scroll-view scroll-y class="list " @scrolltolower="loadMore(index)">
					<!-- 搜索内容 -->
					<view class="searchStye"><uni-search-bar placeholder="搜索内容" bgColor="#EEEEEE" @confirm="search" /></view>
					<!-- 轮播图 -->
					<swiper :indicator-dots="true" class="topic-swiper" :autoplay="true" :interval="3000" :duration="1000">
						<block v-for="(items, index) in topic.swiper" :key="index">
							<swiper-item><image :src="items.url" mode="widthFix"></image></swiper-item>
						</block>
					</swiper>
					<!-- 热门分类 -->
					<hot-class :themes="topic.theme"></hot-class>
					<!-- 最近更新 -->
					<view class="topic-new">
						<view>最近更新</view>
						<block v-for="(item, index) in topic.list" :key="index">
							<topic-list :item="item" :index="index"></topic-list>
						</block>
					</view>
				</scroll-view>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
import newsNavBar from '@/components/news/newsNavBar/newsNavBar.vue';
import list from '@/components/list/list.vue';
import loadMore from '@/components/common/loadMore.vue';

import hotClass from '@/components/news/hotClass/hotClass.vue';
import topicList from '@/components/news/topicList/topicList.vue';

export default {
	components: {
		newsNavBar,
		list,
		loadMore,
		hotClass,
		topicList
	},
	data() {
		return {
			selectedIndex: 1,
			tabIndex: 0,
			tabBars: [{ name: '关注', id: 'focus' }, { name: '话题', id: 'theme' }],
			guanzhu: {
				loadtext: '上拉加载更多',
				list: [
					// 文字
					{
						userLogo: '../../static/img/topicpic/14.jpeg',
						username: '张三',
						age: 23,
						sex: 0, // 0 ：女， 1:男
						isFocus: false,
						title: '这是个标题 呵呵哈哈哈',
						media: {
							type: 'img',
							url: '../../static/img/datapic/13.jpg'
						}, // img,video
						info: {
							share: 100,
							commit: 200,
							collects: 3000
						}
					},
					{
						userLogo: '../../static/img/topicpic/14.jpeg',
						username: '张三',
						age: 23,
						sex: 0, // 0 ：女， 1:男
						isFocus: false,
						title: '这是个标题 呵呵哈哈哈',
						media: {
							type: 'img',
							url: '../../static/img/datapic/13.jpg'
						}, // img,video
						info: {
							share: 100,
							commit: 200,
							collects: 3000
						}
					},
					{
						userLogo: '../../static/img/topicpic/14.jpeg',
						username: '张三',
						age: 23,
						sex: 0, // 0 ：女， 1:男
						isFocus: false,
						title: '这是个标题 呵呵哈哈哈',
						media: {
							type: 'img',
							url: '../../static/img/datapic/13.jpg'
						}, // img,video
						info: {
							share: 100,
							commit: 200,
							collects: 3000
						}
					}
				]
			},
			topic: {
				swiper: [
					{
						url: '../../static/img/datapic/13.jpg'
					},
					{
						url: '../../static/img/datapic/14.jpg'
					},
					{
						url: '../../static/img/datapic/15.jpg'
					}
				],
				theme: [{ name: '最新', id: 1 }, { name: '游戏', id: 2 }, { name: '打卡', id: 3 }, { name: '情感', id: 4 }, { name: '故事', id: 5 }, { name: '喜爱', id: 6 }],
				list: [
					{
						titlepic: '../../static/img/topicpic/13.jpeg',
						title: '话题名称',
						desc: '我是话题描述',
						totalnum: 50,
						todaynum: 10
					}
				]
			}
		};
	},
	onLoad() {
		uni.getSystemInfo({
			success: res => {
				let height = res.windowHeight - uni.upx2px(100);
				this.swiperHeight = height;
			}
		});
	},
	methods: {
		// 编辑按钮
		clickRight() {},
		toggleSelect(index) {
			this.tabIndex = index;
			this.selectedIndex = index;
		},
		tabChange(e) {
			// console.log('detail', e.detail);
			this.tabIndex = e.detail.current;
		},
		// 上拉加载更多
		loadmore() {
			if (this.guanzhu.loadtext != '上拉加载更多') {
				return;
			}
			// 修改状态
			this.guanzhu.loadtext = '加载中...';
			// 获取数据
			setTimeout(() => {
				//获取完成
				let obj = {
					userpic: '../../static/img/datapic/13.jpg',
					username: '哈哈',
					sex: 0, //0 男 1 女
					age: 25,
					isguanzhu: false,
					title: '我是标题',
					titlepic: '../../static/img/datapic/13.jpg',
					video: false,
					share: false,
					path: '深圳 龙岗',
					sharenum: 20,
					commentnum: 30,
					goodnum: 20
				};
				this.guanzhu.list.push(obj);
				this.guanzhu.loadtext = '上拉加载更多';
			}, 1000);
			// this.guanzhu.loadtext="没有更多数据了";
		}
	}
};
</script>
<style lang="scss" scoped>
.topic-swiper {
	padding: 0 20upx 20upx 20upx;
	swiper-item {
		border-radius: 10upx;
	}
}
.topic-swiper image {
	width: 100%;
}
.topic-new {
	padding: 20upx;
}
.topic-new > view:first-child {
	padding-bottom: 5upx;
	font-size: 32upx;
}
</style>
