<template>
	<view class="container">
		<view>
			<view>
				<u-avatar :src="userInfo.avatarUrl" :show-level="true" size="large"></u-avatar>
			</view>
			<view>
				<view>
					<text>158****0989</text>
				</view>
				<view>
					<navigator url="/pages/personalCenter/changePhoneNumber/changePhoneNumber">
						<button type="default">更换手机号</button>
					</navigator>
				</view>
			</view>
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
			},
			changeLogin() {
				// 授权
				// 获取用户详细信息, 可以获取到说明已经授权过, 直接拿到用户信息
				uni.getUserInfo({
					provider: 'weixin',
					//授权成功的回调
					success(res) {
						uni.showToast({
							title: '授权成功',
							icon: 'none'
						})
						console.info(res.data)
						//that.login(res.data);//授权成功调用自己的登录方法就可以了
					},
					//第一次进入小程序
					fail() {
						uni.navigateTo({
							url: '/pages/login/login'
						})
					}
				});
			}
		},
		onLoad() {
			this.changeLogin();
		}
	}
</script>

<style lang="scss" scoped>
	view.container {
		height: 100vh;
		width: 100%;
	}

	view.container>view:first-child {
		width: 100%;
		display: flex;
		justify-content: flex-start;
		padding: 40rpx;
		margin-bottom: 20rpx;

		>view:first-child {
			margin-right: 40rpx;
		}
	}

	navigator {
		width: 400rpx;

		button {
			width: 400rpx;
		}
	}
</style>
