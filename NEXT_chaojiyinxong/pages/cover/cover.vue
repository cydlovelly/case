<template>
	<view>
		<view class="cover">
			<!-- src="https://img3.doubanio.com/view/photo/s_ratio_poster/public/p480747492.jpg" -->
			<image @longtap ="postd" class="cover-img" :src="cover" mode="widthFix"></image>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				cover:""
			}
		},
		onLoad(params){
			var cover = params.large;
			this.cover = cover;
			uni.setNavigationBarColor({
				frontColor:'#fff',
				backgroundColor:"#000"
			})
			console.log(this.cover);
		},
		methods: {
			postd(){
				uni.showActionSheet({  //​显示操作菜单
					itemList:['下载图片','分享'],
					success:(res) =>{
						if(res.tapIndex == 0){
							uni.showLoading({   //显示中间的加载框
								title:"图片保存中..."
							})
							uni.downloadFile({   //下载文件资源到本地，客户端直接发起一个 HTTP GET 请求，返回文件的本地临时路径。
								url:this.cover,
								success:function(result){
									var a = result.tempFilePath;
									uni.saveImageToPhotosAlbum({   // 保存到系统相册
										filePath:a,
										success:function(){
											uni.showToast({
												title:"保存成功",
												duration:2000
											})
										},
										complete:function(){
											uni.hideLoading();
										}
									})
									console.log(a);
								}
							})
						}
					}
				})
			}
		}
	}
</script>

<style>
	.cover{
		width: 100%;
		height:100%;
		background: #000;
		display: flex;
		flex-direction: column;
		justify-content: center;
		position: fixed;
	}
	.cover-img{
		width: 750upx;
		
	}
</style>
