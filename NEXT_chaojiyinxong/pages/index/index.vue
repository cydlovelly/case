<template>
	<view class="content">
		<!-- 自定义组件传值  父传子 -->
		<!-- <helloComp myval="你好我是父传你过来的值"></helloComp> -->
		<!-- 评分 -->
		<!-- <grade innerScore="10" showNum="1"></grade> -->
		<!-- 轮播图 -->
		<swiper class="banner" :indicator-dots="true" :autoplay="true" >
			<swiper-item>
				<image class="banner1" src="../../static/banner.jpg"></image>
			</swiper-item>
			<swiper-item>
				<image class="banner1" src="../../static/banner2.jpg"></image>
			</swiper-item>
		</swiper>
		<!-- 轮播图结束 -->
		
		<!-- 火热项目 -->
		<view class="page-block hot-title">
			<view class="hot-t">
				<image class="hot-img" src="../../static/huore.png"></image>
				<view class="hot-p">热门影片</view>
			</view>
			<scroll-view scroll-x class="page-block hot">
				<view class="single-poster" v-for="lista in list">
					<view class="poster-wapper">
						<image class="poster-img" :src="lista.images.large"></image>
						<view class="movie-name">{{lista.title}}</view>
						<grade :innerScore="lista.rating.average" showNum="1"></grade>
					</view>
				</view>
			</scroll-view>
		</view>
		<!-- 火热结束 -->
		<!-- 热门预告 -->
		<view class="page-block hot-title">
			<view class="hot-t">
				<image class="hot-img" src="../../static/remen.png"></image>
				<view class="hot-p">热门预告</view>
			</view>
			<view  class="hot-movies page-block">
				<video v-for="videoa in listvideo" :src="videoa" class="hot-video" controls></video>
			</view>
		</view>
		<!-- 热门预告结束 -->
		<!-- 猜你喜欢 -->
		<view class="hot-title">
			<view class=" hot-cai">
					<view class="page-block hot-t">
						<image class="hot-img" src="../../static/cainixihaun.png"></image>
						<view class="hot-p">热门预告</view>
					</view>	
					<view class="page-block single-like-video" v-for="(listb,gIndex) in listc">
						<image :src="listb.images.large" class="poster"></image>
						<view class="video-desc">
							<view class="cai-title">{{listb.title}}</view>
							<grade :innerScore="listb.rating.average" showNum="0"></grade>
							<view class="cai-p">{{listb.genres}}</view>
							<!-- <view class="cai-pb">演员:{{listb.casts.name}}</view> -->
							<view class="cai-pb">上映时间:{{listb.year}}</view>
						</view>
						<view class="video-oper"  >
							<image class="oper-img" src="../../static/dianzhan.png" :data-gIndex="gIndex" @click="praiseMe"></image>
							<view class="oper-p" :data-gIndex="gIndex" @click="praiseMe">点赞</view>
							<view :animation="animationDataarr[gIndex]" class="oper-img oper-1">+1</view>
						</view>
					</view>
			</view>
			
		</view>
		<!-- 猜你喜欢结束 -->
	</view>
</template>

<script>
	// 引入脚本
	// import common from "../../common/common/common.js";
	
	// 引入自定组件
	// import helloComp from "../../components/helloComp.vue";
	import helloComp from "../../components/helloComp.vue";
	import grade from "../../components/grade.vue";
	export default {
		data() {
			return {
				title: 'Hello',
				animationData:{},
				animationDataarr:[
					{},{},{},{},{}
				],
				list:[],
				listc:[],
				listvideo:[
					"../../static/fulinas.3gp",
					"../../static/jinqiduiz.3gp",
					"../../static/heiguafu~1.3gp",
					"../../static/zhizux.3gp"
				]
			}
		},
		onUnload(){
			this.animationData = {},
			this.animationDataarr = [
				{},{},{},{},{}
			]
		},
		onpullDownRefresh(){
			this.refresh();
		},
		onLoad() {
			// var serverUrl = common.serverUrl;
			//再页面创建的时候创建有个临时动画
			// #ifdef APP-PLUS || MP-WEIXIN
				this.animation= uni.createAnimation();
			// #endif
			var serverUrl = this.serverUrl;
			//请求轮播图
			// uni.request({
			// 	url:'http://api.douban.com/v2/movie/nowplaying?apikey=0b2bdeda43b5688921839c8ecb20399b',
			// 	method:'POST',
			// 	success: (res) => {
			// 		console.log(res.data);
			// 		if(res.data.status == 200){
						// var a = res.data;
						// this.list = a;
			// 		}
			// 	},
			// 	error:(error) =>{
			// 		console.log(error);
			// 	}
			// }),
			//热门电影
			uni.request({
				url: 'http://t.yushu.im/v2/movie/in_theaters?city=南京&start=0&count=10',
				method:'GET',
				header: {
					'content-type': 'application/json'
				},
				success: (res) => {
					// if(this.status == 200){
						// console.log(res.data.subjects);
						var a = res.data.subjects;
						this.list = a.slice(0,6);
						
						// console.log();
					// }
				},
			}),
			//猜你喜欢
			uni.request({
				url: 'http://t.yushu.im/v2/movie/top250',
				method:'GET',
				header: {
					'content-type': 'application/json'
				},
				success: (res) => {
					// if(this.status == 200){
						console.log(res.data.subjects);
						var a = res.data.subjects;
						this.listc = a.slice(9,20);
						
						// console.log();
					// }
				}
			})
		},
		methods: {
			refresh(){
				uni.showLoading({
					mask:true
				});
				uni.showNavigationBarLoading();
				uni.request({
					url: 'http://t.yushu.im/v2/movie/top250',
					method:'GET',
					header: {
						'content-type': 'application/json'
					},
					success: (res) => {
						// if(this.status == 200){
							console.log(res.data.subjects);
							var a = res.data.subjects;
							this.listc = a.slice(0,9);
							
							// console.log();
						// }
					},
					complete:()=>{
						uni.hideNavigationBarLoading();
						uni.hideLoading();
					}
				})
				
			},
			praiseMe(e){
				var gIndex = e.currentTarget.dataset.gindex;
				console.log(gIndex);
				// return;
				//构建动画·1数据，并且通过step来表达着这组动画完成
				this.animation.translateY(-70).opacity(1).step({
					duration:400
				});
				//导出数据动画到view组件
				// this.animationData = this.animation.export();
				this.animationData = this.animation;
				this.animationDataarr[gIndex] = this.animationData.export();
				// 还原动画
				setTimeout(function(){
					this.animation.translateY(0).opacity(0).step({
						duration:0
					});
						// this.animationData = this.animation.export();
						this.animationData = this.animation;
						this.animationDataarr[gIndex] = this.animationData.export();
				}.bind(this),500)
			}
		},
		components:{   //注册自定组件
			helloComp,
			grade
		}
	}
</script>

<style>
	@import url("./index.css");
</style>
