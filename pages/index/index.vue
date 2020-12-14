<template>
	<view class="container">
		<view>
			<map :latitude="lat" :longitude="lng" :markers="covers" scale="18" :show-location="true" :controls="controls"
			 id="map" @controltap="controltap"></map>
		</view>
		<view>
			<view>
				<navigator url="/pages/site/site">
					附近站点
				</navigator>
			</view>
			<view><button @click="scanCodeTocharge">
					扫码充电
				</button></view>
			<view>
				<navigator url="/pages/personalCenter/personalCenter">
					个人中心
				</navigator>
			</view>
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
	* {
		padding: 0;
		margin: 0;
	}
	
	view.container {
		height: 100vh;
	}

	view.container view:nth-of-type(2) {
		display: flex;
		justify-content: space-evenly;
		align-items: center;
		align-content: center;
		padding: 15rpx;
	}

	map {
		width: 100%;
		height: 85vh;
	}

	navigator {
		border: solid 1px #ddd;
	}
</style>
