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

<div id="demo">
    姓：<input type="text" placeholder="First Name" v-model="fristname"><br>
    名：<input type="text" placeholder="Last Name" v-model="lastname"><br>
    姓名1（单向）：{{fulname1}}<br>
    姓名2（单向）：<input type="text" placeholder="name" v-model="fulname2"><br>
    姓名3（双向）：<input type="text" placeholder="name"><br>
</div>

<script>
    const vm = new Vue({
        el:"#demo",
        data:{
            fristname:"A",
            lastname:"B",
           // fullname1:"A B"
            fulname2:"A B"
        },
        computed:{
            //什么时候执行：初始化的时候，相关的属性数据发生变化的时候
            fulname1(){  //计算属性中的一个方法，方法的返回值作为属性值
                return this.fristname + ' ' + this.lastname;
            }
        },
        watch:{  //配置监视
            fristname:function (value) {    //fristname发生变化
                this.fulname2 = value + ' '+ this.lastname    //this就是vm对象
            }
        }
    })
    vm.$watch('lastname',function (value) {
        //更新fulname2
        this.fulname2 = this.fristname+ ' '+value
    })
</script>
```



## 第四个DEMO（get 和 set）

```vue
<div id="demo">
    姓：<input type="text" placeholder="First Name" v-model="fristname"><br>
    名：<input type="text" placeholder="Last Name" v-model="lastname"><br>
    姓名1（单向）：{{fulname1}}<br>
    姓名2（单向）：<input type="text" placeholder="name" v-model="fulname2"><br>
    姓名3（双向）：<input type="text" placeholder="name" v-model="fname3"><br>
    <p>{{fulname1}}</p>
    <p>{{fulname1}}</p>
    <p>{{fulname1}}</p>

</div>

<script>
    const vm = new Vue({
        el:"#demo",
        data:{
            fristname:"A",
            lastname:"B",
           // fullname1:"A B"
            fulname2:"A B"
        },
        computed:{
            //什么时候执行：初始化的时候，相关的属性数据发生变化的时候
            fulname1(){  //计算属性中的一个方法，方法的返回值作为属性值
                console.log("fulname()");
                return this.fristname + ' ' + this.lastname;
            
            },
            fname3 :{
                //当需要读取当前属性值时，计算并返回当前属性的值，回调函数（你定义的，你没调用，最终执行了）
                get(){
                    return this.fristname + ' ' + this.lastname;
                },
                //回调函数，监视当前属性值变化，当属性值发生改变时回调，更新改变的属性数据
                set(vaule){   //vaule就是fname3的最新属性值
                    const name = vaule.split(" ");
                    this.fristname=name[0];
                    this.lastname=name[1];
                }


            }
        },
        watch:{  //配置监视
            fristname:function (value) {    //fristname发生变化
                this.fulname2 = value + ' '+ this.lastname    //this就是vm对象

            }
        }
    })
    vm.$watch('lastname',function (value) {
        //更新fulname2
        this.fulname2 = this.fristname+ ' '+value
    })
</script>
```



## 第五个DEMO（class和style绑定）

```vue
<style>
        .aclass{
            color: red;
        }
        .bclass{
            color: blue;
        }
        .cclass{
            font-size: 30px;
        }

    </style>
</head>
<body>
<div id="app">
    <h1>class绑定：  :class="XXX"</h1>
    <p :class="a">xxx是字符串</p>
    <p :class="{aclass:isA,bclass:isB}">xxx是对象</p>
    <p :class="[A,cclass]">xxx是数组</p>

    <h1>style绑定</h1>
    <p :style="{color:actcolor,fontSize:fsize+'px'}">45646465</p>
    <button  @click="updata()">更新</button>
</div>

<script src="../js/vue.js"></script>
<script>
    const vm = new Vue({
        el:"#app",
        data:{
            a: "aclass",
            isA:true,
            isB:false,
            A:"aclass",
            actcolor:'red',
            fsize:20
        },
        methods:{
            updata() {
                this.a = 'bclass';
                this.isA=false;
                this.isB=true;
                this.A = 'bclass';
                this.actcolor="blue";
                his.fsize=40;
            }
        }
    })
</script>
```



## 第六个DEMO（条件渲染）

```vue
<div id="app">
    <p v-if="ok">成功了</p>
    <p v-else> 失败了</p>

    <p v-show="ok">转正成功了</p>
    <p v-show="!ok">转正失败了</p>
    <button @click="ok=!ok">切换</button>
</div>
<script src="../js/vue.js"></script>
<script>
    const vm = new Vue({
        el:"#app",
        data:{
            ok:false
        }
    })
</script>
```

