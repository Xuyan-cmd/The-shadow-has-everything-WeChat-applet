<template>
	<view class="me">
		<tab-bar :current="currentTabIndex" @tabClick="tabClick"></tab-bar>
		<view class="info">
			<image src="../../static/logo.png" mode="aspectFit" style="width: 200rpx;height: 200rpx;"></image>
			
			<view class="box" style="margin-left: 30rpx;">
				<view class="title">
					HOANG NGUYEN
					
				</view>
				<view class="subtitle">
					<image src="../../static/icon2.png" mode="aspectFill" style="width: 30rpx;height: 30rpx;"></image>
					<text style="margin-left: 15rpx;">电影爱好者</text>
					<text style="color: #83802D;margin-left: 15rpx;">Vip3</text>
					
				</view>
				<view class="info_footer">
					<text>获赞数396</text>
					<text style="margin-left: 15rpx;">发布150</text>
					
				</view>
				
				
			</view>
		</view>
		
		<view class="content">
			<tab-bar :current="currentTabIndex" @tabClick="tabClick"></tab-bar>
			<view class="title">
				猜你喜欢
			</view>
			<view class="box-img">
				<view class="item" v-for="(item,index) in imgList" :key="index">
					<image :src="item.img" mode="scaleToFill" style="width: 140rpx;height: 240rpx;"></image>
					<view class="subtitle">
						{{item.title}}
					</view>
		
				</view>
		
			</view>
			<view class="news">
				<text class="tex">换一批</text>
					
			</view>
			<view class="ipt" style="font-size: 18px;font-weight: 700;">
				<!-- <u-input placeholder="请输入" border="surround" class="ipt-content">
		
					<image src="../../static/ss.png" mode="" style="width: 40rpx;height: 40rpx;" slot="prefix">
					</image>
		
				</u-input> -->
				收藏夹(1530)
		
			</view>
			
			<view class="footer" style="margin-top: 20rpx;">
				<view class="items" v-for="item in 10">
					<view class="let">
						<image src="https://img9.doubanio.com/icon/u199451629-34.jpg" mode="" style="width: 60rpx;height: 60rpx;"></image>
					</view>
					<view class="righta">
						<view class="top">
							<u-rate :count="count" v-model="value" readonly size="10" active-color="#FBC02D"></u-rate> <text
								style="font-size: 10px;margin-left: 30rpx;">2020-05-04 01:08:27</text>
		
						</view>
						<view class="content-wenz">
							请耐心等待片刻，我想将我作为一名观众的时间延长片刻，这么说只是因为，当我身处于电影的时间中时，才能抓住在影像中稍纵即逝的愤慨，不安，一丝丝的名为“革命”的情愫。但这些又不单单是电影给予我的，它们更像是在电影中被保存着的，从别的什么地方，从一场完全无关的夏天.
						</view>
						<view class="btns">
							<view class="btns-item">
								<image src="https://img3.doubanio.com/f/zerkalo/536fd337139250b5fb3cf9e79cb65c6193f8b20b/pics/up.png" mode="" style="width: 12px;height: 12px;"></image>
								<text style="font-size: 12px;color:#37a">12</text>
							</view>
							
							<view class="btns-item">
								<image src="https://img3.doubanio.com/f/zerkalo/68849027911140623cf338c9845893c4566db851/pics/down.png" mode="" style="width: 12px;height: 12px;"></image>
								<text style="font-size: 12px;color:#37a">6</text>
							</view>
							
							<view class="btns-item">
								
								<text style="font-size: 12px;color:#37a">32回应</text>
							</view>
							
						</view>
					</view>
		
				</view>
		
			</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data(){
			return {
				currentTabIndex: 0,
				count: 8,
				value: 5,
				title: 'Hello',
				imgList: [{
					img: 'https://img0.baidu.com/it/u=955489389,1031453867&fm=253&fmt=auto&app=138&f=JPEG?w=333&h=500',
					title: '阿甘正传'
				}, {
					img: 'https://img0.baidu.com/it/u=1169642874,2626044045&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=771',
					title: '流浪地球'
				}, {
					img: 'https://img2.baidu.com/it/u=2277718020,2921398622&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=741',
					title: '蝙蝠侠'
				}, {
					img: 'https://img2.baidu.com/it/u=2745448953,3321735437&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=734',
					title: '盗梦空间'
				}]
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
	.me{
		
			padding-bottom: 150rpx;
		
	}
	.info{
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding: 40rpx 8%;
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
	
	.content{
		padding-bottom: 150rpx;
	}
	.items {
		background-color: #fff;
		width: 100%;
		box-shadow: 0 12px 5px -10px rgba(0, 0, 0, 0.1), 0 0 4px 0 rgba(0, 0, 0, 0.1);
		-webkit-box-shadow: 0 12px 5px -10px rgba(0, 0, 0, 0.1), 0 0 4px 0 rgba(0, 0, 0, 0.1);
		border-radius: 5px;
		padding: 20rpx;
		margin-top: 10rpx;
		display: flex;
	
		.let {
			width: 75rpx;
		}
	
		.righta {
			flex: 1;
	
			.top {
				display: flex;
			}
	
			.content-wenz {
				font-size: 14px;
				margin-top: 10rpx;
			}
			.btns{
				display: flex;
				margin-top: 7rpx;
				.btns-item{
					color: #3377aa;
					    padding: 4px 6px;
					    margin-right: 4px;
					    border-radius: 2px;
					    background-color: #f0f7f9;
					    display: inline-block;
					    line-height: 1;
				}
			}
		}
	
	}
	
	.content {
		padding: 20rpx 60rpx;
		background-color: #EEEEEE;
		min-height: 100vh;
	
		.title {
			text-align: center;
			color: #000;
			font-size: 48rpx;
			font-weight: 700;
		}
	
		.box-img {
			display: flex;
			justify-content: space-between;
			margin-top: 30rpx;
	
			.subtitle {
				text-align: center;
				font-size: 14px;
				font-weight: 500;
				margin-top: 15rpx;
	
			}
		}
	}
	
	.ipt {
		margin-top: 80rpx;
		padding: 0 40rpx;
	}
	
	.ipt-content ::v-deep .u-input {
		padding-left: 80rpx !important;
	}
	
	.ipt-content {
		position: relative;
	}
	
	.ipt-content::before {
		content: url('../../static/ss.png');
		display: block;
		width: 30rpx;
		height: 30rpx;
		position: absolute;
		top: 8rpx;
		left: 10rpx;
	
	}
	
	.news {
		// position: relative;
		text-align: right;
		margin-top: 20rpx;
	}
	
	.tex::before {
		content: url('../../static/news.png');
		display: block;
		width: 30rpx;
		height: 30rpx;
		position: absolute;
		// top: 8rpx;
		right: 170rpx;
		margin-top: 5rpx;
		// top:8rpx
	}
	
</style>