<template>
	<view>
		<view class="userinfo">
			<u-avatar :src="userInfo.avatarUrl" :show-level="true" size="large"></u-avatar>
			<text>158****0989</text>
			<navigator url="/pages/personalCenter/changePhoneNumber/changePhoneNumber">
				<button type="default">更换手机号</button>
			</navigator>
		</view>
		<view>
			<u-cell-group>
				<u-cell-item icon="setting-fill" title="我的钱包" index="wallet" @click="gotoPages"></u-cell-item>
				<u-cell-item icon="integral-fill" title="我的订单" index="order" @click="gotoPages"></u-cell-item>
				<u-cell-item icon="integral-fill" title="我的券包" index="3" @click="gotoPages"></u-cell-item>
				<u-cell-item icon="integral-fill" title="消息管理" index="4" @click="gotoPages"></u-cell-item>
			</u-cell-group>
		</view>
		<view>
			xx充电
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				userInfo: ''
			};
		},
		methods: {
			gotoPages(index) {
				let url = '/pages/personalCenter/' + index + '/' + index;
				console.log(url)
				uni.navigateTo({
					url: url
				});
			}
		},
		onLoad() {
			uni.getStorage({
				key: 'userInfo',
				success: res => {
					console.log(res.data);
					this.userInfo = res.data;
				}
			});
		}
	}
</script>

<style lang="scss" scoped>
	.userinfo{
		width: 100%;
		height: 300rpx;
		background-color: red;
		display: flex;
		justify-content: space-evenly;
		align-items: center;
		u-avatar{
			float: left;
		}
		navigator{
			height: 80rpx;
			width: 50%;
			button{
				height: 80rpx;
			}
		}
	}
</style>
