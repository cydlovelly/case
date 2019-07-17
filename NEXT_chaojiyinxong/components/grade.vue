<template name="grade">
	<view class="content">
		<view class="poster-star">
			<!-- <image class="star-img" src="../static/wujiaox.png"></image>
			<image class="star-img" src="../static/wujiaox.png"></image>
			<image class="star-img" src="../static/wujiaox.png"></image>
			<image class="star-img" src="../static/wujiaox.png"></image>
			<image class="star-img" src="../static/wujiaox1.png"></image>
			<view class="star-p">9.4分</view> -->
			<!-- {{n}} -->
			<image 
				v-for="yellow in yellowScore"
				class="star-img" 
				src="../static/wujiaox.png"
			></image>
			<image 
				v-for="gray in grayScore"
				class="star-img" 
				src="../static/wujiaox1.png"
			></image>
			<view class="star-p" v-if="showNum == 1">{{innerScore}}分</view>
		</view>
	</view>
</template>

<script>
	export default{
		name:"grade",
		data (){
			return {
				yellowScore:0,   
				grayScore:5,
				n:0         
			}
		},
		props:{   //定义接收传过来的值
			innerScore:0,      //定义外部传来的分数
			showNum:0        //是否显示具体的分数 1：显示  2：不显示
		},
		onLoad(){
			
		},
		created (){
			var tempScore = 0;
			if(this.innerScore != null && this.innerScore != undefined && this.innerScore != ""){   //判断是否为空等条件
				var tempScore = this.innerScore;    
			}
			var yellowScore = parseInt(tempScore/2);  //黄色星星
			var grayScore = 5 - yellowScore;      // 灰色星星
			this.n = tempScore;   //测试
			//动态的绑定到data
			this.yellowScore = yellowScore;
			this.grayScore  = grayScore;
			console.log(tempScore);
		}
		
		
	}
</script>

<style>
	.poster-star{
		display:flex;
		flex-direction:	row;
	}
	.star-img{
		width:20upx;
		height:20upx;
		margin-top:6upx;
	}
	.star-p{
		font-size:12px;
	}
</style>
