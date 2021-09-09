<template>
	<view>
		<button type="primary" @click="scanCode">扫一扫</button>
	</view>
</template>

<script>
	export default {
		methods:{
			scanCode(){
				uni.authorize({
					scope: "scope.camera",
					success(){
						uni.scanCode({
							// onlyFromCamera: true,
							success: function(res) {
								console.log('条码类型：' + res.scanType);
								console.log('条码内容：' + res.result);
							}
						});
					},
					fail(){
						uni.showToast({
							title: "启用此功能可在右上角设置中授权",
							icon: "none"
						})
					}
				})	
			}
		},
		onShow() {
			
		}
	}
</script>
