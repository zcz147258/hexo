---
title: axios的请求封装
date:
updated:
type: "tags"
comments:
categories: React
description: axios的请求封装
keywords: axios的请求封装
cover: https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=2431606259,2554064138&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---

```js
/*
 * @Descripttion:
 * @Author: sueRimn
 * @Date: 2020-07-07 09:31:13
 */

import axios from "axios";
import QS from "qs";
import { message } from "antd";
import store from "../store";
axios.defaults.timeout = 50000; //设置接口响应时间
// axios.defaults.withCredentials = true;
axios.defaults.baseURL = "http://47.101.212.62:4000";

axios.interceptors.request.use(
  //config包含每次请求的信息
  (config) => {
    //拿请求路径
    //console.log('请求路径', config.url)
    //去缓存中拿token
    if (config.url == "/login") {
    } else {
      let token = store.getState().token; //从缓存中取token
      if(config.isUpload){
        config.headers = {
          'Content-Type': 'multipart/form-data',
          'Authorization': token
        }
      }else{
        config.headers.Authorization = token; //将token放到请求头发送给服务器
      }
    }
    //有token
    // if (token) {
    // config.headers.Authorization = token; //将token放到请求头发送给服务器
    // } else {
    //     //localStorage.clear();  //清空缓存
    //     //排除login请求接口
    //     if (router.currentRoute.name && router.currentRoute.name.toLowerCase() == "login") {

    //     } else {
    //         //否则 全部返回null
    //     }
    // }
    // console.log('请求的操作'+ JSON.stringify(config))
    return config;
  },
  (err) => {
    return Promise.reject(err);
  }
);
// http response 拦截器
axios.interceptors.response.use(
  (response) => {
    if (response.status === 200) {
    } else {
      message.error("响应不正常");
    }
    return response; //请求成功的时候返回的data
  },
  (error) => {
    try {
      console.log(error);
      if (error.response.status === 401) {
        message.error(error.response.data.msg);
        window.location.href = "/login";
        return;
      } else {
        return;
      }
    } catch (e) {
      console.log(e);
    }
  }
);
// 封装axios的get请求
export function getData(url, params) {
  return new Promise((resolve, reject) => {
    axios
      .get(url, { params: params })
      .then((response) => {
        resolve(response.data);
      })
      .catch((error) => {
        reject(error);
      });
  });
}
// 封装axios的post请求
export function postData(url, params, end) {
  return new Promise((resolve, reject) => {
    axios
      .post(url, QS.stringify(params))
      .then((response) => {
        if (response.status === 200) {
          resolve(response.data);
        }
      })
      .catch((error) => {
        reject(error);
      });
  });
}

export function UploadFile(url, data) {
  return new Promise((resolve, reject) => {
    // processData: false, // 告诉axios不要去处理发送的数据(重要参数)
    // contentType: false, // 告诉axios不要去设置Content-Type请求头
    console.log(data)
    axios.post(url, data ,{isUpload : true})
      .then((response) => {
        resolve(response);
      })
      .catch((error) => {
        reject(error);
      });
  });
}
export function Postdownload(url, params, responsetype) {
  return new Promise((resolve, reject) => {
    //{responseType:'blob'}
    axios
      .post(url, QS.stringify(params))
      .then((response) => {
        resolve(response);
      })
      .catch((error) => {
        reject(error);
      });
  });
}
```