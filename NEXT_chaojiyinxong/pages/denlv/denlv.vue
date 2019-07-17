<template>
	<view class="denlv">
		<form @submit="submit">
			<view class="photo">
				<image class="img" src="../../static/rento.png"></image>
			</view>
			<view class="zh">
				<text class="">账号:</text>
				<input name="name" class="zh_input" type="number" placeholder="请输入账号" placeholder-style="color:#ddd;"/>
			</view>
			<view class="line"> 
				<view class="linea"></view>
			</view>
			<view class="mm">
				<text>密码:</text>
				<input name="pass" type="text" placeholder="请输入密码" password="true" placeholder-style="color:#ddd;"/>
			</view>
			<view class="line"> 
				<view class="linea"></view>
			</view>
			<button type="primary" form-type="submit" style="margin-top:60upx;width:400upx;">
					注册/登录 
			</button>	
				
		</form>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			submit(e){
				var me = this;
				var name = e.detail.value.name;
				var pass = e.detail.value.pass;
				uni.setStorage({
					key: 'aaa',
					data: {
						// name:name,
						// pass:pass
						name:"hello"
					},
					success: function (res) {
						console.log(res.aaa);
					}
				});
				// console.log(name);
				// console.log(pass);
			}
		}
	}
</script>

<style>
	@import url("./denlv.css");
</style>
