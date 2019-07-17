<template name="helloComp">
	<view class="content">
		{{msg}}
		<input type="text" :value="myval" />
	</view>
</template>

<script>
	export default{
		name:"helloComp",
		data (){
			return {
				msg:"我是自定义模板"
			}
		},
		props:{   //定义接收传过来的值
			myval:{
				type:String    //定义参数类型
			}
		},
		onLoad(){
			
		},
		
	}
</script>

<style>
	
</style>
