<template>
	<view class="tabbar" :style="{'padding-bottom': paddingBottomHeight + 'rpx'}">
		<view class="tabbar-item" v-for="(item,index) in tabNav" :key="index"
			@click="tabbarChange(item.pagePath,index)">
			<image class="item-img" :src="item.selectedIconPath" v-if="NewCurrent == index"></image>
			<image class="item-img" :src="item.iconPath" v-else></image>
			<view class="item-text" :class="{'tabbarActive': NewCurrent == index}"
				style="color: #A3A3A3;font-size: 20rpx" v-if="item.text">{{item.text}}</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			current: String,
		},
		watch: {
			current(val) {
				this.NewCurrent = val
				console.log(this.NewCurrent)
			}
		},
		data() {
			return {
				tabNav: [],
				NewCurrent: 0,
				paddingBottomHeight: 0 //iPhonex以上手机底部适配高度
			}
		},
		created() {
			//适配iPhonex以上的底部
			uni.getSystemInfo({
				success: (res) => {
					let model = ['X', 'XR', 'XS', '11', '12', '13', '14', '15'];
					// console.log('iphone',res)
					for (let i = 0; i <= model.length; i++) {
						if (res.model.indexOf(model[i]) != -1 && res.model.indexOf('iPhone') != -1) {
							this.paddingBottomHeight = 50
							//向父组件传递tabbar高度
							this.$emit('tabbarHeight', 150)
							return
						} else {
							this.$emit('tabbarHeight', 100)
						}
					}
				}
			})
			
			// 根据权限配置对应tab导航
			//管理员
			let list1 = [{
					"pagePath": "../index/index",
					"iconPath": "../../static/home.png",
					"selectedIconPath": "../../static/home-active.png",
					"text": "影评广场",

				}, {
					"pagePath": "../pingjia/index",
					"iconPath": "../../static/add.png",
					"selectedIconPath": "../../static/add-active.png",
					"text": "",

				},
				{
					"pagePath": "../me/index",
					"iconPath": "../../static/me.png",
					"selectedIconPath": "../../static/me-active.png",
					"text": "个人中心",

				}

			]
			//厨师
			let list2 = [{
					"pagePath": "../office/index",
					"iconPath": "../../static/baobiao.png",
					"selectedIconPath": "../../static/baobiao-active.png",
					"text": "票房预测",


				},  {
					"pagePath": "../pingjia/index",
					"iconPath": "../../static/add.png",
					"selectedIconPath": "../../static/add-active.png",
					"text": "",

				},

				{
					"pagePath": "../my/index",
					"iconPath": "../../static/me.png",
					"selectedIconPath": "../../static/me-active.png",
					"text": "个人中心"
				}
			]
			
			
			
			
			let a = uni.getStorageSync('user')
			console.log(a)
			// debugger
			if(a == '影视从业者') {
				this.tabNav  = list2
			} else {
				this.tabNav = list1
			}
			
			
			
		},
		methods: {
			//跳转切换tab
			tabbarChange(path, index) {
				this.$emit('tabClick', index)
				uni.setStorageSync('index', index)
				uni.switchTab({
					url: path
				})
			}
		},
		
	}
</script>

<style scoped lang="scss">
	.tabbarActive {
		color: red !important;
	}

	.tabbar {
		position: fixed;
		bottom: 0;
		left: 0;
		display: flex;
		justify-content: space-around;
		align-items: center;
		width: 100%;
		height: 100rpx;
		background-color: #000;
		border-top: 1px solid #e5eaea;
		z-index: 9999999;
	}

	.tabbar-item {
		flex: 1;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		// height: 100rpx;
	}

	.item-img {
		margin-bottom: 4rpx;
		width: 46rpx;
		height: 46rpx;
	}

	.item-name {
		font-size: 26rpx !important;
		color: #fff !important;
	}
</style>
