<script>
	export default {
		onLaunch: function() {
			uni.login({
			  provider: 'weixin',
			  success: function (loginRes) {
			    console.log(loginRes.authResult);
			    // 获取用户信息
			    uni.getUserInfo({
			      provider: 'weixin',
			      success: function (infoRes) {
			        console.log('用户昵称为：' + infoRes.userInfo.nickName);
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
	@import "uview-ui/index.scss";
</style>
