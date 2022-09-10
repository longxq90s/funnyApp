<template>
	<view>
		<view class="box-bg">
			<uni-nav-bar shadow left-icon="left" leftText="返回" rightText="发布" @clickLeft="goBack" @clickRight="submit" >
				<view class="flex-center" style="width: 100%;" @tap="toggleState">
					{{ showArea }}
					<view class="iconfont icon-arrow-down"></view>
				</view> 
			</uni-nav-bar>
			<!-- textarea输入框 -->
			<view class="uni-textarea">
				<textarea v-model="text" placeholder="发表内容...." class="text-input" />
			</view>
			<!-- 上传多张图片 -->
		</view>
	</view>
</template>

<script>
	import uniNavBar from '../../components/uni-nav-bar/components/uni-nav-bar/uni-nav-bar.vue'
	let itemLists = ['所有人可见', '仅自己可见' ]
	export default {
		data() {
			return {
				showArea:'所有人可见',
				text:""
			}
		},
		components:{
			uniNavBar
		},
		methods: {
			// 发布按钮
			submit(){
				console.log('发布按钮');
			},
			// 返回
			goBack(){
				uni.navigateBack({
					delta:1
				})
			},
			// 切换可见范围
			toggleState(){
				uni.showActionSheet({
					itemList:itemLists ,
					success: (res) => {
						console.log('ress',this.showArea);
						console.log('itemlist',itemLists);
						this.showArea = itemLists[res.tapIndex]
					},
				});
			},
		}
	}
</script>

<style lang="scss" scoped>
 .text-input{
	 border:1px solid #ccc ;  
 }
</style>
