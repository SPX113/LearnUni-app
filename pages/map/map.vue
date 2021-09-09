<template>
	<view>
		<map name="china" :longitude="longitude" :latitude="latitude"  
		  :markers="markers">
			
		</map>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				latitude: 39.908754,
				longitude: 116.397446,
				markers: []
			}
		},
		methods: {
			getLoaction(){
				var that = this;
				uni.authorize({
					scope: "scope.userLocation",
					success: function(res){
						uni.getLocation({
							success: function(posistion){
								that.latitude = posistion.latitude;
								that.longitude = posistion.longitude;
								that.markers.push({
									id: 0,
									latitude: posistion.latitude,
									longitude: posistion.longitude,
									// iconPath: '../../static/icon/location-fill.png',
									callout:{
										content: "当前位置",
										color: "#fff",
										bgColor: "#00c16f",
										display: 'ALWAYS',
										borderRadius: 5,
										padding: 10
									}
								});
							},
							fail: function(error){
								console.log(error);
							}
						});
					},
					fail(error) {
						uni.showToast({
							title: "启用此功能可在右上角设置中授权",
							icon: "none"
						})
					}
				
				})
				
				
			}
		},
		mounted() {
			this.getLoaction();
		}
	}
</script>

<style lang="scss">
	map{
		width: 750rpx;
		height: 100vh;
	}
</style>
