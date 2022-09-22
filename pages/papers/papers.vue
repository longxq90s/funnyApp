<template>
	<view class="body">
		<!-- 操作菜单 -->
		<left-popup :isShow="isShow" 
			@clear="clear" 
			@toggleHide="toggleHide" 
			@addFriend="addFriend"></left-popup>
		<view>
			<block v-for="(item, index) in userList" :key="index"><list :item="item"></list></block>
			<load-more :loadText="loadText"></load-more>
		</view>
	</view>
</template>
<script>
import uniBadge from '../../components/uni-badge/components/uni-badge/uni-badge.vue';
import list from '../../components/paper/list.vue';
import loadMore from '../../components/common/loadMore.vue';
import leftPopup from '../../components/paper/paperLeftPopup.vue';
module.exports = {
	data() {
		return {
			isShow: false,
			loadText: '上拉加载更多',
			userList: [
				{
					pic: '../../static/img/demo8.jpg',
					name: '张三as',
					time: '12:00',
					message: '吃饭',
					messageNum: 333
				}
			]
		};
	},
	components: {
		list,
		loadMore,
		leftPopup
	},
	onPullDownRefresh() {
		this.getData();
	},
	onReachBottom() {
		this.loadMore();
	},
	onNavigationBarButtonTap(e) {
		console.log('e', e);
		switch (e.index) {
			case 0:
				console.log('左侧按钮');
				uni.navigateTo({
					url:"/pages/friendList/friendList"
				})
				this.toggleHide();
				break;
			case 1:
				this.toggleShow();
				break;
		}
	},
	methods: {
		getData() {
			setTimeout(() => {
				let arr = [
					{
						pic: '../../static/img/demo8.jpg',
						name: '张三as',
						time: '12:00',
						message: '吃饭',
						messageNum: 333
					},
					{
						pic: '../../static/img/demo8.jpg',
						name: '张as',
						time: '19:00',
						message: '睡觉',
						messageNum: 333
					},
					{
						pic: '../../static/img/demo9.jpg',
						name: '张s',
						time: '12:00',
						message: '吃饭',
						messageNum: 333
					},
					{
						pic: '../../static/img/demo9.jpg',
						name: '张s',
						time: '12:00',
						message: '吃饭',
						messageNum: 333
					},
					{
						pic: '../../static/img/demo9.jpg',
						name: '张s',
						time: '12:00',
						message: '吃饭',
						messageNum: 333
					},
					{
						pic: '../../static/img/demo9.jpg',
						name: '张s',
						time: '12:00',
						message: '吃饭',
						messageNum: 333
					},
					{
						pic: '../../static/img/demo9.jpg',
						name: '张s',
						time: '12:00',
						message: '吃饭',
						messageNum: 333
					},
					{
						pic: '../../static/img/demo9.jpg',
						name: '张s',
						time: '12:00',
						message: '吃饭',
						messageNum: 333
					},
					{
						pic: '../../static/img/demo9.jpg',
						name: '张s',
						time: '12:00',
						message: '吃饭',
						messageNum: 333
					},
					{
						pic: '../../static/img/demo9.jpg',
						name: '张s',
						time: '12:00',
						message: '吃饭',
						messageNum: 333
					},
					{
						pic: '../../static/img/demo9.jpg',
						name: '张s',
						time: '12:00',
						message: '吃饭',
						messageNum: 333
					},
					{
						pic: '../../static/img/demo9.jpg',
						name: '张s',
						time: '12:00',
						message: '吃饭',
						messageNum: 333
					},
					{
						pic: '../../static/img/demo9.jpg',
						name: '张s',
						time: '12:00',
						message: '吃饭',
						messageNum: 333
					},
					{
						pic: '../../static/img/demo9.jpg',
						name: '张s',
						time: '12:00',
						message: '吃饭',
						messageNum: 333
					},
					{
						pic: '../../static/img/demo9.jpg',
						name: '张s',
						time: '12:00',
						message: '吃饭',
						messageNum: 333
					}
				];
				this.userList = arr;
				uni.stopPullDownRefresh();
			}, 2000);
		},
		loadMore() {
			if (this.loadText !== '上拉加载更多') return;
			this.loadText = '加载中...';
			setTimeout(() => {
				let obj = {
					pic: '../../static/img/demo7.jpg',
					name: '王二麻子',
					time: '12:30',
					message: '睡觉',
					messageNum: 888
				};
				this.userList.push(obj);
				this.loadText = '上拉加载更多';
			}, 4000);
		},
		addFriend() {
			console.log('添加朋友');
		},
		clear() {
			console.log('清理缓存');
		},
		toggleShow() {
			this.isShow = true;
		},
		toggleHide(){
			this.isShow = false;
		}
	}
};
</script>
<style lang="scss" scoped>
.body {
	padding: 0 10upx;
}
</style>
