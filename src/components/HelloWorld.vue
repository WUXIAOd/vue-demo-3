<template>
  <div class="hello">
   <h3>这是axios项目，用来发送请求，拦截响应</h3>
   <button @click='getData'>GET方式发送请求</button>
   <button @click='postData'>post方式发送请求</button>
   <ul>
     <li v-for="item in items">
       {{item.title}}
     </li>
   </ul>
  </div>
</template>

<script>

Vue.prototype.$http = axios  //将axios 全局挂载到Vue原型上
import axios from 'axios' //引入加载
import Vue from 'vue'
import qs from 'qs'

export default {
  name: 'HelloWorld',
  data () {
    return {
      items:[]
    }
  },
  methods:{
    getData(){//请求以cnode社区API为例子
      this.$http.get('https://cnodejs.org/api/v1/topics',{
        params:{//这是参数
          page: 2,
          limit:5
        }
      })
      .then((res)=>{//此处用了ES6语法，不用箭头函数下面使用this.items 会出错
        this.items = res.data.data
        console.log(this.items)
      })
      .catch((err)=>{
        console.log(err)
      })
    }
  },
  postData(){
      this.$http.post(url,qs.stringify({
        params:{//这里的参数必须经过qs插件使用stringify使其格式为 form-data 
        //因为在axios中，post请求接收的参数必须是 form-data
          page: 2,
          limit:5
        }
      }))
      .then((res)=>{
        this.items = res.data.data
        console.log(this.items)
      })
      .catch((err)=>{
        console.log(err)
      })
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
