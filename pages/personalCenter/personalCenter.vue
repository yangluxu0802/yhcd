<template>
	<view>
		<view>
			<u-avatar :src="src" :show-level="true" size="large"></u-avatar>
			<h1>158****0989</h1>
			<u-button size="medium" plain>更换手机号</u-button>
		</view>
		<view>
			<view>
				<u-cell-group>
					<u-cell-item icon="setting-fill" title="我的钱包"></u-cell-item>
					<u-cell-item icon="integral-fill" title="我的订单"></u-cell-item>
					<u-cell-item icon="integral-fill" title="我的券包"></u-cell-item>
					<u-cell-item icon="integral-fill" title="消息管理"></u-cell-item>
				</u-cell-group>
			</view>
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
				src: 'http://pic2.sc.chinaz.com/Files/pic/pic9/202002/hpic2119_s.jpg',
			};
		}
	}
</script>

<style lang="scss" scoped>

</style>
