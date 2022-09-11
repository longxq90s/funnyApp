<template>
	<view>
		<view class="box-bg">
			<uni-nav-bar shadow left-icon="left" leftText="返回" rightText="发布" @clickLeft="goBack" @clickRight="submit">
				<view class="flex-center" style="width: 100%;" @tap="toggleState">
					{{ showArea }}
					<view class="iconfont icon-arrow-down"></view>
				</view>
			</uni-nav-bar>
			<!-- textarea输入框 -->
			<view class="uni-textarea"><textarea v-model="text" placeholder="发表内容...." class="text-input" /></view>
			<!-- 上传多张图片 -->
			<upload-image @selectImg="selectImg"></upload-image>
			<!-- 提示信息 -->
			<!-- <button @click="openModal('center')">开启模态框</button> -->
			<uni-popup ref="popup" backgroundColor="#fff" @change="change" >
				<view class="popup-content">
					<view class="pop-img"><image src="@/static/img/inputWarning.png" mode=""></image></view>
					<text class="warningWord">
						<p>1.严禁发布涉黄图片或文字！</p>
						<p>2.设计人身攻击</p>
						<p>3.留联系方式，透露他人隐私</p>
						<p>
							一经核实将被封禁，情节严重则永久封禁
						</p>
					</text>
					<view class="btn">
						<button @click="dialogClose">朕知道了</button>
					</view>
				</view>
			</uni-popup>
		</view>
	</view>
</template>

<script>
import uniNavBar from '../../components/uni-nav-bar/components/uni-nav-bar/uni-nav-bar.vue';
import uploadImage from '@/components/common/uploadImage.vue';
import uniPopup from '@/components/uni-popup/uni-popup.vue';

let itemLists = ['所有人可见', '仅自己可见'];

export default {
	data() {
		return {
			showArea: '所有人可见',
			text: '',
			imageList: [],
			isget:false,
		};
	},
	components: {
		uniNavBar,
		uploadImage,
		uniPopup
	},
	onLoad() {},
	onBackPress() {
		if(!this.text && this.imageList.length < 1){return ;}
		if(!this.isget){
			this.saveToPaper()
			return true;
		}
	},
	mounted() {
		this.openModal('center');
	},
	methods: {
		// 发布按钮
		submit() {
			console.log('发布按钮');
		},
		// 返回
		goBack() {
			uni.navigateBack({
				delta: 1
			});
		},
		// 切换可见范围
		toggleState() {
			uni.showActionSheet({
				itemList: itemLists,
				success: res => {
					this.showArea = itemLists[res.tapIndex];
				}
			});
		},
		selectImg(imgArr) {
			this.imageList = imgArr;
		},
		// 切换开启弹框
		openModal(type) {
			console.log(this.$refs.popup);
			// this.$refs.popup.open()
			this.$refs.popup.open(type);
		},
		dialogClose() {
			this.$refs.popup.close()
		},
		change() {
			showPopup: false;
			show: false;
		},
		// 保存草稿
		saveToPaper(){
			uni.showModal({
				content:"是否保存为草稿？",
				cancelText:"不保存",
				confirmText:"保存",
				success: (res) => {
					if(res.confirm){
						console.log("保存");
					}else{
						console.log("不保存");
					}
					this.isget=true
					uni.navigateBack({
						delta:1
					})
				},
			})
			return true
		}
	}
};
</script>

<style lang="scss" scoped>
.text-input {
	border: 1px solid #ccc;
}
.cell-pd {
	padding: 22rpx 30rpx;
}

.popup-content {
	width: 600upx;
	.pop-img {
		display: flex;
		justify-content: center;
		align-items: center;
		& image {
			width: 300upx;
			height: 250upx;
			padding: 20upx;
			object-fit: scale-down;
		}
	}
	.warningWord {
		margin-left: 40upx;
		width: 550upx;
		height:150upx;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: space-around;
		// background-color: red; 
		font-weight: bold;
		& p{
			font-weight: bold;
		}
	}
	.btn button{
		background-color: #ffff00;
	}
}
</style>
