<template>
	<view class="content">
		<!-- 影片基本信息 -->
		<view class="info">
			<navigator :url="'../cover/cover?large=' + infolist.images.large">
						<image  class="info_img" :src="infolist.images.large"></image>
			</navigator>
			<view class="info_p">
				<view class="info_title">{{infolist.title}}</view>
				<view class="info_ps">{{infolist.year}}/{{infolist.genres}}</view>
				<view class="info_ps">原名:{{infolist.original_title}}</view>
				<view class="info_ps">上映地区:{{infolist.countries}}</view>
				<view class="l_p">
					<view class="l_pf">
						<view>综合评分:</view>
						<view class="l_fenshu">{{infolist.rating.average}}</view>
					</view>
					<view class="zong">
						<block v-if="infolist.rating.average >= 0">
							<grade :innerScore="infolist.rating.average" showNum="0"></grade>
						</block>
						<view >综合点赞数</view>
					</view>
				</view>
			</view>
			<view
		</view>
	</view>
</template>

<script>
	import grade from "../../components/grade.vue";
	export default {
		data() {
			return {
				infolist:{},
				fens: 0,
			}
		},
		onLoad(params){   //上个页面传进来的ID
			var id = params.id;
			uni.setNavigationBarColor({
				frontColor:'#fff',
				backgroundColor:"#000"
			}),
			uni.request({
				url:'http://t.yushu.im/v2/movie/subject/'+id,
				method:"GET",
				data:"JSON",
				success:(res) =>{
					// console.log(res.data);
					var f =  res.data;
					this.infolist = f;
					this.fens = f.rating.average;
					console.log(this.fens);   //  9.2
					// console.log(this);
				}
			})
			// .then(data =>{
			// 			// console.log(res.data);
			// 		var f =  res.data;
			// 		this.infolist = f;
			// 		this.fens = f.rating.average;
			// 		console.log(this.fens);   //  9.2
			// 		// console.log(this);
			// })
			console.log(this.fens);   // 0
			console.log(this.infolist);
		},
		onShareAppMessage(res) {
			  return {
					  title: this.infolist.title,
					  path: '/pages/info/info?id='+ this.infolist.id
				}
		},
		methods: {

		},
		components:{   //注册自定组件
			// helloComp,
			grade
		}
	}
</script>

<style>
	@import url("./info.css");
</style>
