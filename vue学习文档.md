#  <img src="https://cn.vuejs.org/images/logo.png" width="100" height="100" alt="图片名称" align=left>渐进式 JavaScript 框架

中文官网 <https://cn.vuejs.org/>



### 什么是vue？

+ 作者:尤雨溪
+ 作用：动态构建用户界面
+ 遵循MVVM模式
+ 编码简洁，体积小、运行效率高，适合移动/PC端开发
+ 它本身只关注UI，可以轻松引入Vue插件或第三方库
+ 借鉴angular的**模板**和**数据绑定**技术
+ 借鉴react的__组件化__和**虚拟DOM**技术



## 第一个DEMO

```vue
<div id="app">     <!--view-->
    <input type="text" v-model="username">
    <p>Hello {{username}}</p>
</div>

<script>
    //创建VUE实例
    const vm = new Vue({  //配置对象
        el:"#app",   //element:选择器
        data:{       //数据（model）
            username:"大V!"
        }
    })
</script>
```

![1560826162835](C:\Users\家浩\AppData\Roaming\Typora\typora-user-images\1560826162835.png)

1. 引入vue.js

2. 创建vue对象

   el : 指定根element(选择器)

   data : 初始化数据

3. 双向数据绑定 ： v-model

4. 显示数据 ：{{ xxx }}

5. 理解Vue的MVVM

   ![1560827596121](C:\Users\家浩\AppData\Roaming\Typora\typora-user-images\1560827596121.png)



## 第二个DEMO（模板语法）

```html
<div id="app">
    <h1>双括号表达式</h1>
    <p>{{msg}}</p>
    <p>{{msg.toUpperCase()}}</p>    <!----textcontent--->
    <p v-text="msg"></p>          <!----textcontent--->
    <p v-html="msg"></p>          <!---innerHTML------>

    <h1>强制数据绑定</h1>
    <img src="imgUrl">
    <img v-bind:src="imgUrl"  width="100" height="100">
    <img :src="imgUrl"  width="100" height="100">  <!---简写-->

    <h1>绑定事件监听</h1>
    <button v-on:click="test">test1</button>
    <button @click="test2(msg)">test2</button>
</div>

<script>
    new Vue({
        el:"#app",
        data:{
            msg:"<a href='#'>I love bigV!</a>",
            imgUrl:"https://cn.vuejs.org/images/logo.png"
        },
        methods:{
            test() {
                alert("大V!!")
            },
            test2(la){
                alert(la)
            }
        }
    })
</script>
```

![1560839405362](C:\Users\家浩\AppData\Roaming\Typora\typora-user-images\1560839405362.png)



## 第三个DEMO(计算属性和监视)

```vue

```