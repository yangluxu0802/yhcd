<script>
	export default {
		onLaunch: function() {
			uni.login({
				provider: 'weixin',
				scopes: ['auth_user'],
				success: function(loginRes) {
					console.log(loginRes);
					console.log(loginRes.code);
					// 获取用户信息
					uni.getUserInfo({
						provider: 'weixin',
						success: function(infoRes) {
							console.log(infoRes.userInfo);
							uni.setStorage({
								key: 'userInfo',
								data: infoRes.userInfo,
								success: function() {
									console.log('success');
								}
							});
						}
					});
				}
			});
		},
		onShow: function() {},
		onHide: function() {}
	}
</script>


<style lang="scss">
	@import "uview-ui/index.scss";
	@import "colorui/main.css";
	@import "colorui/icon.css";
	@import "colorui/animation.css";

	page {
		height: 100vh;
	}
</style>
