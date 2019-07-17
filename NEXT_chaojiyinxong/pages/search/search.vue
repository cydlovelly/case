<template>
	<view class="content">
		<view class="search"> 
			<view class="test">&#xe635;</view>
			<input id="search_input" type="text" confirm-type="search" @confirm="searchshow" placeholder="搜索影片" />
		</view>
		<view class="s_ul">
			<image v-for="item in sList" class="s_li" :src="item.images.large" :data-id="item.id" @click="showinfo"></image>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				sList:[],
				keywords:"",   //搜索的内容
				page:1 ,//当前第几页
				totalpage:1 //总页数
			}
		},
		onLoad(){
			uni.showLoading({
				mask:true,
				title:"请等一下...."
			});
			uni.showNavigationBarLoading();
			uni.request({
				url:"http://t.yushu.im/v2/movie/top250",
				method:"GET",
				success: (res)=> {
					console.log(res.data.subjects);
					var a = res.data.subjects;
					this.sList = a;
				},
				complete:() =>{
					uni.hideNavigationBarLoading();
					uni.hideLoading();
				}
				
			})
		},
		onReachBottom(){
			var page = this.page;   
			var keywords = this.keywords;
			var totalpage = this.totalpage;
			
			if( page > totalpage){
				return ;
			}
			
			this.pagedTrailerList(keywords,page,5);
		},
		methods: {
			showinfo(e){
				var id = e.currentTarget.dataset.id;
				uni.navigateTo({
					url:"../info/info?id="+id
				})
			},
			pagedTrailerList(keywords,page,totalpage){
				uni.showLoading({
					mask:true,
					title:"请等一下...."
				});
				uni.showNavigationBarLoading();
				uni.request({
					url:'http://t.yushu.im/v2/movie/top250?start='+page+'&count='+totalpage,
					method:"GET",
					success: (res)=> {
						console.log(res.data.subjects);
						var a = res.data.subjects;
						this.sList = this.sList.concat(a);
						this.totalpage  = res.data.total;
						this.page = page;
					},
					complete:() =>{
						uni.hideNavigationBarLoading();
						uni.hideLoading();
					}
					
				})
			},
			searchshow(e){
				var value = e.detail.title;
				console.log(value);
				this.keywords = value;
				this.sList = [];
				this.pagedTrailerList(value,1,15);
			}
		}
	}
</script>

<style>
	@import url("./search.css");
	@font-face {
  font-family: 'iconfont';  /* project id 1235831 */
  src: url('//at.alicdn.com/t/font_1235831_bih3qpzmefk.eot');
  src: url('//at.alicdn.com/t/font_1235831_bih3qpzmefk.eot?#iefix') format('embedded-opentype'),
  url('//at.alicdn.com/t/font_1235831_bih3qpzmefk.woff2') format('woff2'),
  url('//at.alicdn.com/t/font_1235831_bih3qpzmefk.woff') format('woff'),
  url('//at.alicdn.com/t/font_1235831_bih3qpzmefk.ttf') format('truetype'),
  url('//at.alicdn.com/t/font_1235831_bih3qpzmefk.svg#iconfont') format('svg');
}
    .test {
        font-family: iconfont;
        margin-left: 20upx;
    }
</style>
