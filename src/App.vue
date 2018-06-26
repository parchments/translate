<template>
  <div id="app">
    <h1>羊皮卷在线翻译</h1>
    <h5>学习自：<a href="">腾讯课堂</a></h5>
    <translateForm v-on:formSubmit="translateText"></translateForm>
    <!--调用组件并且绑定方法，在methods里面实现一下-->
    <translateOutPut v-text="translatedText"></translateOutPut>
  </div>
</template>

<script>
import translateForm from './components/translateForm' //import引入translateForm组件
import translateOutPut from './components/translateOutPut' //import引入组件
export default {
  name: 'app',
  data: function(){
    return {
      translatedText: ""
    }
  },
  components: {
    translateForm,translateOutPut //调用组件
  },
  methods: {
    translateText: function(text,language){//形参text就是在translateForm里的this.textToTranslate
      console.log("点击了翻译按钮，即说明事件注册以及调用都完成");
      console.log(text);
      //这里也代表多个组件传值也就实现了。
      this.$http.get('https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20170721T082515Z.54cf3dc583f679db.f4a96182281281d8b5dfe24b4e88298e2133f219&lang='+language+'&text='+text)
      .then((response)=>{
        console.log(response);//这里会返回一个Response对象
        console.log(response.body.text[0]);//这里会拿Response对象下面body下的text的值
        this.translatedText = response.body.text[0];//translatedText就拿到了翻译好的内容，现在要把这个值传递到outPut组件中去
      })
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}

</style>
