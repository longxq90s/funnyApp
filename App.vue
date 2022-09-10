<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/*每个页面公共css */
	@import "@/common/uni.css";
	/* 引入图标 */
	@import "@/common/icon.css";
	/* 引入动画库 */
	@import "@/common/animate.css";
	/* 引入全局公共样式 */
	@import "@/common/common.css";
</style>
