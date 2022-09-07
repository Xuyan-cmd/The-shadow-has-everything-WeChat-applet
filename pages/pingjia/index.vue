<template>
	<view class="pingjia">
		<tab-bar :current="currentTabIndex" @tabClick="tabClick"></tab-bar>
		<view class="upload" v-if="type">
			<view class="title">
				点击上传文件

			</view>
			<view class="" style="margin: 0 auto; width: 100%;">
				<u-upload :fileList="fileList1" name="6" multiple :maxCount="1" width="250" height="150">
					<image src="../../static/upload.jpg" mode="widthFix" style="width: 300px;height: 150px;    margin-left: 30px;"></image>
				</u-upload>
			</view>
		</view>
	
		<view class="box" v-else>
			<image src="../../static/yinpian.png" mode="" style="width: 100%;height: 300rpx;"></image>
			<view class="heads">
				<text style="font-weight: 700;">评分：</text>
				<u-rate :count="count" v-model="value"  size="28" active-color="#FBC02D"></u-rate> <text
					style="color: #FBC02D;">80</text>

			</view>
			<view class="text">
				<view class="title">
					流浪地球
				</view>
				<view class="" style="margin-bottom: 20rpx;">

					<u--textarea v-model="value1" placeholder="写下你的影评吧"   height="250"></u--textarea>
				</view>
				<u-button type="primary" text="发布"></u-button>

			</view>
			<view class="footer">
				分享至: <u-icon name="qq-fill" size="24px"></u-icon>
				<u-icon name="weixin-circle-fill" size="24px"></u-icon>
				<u-icon name="moments" size="24px"></u-icon>
				<u-icon name="weibo" size="24px"></u-icon>  <text style="font-size: 16px;">预览</text>

			</view>
		</view>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				currentTabIndex: 0,
				type: true,
				count: 5,
				value: 3,
				value1: '',
				fileList1: [],
			}
		},
		methods: {
			tabClick(index) {
				console.log('返回tabBar索引：' + index)
				this.currentTabIndex = index
			},
		},
		onShow() {
			uni.hideTabBar()
			let index = uni.getStorageSync('index')
			let flag = uni.getStorageSync('user')
			if (flag == '影视从业者') {
				this.type = true
			} else {
				this.type = false
			}
			if (index) {
				this.currentTabIndex = index

			}
		}
	}
</script>

<style scope lang="scss">
	.pingjia {
		padding-bottom: 150rpx;
	}
	.upload{
		.title{
			text-align: center;
      font-size: 28px;
	  color: #9B9B99;
	  margin-bottom: 40rpx;
		}
	}

	.box {
		padding: 30rpx 8%;

		.heads {
			margin-top: 40rpx;
			display: flex;
			justify-content: space-between;
		}

		.text {
			margin-top: 20rpx;

			.title {
				font-size: 48rpx;
				font-weight: 700;
				color: #9B9B99;
				text-align: center;
				padding: 15rpx;

			}
		}

		.footer {
			display: flex;
			padding: 20rpx 40rpx;
			font-size: 24px;
			justify-content: space-between;
			color: #9B9B99;
		}
	}
</style>
