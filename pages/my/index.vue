<template>
	<view class="my">
		<tab-bar :current="currentTabIndex" @tabClick="tabClick"></tab-bar>
		<view class="info">
			<image src="../../static/logo.png" mode="aspectFit" style="width: 200rpx;height: 200rpx;"></image>
			
			<view class="box" style="margin-left: 30rpx;">
				<view class="title">
					HOANG NGUYEN
					
				</view>
				<view class="subtitle">
					<image src="../../static/icon2.png" mode="aspectFill" style="width: 30rpx;height: 30rpx;"></image>
					<text style="margin-left: 15rpx;">电影从业者</text>
					<text style="color: #83802D;margin-left: 15rpx;">Vip6</text>
					
				</view>
				<view class="info_footer">
					<text>获赞数1396</text>
					<text style="margin-left: 15rpx;">发布550</text>
					
				</view>
				
				
			</view>
		</view>
		
		<view class="yijiantu" style="margin: 30rpx 0;">
			<view class="titles">
				今日意见词云图
				
			</view>
			<view class="yijiantu_box">
				<image src="../../static/2.jpg" mode="aspectFill" style="width: 450rpx;height: 300rpx;"></image>
				<view class="right">
					<view class="">
						重点关注:
						
					</view>
					<view class="" style="border-bottom: 1px solid #ccc;font-weight: 700;">
						角色
						
					</view>
					<view class="" style="border-bottom: 1px solid #ccc;font-weight: 700;">
						小说改编
					</view>
					
				</view>
			</view>
			
		</view>
		
		<view class="title">
			搜索记录(37)
			
		</view>
		
		<view class="footer">
			<view class="title">
				总体评价
		
			</view>
			<view class="">
				<u-grid :border="false" :col="4">
					<u-grid-item v-for="(baseListItem,baseListIndex) in baseList" :key="baseListIndex">
						<view :customStyle="{paddingTop:40+'rpx'}" v-html="baseListItem.name" :size="10"></view>
						<text class="grid-text" style="color:#386FF2 ;padding-top: 20rpx;">{{baseListItem.title}}</text>
					</u-grid-item>
				</u-grid>
		
			</view>
		
			
			
		</view>
		<view class="footer">
			<view class="title">
				总体评价
		
			</view>
			<view class="">
				<u-grid :border="false" :col="4">
					<u-grid-item v-for="(baseListItem,baseListIndex) in baseList" :key="baseListIndex">
						<view :customStyle="{paddingTop:40+'rpx'}" v-html="baseListItem.name" :size="10"></view>
						<text class="grid-text" style="color:#386FF2 ;padding-top: 20rpx;">{{baseListItem.title}}</text>
					</u-grid-item>
				</u-grid>
		
			</view>
		
			
			
		</view>
		<view class="footer">
			<view class="title">
				总体评价
		
			</view>
			<view class="">
				<u-grid :border="false" :col="4">
					<u-grid-item v-for="(baseListItem,baseListIndex) in baseList" :key="baseListIndex">
						<view :customStyle="{paddingTop:40+'rpx'}" v-html="baseListItem.name" :size="10"></view>
						<text class="grid-text" style="color:#386FF2 ;padding-top: 20rpx;">{{baseListItem.title}}</text>
					</u-grid-item>
				</u-grid>
		
			</view>
		
			
			
		</view>
		
	</view>
</template>

<script>
	export default {
		data(){
			return {
				currentTabIndex: 0,
				baseList: [{
						name: '整体评价',
						title: '受众较广'
					},
					{
						name: '总体得分',
						title: '85分'
					},
					{
						name: '类型题材',
						title: '中上'
					},
					{
						name: '等级评价',
						title: 'A-'
					},
				],
			}
		},
		methods:{
			tabClick(index) {
				console.log('返回tabBar索引：' + index)
				this.currentTabIndex = index
			},
		},
		onShow() {
			uni.hideTabBar()
			let index = uni.getStorageSync('index')
			if (index) {
				this.currentTabIndex = index
			
			}
		}
	}
</script>

<style scope lang="scss">
	.my{
			padding-bottom: 150rpx !important;
			padding:40rpx 8%;
			background-color: #EEEEEE;
	}
	.info{
		display: flex;
		align-items: center;
		justify-content: space-between;
		// padding: 40rpx 8%;
		height: 200rpx;
		background-color: #EEEEEE;
		.box{
			display: flex;
			flex-direction: column;
			justify-content: space-between;
			height: 200rpx;
		}
		.title{
			font-weight: 700;
		}
		.subtitle{
			display: flex;
			align-items: center;
		}
		
	}
	.yijiantu{
			margin: 20rpx 0;
			.titles{
				font-size: 16px;
				font-weight: 700;
				margin-bottom: 20rpx;
			}
			
			.yijiantu_box{
				display: flex;
				justify-content: space-between;
				.right{
					height: 300rpx;
					text-align: center;
					display: flex;
					flex-direction: column;
	justify-content: space-between;
				}
				
			}
		}
		.title{
			font-size: 16px;
			font-weight: 700;
			margin-bottom: 20rpx;
		}
		
		.footer {
			margin-top: 20rpx;
		
			border: 3px solid #000;
			width: 100%;
			height: 200rpx;
			padding: 15rpx;
			border-radius: 10px;
		
			.title {
				font-size: 36rpx;
				font-weight: 700;
				color: #ccc;
				border-bottom: 1px solid #ccc;
				padding-bottom: 5rpx;
			}
		}
</style>