<template>
	<view>
		<!-- 顶部切换栏 -->
		<uni-nav-bar :statusBar="true" @clickRight="clickRight" class="head">
			<!-- 左边 -->
			<block slot="left"><view class="iconfont icon-qiandaoicon"></view></block>
			<!-- 中间 -->
			<view class="head-middle flex-center">
				<block v-for="(item, index) in tabBars" :key="item.id">
					<view class="flex-center " :class="selectedIndex === index ? 'active' : ''" @tap="toggleSelect(index)">
						{{ item.name }}
						<view v-if="selectedIndex === index" class="nav-tab-line"></view>
					</view>
				</block>
			</view>
			<!-- 右边 -->
			<block slot="right"><view class="iconfont icon-bianjishuru"></view></block>
		</uni-nav-bar>
	</view>
</template>

<script>
	import uniNavBar from '@/uni_modules/uni-nav-bar/components/uni-nav-bar/uni-nav-bar.vue';
	export default {
		props:{
			tabBars:Array,
			selectedIndex:Number
		},
		components:{
			uniNavBar,
		},
		data() {
			return {
				
			}
		},
		methods: {
			// 切换激活选项
			toggleSelect(index) {
				this.$emit("toggleSelect",index)
				// this.selectedIndex = index;
			},
			clickRight(){
				uni.navigateTo({
					url:"/pages/addInput/addInput"
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
.head {
	background-color: red;
	.iconfont {
		font-size: 50upx;
	}
	.icon-qiandaoicon {
		color: orange;
	}
	.head-middle {
		width: 100%;
		.nav-tab-line {
			border-bottom: 5upx solid #fede33;
			border-top: 5upx solid #fede33;
			width: 70upx;
			border-radius: 20upx;
			position: absolute;
			bottom: 12upx;
		}
	}
	.head-middle > view {
		width: 30%;
		height: 60%;
	}
	.active {
		color: #fede33;
	}
}
</style>
