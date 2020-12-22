<template>
	<view>
		<button open-type="getPhoneNumber" @getphonenumber="getPhoneNumber" type="primary">获取电话号码</button>
	</view>
</template>

<script>
	var RdWXBizDataCrypt = require('@/pages/login/RdWXBizDataCrypt.js');
	export default {
		data() {
			return {
				code: '',
			}
		},

		onLoad: function() {
			var that = this;
			uni.login({
				success: res => {
					// 获取code    
					console.log(JSON.stringify(res));
					//{"errMsg":"login:ok","code":"071JIp1t1pv马赛克t1Ran1t1JIp1l"}  
					this.code = res.code;
				}
			});

		},
		methods: {
			getPhoneNumber: function(e) {
				console.log(e);
				if (e.detail.errMsg == 'getPhoneNumber:fail user deny') {
					console.log('用户拒绝提供手机号');
				} else {
					console.log('用户同意提供手机号');

					console.log(JSON.stringify(e.detail.encryptedData));
					console.log(JSON.stringify(e.detail.iv));

					uni.request({
						url: 'https://api.weixin.qq.com/sns/jscode2session?appid=wxec2137d7d7c2bc3b&secret=d98f2f0ae5151bcbf1e29f5795ca8644&js_code=' +
							this.code + '&grant_type=authorization_code',
						success(re) {
							console.log('session_key:' + re.data.session_key);

							var appId = "wxec2137d7d7c2bc3b";
							var sessionKey = re.data.session_key;

							var pc = new RdWXBizDataCrypt(appId, sessionKey);
							var data = pc.decryptData(e.detail.encryptedData, e.detail.iv);

							console.log('------------------->');
							console.log('解密后 data: ', data);
							console.log('------------------->');

						}
					});
				}
			}
		},
	}
</script>

<style>

</style>
