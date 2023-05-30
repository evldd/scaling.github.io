# vue 
## vue起步
### 在 Vue 构造器中有一个el 参数，它是 DOM 元素中的 id,data 用于定义属性，实例中有三个属性分别为：site、url、alexa。methods 用于定义的函数，可以通过 return 来返回函数值。{{ }} 用于输出对象属性和函数返回值。
    <div id="vue_det">
    <h1>site : {{site}}</h1>
    <h1>url : {{url}}</h1>
    <h1>{{details()}}</h1>
    </div>
    <script type="text/javascript">
        var vm = new Vue({
            el: '#vue_det',
            data: {
                site: "菜鸟教程",
                url: "www.runoob.com",
                alexa: "10000"
            },
            methods: {
                details: function() {
                    return  this.site + " - 学的不仅是技术，更是梦想！";
                }
            }
        })
    </script>
## Vue.js 模板语法
### HTML 属性中的值应使用 v-bind 指令。  
### v-if 指令根据表达式 seen 的值(true 或 false )来决定是否插入 p 元素。
    <div id="app">
    <p v-if="seen">现在你看到我了</p>
    </div>        
    <script>
    new Vue({
      el: '#app',
      data: {
        seen: true
      }
    })
    </script>
### v-on 指令，它用于监听 DOM 事件  
      <a v-on:click="doSomething">
### 在 input 输入框中我们可以使用 v-model 指令来实现双向数据绑定：
    <div id="app">
    <p>{{ message }}</p>
    <input v-model="message">
    </div>
        
    <script>
    new Vue({
      el: '#app',
      data: {
        message: 'Runoob!'
      }
    })
    </script>
### Vue.js 允许你自定义过滤器，被用作一些常见的文本格式化。由"管道符"指示, 格式如下：
    <!-- 在两个大括号中 -->
    {{ message | capitalize }}
    
    <!-- 在 v-bind 指令中 -->
    <div v-bind:id="rawId | formatId"></div>


