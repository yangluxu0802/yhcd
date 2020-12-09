<template>
	<view>
		<view>
			<map :latitude="lat" :longitude="lng" :markers="covers" scale="18" :show-location="true" :controls="controls" id="map"
			 @controltap="controltap"></map>
		</view>
		<view class="flex">
			<navigator url="/pages/site/site" class="flex-sub padding-sm margin-xs radius">
				<image src="/static/index/personalCenter.png">附近站点</image>
			</navigator>
			<button @click="scanCodeTocharge" class="cu-btn line-orange round lg shadow">扫码充电</button>
			<navigator url="/pages/personalCenter/personalCenter" class="flex-sub padding-sm margin-xs radius">
				<image src="/static/index/personalCenter.png">个人中心</image>
			</navigator>
		</view>
	</view>
</template>

<script>
	import coordinateConversionUtil from '../../utils/coordinateConversionUtil.js';
	export default {
		data() {
			return {
				mapContext: null,
				lat: "",
				lng: "",
				covers: [],
				controls: [{
					id: 100,
					position: {
						left: 0,
						top: 60,
						width: 30,
						height: 30
					},
					iconPath: '/static/index/aim.png',
					clickable: true
				}]
			}
		},
		onLoad() {
			this.mapContext = uni.createMapContext("map");
			console.log(this.mapContext);
		},
		onShow() {
			uni.getLocation({
				type: 'wgs84',
				success: res => {
					let wgs84togcj02 = coordinateConversionUtil.wgs84togcj02(res.longitude, res.latitude);
					this.lat = wgs84togcj02[1];
					this.lng = wgs84togcj02[0];
					if (this.covers.size === 1) {
						this.covers.clear();
					}
					this.covers.push({
						id: 1,
						latitude: this.lat,
						longitude: this.lng,
						iconPath: ""
					});
				}
			});
		},
		methods: {
			scanCodeTocharge() {
				uni.scanCode({
					success: function(res) {
						console.log('条码类型：' + res.scanType);
						console.log('条码内容：' + res.result);
					}
				});
			},
			controltap() {
				this.mapContext.moveToLocation();
			}
		}
	}
</script>

<style lang="scss" scoped>
	map {
		width: 100%;
		height: 1000rpx;
	}

	image {
		width: 50rpx;
		height: 50rpx;
	}
</style>
