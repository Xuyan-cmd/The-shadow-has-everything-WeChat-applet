<template>
	<view>
		<!-- login view html start -->
		<view>
			<view>
				<view class="header">
					<image src="../../static/logo.png"></image>
				</view>
				<view class="content" v-if="!getinfoed">
					<view>申请获取以下权限</view>
					<text>获得你的公开信息(昵称，头像、地区等)</text>
					<button class="bottom" type="primary" open-type="getUserInfo" withCredentials="true" lang="zh_CN"
						@click="wxGetUserInfo">授权登录</button>

				</view>
			<!-- 	<view v-if="!getphoned && getinfoed">
					<button class='bottom' type='primary' open-type="getPhoneNumber"
						@getphonenumber="getPhoneNumber">授权手机号</button>
				</view> -->
				<view class="section" v-if="!getphoned">
					<view class="titlea">
						请选择您的身份
						
					</view>
					 <u-radio-group
					    v-model="radiovalue1"
					    placement="column"
					    @change="groupChange"
						labelSize="24px"
						iconColor="#fff"
						
					  >
					    <u-radio
					      :customStyle="{marginBottom: '8px'}"
					      v-for="(item, index) in radiolist1"
					      :key="index"
					      :label="item.name"
					      :name="item.name"
					      @change="radioChange"
						  size="24px"
						  labelSize="24px"
						  activeColor="#000"
						  shape="square"
					    >
					    </u-radio>
					  </u-radio-group>
					  
					  <button class="bottom" type="primary" @click="ored">确定</button>
					
				</view>


			</view>
		</view>
		<!-- login view html end -->
	</view>
</template>
<script>
	import WXBizDataCrypt from "@/common/WXBizDataCrypt.js";
	export default {
		data() {
			return {
				 radiolist1: [{
				            name: '影视从业者',
				            disabled: false
				          },
				            {
				              name: '电影爱好者',
				              disabled: false
				            },
				            
				          ],
				          // u-radio-group的v-model绑定的值如果设置为某个radio的name，就会被默认选中
				          radiovalue1: '影视从业者',
				appid: 'wx0c6ff53ca808b76a',
				secret: 'a5f78dfaeb27dbc80f82c9a7da726245',
				code: '',
				sessionKey: '',
				openId: '',
				getinfoed: true,
				getphoned: true,
				userInfo: {
					avatarUrl: '',
					city: '',
					country: '',
					gender: 1,
					language: '',
					nickName: '',
					phone: ''
				},
				pageOption: {}
			};
		},
		methods: {
			 groupChange(n) {
			        console.log('groupChange', n);
			      },
			      radioChange(n) {
			        console.log('radioChange', n);
			      },
			UserPush() {
				let _self = this;
				uni.showToast({
					title:'授权成功！'
				})
				this.getphoned = false
				// setTimeout(() => {
				// 	uni.switchTab({
				// 		url: '../index/index'
				// 	});
				// },1000)
				// this.getphoned = false
			},
			// 第一授权获取用户信息 ===》按钮触发
			wxGetUserInfo() {
				let _self = this;
				// 1.获取用户的信息
				uni.getUserProfile({
					desc: 'weixin',
					success: (infoRes) => {
						console.log(infoRes)
						_self.userInfo = infoRes.userInfo
						console.log(_self.userInfo, 'userinfo')
						_self.getinfoed = true
						uni.showToast({
										title: '授权成功！',
										
									});
						this.UserPush()

					},
					fail: () => {
						uni.showToast({
							title: '获取用户信息失败',
							icon: 'none'
						});
					}
				});
				return false
			},
			// 登录
			login() {
				
				let _self = this;
				// 0. 显示加载的效果
				uni.showLoading({
					title: '登录中...'
				});
				// 1. wx 获取登录用户 code
				uni.login({
					provider: 'weixin',
					success: loginRes => {
						console.log(loginRes);
						_self.code = loginRes.code;
						
						uni.request({
							url: 'https://api.weixin.qq.com/sns/jscode2session?appid=' +
								_self.appid +
								'&secret=' +
								_self.secret +
								'&js_code=' +
								_self.code +
								'&grant_type=authorization_code',
							success: codeRes => {
								console.log(codeRes);
								_self.openId = codeRes.data.openid;
								_self.sessionKey = codeRes.data.session_key;
							this.getinfoed = false
							uni.hideLoading();
							
								// uni.request({
								// 	url: _self.apiServer + 'api/loginApplets',
								// 	data: {
								// 		openid: _self.openId
								// 	},
								// 	method: 'POST',
								// 	success: openIdRes => {
								// 		console.log(openIdRes);
								// 		// 隐藏loading
								// 		uni.hideLoading();
								// 		// 还没授权登录、请先授权然后登录
								// 		if (openIdRes.data.code == 201 || openIdRes
								// 			.data.code == 202) {
								// 			// 提示消息、让用户授权
								// 			uni.showToast({
								// 				title: openIdRes.data.msg,
								// 				icon: 'none'
								// 			});
								// 			this.getinfoed = false
								// 		} else

								// 		if (openIdRes.data.code == 203) {
								// 			// 提示消息、让用户授权
								// 			uni.showToast({
								// 				title: openIdRes.data.msg,
								// 				icon: 'none'
								// 			});
								// 			this.userInfo = openIdRes.data.info
								// 			this.getinfoed = true
								// 			this.getphoned = false
								// 		} else

								// 			// 已经授权了、查询到用户的数据了
								// 			if (openIdRes.data.code == 200) {
								// 				// 用户信息写入缓存
								// 				uni.showToast({
								// 					title: '登录成功'
								// 				})
								// 				uni.setStorageSync('user_id', openIdRes
								// 					.data.info.id);
								// 				uni.setStorageSync('user_nm', openIdRes
								// 					.data.info.nickName);
								// 				uni.setStorageSync('user_fa', openIdRes
								// 					.data.info.avatarUrl);
								// 				uni.setStorageSync('user_nu', openIdRes
								// 					.data.info.create_time);
								// 				uni.setStorageSync('access_token',
								// 					openIdRes.data.token);
								// 				uni.setStorageSync('role', openIdRes
								// 					.data.info.role);
								// 				uni.setStorageSync('user_gender',
								// 					openIdRes.data.info.gender)
								// 				uni.switchTab({
								// 					url: '../index/index'
								// 				});

								// 			}
								// 	},
								// 	fail: () => {
								// 		uni.showToast({
								// 			title: '获取授权信息失败',
								// 			icon: 'none'
								// 		});
								// 		return false;
								// 	}
								// });
							},
							fail: () => {
								uni.showToast({
									title: '获取 SesssionKey OpenId 失败',
									icon: 'none'
								});
								return false;
							}
						});
					},
					fail: () => {
						uni.showToast({
							title: '获取 code 失败',
							icon: 'none'
						});
						return false;
					}
				});
				return false;
			},
			ored(){
				console.log(this.radiovalue1)
				uni.setStorageSync('user',this.radiovalue1)
				if(this.radiovalue1 == '影视从业者'){
					uni.switchTab({
						url: '../office/index'
					});
				} else {
					uni.switchTab({
						url:'../index/index'
					})
				}
					
				
			},
			getPhoneNumber(e) {
				let _self = this
				if (e.detail.errMsg == "getPhoneNumber:fail user deny") { //用户决绝授权  

					//拒绝授权后弹出一些提示  

				} else { //允许授权  
					console.log(e)

					let pc = new WXBizDataCrypt(this.appid, this.sessionKey); //wxXXXXXXX为你的小程序APPID  
					let data = pc.decryptData(e.detail.encryptedData, e.detail.iv);
					console.log(data)
					//data就是最终解密的用户信息  

					_self.userInfo.phone = data.phoneNumber
					uni.setStorageSync('user_id', _self.userInfo.phone);

					// 2.提交数据到后台、写入数据库
					// uni.request({
					// 	url: this.apiServer + 'api/updUser',
					// 	data: this.userInfo,
					// 	method: 'POST',
					// 	success: res => {
					// 		if (res.data.code != 200) {
					// 			uni.showToast({
					// 				title: res.data.msg,
					// 				icon: 'none'
					// 			});
					// 			return false;
					// 		}
					// 		// 用户信息写入缓存
					// 		uni.showToast({
					// 			title: '登录成功'
					// 		})
					// 		console.log(res, '2222')
					// 		uni.setStorageSync('user_id', res.data.info.id);
					// 		uni.setStorageSync('user_nm', res.data.info.nickName);
					// 		uni.setStorageSync('user_fa', res.data.info.avatarUrl);
					// 		uni.setStorageSync('user_nu', res.data.info.create_time);
					// 		uni.setStorageSync('access_token', res.data.token);
					// 		uni.setStorageSync('role', res.data.info.role);
					// 		uni.setStorageSync('user_gender', res.data.info.gender)
					// 		uni.switchTab({
					// 			url: '../index/index'
					// 		});
					// 	},
					// 	fail: () => {
					// 		uni.showToast({
					// 			title: '用户信息操作失败',
					// 			icon: 'none'
					// 		});
					// 	}
					// });
				}
			}

		},
		
		onLoad(options) {
			
			// 接收跳转的参数
			// console.log(options)
			var user_id = uni.getStorageSync('user_id');
			
			if (user_id != '') {
				// 使用重定向的方式跳转至登录页面
				uni.switchTab({
					url: '../index/index'
				});
				return;
			}

			this.login();
		}
	};
</script>
<style>
	.section{
		padding: 20rpx 100rpx;
	}
	.titlea{
		text-align: center;
   font-size: 24px;
   color: #000;
   margin-bottom: 40rpx;
	}
	.header {
		margin: 90rpx 0 90rpx 50rpx;
		border-bottom: 1px solid #ccc;
		text-align: center;
		width: 650rpx;
		height: 300rpx;
		line-height: 450rpx;
	}

	.header image {
		width: 200rpx;
		height: 200rpx;
	}

	.content {
		margin-left: 50rpx;
		margin-bottom: 90rpx;
	}

	.content text {
		display: block;
		color: #9d9d9d;
		margin-top: 40rpx;
	}

	.bottom {
		border-radius: 80rpx;
		margin: 70rpx 50rpx;
		font-size: 35rpx;
	}
</style>
