<template>
  <div>
  <div id="app" ref="container">
    <pre>
      {{code}}
    </pre>
   
  </div>
  <div class="resumeEditor" >
       <pre>
         {{resumeCode}}
       </pre>
  </div>
  <pre>
     <code v-html="styleCode">

  </code>
  </pre>
 
  </div>
  
</template>

<script>
import HelloWorld from './components/HelloWorld'


export default {
  name: 'App',
  components: {
  },
  data(){
    return {
      
      code:``,
      finalCode:`
/*
* Inspired by http://strml.net/
* 大家好，我是吴逸飞
* 
* 我也来写一份简历！
*/

/* 首先给所有元素加上过渡效果 */
* {
  transition: all .3s;
}
/* 白色背景太单调了，我们来点背景 */
html {
  color: rgb(222,222,222); background: #666;
}
/* 文字离边框太近了 */
#app {
  padding: .5em;
  border: 1px solid;
  margin: .5em;
  overflow: auto;
  width: 45vw; height: 90vh;
}

/* 加点 3D 效果呗 */
html{
  perspective: 1000px;
}
#app {
  position: fixed; left: 0; top: 0;
  transform: rotateY(10deg) translateZ(-100px) ;
  animation: breath 0.5s infinite alternate-reverse;
}

/* 接下来我给自己准备一个编辑器 */
.resumeEditor{
  position: fixed; right: 0; top: 0;
  padding: .5em;  margin: .5em;
  width: 48vw; height: 90vh;
  border: 1px solid;
  background: white; color: #222;
  overflow: auto;
}
      `,
finalCode2 :`
吴逸飞
----
合肥工业大学大三学生
技能
----
* js
* html&css
* vue
* python(接触过django和)
工作经历
----
暂无
链接
----
* [GitHub](https://github.com/Mamba-working)
> 如果你喜欢这个效果，Fork [我的项目](https://github.com/_demo)，打造你自己的简历！
`
,
      resumeCode:`
      `
    }
  },
  created:function(){
     this.makeResume();
  },
  computed:{
    styleCode(){
      return "<style>"+this.code+"</style>"
    },
   
  }
  ,
  methods:{
       makeResume: async function () {
        await this.firstCode();
        await this.highLight();
        await this.editResume();
      },
     firstCode(){
       return new Promise((resolve,reject) =>{
         let n = 0;
         var container = this
         let timer = setInterval(() =>{
         if(n < this.finalCode.length){
           app.scrollTo(0,100000);
           this.code = this.finalCode.substring(0,n);
           n = n+1;
         }else{
           clearInterval(timer);
           resolve();
         }
       },20);
      
       })
     
    },
    highLight(){
      return new Promise((resolve,reject) =>{
        // let app = document.querySelector("#app")
        // app.innerHTML = Prism.highlight(prefix + code.substring(0, n), Prism.languages.css);
        resolve();
      })
    },
    editResume(){
      return new Promise((resolve,reject) =>{
        let n = 0;
        let timer = setInterval(()=>{
            if(n<this.finalCode2.length){
              
              
              this.resumeCode= this.finalCode2.substring(0,n);
              n = n+1;
            }
        },20)
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
  position:fixed;
  height:90%;
  width:50%;
  
}
@keyframes breath{
  0%{
    box-shadow: 0 0 10px rgba(0,0,0,1)
  }
  100%{
    box-shadow: 0 0 10px rgba(0,0,0,0.2)
  }
}
</style>
