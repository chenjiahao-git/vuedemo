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



下文引自https://baijiahao.baidu.com/s?id=1617561807695947783&wfr=spider&for=pc

在近两年的web及项目开发中，vue技术的使用越来越普遍，其各种资料、介绍以及使用攻略内容资料非常多，那么vue到底什么？在项目开发中，vue起到什么作用？它与传统的html+css+js+lamp开发网站项目又有什么区别呢？

![img](https://ss1.baidu.com/6ONXsjip0QIZ8tyhnq/it/u=2360926390,1339812252&fm=173&app=49&f=JPEG?w=640&h=397&s=49813C7272F477846757E64D020090E6)vue到底是什么？

**什么是vue？**Vue.js是一套构建用户界面的渐进式框架，Vue 采用自下向上增量开发的设计，其核心库只关注视图层，易于上手，同时vue完全有能力驱动采用单文件组件和 Vue 生态系统支持的库开发的复杂单页应用。其实抛开官方的一些不知所云的说法，简单来说，在传统web开发中，我们搭建项目都以html结构为基础，然后通过jquery或者js来添加各种特效功能，需要去选中每一个元素进行命令，这些内容在简单的项目中或者不变的项目中还能应付得来，一旦项目改动或者项目工程较大，代码的修改将是复杂繁琐的，而这时候用了vue，这些问题都不复存在。在比如一些单网页制作成的应用程序，一般涉及到数据交互的内容都很多，而应用了vue之后将大大缩减工作量。

![img](https://ss0.baidu.com/6ONWsjip0QIZ8tyhnq/it/u=4197573279,1693023772&fm=173&app=49&f=JPEG?w=513&h=300&s=2A087C22C5B059804CF86CD70100C0A2)传统网站制作开发

**vue在web开发，网站制作中有哪些显著优势？**1.数据绑定：vue会根据对应的元素，进行设置元素数据，通过输入框，以及get获取数据等多种方式进行数据的实时绑定，进行网页及应用的数据渲染 。2.组件式开发：通过vue的模块封装，它可以将一个web开发中设计的各种模块进行拆分，变成单独的组件，然后通过数据绑定，调用对应模版组件，同时传入参数，即可完成对整个项目的开发。

![img](https://ss0.baidu.com/6ONWsjip0QIZ8tyhnq/it/u=2606932620,2495448344&fm=173&app=49&f=JPEG?w=400&h=400&s=06D0E8326A4246C8042A2FED0300E02E)传统前端人员工作neirong

**对于前端开发者来说为什么要学习vue？**由于近两年前端技术变革速度太快，vue不论针对web项目开发，网站制作，还是app，小程序开发，都越来越流行，其便捷性及易用程度都让你不得不考虑去学习。如果仅仅还是传统的各种cms开源代码建站仿站，显然你的技术已经跟不上了，如果你开发的项目数据交互较多，并且前后端分离明显，那么vue将会使你未来技术长足成长的不二选择。



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



### v-model基础用法

(详见[https://cn.vuejs.org/v2/guide/forms.html#%E5%9F%BA%E7%A1%80%E7%94%A8%E6%B3%95](https://cn.vuejs.org/v2/guide/forms.html#基础用法))

你可以用 `v-model` 指令在表单 `<input>`、`<textarea>` 及 `<select>` 元素上创建双向数据绑定。它会根据控件类型自动选取正确的方法来更新元素。尽管有些神奇，但 `v-model` 本质上不过是语法糖。它负责监听用户的输入事件以更新数据，并对一些极端场景进行一些特殊处理。

`v-model` 会忽略所有表单元素的 `value`、`checked`、`selected` 特性的初始值而总是将 Vue 实例的数据作为数据来源。你应该通过 JavaScript 在组件的 `data` 选项中声明初始值。

`v-model` 在内部为不同的输入元素使用不同的属性并抛出不同的事件：

- text 和 textarea 元素使用 `value` 属性和 `input` 事件；
- checkbox 和 radio 使用 `checked` 属性和 `change` 事件；
- select 字段将 `value` 作为 prop 并将 `change` 作为事件。

对于需要使用输入法 (如中文、日文、韩文等) 的语言，你会发现 `v-model` 不会在输入法组合文字过程中得到更新。如果你也想处理这个过程，请使用 `input` 事件。

在文本区域插值 (`<textarea>{{text}}</textarea>`) 并不会生效，应用 `v-model` 来代替。





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



## 第八个DEMO(查询和排序)

```vue
<div id="bigv">
    <input type="text" v-model="searchperson">
    <ul>
        <li v-for="(p,index) in filterperson" :click="index">
            {{index}}---{{p.name}}---{{p.age}}--{{p}}
        </li>
    </ul>
    <button @click="setordertype(1)">年龄升序</button>
    <button @click="setordertype(2)">年龄降序</button>
    <button @click="setordertype(0)">原本顺序</button>
</div>

<script src="../js/vue.js"></script>
<script>
    const vm = new Vue({
        el:"#bigv",
        data:{
            searchperson:'',
            orderType:0,   //0代表原序，1升序，2降序
            person:[
                {name:'林凯森',age:18 },
                {name:'森林凯',age:14 },
                {name:'凯林森',age:10 },
                {name:'森凯林',age:108 },
            ]
        },
        computed:{
            filterperson(){
                //取出相关的数据
                const{ searchperson ,person,orderType }=this
                //最终返回显示的数组
                let fperson;
                fperson = person.filter( p => p.name.indexOf(searchperson)!== -1 )
                if(orderType) {
                    fperson .sort(function (p1, p2) {

                        if (orderType === 2) {
                      
                            return p2.age - p1.age
                        } else {
                            return p1.age - p2.age
                        }
                    })
                }
                return fperson
            }
        },
        methods:{
            setordertype(orderType){
                this.orderType=orderType
            }
        }
    })
</script>

```



### 拓展 (ES6变量的结构赋值)

#### 1.数组的解构赋值

ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。

以前，为变量赋值，只能直接指定值。

```javascript
let a = 1;
let b = 2;
let c = 3;
```

ES6 允许写成下面这样。

```javascript
let [a, b, c] = [1, 2, 3];
```

上面代码表示，可以从数组中提取值，按照对应位置，对变量赋值。

本质上，这种写法属于“模式匹配”，只要等号两边的模式相同，左边的变量就会被赋予对应的值。下面是一些使用嵌套数组进行解构的例子。

```javascript
let [foo, [[bar], baz]] = [1, [[2], 3]];
foo // 1
bar // 2
baz // 3

let [ , , third] = ["foo", "bar", "baz"];
third // "baz"

let [x, , y] = [1, 2, 3];
x // 1
y // 3

let [head, ...tail] = [1, 2, 3, 4];
head // 1
tail // [2, 3, 4]

let [x, y, ...z] = ['a'];
x // "a"
y // undefined
z // []
```

如果解构不成功，变量的值就等于`undefined`。

```javascript
let [foo] = [];
let [bar, foo] = [1];
```

以上两种情况都属于解构不成功，`foo`的值都会等于`undefined`。

另一种情况是不完全解构，即等号左边的模式，只匹配一部分的等号右边的数组。这种情况下，解构依然可以成功。

```javascript
let [x, y] = [1, 2, 3];
x // 1
y // 2

let [a, [b], d] = [1, [2, 3], 4];
a // 1
b // 2
d // 4
```

上面两个例子，都属于不完全解构，但是可以成功。

如果等号的右边不是数组（或者严格地说，不是可遍历的结构，参见《Iterator》一章），那么将会报错。

```javascript
// 报错
let [foo] = 1;
let [foo] = false;
let [foo] = NaN;
let [foo] = undefined;
let [foo] = null;
let [foo] = {};
```

上面的语句都会报错，因为等号右边的值，要么转为对象以后不具备 Iterator 接口（前五个表达式），要么本身就不具备 Iterator 接口（最后一个表达式）。

解构赋值允许指定默认值。

```javascript
let [foo = true] = [];
foo // true

let [x, y = 'b'] = ['a']; // x='a', y='b'
let [x, y = 'b'] = ['a', undefined]; // x='a', y='b'
```

注意，ES6 内部使用严格相等运算符（`===`），判断一个位置是否有值。所以，只有当一个数组成员严格等于`undefined`，默认值才会生效。

```javascript
let [x = 1] = [undefined];
x // 1

let [x = 1] = [null];
x // null
```

上面代码中，如果一个数组成员是`null`，默认值就不会生效，因为`null`不严格等于`undefined`。

如果默认值是一个表达式，那么这个表达式是惰性求值的，即只有在用到的时候，才会求值。

```javascript
function f() {
  console.log('aaa');
}

let [x = f()] = [1];
```

上面代码中，因为`x`能取到值，所以函数`f`根本不会执行。上面的代码其实等价于下面的代码。

```javascript
let x;
if ([1][0] === undefined) {
  x = f();
} else {
  x = [1][0];
}
```

默认值可以引用解构赋值的其他变量，但该变量必须已经声明。

```javascript
let [x = 1, y = x] = [];     // x=1; y=1
let [x = 1, y = x] = [2];    // x=2; y=2
let [x = 1, y = x] = [1, 2]; // x=1; y=2
let [x = y, y = 1] = [];     // ReferenceError: y is not defined
```

上面最后一个表达式之所以会报错，是因为`x`用`y`做默认值时，`y`还没有声明。

####  2.对象的解构赋值

解构不仅可以用于数组，还可以用于对象。

```javascript
let { foo, bar } = { foo: 'aaa', bar: 'bbb' };
foo // "aaa"
bar // "bbb"
```

对象的解构与数组有一个重要的不同。数组的元素是按次序排列的，变量的取值由它的位置决定；而对象的属性没有次序，变量必须与属性同名，才能取到正确的值。

```javascript
let { bar, foo } = { foo: 'aaa', bar: 'bbb' };
foo // "aaa"
bar // "bbb"

let { baz } = { foo: 'aaa', bar: 'bbb' };
baz // undefined
```

上面代码的第一个例子，等号左边的两个变量的次序，与等号右边两个同名属性的次序不一致，但是对取值完全没有影响。第二个例子的变量没有对应的同名属性，导致取不到值，最后等于`undefined`。

如果解构失败，变量的值等于`undefined`。

```javascript
let {foo} = {bar: 'baz'};
foo // undefined
```

上面代码中，等号右边的对象没有`foo`属性，所以变量`foo`取不到值，所以等于`undefined`。

对象的解构赋值，可以很方便地将现有对象的方法，赋值到某个变量。

```javascript
// 例一
let { log, sin, cos } = Math;

// 例二
const { log } = console;
log('hello') // hello
```

上面代码的例一将`Math`对象的对数、正弦、余弦三个方法，赋值到对应的变量上，使用起来就会方便很多。例二将`console.log`赋值到`log`变量。

如果变量名与属性名不一致，必须写成下面这样。

```javascript
let { foo: baz } = { foo: 'aaa', bar: 'bbb' };
baz // "aaa"

let obj = { first: 'hello', last: 'world' };
let { first: f, last: l } = obj;
f // 'hello'
l // 'world'
```



## 第九个DEMO（事件的处理）

<div id="demo">
			<h2>1.绑定监听</h2>
			<button @click="test1">test1</button>
			<button @click="test2('bigbigv')">test2</button>
			<button @click="test3($event)">test3</button>
			<button @click="test4('bigv',$event)">test4</button>	
			<h2>2.事件修饰符</h2>
			<div style="width: 200px;height: 200px;background-color: #FF0000;" @click="test5">
				<div style="width: 100px;height: 100px; background-color: #0000FF;" @click.stop="test6"></div> 
				<!-- 阻止冒泡事件 -->
			</div>
			<br>
			<a href="http://www.baidu.com" @click.prevent="test7"> 百度一下，你还不知道</a>
			<!-- 阻止事件默认行为 -->
			<h2>3.按键修饰符</h2>
			<input type="text" @keyup.13="test8">
			<input type="text" @keyup.enter="test8">
		</div>
```vue
	<script src="../js/vue.js"></script>
	<script>
		const vm = new Vue({
			el: "#demo",
			data: {
				test1() {
					alert("bigv")
				},
				test2(msg) {
					alert(msg)
				},
				test3(event) {
					alert(event.target.textContent)
				},
				test4(v,event) {
					alert(v+" and "+event.target.textContent)
				},
				test5(){
					alert("out")
				},
				test6(){
					//event.stopPropagation() //传统的阻止冒泡事件
					alert("inner")
				},
				test7(){
					// event.preventDefault()  //传统的阻止事件默认行为
					alert("别百了回来吧！")
				},
				test8(event){
					alert(event.target.value)
				}
			}
		})
	</script>
```


## 第十个DEMO（引入模板）

<template id="foreignerName">
			<!-- <template/>标签内部被包裹着的内容必须有且只有一个根元素，在这里的根元素是ul -->
			<ul>
				<li v-for="item in nameArr">{{item}}</li>
			</ul>
		</template>
		<!-- 这个模板要写在Vue实例的外面，这里template的id属性的值是自定义的，
配合js部分用来标识模板内容；但是有一点值得注意，
那就是被template包裹着的内容有且只有一个根元素，
在这里是ul元素 -->

```vue
	<div id="bigv">
		<h3>{{name}}</h3>
		<my-comp></my-comp>
		<!-- 当自定义组件的template模板内容比较复杂的时候 -->
		<my-haha></my-haha>
	</div>
	
	<script src="../js/vue.js"></script>
	<script>
		const vm = new Vue({
			el: "#bigv",
			template: "#foreignerName", //对应于template中的id属性
			data: function() {
				return {
					nameArr: ["Alice", "Marry", "Athena"]
				}
			}

		})
	</script>
```


## 第十一个DEMO（ajax）

demo.html

```vue
<div id="app">
   <ul>
       <li v-for="(p ,index) in user" :key="index">
           {{index}}---{{p.username}}---{{p.age}}
         
       </li>
   </ul>
</div>
</body>
<script>
    var vm = new Vue({
        el: "#app",
        data: {
            user: ''
        },
		 created: function () {
　　　　　　//为了在内部函数能使用外部函数的this对象，要给它赋值了一个名叫self的变量。
            var self = this;
            $.ajax({
                url: '../data/user.json',
                type: 'get',
                data: {},
                dataType: 'json'
            }).then(function (res) {
                console.log(res);
　　　　　　　　　　//把从json获取的数据赋值给数组
                self.user = res;
            }).fail(function () {
                console.log('失败');
            })
        }
    });
</script>
```

user.json

```json
[
  {"username":"张三","age":22},
  {"username":"李四","age":21},
  {"username":"王五","age":20},
  {"username":"赵六","age":23}
]
```

