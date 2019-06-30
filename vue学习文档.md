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



###  computed与method的区别

在官方文档中，强调了computed区别于method最重要的两点

1. computed是**属性调用**，而methods是**函数调用**

2. computed带有**缓存功能**，而methods不是

3. computed定义的方法我们是以属性访问的形式调用的，`{{computedTest}}`

4. 但是methods定义的方法，我们必须要加上`()`来调用，如`{{methodTest()}}`，**否则，视图会出现test1的情况**，见下图

   ![img](https://segmentfault.com/img/bV8UtL?w=480&h=76)

   官方文档反复强调**对于任何复杂逻辑，你都应当使用计算属性**

   > **computed依赖于data中的数据，只有在它的相关依赖数据发生改变时才会重新求值**

   如上例，在Vue实例化的时候，computed定义fulname1方法会做一次计算，返回一个值，**在随后的代码编写中，只要fulname1方法依赖的数据不发生改变，fulname1方法是不会重新计算的**，也就是说后面三个`fulname1`是直接拿到了**返回值**，而非是重新计算的结果。

   这样的好处也是显而易见的，同样的，如果我们碰到一个场景，需要1000个`返回值`，那么毫无疑问，这相对于`methods`而言，将大大地节约内存
   哪怕你改变了fristname的值，`fulname1`也只会计算一次而已

   

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



## 第七个DEMO（列表渲染）

### 数组更新检查

Vue 将被侦听的数组的变异方法进行了包裹，所以它们也将会触发视图更新。这些被包裹过的方法包括：

- `push()`
- `pop()`
- `shift()`
- `unshift()`
- `splice()`
- `sort()`
- `reverse()`

先调用原生方法，再更新界面



```vue
<div id="app">
   <h1>v-for遍历数组</h1>
    <ul>
        <li v-for="(p ,index) in person" :key="index">
            {{index}}---{{p.name}}---{{p.age}}
            ---<button @click="del(index)">删除</button>
            ---<button @click="updata(index,{name:'凯森林',age:15})">更新</button>
        </li>
    </ul>

    <h1>v-for遍历对象</h1>
    <ul>
        <li v-for="(v ,k) in person[1]" :key="k">
            {{v}}--{{k}}
        </li>
    </ul>
</div>
<script src="../js/vue.js"></script>
<script>
    const vm = new Vue({
        el:"#app",
        data:{
           person:[ //vue只是监视了person的改变，没有监视数组内部数据的改变
               {name:'林凯森',age:18 },
               {name:'森林凯',age:14 },
               {name:'凯林森',age:10 },
               {name:'森凯林',age:108 },
           ]
        },
        methods:{
            del(index){
                //删除person中指定index的p
                console.log(this)
                console.log(this.person)
                this.person.splice(index,1)
            },
            updata(index,newperson){
                //this.person[index]=newperson   //没有改变person本身，数组内部发生了变化但并没有调用变异方法，vue不会更新界面
                this.person.splice(index,1,newperson)
            }
        }
    })
</script>
```

