---
title: vuex的简单使用和模块化
date:
updated:
type: "tags"
comments:
categories: Vue
description: vuex的简单使用和模块化
keywords: vuex的简单使用和模块化
cover: https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=22130535,2850036426&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---

vuex的简单使用
```js
// src 目录中 创建 store 文件夹  再创建 index.js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export const store = new Vuex.Store({
    state:{//设置属性 用来存储数据

    },
    getters:{//对应方法 用来获取属性的状态
    //对于getters的理解主要作用是对state属性进行计算，可以理解类似于Vue中computed。接下来让我通过一个例子如何使用这两个功能的。
        //【getters】是store的计算属性。

    },
    mutations:{//更改属性的状态

    },
    actions:{//应用 mutation

    }
})
//再 main.js 中使用 store
new Vue({
    el: '#app',
    router,
    store,
        render: h => h(app)
})

//添加更改方法
mutations:{//更改属性的状态
        setMessage(state, data){//定义的修改 属性的方法
            state.message = data
        }
},
//调用方法
this.$store.commit('setMessage',data.message)

//获取属性
this.$store.state.message

//dispatch action
////dispath调用action方法
export const store = new Vuex.Store({
    state:{//设置属性 用来存储数据
        message:{},
        localuser:{},
    },
    getters:{//对应方法 用来获取属性的状态
        getMessage:state => state.message
    },
    mutations:{//更改属性的状态
        setMessage(state, data){
            state.message = data
        },

        //更改用户状态信息
        setLocalUser(state,data){
            if(data){
                state.localUser = data
            }else{
                state.localUser = null
            }
        }
    },
    actions:{//应用 mutation   
        setUser({commit},data){
            commit('setLocalUser', data)
        }
    }
})
```

模块化vuex
```js
  //index.js
import Vue from 'vue'
import Vuex from 'vuex'

import moduleAchat from '/module/moduleA/ChatInfo.js'
import moduleAuser from '/module/moduleA/UserInfo.js'

Vue.use(Vuex)

export const store = new Vuex.Store({
    modules:{
        chat:moduleAchat,
        user:moduleAuser
    }
})
//store.state.chat   // 获取moduleAchat
//store.state.user   // 获取moduleAuser

//ChatInfo.js
const state = {
    //设置属性 用来存储数据
    message: {}
    name: {}
}
const getters = {

}
const mutations = {
    //更改用户状态信息
    setLocalUser(state, data) {
        if (data) {
            state.name = data
        } else {
            state.name = null
        }
    },
    //更改属性的状态
    setMessage(state, data) {
        state.message = data
    }
}
const actions = {

}

export default {
    state,
    getters,
    mutations,
    actions
}


//UserInfo.js

const state = {
    //设置属性 用来存储数据
    message: {},
    localuser: {},
    isLogin: false
}

const getters = {
    //对应方法 用来获取属性的状态
    getMessage: state => state.message
}

const mutations = {
    //更改属性的状态
    setMessage(state, data) {
        state.message = data
    }
}

const actions = {
    //应用 mutation
    setUser({
        commit
    }, data) {
        commit('setMessage', data)
    }
}

export default {
    state,
    getters,
    mutations,
    actions
}
```