<template>
	<view>
		<view>
			<map style="width: 750rpx; height: 750rpx;" :latitude="lat" :longitude="lng" :markers="covers" scale="18"
			 :show-compass="true" :controls="controls"></map>
		</view>
		<view>
			<navigator url="/pages/site/site">
				<button type="default">附近站点</button>
			</navigator>
			<u-button type="primary" shape="circle" size="medium" @click="scanCodeTocharge">扫码充电</u-button>
			<navigator url="/pages/personalCenter/personalCenter">
				个人中心
			</navigator>
		</view>
	</view>
</template>

<script>
	import coordinateConversionUtil from '../../utils/coordinateConversionUtil.js';
	export default {
		data() {
			return {
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
			}
		}
	}
</script>

<style lang="scss" scoped>

</style>
