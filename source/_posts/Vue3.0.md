---
title: Vue3
date:
updated:
type: "tags"
comments:
categories: Vue
description: Vue3
keywords: Vue3
top_img: https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=22130535,2850036426&fm=26&gp=0.jpg
cover: https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=22130535,2850036426&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---
# 1.Vue3.0亮点

```
六大亮点
	1.performance: 性能比Vue2.x快 1.2-2倍
	2.Tree shaking support: 按需编译 体积更小
	3.Composition APi:组合Api 类似React Hooks
	4.Better TypeScript support: 更加好的Ts支持
	5.Custom Render Api：暴露了自定义渲染APi
	6.Fragment,Teleport,Supense:更加先进的组件
	
```

# 2.Vue3.0是如何变得更快

```
-diff方法优化
	Vue2是进行全量对比
	Vue3新增了静态标记(PatchFlag)
-hositStatic 静态提升
	Vue2中无论元素食肉参与更新,每次都会重新创建,然后在渲染
	Vue3对于不参与更新的元素,会做静态提升,只会被创建一次,在渲染的时候直接复用即可.
-cachehandlers 事件侦听缓存
	默认情况下onClick会被视为动态绑定,所以每次都会去追踪他的变化
	但是因为是同一个函数,所以没有追踪变化,直接缓存起来复用即可
-ssr 渲染
	当有大量静态的内容的时候，这些内容会被当作纯字符串推进一个buffer面
	即使存在动态绑定，会通过模板插值嵌入进去,这样会比通过虚拟dom来渲染快上很多
	当静态内容大到一定量级的时候,会用_createStateVNode方法在客户端生成一个static node.
	这些静态 node。会被直接innerHtml,就不需要创建对象,然后根据对象渲染。 		
```

# 3.vue3.0项目搭建

```js
//安装vite
cnpm install -g create-vite-app
//使用vite创建项目
create-vite-app peojectName
//cd npm run dev

Vue3是兼容vue2的
```

# 4.组合Api

```
为了解决 vue2.0数据和业务逻辑分离的问题 推出了组合Api
```

## 4.1简单组合函数使用

```js
import {
    ref
} from "vue";
export default {
    name: "App",
    //组合api的入口函数
    setup(props) {
        //定义了一个名称count变量 变量发生改变会自动更新
        let count = ref(0);
        //在组合中定义的方法或者变量 想要在外界使用 必须使用return 暴露出去
        function fn() {
            count.value++
        }
        return {
            count,
            fn
        }
    },
};
```

## 4.2 抽取数据

```js
<div>
    <ul>
        <li v-for="(stu, index) in state.stus" :key="stu.id" @click="rmstu(index)">
            {{ stu.name }}-{{ stu.age }}
        </li>
    </ul>
</div>
</template>

<script>
import {
    reactive
} from "vue";
export default {
    name: "App",
    setup(props) {
        let {
            state,
            rmstu
        } = usestus()

        return {
            state,
            rmstu
        }
    },
};

function usestus() {
    let state = reactive({
        stus: [{
            id: 1,
            name: 'zs',
            age: 10
        }, {
            id: 2,
            name: 'gff',
            age: 20
        }, {
            id: 3,
            name: 'ds',
            age: 30
        }, ]
    })

    function rmstu(index) {
        console.log(index)
        state.stus = state.stus.filter((stu, idx) =>
            idx !== index
        )
        console.log(state.stus)
    }

    return {
        state,
        rmstu
    }
}
```

## 4.3分离高级

```js
<div>
    <form>
        <input type="text" v-model="state2.stu.id">
        <input type="text" v-model="state2.stu.name">
        <input type="text" v-model="state2.stu.age">
        <input type="submit" @click="onsubmit">
    </form>
    <ul>
        <li v-for="(stu, index) in state.stus" :key="stu.id" @click="rmstu(index)">
            {{ stu.name }}-{{ stu.age }}
        </li>
    </ul>
</div>
</template>

<script>
import {
    reactive
} from "vue";
export default {
    name: "App",
    setup(props) {
        let {
            state,
            rmstu
        } = usestus()
        let { state2,onsubmit } = addstatus(state)
        return {
            state,
            rmstu,
            state2,
            onsubmit
        }
    },
};

function addstatus(state){
    let state2 = reactive({
            stu: {
                id: '',
                name: '',
                age: ''
            }
        })
    function onsubmit(e){
        e.preventDefault()
        const stu = Object.assign({},state2.stu)
        state.stus.push(stu)
        state2.stu.id = ''
        state2.stu.name = ''
        state2.stu.age = ''
    }
    return { state2,onsubmit }
}
function usestus() {
    let state = reactive({
        stus: [{
            id: 1,
            name: 'zs',
            age: 10
        }, {
            id: 2,
            name: 'gff',
            age: 20
        }, {
            id: 3,
            name: 'ds',
            age: 30
        }, ]
    })

    function rmstu(index) {
        console.log(index)
        state.stus = state.stus.filter((stu, idx) =>
            idx !== index
        )
        console.log(state.stus)
    }

    return {
        state,
        rmstu
    }
}
```

## 4.4执行时间注意点

```
1.setup执行时机  
	在beforeCreated  //组件刚被创建出来 data还没初始化好
		-setup中不能使用 data或者 methods
		-setup中的this被改成了underfined
		-setup只能是同步的不能是异步的
	和creatd之间	//组件创建出来,数据初始化完毕
```

## 4.5 reactive

```
Vue2中是 defineproPerty来实现的
Vue3中是 Es6的Proxy来实现的

reactive注意点
	-reactive 方法参数必须是一个(json/arr) 必须是一个对象
	-如果给reactive传递了其他对象 
		默认情况下修改对象 界面不会更新
		如果想更新,可以通过重新赋值的方法
```

## 4.6 ref

```
ref的本质还是底层使用 rective 转变成对象
	ref(18)  = reactive( { value:18 } )
```

# 5.监听

## 1.递归监听

```
通过ref或者reactive创建的都是递归监听
递归监听存在的问题  如果数据量较大 非常消耗性能
```

## 2.非递归监听

```
引入 import { shallowReactive,shallowRef } from 'vue'
//只会监听第一层   不更新第一层 试图不会改变
```

## 3.toRow

```
let obj = { name:'dsad',age:123 }
let state = reactive(obj)
let obj2 = toRaw(state)  //obj === obj
拿到原始数据  不去更新界面
如果想通过  toRaw 拿到ref的原始数据  那么就必须明确地
let obj2 = toRaw(state.value)
```

## 4.markRaw

```
永远不要被追踪
let raw = markRaw(obj)
```

## 5.toRef

```
如果利用  toRef 某一个对象的属性变成响应式的数据 
修改响应式的数据  会影响原始的数据
但是界面并不会发生改变
//ref是复制 数据发生改变救会自动更新
//toRef 引用	不会更新
```

## 6.toRefs

```
let state = toRefs(obj)  //批量修改
```

## 7.cunstomRef

```
自定义ref
 function myref(){
     return ((track,trigger)=>{
         return {
             get(){
                 track()//这个数据是需要追踪变化的
                 return value
             },
             set(newvalue){
                 return newvalue
                 trigger(); //需要触发界面更新
             }
         }
     })
 }
 
 可以在自定义ref里面发送请求  不能放在  get里面
```

## 8.ref获取元素

```
<div ref="box"> </div>

setup(){
    let box = ref(null)
    onMounted(){
        console.log(box.value)
    }
    return {box}
}
```

## 9.readonly

```
只读
import { readonly } from 'vue'
setup(){
    let state = readonly({name:'lnj'}) 
}
```

