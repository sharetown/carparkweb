<template>
	<view>
		<view class="page-body">
			<view class="page-section page-section-gap">
				<map show-compass :style="mapStyle" :latitude="latitude" :longitude="longitude" :markers="markers"
					:polyline="polyline" :circles="circles">
				</map>
			</view>
			<view class="map-search">
				<u-search height=84 placeholder="查找停车场" v-model="searchValue"></u-search>
			</view>
		</view>
	</view>
</template>


<script>
	export default {
		data() {
			return {
				id: 123654, // 使用 marker点击事件 需要填写id
				title: 'map',
				latitude: 39.908823,
				longitude: 116.39747,
				//地图上标记点信息
				markers: [{
					id: 121654, //标记点id,marker点击事件回调会返回此id。建议为每个marker设置上Number类型id，保证更新marker时有更好的性能。最大限制9位数
					latitude: 39.908823, //纬度
					longitude: 116.39747, //经度
					title: '天安门', //标注点名
					iconPath: '/static/map.png', //标记点显示的图标
					rotate: 0, //图标旋转角度。顺时针旋转的角度，范围 0 ~ 360，默认为 0
					alpha: 1, //标注的透明度。默认1，无透明，范围 0 ~ 1
					width: 40, //标注图标宽度
					height: 40, //标注图标高度
					//自定义标记点上方的气泡窗口
					callout: {
						content: "这也是天安门", //文本
						color: 'red', //文本颜色
						fontSize: 24, //文字大小
						borderRadius: 15, //callout边框圆角
						borderWidth: 50, //边框宽度。微信小程序、京东小程序、百度小程序
						borderColor: 'blue', //边框颜色。微信小程序、京东小程序、百度小程序
						bgColor: 'green', //背景色
						padding: 20, //文本边缘留白
						display: 'ALWAYS', //'BYCLICK':点击显示; 'ALWAYS':常显
						textAlign: 'left', //文本对齐方式。 有效值: left,right,center
						anchorX: 0, //横向偏移量，向右为正数。微信小程序2.11.0
						anchorY: 0 //纵向偏移量，向下为正数。微信小程序2.11.0
					},
					//为标记点旁边增加标签
					label: {
						content: '标签',
						color: 'black',
						fontSize: 28,
						x: 39, //label的坐标，原点是 marker 对应的经纬度
						y: 116, //label的坐标，原点是 marker 对应的经纬度
						//其他一些属性各家小程序有差异，见详细文档
					},
					//经纬度在标注图标的锚点，默认底边中点
					anchor: {

					},
					//自定义点聚合簇效果时使用
					clusterId: 0,
					//自定义气泡窗口
					customCallout: {

					},
					//无障碍访问，（属性）元素的额外描述
					// 'aria-label':"",
					//是否参与点聚合
					// joinCluster:false
				}],
				//路线。指定一系列坐标点，从数组第一项连线至最后一项
				polyline: [{
					//经纬度数组[{latitude: 0, longitude: 0}]
					points: [{
							latitude: 39.908739,
							longitude: 116.397513
						},
						{
							latitude: 39.90693,
							longitude: 116.39757
						},
						{
							latitude: 39.907773,
							longitude: 116.401273
						},
						{
							latitude: 39.90374,
							longitude: 116.397827
						},
						{
							latitude: 39.9025,
							longitude: 116.39778
						}
					], //经纬度数组[{latitude: 0, longitude: 0}]
					color: 'blue', //线的颜色
					width: 2, //线的宽度
					dottedLine: false, //是否虚线
					arrowLine: false, //带箭头的线

				}],
				circles: [{
					latitude: 39.90693,
					longitude: 116.39757,
					color: 'red', //描边的颜色					
					fillColor: '#9AC5F4', //填充的颜色
					radius: 100
				}],
				mapStyle: {
					width: '750rpx',
					height: '1536rpx'
				},
				searchValue: ""
			}
		},
		onLoad() {
			try {
				const res = uni.getSystemInfoSync();
				let newHeight = res.windowHeight / res.windowWidth * 750
				this.mapStyle.height = newHeight + 'rpx'
			} catch (e) {
				// error
			}
		},
		methods: {

		}
	}
</script>


<style lang="scss">
	.page-body {
		width: 750rpx;

		// 设置地图和搜索框两个盒子之间的
		.page-section {
			position: relative
		}

		.map-search {
			width: 750rpx;
			position: absolute;
			top: 120rpx;
			padding: 20rpx;
		}

	}
</style>