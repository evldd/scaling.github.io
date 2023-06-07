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
    v-on 可以接收一个定义的方法来调用。
        <div id="app">
       <!-- `greet` 是在下面定义的方法名 -->
      <button v-on:click="greet">Greet</button>
    </div>
     
    <script>
    var app = new Vue({
      el: '#app',
      data: {
        name: 'Vue.js'
      },
      // 在 `methods` 对象中定义方法
      methods: {
        greet: function (event) {
          // `this` 在方法里指当前 Vue 实例
          alert('Hello ' + this.name + '!')
          // `event` 是原生 DOM 事件
          if (event) {
              alert(event.target.tagName)
          }
        }
      }
    })

     也可以用 JavaScript 直接调用方法
    app.greet() // -> 'Hello Vue.js!'
    </script>
        可以用内联 JavaScript 语句：
              <div id="app">
          <button v-on:click="say('hi')">Say hi</button>
          <button v-on:click="say('what')">Say what</button>
        </div>
         
        <script>
        new Vue({
          el: '#app',
          methods: {
            say: function (message) {
              alert(message)
            }
          }
        })
        </script>

### 事件修饰符：
    Vue.js 为 v-on 提供了事件修饰符来处理 DOM 事件细节，如：event.preventDefault() 或 event.stopPropagation()。
    Vue.js 通过由点 . 表示的指令后缀来调用修饰符。
     .stop - 阻止冒泡
     .prevent - 阻止默认事件
     .capture - 阻止捕获
     .self - 只监听触发该元素的事件
     .once - 只触发一次
     .left - 左键事件
     .right - 右键事件
     .middle - 中间滚轮事件
     <!-- 阻止单击事件冒泡 -->
    <a v-on:click.stop="doThis"></a>
    <!-- 提交事件不再重载页面 -->
    <form v-on:submit.prevent="onSubmit"></form>
    <!-- 修饰符可以串联  -->
    <a v-on:click.stop.prevent="doThat"></a>
    <!-- 只有修饰符 -->
    <form v-on:submit.prevent></form>
    <!-- 添加事件侦听器时使用事件捕获模式 -->
    <div v-on:click.capture="doThis">...</div>
    <!-- 只当事件在该元素本身（而不是子元素）触发时触发回调 -->
    <div v-on:click.self="doThat">...</div>
    
    <!-- click 事件只能点击一次，2.1.4版本新增 -->
    <a v-on:click.once="doThis"></a>
    
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
    
       v-model 修饰符
    语法：v-model.修饰符=”变量” 《=》v-model.lazy="aaa"
     lazy，       文本框失去焦点后再去更新数据
     number，当输入数字时，字符串类型将自动转换为number（先输数字，截取前面的数字返回）
     trim，       删除文本框中的前后空格
### Vue.js 允许你自定义过滤器，被用作一些常见的文本格式化。由"管道符"指示, 格式如下：
    <!-- 在两个大括号中 -->
    {{ message | capitalize }}
    
    <!-- 在 v-bind 指令中 -->
    <div v-bind:id="rawId | formatId"></div>
## Vue.js 计算属性
    计算属性关键词: computed。、
    计算属性在处理一些复杂逻辑时是很有用的。
    可以看下以下反转字符串的例子：
    <div id="app">
    {{ message.split('').reverse().join('') }}
    </div>
    使用了计算属性的实例：  
        <div id="app">
      <p>原始字符串: {{ message }}</p>
      <p>计算后反转字符串: {{ reversedMessage }}</p>
    </div>
     
    <script>
    var vm = new Vue({
      el: '#app',
      data: {
        message: 'Runoob!'
      },
      computed: {
        // 计算属性的 getter
        reversedMessage: function () {
          // `this` 指向 vm 实例
          return this.message.split('').reverse().join('')
        }
      }
    })
    </script>
    我们可以使用 methods 来替代 computed，效果上两个都是一样的，但是 computed 是基于它的依赖缓存，只有相关依赖发生改变时才会重新取值。而使用 methods ，在重新渲染的时候，函数总会重新调用执行。
### 过滤器
    ​	过滤器，就是将数据被渲染到视图之前进行格式化处理，而不会修改作用域中原有的数据
    原则是：左值右量（变量也可以不写）
    语法：  **定义过滤器（全局过滤器** **局部过滤器）**
    ​		filters:{
    ​      	过滤器1:function(参数1,参数2…){}
         或
    ​		过滤器2 (参数1,参数2…){}   
    ​		}
    ​		Vue.filter()
    说明：定义过滤器时，必须声明参数，并且参数1是固定的，指的是要操作的数据，剩余的参数是调用过滤器时传递进来的

               **代码演示：**

    <div id="app">
        <dl>
            <dt>{{product.name}}</dt>
            <dd>{{product.price|toprice('$')|tejia}}</dd>
          </dl>
    </div>
    <script>
## Vue.js 样式绑定
###  class 属性绑定：
     我们可以为 v-bind:class 设置一个对象，从而动态的切换 class:
         <style>
    .active {
    	width: 100px;
    	height: 100px;
    	background: green;
    }
    .text-danger {
    	background: red;
    }
    </style>
    </head>
    <body>
    <div id="app">
      <div class="static"
         v-bind:class="{ 'active': isActive, 'text-danger': hasError }">
      </div>
    </div>
    
    <script>
    new Vue({
      el: '#app',
      data: {
        isActive: true,
    	hasError: true
      }
    })
    </script>

    我们也可以直接绑定数据里的一个对象：
    <div id="app">
      <div v-bind:class="classObject"></div>
    </div>
    <script>
    new Vue({
      el: '#app',
      data: {
        classObject: {
          active: true,
          'text-danger': true
        }
      }
    })
    </script>
    
    我们可以把一个数组传给 v-bind:class ，实例如下：
    <div v-bind:class="[activeClass, errorClass]"></div>

    还可以使用三元表达式来切换列表中的 class ：
    <div v-bind:class="[errorClass ,isActive ? activeClass : '']"></div>
### Vue.js style(内联样式) 
    写法同class 属性绑定   
## Vue.js 组件
    注册一个全局组件语法格式如下：
    Vue.component(tagName, options)
    tagName 为组件名，options 为配置选项。注册后，我们可以使用以下方式来调用组件：
    <tagName></tagName>
  ### 全局组件实例
    注册一个简单的全局组件 runoob，并使用它：
    <div id="app">
        <runoob></runoob>
    </div>
     
    <script>
    // 注册
    Vue.component('runoob', {
      template: '<h1>自定义组件!</h1>'
    })
    // 创建根实例
    new Vue({
      el: '#app'
    })
    </script>
### 局部组件实例
注册一个简单的局部组件 runoob，并使用它：
    <div id="app">
        <runoob></runoob>
    </div>
     
    <script>
    var Child = {
      template: '<h1>自定义组件!</h1>'
    }
     
    // 创建根实例
    new Vue({
      el: '#app',
      components: {
        // <runoob> 将只在父模板可用
        'runoob': Child
      }
    })
    </script>
### Prop
    prop 是子组件用来接受父组件传递过来的数据的一个自定义属性。
    
    父组件的数据需要通过 props 把数据传给子组件，子组件需要显式地用 props 选项声明 "prop"：
    
    Prop 实例
    <div id="app">
        <child message="hello!"></child>
    </div>
     
    <script>
    // 注册
    Vue.component('child', {
      // 声明 props
      props: ['message'],
      // 同样也可以在 vm 实例中像 "this.message" 这样使用
      template: '<span>{{ message }}</span>'
    })
    // 创建根实例
    new Vue({
      el: '#app'
    })
    </script>

        动态 Prop
    类似于用 v-bind 绑定 HTML 特性到一个表达式，也可以用 v-bind 动态绑定 props 的值到父组件的数据中。每当父组件的数    据变化时，该变化也会传导给子组件：
    <div id="app">
        <div>
          <input v-model="parentMsg">
          <br>
          <child v-bind:message="parentMsg"></child>
        </div>
    </div>
     
    <script>
    // 注册
    Vue.component('child', {
      // 声明 props
      props: ['message'],
      // 同样也可以在 vm 实例中像 "this.message" 这样使用
      template: '<span>{{ message }}</span>'
    })
    // 创建根实例
    new Vue({
      el: '#app',
      data: {
        parentMsg: '父组件内容'
      }
    })
    </script>

### Prop 验证
    组件可以为 props 指定验证要求。
    为了定制 prop 的验证方式，你可以为 props 中的值提供一个带有验证需求的对象，而不是一个字符串数组。例如：
    Vue.component('my-component', {
      props: {
        // 基础的类型检查 (`null` 和 `undefined` 会通过任何类型验证)
        propA: Number,
        // 多个可能的类型
        propB: [String, Number],
        // 必填的字符串
        propC: {
          type: String,
          required: true
        },
        // 带有默认值的数字
        propD: {
          type: Number,
          default: 100
        },
        // 带有默认值的对象
        propE: {
          type: Object,
          // 对象或数组默认值必须从一个工厂函数获取
          default: function () {
            return { message: 'hello' }
          }
        },
        // 自定义验证函数
        propF: {
          validator: function (value) {
            // 这个值必须匹配下列字符串中的一个
            return ['success', 'warning', 'danger'].indexOf(value) !== -1
          }
        }
      }
    })
    当 prop 验证失败的时候，(开发环境构建版本的) Vue 将会产生一个控制台的警告。
    
    type 可以是下面原生构造器：
    
    String
    Number
    Boolean
    Array
    Object
    Date
    Function
    Symbol
    type 也可以是一个自定义构造器，使用 instanceof 检测。
## vue自定义指令
    添加一个自定义指令，有两种方式：
    
     通过 Vue.directive() 函数注册一个全局的指令。
     通过组件的 directives 属性，对该组件添加一个局部的指令。
    创建全局指令：
    
    需要传入指令名称以及一个包含指令钩子函数的对象，该对象的键即钩子函数的函数名，值即函数体，钩子函数可以有多个。
    
    Vue.directive('self_defined_name',{
      bind:function(el,binding){
      //do someting
      },
      inserted: function(el,binding){
      //do something
      },
    }
    创建局部指令：
    
    直接向创建的 Vue 实例的 directives 字典属性添加键值对，键值对即需要添加的自定义指令及对应钩子函数字典对象。键值    对可以有多个，对应多个自定义指令。
    
    new Vue({
      el:'#app',
      directives:{
        self_defined_name1:{
            bind:function(el,binding){
              //do something
            }
            inserted:function(el,binding){
                      //do something
            },
         }
    
        self_defined_name2:{
            bind:function(el,binding){
              //do something
            }
            inserted:function(el,binding){
                      //do something
            },
         }
      }
    
    })  
## Vue传值
    1.父传子 
    简单描述
    父组件是通过props属性给子组件通信的
    数据是单向流动 父—>子 （子组件中修改props数据，是无效的，会有一个红色警告）
    
    实现步骤
    1.子组件在props中创建一个属性，用于接收父组件传过来的值；
    2.父组件 引入子组件–>注册子组件–>引用子组件；
    3.在子组件标签中添加子组件props中创建的属性；
    4.将所要传递的值赋值给该属性。
    
    props接收的几种写法
    1.直接使用 props 以一维数组的方式接收
    props: ['childCom']

    2.接收字符串
    
    props: {
        childCom: String //这里指定了字符串类型，如果类型不一致会警告的哦
    }

    3.使用对象形式接收，并赋予默认值，但是在数组这里接收有问题，一个大坑，请看第四种
    
    props: {
        childCom: {
            type: String,
            default: 'sichaoyun' 
        }
    }
   
    4.第三种写法：接收数组，是需要以函数形式接收
    
     props: {
        minetlist: {
          type: Array,
          default: function () {
            return []
          }
        }
      }

     Ø  type，类型约束，约束父组件给子组件传递的数据类型，类型可以是：Object、Array、
      Number、String、Boolean
     
     Ø  default，指定默认值，如果父组件没有传递数据，可以指定默认值
     
     Ø  required，指定该数据项是否必须传递
## This.$parent.数据（父组件中的数据名） (可以对父组件的数据进行操作)
## 子传父具体实现步骤
    1.父组件通过$on监听事件，事件处理函数的参数则为接收的数据
    2.子组件通过$emit可以触发事件，
    3.第一个参数为要触发的事件，第二个事件为要传递的数据
    4.sync修饰符：对一个 prop 进行双向绑定

    **代码演示：**（子组件传值给父组件）

    <div id='div1'>   
            <com1  @passsc="parentMethods"></com1>   
        </div>
        <script type="text/javascript">
            var com1={
                template:`
                        <button @click="cbtn">子传父</button>              
                `,
                data:function(){
                    return {
                        sc:'这是子组件的秘密'
                    }
                },
                methods:{
                    cbtn:function(){
                        //发送事件 相当于打电话
                        this.$emit('passsc',this.sc);
                    }
                }
            }
            new Vue({
                el:'#div1',
                components:{com1},
                methods:{
                    parentMethods:function(mimi){
                        console.log(mimi)
                        alert(mimi);
                    }
                }
            });
        </script>
##   插槽(slot)  
    作用：让父组件可以向子组件指定位置插入html结构，也是一种组件间通信的方式，适用于 父组件 ===> 子组件
    分类：默认插槽、具名插槽、作用域插槽
    <slot> 元素作为组件模板之中的内容分发插槽。<slot> 元素自身将被替换。
 ###    默认插槽
     父组件：<zujianming> 插槽内容 </zujianming>
     子组件：<slot></slot> （标签放在哪插槽内容就在哪）
 ###   具名插槽
     父组件：<zujianming slot='myslot' > 插槽内容 </zujianming>
             <zujianming v-slot:myslot > 插槽内容 </zujianming> （vue2.6以上写法）
     子组件：<slot name='myslot' ></slot> （标签放在哪插槽内容就在哪）
 ###   作用域插槽  
    作用域插槽代码演示：
    父组件：<template>
    <div>
        <h1>这里是父组件</h1>
        <child>
            <template slot-scope="slotsProps">
                {{slotsProps.info}}
            </template>
        </child>
        <!-- 自Vue2.6起，语法变成了这样 -->
        <child>
            <template v-slot:default="slotProps">
                {{slotProps.info}}
            </template>
        </child>
    </div>
    </template>

    子组件：<template>
    <div>
        <h2>这里是子组件</h2>
        <slot :info="info"></slot>
    </div>
    </template>
    