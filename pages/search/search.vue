<template>
	<view>
		搜索页面
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		onNavigationBarButtonTap(e){
			if(e.index === 0){
				uni.navigateBack({
					delta:1
				})
			}
		},
		onNavigationBarSearchInputChanged(e){
			console.log(e.text);
		},
		onNavigationBarSearchInputConfirmed(e){
			console.log(e.text);
		},
		methods: {
			
		}
	}
</script>

<style>

</style>
