<script>
	export default {
		onLaunch: function() {
			uni.login({
				provider: 'weixin',
				success: function(loginRes) {
					console.log(loginRes.authResult);
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
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>


<style lang="scss">
	//@import "uview-ui/index.scss";
	@import "colorui/main.css";
	@import "colorui/icon.css";
	@import "colorui/animation.css";
	
	page{
		height: 100vh;
	}
</style>
