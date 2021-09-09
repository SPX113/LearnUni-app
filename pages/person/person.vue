<template>
	<view class="container">
		<view class="header">
			<view class="photo">
				<image :src="photo" mode=""></image>
			</view>
			<view class="info" v-if="isLogin">
				<view id="name">
					<text>{{name}}</text>
				</view>
				<view id="ID">
					<text space="ensp">APP ID:{{ID}}</text>
				</view>
			</view>
			<view class="info" v-else  
			<!-- #ifdef MP-WEIXIN -->
			@click="login"
			<!-- #endif -->
			>
				<view>
					<text id="name">未登录/点击登录</text>
				</view>
			</view>
			
		</view>
		<view class="body">
			<navigator class="item"  url="../personalInfo/personalInfo">	
				<view class="icon_1 iconfont icon-gerenxinxi_o"></view>
				<view class="icon_2 iconfont icon-jinru"></view>
				<view class="des">个人信息</view>
			</navigator>
			<view class="item">
				<view class="icon_1 iconfont icon-gongneng"></view>
				<view class="icon_2 iconfont icon-jinru"></view>
				<view class="des">功能</view>
			</view>
			<view class="item">
				<view class="icon_1 iconfont icon-shezhi"></view>
				<view class="icon_2 iconfont icon-jinru"></view>
				<view class="des">设置</view>
			</view>
			<navigator target="miniProgram" open-type="exit">
				<view class="item">
					<view class="icon_1 iconfont icon-tuichu"></view>
					<view class="icon_2 iconfont icon-jinru"></view>
					<view class="des">退出</view>
				</view>
			</navigator>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				isLogin: false,
				name: "",
				ID: "SPX113",
				photo: "../../static/photo.jpg"
			}
		},
		methods:{
			// #ifdef MP-WEIXIN
			login(){
				let that = this;
				uni.getUserProfile({
					desc: "登录",
					success(res) {
						uni.setStorage({
						    key: 'login',
						    data: res,
						    success: function () {
						        that.isLogin = true;
								that.name = uni.getStorageSync('login').userInfo.nickName;
								that.photo = uni.getStorageSync('login').userInfo.avatarUrl;
						    }
						});
					},
					fail(err){
						console.log(err);
					}
				})
			},
			checkLogin(){
				let loginMessage = uni.getStorageSync('login');
				if(loginMessage){
					this.isLogin = true;
					this.name = uni.getStorageSync('login').userInfo.nickName;
					this.photo = uni.getStorageSync('login').userInfo.avatarUrl;
				}
			},
			// #endif
			
		},
		mounted() {
			// #ifdef MP-WEIXIN
			this.checkLogin();
			// #endif
		}
	}
</script>

<style lang="scss">
	@import url("~@/static/iconfont/iconfont.css");
	page{
		background-color: #F2F3F4;
	}
	.header{
		background-color: #FFFFFF;
		display: flex;
		justify-content: center;
		align-items: center;
		.photo{
			padding: 75rpx 50rpx;
			image{
				width: 150rpx;
				height: 150rpx;
				border-radius: 10rpx;
			}
		}
		.info{
			flex:1;
			#name{
				font-size: 50rpx;
			}
			#ID{
				color: gray;
			}
		}
	}
	.icon-tuichu{
		color: rgb(216,0,0);
	}
	.icon-gerenxinxi_o{
		color: rgb(0,178,106);
	}
	.icon-shezhi{
		color: blue;
	}
	
	.item{
		background-color: #FFFFFF;
		margin: 28rpx 0;
		height: 100rpx;
		line-height: 100rpx;
		// &:hover{
		// 	background-color: rgba(119,119,119,0.2);
		// }
		.icon_1{
			width: 75rpx;
			font-size: 60rpx;
			float: left;
			margin-left: 50rpx;
		}
		.icon_2{
			width: 75rpx;
			float: right;
		}
		.des{
			overflow: hidden;
			padding-left: 20rpx;
		}
	}
</style>
