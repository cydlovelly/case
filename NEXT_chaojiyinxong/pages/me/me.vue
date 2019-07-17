<template>
	<view class="page">
		<view class="header">
			<view class="photo" v-if="flag">
				<image class="face" src="../../static/banner.jpg"></image>
			</view>
			<view class="photo" v-else>
				<image class="face" src="../../static/rento.png"></image>
			</view>
			<view class="den" v-if="flag">
				<view class="den_p">NEXT 学院</view>
				<view class="den_id den_p">ID: 123456789</view>
			</view>
			<view class="den" v-else>
				<navigator url="../denlv/denlv">
					<view class="den_p" style="margin-top:40upx;">注册/登录</view>
				</navigator>
			</view>
			<view class="set-wapper" v-if="flag">
				<text class="test">&#xe68d;</text>
			</view>
			<view class="set-wapper" v-else>
				<!-- <text class="test">&#xe68d;</text> -->
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				flag:false
			}
		},
		methods: {
			
		}
	}
</script>

<style>
	@import url("./me.css");
		@font-face {
  font-family: 'iconfont';  /* project id 1235831 */
  src: url('//at.alicdn.com/t/font_1235831_cwbp5gihy0t.eot');
  src: url('//at.alicdn.com/t/font_1235831_cwbp5gihy0t.eot?#iefix') format('embedded-opentype'),
  url('//at.alicdn.com/t/font_1235831_cwbp5gihy0t.woff2') format('woff2'),
  url('//at.alicdn.com/t/font_1235831_cwbp5gihy0t.woff') format('woff'),
  url('//at.alicdn.com/t/font_1235831_cwbp5gihy0t.ttf') format('truetype'),
  url('//at.alicdn.com/t/font_1235831_cwbp5gihy0t.svg#iconfont') format('svg');
}
		.test {
		      font-family: iconfont;
		      margin-left: 20upx;
		}
</style>
