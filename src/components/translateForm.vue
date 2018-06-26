<template>
  <div id="translateForm" class="row">
  	<div class="col-md-6 col-xs-6"></div>
    <form v-on:submit="formSubmit" class="well">
    	<div class="form-group">
    		<input type="" name="" placeholder="请输入" class="form-inline form-control" v-model="textToTranslate">
    	</div>
    	<div class="form-group">
	    	<select v-model="language" class="form-control"><!--为了知道点击的是哪个-->
		        <option value="zh">中文</option>
		        <option value="en">英语</option>
		        <option value="ru">俄语</option>
		        <option value="ko">朝鲜语</option>
		        <option value="ja">日语</option>
		        <option value="es">西班牙语</option>
		        <option value="it">意大利语</option>
		        <option value="de">德语</option>
	    	</select>
    	</div>
    	<input type="submit" value="翻译" name="" class="btn btn-primary">
    </form>
  </div>
</template>

<script>
export default {
  name: 'translateForm',
  data: function(){
  	return {
  		textToTranslate: "",
  		language: ""//在这实现一下，为了确定点击的是哪个下拉,传递到App.vue中去，因为在App.vue中请求的时候是要用到language的，只需要把en替换成选中的内容就行，language
  	}
  },
  methods: {
  	formSubmit: function(e){
  		console.log(this.textToTranslate);//拿到用户输入的内容
  		//点击的时候拿到内容，接着要把内容参数传递给根组件，最终需要的只是在translateForm中输入的内容传递到APP中，然后在根组件中将用户输入的内容翻译过来，将翻译好的内容传给outPut里面。
  		this.$emit("formSubmit",this.textToTranslate,this.language);
  		//vue提供一个事件注册的方法，这个方法默认是一个参数，参数就是你要注册的一个事件，其他参数就是你要传递的具体的实参。
  		//this.textToTranslate参数传递到App.vue中，然后在App.vue里面拿一个变量接收
  		if(this.textToTranslate == ""){
  			alert('请先输入需要翻译的文字')
  			return;
  		}
  		e.preventDefault();//阻止表单提交默认事件
  	}
  },
  created: function(){
  	this.language = "zh"
  }
}
</script>

<style>

</style>
