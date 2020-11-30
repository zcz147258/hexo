---
title: Vue
date:
updated:
type: "tags"
comments:
categories: Vue
description: Vue
keywords: Vue
top_img: https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=2895639571,4121634512&fm=26&gp=0.jpg
cover: https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=2895639571,4121634512&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---
# 1.VUE介绍

## 1.1什么是Vue?

 Vue (读音 /vjuː/，类似于 view) 是一套用于构建用户界面的渐进式框架。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与现代化的工具链以及各种支持类库结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。

## 1.2什么是渐进式？

渐进式就是说框架本身有很大包容性，只做自己该做的事，你可以在已经建立好的网站代码上，把一两个组件改用它实现，当jQuery用；也可以整个网站都用它开发，当Angular用； 还可以用它的视图，搭配自己设计的整个下层用。

## 1.3用户界面，视图层是什么意思？

它是指，数据如何渲染到页面中。 说白了，就是如何将数据固定的静态页面变成数据从后台请求过来然后再渲染出来的动态页面。

Vue可以和ui框架进行组合使用。Vue负责渲染数据，ui框架负责搭建页面及效果。相得益彰，配合默契。Vue.js 的作者也说了，目标是通过尽可能简单的 API 实现响应的数据绑定和组合的视图组件。

## 1.4前端库library与框架framework的区别

***\*库\****：库是更多是一个封装好的特定的集合，提供给开发者使用，而且是特定于某一方面的集合（方法和函数），库没有控制权，控制权在使用者手中，在库中查询需要的功能在自己的应用中使用，我们可以从封装的角度理解库；提供某一个小功能，对项目的侵入性较小，如果某个库无法完成某些需求，可以很容易切换到其它库实现需求。

***\*框架\****：框架顾名思义就是一套架构，会基于自身的特点向用户提供一套相当于叫完整的解决方案，而且控制权的在框架本身，使用者要照框架所规定的某种规范进行开发，对项目的侵入性较大，项目如果需要更换框架，则需要重新架构整个项目。

## 1.5、模块化与组件化的区别

前者是从代码的角度来进行分析的，把一些可利用的代码抽离为单个模块，便于项目的维护和开发；

后者是从UI界面的角度来进行分析的，把一些可复用的UI元素抽离为单独的组件，便于项目的维护和开发。

## 1.6、Vue.js中怎么实现组件化的？

```
Template:结构

Script:行为

Style:样式

**1.2** ***\*框架特点\****

**n** ***\*特点\****

² mvvm

² 组件化

² 模块化

**n** ***\*应用场景：\**** 

² 单页面应用(single page Application); 

² webapp；

**n** ***\*Vue框架有哪些出名的上线产品\*******\*：\****

² 饿了吗

² 掘金

² 滴滴打车
```

## 1.7创建vue代码

```vue
let ap = new Vue({
            el: '#app',  //挂载的函数
            data: {   //渲染的数据
            },
            methods: {  //调用的方法
            }
        })
 其他
 除了数据属性、挂载元素等选项，Vue 实例还暴露了一些有用的实例属性与方法。它们都有前缀 $，以便与用户定义的属性区分开来。
 
 例如 this.$el
 	this.$data.   获取数据
 	
 	
 获取DOM
 获取dom节点可以用ref属性，这个属性就是来获取dom对象的。
```

# 2.VUE指令

```vue
一.数据绑定
1.1 v-text  v-text主要用来更新textContent，可以等同于JS的text属性。
	<span v-text="msg"></span>
	<span>{{msg}}</span>
1.2. v-html 双大括号的方式会将数据解释为纯文本，而非HTML。会渲染标签
	<div v-html="rawHtml"></div>
1.3 v-pre v-pre主要用来跳过这个元素和它的子元素编译过程。可以用来显示原始的Mustache标签。跳过大量没有指令的节点加快编译。
1.4 v-cloak 这个指令是用来保持在元素上直到关联实例结束时进行编译
在页面加载时会闪烁，先显示:  会跳过闪烁
1.5 v-model 这个指令用于在表单上创建双向数据绑定。
v-model会忽略所有表单元素的value、checked、selected特性的初始值。因为它选择Vue实例数据做为具体的值。


二. 条件指令
2.1 v-once  v-once关联的实例，只会渲染一次 之后的重新渲染，实例极其所有的子节点将被视为静态内容跳过，这可以用于优化更新性能。
2.2 v-if v-if可以实现条件渲染，Vue会根据表达式的值的真假条件来渲染元素。
	<a v-if="ok">yes</a>
	如果属性值ok为true，则显示。否则，不会渲染这个元素。
2.3 v-else v-else是搭配v-if使用的，它必须紧跟在v-if或者v-else-if后面，否则不起作用。
2.4 v-else-if v-else-if充当v-if的else-if块，可以链式的使用多次。可以更加方便的实现switch语句。
2.5 v-show 也是用于根据条件展示元素。和v-if不同的是，如果v-if的值是false，则这个元素被销毁，不在dom中。但是v-show的元素会始终被渲染并保存在dom中，它只是简单的切换css的dispaly属性。
2.6 v-for  用v-for指令根据遍历数组来进行渲染
<div v-for="(item,index) in items"></div>   //使用in，index是一个可选参数，表示当前项的索引
<div v-for="item of items"></div>   //使用of

三.属性指令
v-bind用来动态的绑定一个或者多个特性。没有参数时，可以绑定到一个包含键值对的对象。常用于动态绑定class和style。以及href等。
简写为一个冒号【 ：】

四.事件指令
v-on v-on主要用来监听dom事件，以便执行一些代码块。表达式可以是一个方法名。
可以简写为 @
```

# 3.修饰符

```vue
v-model修饰符、

<1> .lazy 默认情况下，v-model同步输入框的值和数据。可以通过这个修饰符，转变为在change事件再同步。
<2> .number 自动将用户的输入值转化为数值类型
<3> .trim 自动过滤用户输入的首尾空格


事件修饰符
.stop 阻止事件继续传播
.prevent 事件不再重载页面
.capture 使用事件捕获模式,即元素自身触发的事件先在此处处理，然后才交由内部元素进行处理
.self 只当在 event.target 是当前元素自身时触发处理函数
.once 事件将只会触发一次
.passive 告诉浏览器你不想阻止事件的默认行为

使用修饰符时，顺序很重要；相应的代码会以同样的顺序产生。因此，用v-on:click.prevent.self会阻止所有的点击，而 v-on:click.self.prevent 只会阻止对元素自身的点击。


```

# 4.vue计算属性

```
所以，对于任何复杂逻辑，你都应当使用计算属性。

所有的计算属性都写在 Vue 实例的 computed 属性中，这个计算属性就是一个函数，返回值为最后属性的值。
```

## 4.1计算属性的特点

```
总体就是一句话，在使用的时候，感觉像属性，在定义的时候，感觉像方法。计算属性的本质就是方法。和方法有什么区别呢？和方法相比，计算属性的性能更高，因为它有缓存。

1.计算属性在多次重复调用的时候，只会执行一次，而methods中的方法则会执行多次
2.如果属性有变化，但是不是计算属性，那么计算属性对应的方法不会执行，但是methods 中定义的方法会重新执行 ，依赖缓存
```

## 4.2用法

```vue
<span>年龄: </span><span>{{ age }}</span>
    <!--<span>年龄: </span><span>{{ age() }}</span>-->
new Vue({
        el: '#app',
        data: {
            birthday: ''
        },
        computed: {
            age() {
                let age = new Date().getFullYear() - new Date(this.birthday).getFullYear();
                return age;
            }
        }
    })
```

## 4.3watch

```
他们之间的区别
vm.$watch( expOrFn, callback, [options] )
计算属性是依赖的值改变会重新执行函数，计算属性是取返回值作为最新结果，所以里面不能异步的返回结果。不能写异步逻辑。
watch
侦听属性是侦听的值改变会重新执行函数，将一个值重新赋值作为最新结果，所以赋值的时候可以进行一些异步操作。
```



# 5.过滤器

```
在模板中，使用{{}} 输出内容的时候，可以进一步对输出的内容做格式化的处理，这个处理的方式，就是过滤器，本质上还是一个函数。其作用在于用户输入数据后，它能够进行处理，并返回一个数据结果。
```

## 5.1全局过滤的写法 

```
Vue.filter('adj',(num,n)=>{
            num = Number(num);
            let temp = num.toFixed(2);
            return temp;

    })
```

## 5.2局部过滤的写法

```vue
{{ num | adj(2) }} //可以进行多次过滤
filters: {
            adj(num,n) {
                num = Number(num);
                let temp = num.toFixed(2);
                return temp;
            }
        }
```

# 6.事件处理

## 6.1事件的三要素

```vue
事件源 时间类型  事件处理函数(监听器)
鼠标事件：click，dblclick，mouseover，mouseout，mouseenter，mouseleave，mousedown，mousemove，mouseup
键盘事件：
	keydown
	keypress：（keypress = keydown + keyup）输入。可以通过事件对象e.keyCode获取字符编码，但不能获取键值，比如：esc，但keydown和keyup可以。
	keyup  
	
ui事件：scroll，resize，load，unload
焦点事件：focus，blur
表单事件:
	change: 当表单组的内容发生改变且失焦时才触发
	submit：作用的对象只能是form
	input: input和keypress都是输入字符时触发该事件。区别：input不能获取字符编码，而keypress可以通过事件对象e.keyCode获取。

```

## 6.2事件对象

```
事件对象就是一个对象，记录了发生事情时候的一些信息，就像飞机的黑匣子
事件对象是人家已经定义好的，我们只需要以相应的方式来获取就可以了。在Vue中，事件对象也是预定义好的，并且它的名字是固定的 --- $event。
```

## 6.3时间修饰符

```vue
事件修饰符
.stop 阻止事件继续传播
.prevent 事件不再重载页面
.capture 使用事件捕获模式,即元素自身触发的事件先在此处处理，然后才交由内部元素进行处理
.self 只当在 event.target 是当前元素自身时触发处理函数
.once 事件将只会触发一次
.passive 告诉浏览器你不想阻止事件的默认行为
```

## 6.4按键修饰符

```vue
enter
tab
delete
esc
space
up
down
left
right

键值：
esc: 27
space: 32
backspace: 8
enter: 13
shift: 16
ctrl: 17
alt: 18
<-: 37
向上光标: 38
->: 39
向下光标:38
delete: 46

ASCII码值：
A: 65
a: 97
0: 48
```

## 6.5 v-model修饰符

```
v-model修饰符、
lazy默认情况下，v-model同步输入框的值和数据。可以通过这个修饰符，转变为在change事件再同步。
number 自动将用户的输入值转化为数值类型
trim    自动过滤用户输入的首尾空格
```

# 7.Vue—cli(脚手架)

Vue-cli是快速构建这个单页应用的脚手架，这个可是官方的。

vue-cli是脚手架工具，其作用就是用配置好的模板迅速搭建起一个项目工程来

```vue
1.使用npm全局安装webpack：使用 webpack -v 检查是否成功
npm install webpack -g
2.安装 VUE-cli  使用 vue -V 检查
npm install vue-cli -g  
3.使用Vue-cli快速构建应用
vue init webpack project（名称）
·················
Project name (project)： -----项目名称，直接回车，按照括号中默认名字（注意这里的名字不能有大写字母，如果有会报错Sorry, name can no longer contain capital letters）
Project description (A Vue.js project)： ----项目描述，也可直接点击回车，使用默认名字
Author ()： ----作者，输入你的大名
Runtime + Compiler: recommended for most users 运行加编译，既然已经说了推荐，就选它了
Runtime-only: about 6KB lighter min+gzip, but templates (or any Vue-specificHTML) are ONLY allowed in .vue files - render functions are required elsewhere 仅运行时，已经有推荐了就选择第一个了
Install vue-router? (Y/n) 是否安装vue-router，这是官方的路由，大多数情况下都使用，这里就输入“y”后回车即可。
Use ESLint to lint your code? (Y/n) 是否使用ESLint管理代码，ESLint是个代码风格管理工具，是用来统一代码风格的，一般项目中都会使用。
接下来也是选择题Pick an ESLint preset (Use arrow keys) 选择一个ESLint预设，编写vue项目时的代码风格，直接y回车
Setup unit tests with Karma + Mocha? (Y/n) 是否安装单元测试，选择安装y回车
Setup e2e tests with Nightwatch(Y/n)? 是否安装e2e测试 ，选择安装y回车

4.配置完成 npm install 安装依赖
5.目录
build 构建项目的配置目录
config 配置目录，默认配置没有问题
node_modules 项目开发依赖的一些模块
src 开发目录，基本上绝大部分工作是在这里展开的。
static 资源目录，我们可以把一些字体啊，图片啊，放在这里
index.html 首页入口文件
package.json 项目配置文件
README.md 说明文件

6.启动项目
npm run dev

7.浏览器访问

8.打包上线
```

# 8.组件

## 8.1.定义组件

```vue


 let HomeHeader = {
        //局部组件
      template: '<p><span>{{message}}</span><span>武极天下武极武极天下武极</span>天下武极天下武极天下武极天下武极天下</p>',
        data() {
            return {
                message: '前端教育'
            }
        }
    };

```

## 8.2.注册组件

```vue
1.全局注册
Vue.component('home-header',HomeHeader)
2.局部注册
  components: {
      HomeHeader
  }
  
  
 命名的规则
1.定义组件时，在定义和注册相分离的时候，组件通常是有个名称的，此时使用的是大驼峰命名法则。注意： 如果定义组件和注册组件是一步完成，此时就没有名称
2.注册组件时的名称在components选项中，注册组件时对应的键名，可以有如下三种命名方式：中划线式 小驼峰 大驼峰 ，其中，如果是中划线式，就必须要加引号。
3.使用组件时 ，在使用组件的时候，不管注册的时候使用哪一种，在使用组件的时候，只能使用中划线方式。如果没有中划线，就直接使用小写的单词即可。 
在vue.js中，并没有说哪个最好，都允许。我们需要选择其中的一种，保持一致即可。
```

## 8.3.使用组件

```
<div id="app">
        <home-header />
   </div>
```

## 8.4 data

```vue
在组件中定义data时，data必须是使用function的方式来定义的。
let HomeHeader = {
        //局部组件
      template: '<p><span>{{message}}</span><span>武极天下武极武极天下武极</span>天下武极天下武极天下武极天下武极天下</p>',
        data() {
            return {
                message: '前端教育'
            }
        }
    };
 写到组件里面
```

## 8.5使用多个组件

```
使用多个组件会产生不方便,那么需要模板  template 给一个id
然后 定义组件的时候 不用写入所有的标签 ，只需要写入 id即可

尽量用双标签,不然会出现之后的标签无法显示的问题
```

## 8.6组件数据的传递

### 8.6.1 父组件向子组件传递以及验证

```vue
<comment :aaa="aaa"></comment>
//父组件向子组件传值
        props: ['aaa'],
        <li v-for="item of aaa">
 
 
 props:传值的几种方式
 props验证方法一 (可以验证的数据的类型有：String、Number、Boolean、Array、Object、Date、Function、Symbol）
    /*props:{
      comments: Array,
      age: [String, Number]
    },*/

props验证方法二
    props:{
      comments: {
        required: true,// true表示必须通过父组件传值过来
        type: Array,
        default: [1,2,3]// 如果传过来的值是undefined，这里将用提供的默认值去视图层完成渲染
      }
    },
```

### 8.6.2 *子组件向父组件传递

```vue
第一步 在父组件自定义一个事件
<submit  @myevent="passdata"></submit>
第二步骤  子组件里面调用 click 相应按钮的函数 

data() {
            return {
                text: ''
            }
        },
        methods: {
            send() {
                this.$emit('myevent',this.text);//myevent就是自定义事件
            }
        }
        
        
第三步骤 父组件调用自定义事件的方法 获取数据，然后添加到父组件上的相应数据中
	passdata(data) {
                let obj = {};
                obj.imgUrl = 'block.jpg';
                obj.author = 'zzz';
                obj.content = data;
                this.aaa.push(obj);
            }
```

### 8.6.3兄弟元素之间传值

<script src="https://cdn.jsdelivr.net/npm/vue-bus/dist/vue-bus.js"></script>
引入vue-bus文件  基于 vue

```vue
 1.发送数据
send() {
                // this.$emit('myevent',this.text);
                this.$bus.$emit('ppp',this.text);
   }
  2.利用钩子函数接受数据
  created() {
            this.$bus.$on('ppp', (data) => {
                let obj = {};
                obj.imgUrl = 'block.jpg';
                obj.author = 'zzz';
                obj.content = data;
                this.aaa.push(obj);
            })
        },
```

# 9.created和mounted钩子函数

```
一般creadted钩子函数主要是用来初始化数据。 即模板还未渲染成html

：mounted钩子函数一般是用来向后端发起请求拿到数据以后做一些业务处理。
```

# 10.slot

```
Vue的slot，是组件的一块HTML模版，这块模版由使用组件者即父组件提供。可以说是子组件暴露的一个让父组件传入自定义内容的接口。
作用：让用户可以拓展组件，去更好地复用组件和对其做定制化处理。

即父组件放在子组件里的内容，插到了子组件的<slot></slot>位置；此时即使有多个标签，也会一起被插入。
```

## 10.1slot的使用

```vue
slot的用法可以分为三类，分别是默认插槽、具名插槽和作用域插槽

插槽用<slot>标签来确定渲染的位置，里面放如果父组件没传内容时的后备内容
具名插槽用name属性来表示插槽的名字，不传为默认插槽
作用域插槽在作用域上绑定属性来将子组件的信息传给父组件使用，这些属性会被挂在父组件slot-scope接受的对象上。

多个slot的使用
为了将放在子组件里的不同html标签放在不同的位置，可在父组件中要分发的标签里添加 slot=”name名” 属性，子组件在对应分发的位置的slot标签里，添加name=”name名” 属性，然后就会将对应的标签放在对应的位置了。

分发内容的作用域名
被分发的内容的作用域，由其所在模板决定。例如在之前的例子中，被分发的内容在父组件的模板中（虽然其被子组件的children标签所包括，但由于他不在子组件的template属性中，因此不属于子组件）则受父组件所控制。


<span slot="first" @click="al">第一个</span>
<span slot="second">第二个</span>
<slot name="first"></slot>
<slot name="second"></slot>
```

# 11.refs

```
在vue.js中，是需要尽量的避免DOM操作。但是，在一些场景中，需要获取组件中的某个元素，或者是获取某个组件，那么就用到了属性$refs
在元素上添加一个ref属性，指定一个值；然后就可以在组件中 通过 this.$refs.值 来获取这个元素。
```

# 12.生命周期钩子

```vue
Vue 实例有一个完整的生命周期，也就是从开始创建、初始化数据、编译模板、挂载Dom→渲染、更新→渲染、卸载等一系列过程，我们称这是 Vue 的生命周期。通俗说就是Vue 实例从创建到销毁的过程，就是生命周期。就像人从生到死的过程。
在Vue的整个生命周期中，它提供了一些生命周期钩子，给了我们执行自定义逻辑的机会。所谓的生命周期钩子，就是一些函数，为我们提供了一个编写函数的机会，可以在这个函数中编写代码，来完成某些功能。
beforeCreate	组件实例刚刚被创建，组件属性计算之前，如data属性
***created				组件实例创建完成，属性已绑定，但DOM还未生成，$el属性还不存在
beforeMount			模板编译/挂载之前
***mounted				模板编译/挂载之后
beforeUpdate			组件更新之前
***update				组件更新之后
beforeDestroy			组件销毁前调用
***destroyed				组件销毁后调用
 
 当 使用 keep live 增加一个缓存阶段
***activated				组件被激活时调用
***deactivated				组件被移除时调用 
```

# 13.mvvm思想

```vue
mvvm是一种思想，是我们编程的一种思想，源于后台语言的mvc
•m：model，模型，就是数据java bean setXxx getXxx
•v：view，视图，就是html结构，就是界面
•c：controller，控制器，将m和v结合到一起的粘合剂 java servlet
•Java python php .net node.js
•vm：view model，视图模型，和c是一样，将m和v结合到一起的粘合剂。

v-model
•通过数据绑定，将数据输出到视图上 --- 通过data 绑定
•可以在视图上，进行操作，然后修改模型中的数据 --- 通过 DOM 监听
```

# 14.动态组建

```vue
动态组件的实现很简单，就是使用保留的  <component>元素，动态地绑定到它的 is 特性：根据 v-bind:is="组件名" 中的组件名去自动匹配组件，如果匹配不到则不显示。
<component :is='组件名'></component>

<ul>
        <li @click="change('1')">门票</li>
        <li @click="change('2')">一日游</li>
    </ul>
    <!--<component is="Ticket"></component>&lt;!&ndash;静态&ndash;&gt;-->
    <component :is="ppp"></component><!--动态-->
```

# 15.css过渡以及封装

## 15.1过渡

```vue
Vue 提供了 transition 的封装组件，在下列情形中，可以给任何元素和组件添加 entering/leaving 过渡

过渡的应用
条件渲染 （使用 v-if）
条件展示 （使用 v-show）
动态组件
组件根节点


.tgcom-enter,.tgcom-leave-to {
      opacity: 0;
      background: #0e90d2;
      /*font-size: 30px;
      transform: translateX(-100px);*/
      /*transform: scale(.5);*/
      /*transform: rotate(30deg);*/
    }
    .tgcom-enter-to,.tgcom-leave-active{
      transition: all 500ms ease-in-out;/*linear:匀速,ease-in:由慢到快,ease-out:由快到慢,ease-in-out,ease-out-in*/
    }
//////////////////
 .ticket,.travel{
            background: red;
        }
        .fade-enter{
            opacity: 1;
            background: blue;
        }
        .fade-enter-active{
            transition: all 2s;
        }
        .fade-leave-active{
            background: red;
            opacity: 0;
        }
        .fade-leave-to{
            transition: all 2s;
        }
        
 <transition name="fade">
        <component :is="ppp"></component><!--动态-->
    </transition>
    
    
    当引入animate.css时候 
    放在transition里面
    enter-active-class="animated zoomIn" leave-active-class="animated zoomOut"
```

## 15.2动画

```vue
用法同CSS过渡。区别是动画中 v-enter 类名在节点插入 DOM 后不会立即删除，而是在 animationend 事件触发时删除。
<transition name="bonce">
		<div class="box" v-show="show"></div>
</transition>

@keyframes bonce-in{
		0%{transform: scale(0);}
		50%{transform: scale(1.5);}
		100%{transform: scale(1);}
		
	}
	@keyframes bonce-out{
		0%{transform: scale(1);}
		50%{transform: scale(1.5);}
		100%{transform: scale(0);}
	}
	
/*使用这两个动画*/
.bonce-enter-active{
	animation:bonce-in 1s ;
  }
.bonce-leave-active{
     animation: bonce-out 1s;
  }
```

# 16.VUE-router

## 16.1实现一个简单的路由

过程：

1.配置路由

2.实例化路由对象

3.注入路由

4.设置路由出口

5.访问路由设置

```vue
 引入文件
 <script src="https://cdn.bootcss.com/vue/2.6.10/vue.js"></script>
<script src="https://cdn.bootcss.com/vue-router/3.1.3/vue-router.min.js"></script>
 
 //1.配置路由
    const routers = [
        {
            path: '/cat',
            component: Cat,
        },
        {
            path: '/boom',
            component: Boom,
        }
    ]
    
    //2.实例化路由对象
    const router = new VueRouter({
        routes: routers
    })

    //3.注入路由
    new Vue({
        el: '#app',
        components: {
            Home,
        },
        router,
    })
    4.设置路由出口
    <ul>
            <li><router-link to="/cat">天猫</router-link></li>
            <li><router-link to="/boom">爆款</router-link></li>
        </ul>
        <router-view></router-view>
   5.访问路由设置
   设置的时候
   <li><router-link to="/cat">天猫</router-link></li>
   <li><router-link to="/boom">爆款</router-link></li>
```

## 16.2动态路由

```vue
我们经常需要把某种模式匹配到的所有路由，全都映射到同个组件。例如，我们有一个 User 组件，对于所有 ID 各不相同的用户，都要使用这个组件来渲染。那么，我们可以在vue-router 的路由路径中使用“动态路径参数”来达到这个效果。

在vue-router中，要实现动态路由，从两个方面出发：
在网址中传入参数，传参的固定格式为： /路径/参数
如何在代码中接受这个参数。


配置的路由用 
path: '/user/:id',
接收的时候使用
this.$route.params.id  就可以接受到

mounted(){
            console.log(this)
            console.log(this.$route.params.id)
            if(this.$route.params.id == 'cat'){
                this.rs = '这是一个cat页面'
            }else{
                this.rs = '这是一个boom页面'
            }

        }

<li><router-link to="/home/cat">天猫</router-link></li>
<li><router-link to="/home/boom">爆款</router-link></li>


{
            path: '/home/:id',
            component: Home,
        },
        //路由传值
        this.$router.push({
    path: "/login?uname=" + this.userName
});
```

