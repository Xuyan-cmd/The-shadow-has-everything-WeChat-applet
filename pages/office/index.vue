<template>
	<view class="content">
		<!-- <view class="">
			<u-upload :fileList="fileList1" name="6" multiple :maxCount="1" width="250" height="150">
				<image src="../../static/upload.jpg" mode="widthFix" style="width: 300px;height: 150px;"></image>
			</u-upload>
		</view> -->
		<tab-bar :current="currentTabIndex" @tabClick="tabClick"></tab-bar>
		<view class="label">
			<view class="label-left">
				<image
					src="https://img0.baidu.com/it/u=1169642874,2626044045&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=771"
					mode="" style="width:150rpx;height:200rpx"></image>
			</view>
			<view class="label-right">
				<view class="">
					流浪地球

				</view>
				<view class="">
					导演；郭帆

				</view>
				<view class="">
					主演： 吴京 屈楚萧 赵今麦 李光洁 吴孟达

				</view>
				<view class="">
					预计上映时间:2019年2月5日

				</view>
			</view>


		</view>
		<view class="box">
			<view class="content-box">
				<view class="items">
					<canvas canvas-id="IFxCHdwzFMSVZuzNoMDuwOkTjxWJiMsCa" id="IFxCHdwzFMSVZuzNoMDuwOkTjxWJiMsC"
						class="charts" @touchend="tap" />
					<view class="" style="font-size:12px;color:#2fc25b;text-align: center;">
						预告片搜索

					</view>
				</view>

				<view class="items">
					<canvas canvas-id="IFxCHdwzFMSVZuzNoMDuwOkTjxWJiMsCb" id="IFxCHdwzFMSVZuzNoMDuwOkTjxWJiMsC"
						class="charts" @touchend="tap" />
					<view class="" style="font-size:12px;color:#976C9E;text-align: center;">
						微博话题度

					</view>
				</view>

				<view class="items">
					<canvas canvas-id="IFxCHdwzFMSVZuzNoMDuwOkTjxWJiMsCc" id="IFxCHdwzFMSVZuzNoMDuwOkTjxWJiMsC"
						class="charts" @touchend="tap" />
					<view class="" style="font-size:12px;color:#DA4279;text-align: center;">
						剧情新鲜度

					</view>
				</view>

			</view>

			<view class="">
				<Eatch></Eatch>
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

			<view class="title">
				智能建议

			</view>
			<view class="" style="font-size: 12px;padding: 10rpx;">
				<view class="">
					节制过渡旁白:
					
				</view>
				<text style="text-indent: 2em;">
					对于许多适应在电影行业中工作的编剧来说,采用“作者画外音”的诱惑是有道理的。但是,正知约翰·奥古斯特所指出的那样(确实知道一些关于适应写作的方法，其中还有笑于改编内容的技巧,《大鱼》，《查理的天使》，《查理和巧克力工厂》等.
				</text>


			</view>
		</view>
	</view>
</template>

<script>
	import uCharts from '@/uni_modules/qiun-data-charts/js_sdk/u-charts/u-charts.js';
	var uChartsInstance = {};
	import Eatch from '../../common/eatch.vue'
	export default {
		components: {
			Eatch
		},
		data() {
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
				cWidth: 220,
				cHeight: 200,
				fileList1: [],
			}
		},
		onReady() {
			//这里的 750 对应 css .charts 的 width
			this.cWidth = uni.upx2px(220);
			//这里的 500 对应 css .charts 的 height
			this.cHeight = uni.upx2px(200);
			this.getServerData();
		},
		onShow() {
			uni.hideTabBar()
			let index = uni.getStorageSync('index')
			if (index == 0) {
				this.currentTabIndex = index
			}
		},
		methods: {
			tabClick(index) {
				console.log('返回tabBar索引：' + index)
				this.currentTabIndex = index
			},

			getServerData() {
				//模拟从服务器获取数据时的延时
				setTimeout(() => {
					//模拟服务器返回数据，如果数据格式和标准格式不同，需自行按下面的格式拼接
					let res = {
						series: [{
							name: "80",
							color: "#2fc25b",
							data: 0.8
						}]
					};
					let b = {
						series: [{
							name: "50",
							color: "#996EA4",
							data: 0.5
						}]
					};
					let c = {
						series: [{
							name: "30",
							color: "#CE4175",
							data: 0.3
						}]
					};
					this.drawCharts('IFxCHdwzFMSVZuzNoMDuwOkTjxWJiMsC', 'IFxCHdwzFMSVZuzNoMDuwOkTjxWJiMsCa', res);
					this.drawCharts('IFxCHdwzFMSVZuzNoMDuwOkTjxWJiMsC', 'IFxCHdwzFMSVZuzNoMDuwOkTjxWJiMsCb', b);
					this.drawCharts('IFxCHdwzFMSVZuzNoMDuwOkTjxWJiMsC', 'IFxCHdwzFMSVZuzNoMDuwOkTjxWJiMsCc', c);

				}, 500);
			},
			drawCharts(id, ids, data) {
				const ctx = uni.createCanvasContext(ids, this);
				uChartsInstance[id] = new uCharts({
					type: "arcbar",
					context: ctx,
					width: this.cWidth,
					height: this.cHeight,
					series: data.series,
					animation: true,
					background: "#FFFFFF",
					color: ["#1890FF", "#91CB74", "#FAC858", "#EE6666", "#73C0DE", "#3CA272", "#FC8452", "#9A60B4",
						"#ea7ccc"
					],
					padding: undefined,
					title: {
						name: data.series[0].name,
						fontSize: 16,
						color: "#2fc25b"
					},

					extra: {
						arcbar: {
							type: "default",
							width: 6,
							backgroundColor: "#E9E9E9",
							startAngle: 0.75,
							endAngle: 0.25,
							gap: 2,
							linearType: "custom"
						}
					}
				});
			},
			tap(e) {
				uChartsInstance[e.target.id].touchLegend(e);
				uChartsInstance[e.target.id].showToolTip(e);
			}
		}
	}
</script>

<style scoped lang="scss">
	.content {
		padding-bottom: 150rpx;
	}

	.charts {
		width: 220rpx;
		height: 200rpx;
	}

	.content {
		width: 80%;
		// padding:20rpx 60rpx;
		margin: 20rpx auto;

		.label {
			display: flex;
			margin-top: 20rpx;

			border: 3px solid #000;
			width: 100%;
			height: 200rpx;
			padding: 15rpx;
			border-radius: 10px;

			.label-right {
				font-size: 14px;
				margin-left: 8rpx;
			}
		}

		.content-box {

			display: flex;

			.items {
				width: 33%;
			}
		}
	}

	.box {
		margin-top: 20rpx;

		border: 3px solid #000;
		width: 100%;
		height: 760rpx;
		padding: 15rpx;
		border-radius: 10px;
	}

	.footer {
		margin-top: 20rpx;

		border: 3px solid #000;
		width: 100%;
		height: 450rpx;
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
