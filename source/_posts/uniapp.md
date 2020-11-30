---
title: Uni-App
date:
updated:
type: "tags"
comments:
categories: Uni-App
description: Uni-App
keywords: Uni-App
top_img: https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=2182504131,1408054639&fm=11&gp=0.jpg
cover: https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=2182504131,1408054639&fm=11&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---
# 一.真机测试

```
小米  数据线连接  文档传输  开发者选项  usb调试  usb安装 安全设定
华为  文件传输   开发者选项 usb调试 
苹果  itunes 连接苹果  安装失败百度有解决方案  可以解压缩 设置 通用 设备管理（描述文件） 信任dcloud
微信开发者工具调试 设置小程序路径  开启小程序的服务代理端口  调试成功
```

# 二.引入官方样式库和自定义图标库,动画库

```
uni.css   在VUE导入 @import
例如  ulist
引入自定义 例如阿里巴巴图标库 
animate.css  样式分开使用  
```

# 三.底部导航

```
"tabBar": {
		"color":"",
		"selectedColor":"",
		"backgroundColor":"",
		"borderStyle":"",
		"list": []
	}
```

# 四.样式与class绑定

```
可以传一个数组
：class = [name,age]  通过判断实现加载不同的样式  等等
不是变量用单引号或双引号包括起来
```

# 五.uniapp事件处理器

```
// 事件映射表，左侧为 WEB 事件，右侧为 ``uni-app`` 对应事件
{
    click: 'tap',
    touchstart: 'touchstart',
    touchmove: 'touchmove',
    touchcancel: 'touchcancel',
    touchend: 'touchend',
    tap: 'tap',
    longtap: 'longtap', //推荐使用longpress代替
    input: 'input',
    change: 'change',
    submit: 'submit',
    blur: 'blur',
    focus: 'focus',
    reset: 'reset',
    confirm: 'confirm',
    columnchange: 'columnchange',
    linechange: 'linechange',
    error: 'error',
    scrolltoupper: 'scrolltoupper',
    scrolltolower: 'scrolltolower',
    scroll: 'scroll'
}

阻止事件冒泡  .stop
```

# 六.app-plus配置

```
"app-plus": {/* 配置编译到 App 平台时的特定样式，部分常用配置 H5 平台也支持 */
					"scrollIndicator":"none",/* 隐藏滚动条 */
					"titleNView": {
						"searchInput": {
							"align":"center",
							"backgroundColor":"#F7F7F7",
							"placeholder":"搜索糗事",
							"borderRadius":"4px",
							"placeholderColor":"#CCCCCC",
							"disabled": true
						},
						"buttons":[
							//左边
							{
								"color":"#FF9619",
								"colorPressed":"#BBBBBB",
								"float":"left",
								"fontSize":"22px",
								"fontSrc":"/static/fonts/iconfont.ttf",
								"text":"\ue609"
							},
							{
								"color":"#BBBBBB",
								"colorPressed":"#BBBBBB",
								"float":"right",
								"fontSize":"22px",
								"fontSrc":"/static/fonts/iconfont.ttf",
								"text":"\ue653"
							}
						]
					}
```

# 七.tab选项卡切换

```
用uni-app的样式，上面选项卡组件
<view class="uni-tab-bar">
			<scroll-view scroll-x="true"
			 class="uni-swiper-tab"
			 :scroll-left="scrollwidth"
			 scroll-with-animation="true">
				<block v-for="(tab,index) in tarBars" :key="tab.id">
					<view class="swiper-tab-list"
					 :class="{ 'active': tabIndex == index}"
					 @tap="tabtap(index)">
						{{ tab.name }}
						<view class="swiper-tab-line"></view>
					</view>
				</block>
			</scroll-view>
		</view>
		
轮播滚动滑动   上面的随着动  	
		
<view class="content">
		<index-swiper-tab 
		:tabIndex="tabIndex" 
		:tarBars="tarBars"
		@tabtap="tabtap"></index-swiper-tab>
		<view class="uni-tab-bar">
		<swiper class="swiper-box"
		 :style="{height: swiperheight+'px'}"
		 :current="tabIndex"
		 @change="tabChange">
			<swiper-item v-for="(items,index) in newslist" :key="index">
				<scroll-view scroll-y="true" class="list">
					<view>
						<index-list :items="items"></index-list>
					</view>
				</scroll-view>
			</swiper-item>
		</swiper>
		</view>
	</view>
	
	
	
内容组件
<view class="index-list" v-for="(item,index) in items.list" :key="index">
			<view class="index-list1">
				<view>
					<image :src="item.userpic"
					 mode="widthFix"
					 lazy-load></image>
					 {{ item.username }}
				</view>
				<view v-show="item.isguanzhu">
					<view class="iconfont icon icon-zengjia"></view>关注
				</view>
			</view>
			<view class="index-list2">{{ item.title }}</view>
			<view class="index-list3">
				<image :src="item.titlepic"
				 mode="widthFix"
				 lazy-load></image>
				 <!-- 视频 -->
				 <template v-if="item.type == 'video'">
				 	<view class="index-list-play icon iconfont icon-bofang"></view>
				 	<view class="index-list-playinfo">{{ item.playnum }} {{ item.long }}</view>
				 </template>
			</view>
			<view class="index-list4">
				<view>
					<view class="icon iconfont icon-icon_xiaolian-mian"
					:class="{'active':(item.infonum.index == 1)}"></view><view>
					{{item.infonum.dingnum}}</view>
					<view class="icon iconfont icon-kulian"
					:class="{'active':(item.infonum.index == 2)}"></view><view>
					{{item.infonum.cainum}}</view>
				</view>
				<view>
					<view class="icon iconfont icon-pinglun1"></view><view>
					{{item.commentnum}}</view>
					<view class="icon iconfont icon-zhuanfa"></view><view>
					{{item.sharenum}}</view>
				</view>
			</view>
		</view>
```

# 八.默认组件（没有数据的时候的组件）

```
<template v-if="items.list.length>0">
					<!-- 图文列表 -->
					<block v-for="(item,index1) in items.list" :key="index1">
						<index-list @changeevent="updateData" :item="item" :index="index1"></index-list>
					</block>
					<!-- 上拉加载 -->
					<load-more :loadtext="items.loadtext"></load-more>
				</template>
				<template v-else-if="!items.firstload">
					<view style="font-size: 50upx;font-weight: bold;color: #CCCCCC;
					padding-top: 100upx;" class="u-f-ajc">Loading ...</view>
				</template>
				<template v-else>
					<!-- 无内容默认 -->
					<no-thing></no-thing>
				</template>
				
				
 默认组件
 <view class="nothing u-f-ajc animated fadeIn">
		<image src="../../static/common/nothing.png" 
		mode="widthFix"></image>
	</view>
```

# 九.自定义导航

```
引入官方 uni nav bar  和 其他两个附带组件 icon status

<view>
		<!-- 自定义导航栏 -->
		<uni-nav-bar 
		:statusBar="true" 
		rightText="发布" 
		left-icon="arrowleft" 
		@clickLeft="back"
		@clickRight="submit"
		>
		<view class="xila" @tap="changelook">
			{{yinsi}}
			<view class="icon iconfont icon-xialazhankai"></view>
			</view>
		</uni-nav-bar>
	</view>
	//调用官方接口
	changelook(){
				//调用官方接口
				uni.showActionSheet({
					itemList: arr,
					success:(res)=>{
							this.yinsi = arr[res.tapIndex]
					}
				});
			}
```

# 十.引用官方组件

```
uni-app官方组件使用  拍照等
```

# 十一.微信自定义组件和兼容父子组件

```
1.app的父子传值可能不适用于微信小程序的父子之间的传值，不可以直接更改
关于v-show在微信小程序里面不起作用  关于他们的坑
2.
```

# 十二。模糊背景和下拉刷新，角标组件，点击外围关闭菜单

```
filter:blur(5upx)
刷新实现style 导航栏配置  赋值完了关闭  配置  
接口  uni.stop  关闭刷新
点击外围关闭菜单  给v-show  屏幕加一层蒙版  点击蒙版 关闭
```

# 十三.showActionSheet(OBJECT)]显示操作菜单

# 十四.三级联动选择城市

```
pick 组件
```

# 十五.微信登陆 扣扣登陆 微博登录

```

```

# 十六。配置文件封装

```
api请求前缀  
封装 cinfig.js 
url地址 


导出 config  export default{
    
}


在main.js中全局挂载
Vue.prototype.config = config


要在其他文件.js引入必须  重新引入 import
```

# 十七.监听网络状态

```
const NetWork = {
	// 网络状态
	isConnect:false,
	// 监听网络状态
	On(){
		// 获取当前网络状态
		uni.getNetworkType({
			success: (res) => {
				if(res.networkType!=='none'){ this.isConnect=true; return;}
				uni.showToast({
					icon:"none",
					title: '请先连接网络',
				});
			}
		})
		// 监听网络状态变化
		uni.onNetworkStatusChange((res)=>{
			this.isConnect = res.isConnected;
			if(!res.isConnected){
				uni.showToast({
					icon:"none",
					title: '您目前处于断网状态',
				});
			}
		})
	}
}

// app更新   热更新
const Update = function(){
	// #ifdef APP-PLUS  
	plus.runtime.getProperty(plus.runtime.appid, function(widgetInfo) {  
		uni.request({  
			url: 'http://www.example.com/update/',  
			data: {  
				version: widgetInfo.version,  
				name: widgetInfo.name  
			},  
			success: (result) => {  
				var data = result.data;  
				if (data.update && data.wgtUrl) {  
					uni.downloadFile({  
						url: data.wgtUrl,  
						success: (downloadResult) => {  
							if (downloadResult.statusCode === 200) {  
								plus.runtime.install(downloadResult.tempFilePath, {  
									force: false  
								}, function() {  
									console.log('install success...');  
									plus.runtime.restart();  
								}, function(e) {  
									console.error('install fail...');  
								});  
							}  
						}  
					});  
				}  
			}  
		});  
	});  
	// #endif  
}

import config from "./config.js"
export default {
	NetWork,
	Update
}
```

# 18.动画优化

```
1.窗口动画 接口 uniapp官方
在导航  pages.json  页面导航进行配置
html导航栏代码重写 
放在  #ifndef  APP-PLUS  代码里面

script  加入  包括组件也加入
在 #ifndef  APP-PLUS

如果是 app端才会显示  状态栏目
2.有卡顿  加淡入  

3.image  {well-change: transform}
```

# 19.小程序导航栏

```
1.uniapp开发的移动端  在小程序中导航栏没有出现 
在首页加判断  app.vue 加一个判断
#if
2.底部导航栏不出现
3.隐藏版本更新
4.隐藏滚动条 
APP.VUE
加入  ：：webkit-scroller{
    display:none;
}
5.小程序分享

微信小程序打包实现

配置  appid 
配置 安全域名
不能带端口号 socket  nginx
删除demo图片
压缩代码  上传时自动压缩
上传
提交审核
```

# 20.热更新和app打包

```
修改版本号  
1制作资源升级资源包
2.云打包
两种方法
wgt文件  



打包 
1.应用名称  描述 版本号
2.图标   png
3.启动图配置 
4.配置 SDK
5.APP模块权限 配置  
6.获取  证书   java环境
安卓  
ios
ios证书申请指南  600快 
```

# 21.支付宝小程序

```
1.调试报错   发行包调试  不用运行调试 
2.图标引用问题 支付宝小程序白名单
icon.css 条件判断 加入 src: url('') format('truetype)
3.scroll-view引用高度问题  
三个都有需要高度 
4.点击出不来 滑动德出来
需要滑动获取 列表
5.动态页面 话题搜索框 轮播图  轮播图也需要给出高度  
6.个人空间  
```

# 22.请求封装

```js
import configdata from './config'
import cache from './cache'

module.exports = {
    config: function (name) {
        var info = null;
        if (name) {
            var name2 = name.split("."); //字符分割
            if (name2.length > 1) {
                info = configdata[name2[0]][name2[1]] || null;
            } else {
                info = configdata[name] || null;
            }
            if (info == null) {
                let web_config = cache.get("web_config");
                if (web_config) {
                    if (name2.length > 1) {
                        info = web_config[name2[0]][name2[1]] || null;
                    } else {
                        info = web_config[name] || null;
                    }
                }
            }
        }
        return info;
    },
    post: function (url, data, header) {
        header = header || "application/x-www-form-urlencoded";
        url = this.config("APIHOST") + url;
        return new Promise((succ, error) => {
            uni.request({
                url: url,
                data: data,
                method: "POST",
                header: {
                    "content-type": header
                },
                success: function (result) {
                    succ.call(self, result.data)
                },
                fail: function (e) {
                    error.call(self, e)
                }
            })
        })
    },
    postT: function (url, data, header) {
        header = header || "application/x-www-form-urlencoded";
        url = this.config("APIHOST1") + url;
        let token = uni.getStorageSync("token");
        if (token) {
            return new Promise((succ, error) => {
                uni.request({
                    url: url,
                    data: data,
                    method: "POST",
                    header: {
                        "content-type": header,
                        "token": token
                    },
                    success: function (result) {
                        console.error(result);
                        succ.call(self, result.data)
                    },
                    fail: function (e) {
                        error.call(self, e)
                    }
                })
            })
        } else {
            return new Promise((succ, error) => {
                uni.request({
                    url: url,
                    data: data,
                    method: "POST",
                    header: {
                        "content-type": header,
                    },
                    success: function (result) {
                        succ.call(self, result.data)
                    },
                    fail: function (e) {
                        error.call(self, e)
                    }
                })
            })
        }
    },

    postJson: function (url, data, header) {
        header = header || "application/json";
        url = this.config("APIHOST1") + url;
        let token = uni.getStorageSync("token");
        if (token) {
            return new Promise((succ, error) => {
                uni.request({
                    url: url,
                    data: data,
                    method: "POST",
                    header: {
                        "content-type": header,
                        "token": token
                    },
                    success: function (result) {
                        console.error(result);
                        succ.call(self, result.data)
                    },
                    fail: function (e) {
                        error.call(self, e)
                    }
                })
            })
        } else {
            return new Promise((succ, error) => {
                uni.request({
                    url: url,
                    data: data,
                    method: "POST",
                    header: {
                        "content-type": header,
                    },
                    success: function (result) {
                        succ.call(self, result.data)
                    },
                    fail: function (e) {
                        error.call(self, e)
                    }
                })
            })
        }
    },
    getT: function (url, data, header) {
        header = header || "application/x-www-form-urlencoded";
        url = this.config("APIHOST1") + url;
        let token = uni.getStorageSync("token");
        if (token) {
            return new Promise((succ, error) => {
                uni.request({
                    url: url,
                    data: data,
                    method: "GET",
                    header: {
                        "content-type": header,
                        "token": token
                    },
                    success: function (result) {
                        succ.call(self, result.data)
                    },
                    fail: function (e) {
                        error.call(self, e)
                    }
                })
            })
        } else {
            return new Promise((succ, error) => {
                uni.request({
                    url: url,
                    data: data,
                    method: "GET",
                    header: {
                        "content-type": header
                    },
                    success: function (result) {
                        succ.call(self, result.data)
                    },
                    fail: function (e) {
                        error.call(self, e)
                    }
                })
            })
        }

    },
    posts: function (url, data, header) {
        header = header || "application/x-www-form-urlencoded";
        return new Promise((succ, error) => {
            uni.request({
                url: url,
                data: data,
                method: "POST",
                header: {
                    "content-type": header
                },
                success: function (result) {
                    succ.call(self, result.data)
                },
                fail: function (e) {
                    error.call(self, e)
                }
            })
        })
    },
    postF: function (url, data, header) {
        header = header || "application/json";
        url = this.config("APIHOST") + url;
        return new Promise((succ, error) => {
            uni.request({
                url: url,
                data: data,
                method: "POST",
                header: {
                    "content-type": header
                },
                success: function (result) {
                    succ.call(self, result.data)
                },
                fail: function (e) {
                    error.call(self, e)
                }
            })
        })
    },
    postFs: function (url, data, header) {
        header = header || "application/json";
        return new Promise((succ, error) => {
            uni.request({
                url: url,
                data: data,
                method: "POST",
                header: {
                    "content-type": header
                },
                success: function (result) {
                    succ.call(self, result.data)
                },
                fail: function (e) {
                    error.call(self, e)
                }
            })
        })
    },
    get: function (url, data, header) {
        header = header || "application/x-www-form-urlencoded";
        url = this.config("APIHOST") + url;
        return new Promise((succ, error) => {
            uni.request({
                url: url,
                data: data,
                method: "GET",
                header: {
                    "content-type": header
                },
                success: function (result) {
                    succ.call(self, result.data)
                },
                fail: function (e) {
                    error.call(self, e)
                }
            })
        })
    },
	getJd: function (url, data, header) {
	    header = header || "application/x-www-form-urlencoded";
	    return new Promise((succ, error) => {
	        uni.request({
	            url: url,
	            data: data,
	            method: "GET",
	            header: {
	                "content-type": header
	            },
	            success: function (result) {
	                succ.call(self, result.data)
	            },
	            fail: function (e) {
	                error.call(self, e)
	            }
	        })
	    })
	},
    get1: function (url, data, header) {
        header = header || "application/json";
        url = this.config("APIHOST") + url;
        return new Promise((succ, error) => {
            uni.request({
                url: url,
                data: data,
                method: "GET",
                success: function (result) {
                    succ.call(self, result.data)
                },
                fail: function (e) {
                    error.call(self, e)
                }
            })
        })
    }
}

```

配置封装

```js
// const ROOTPATH = "https://www.gomyorder.cn";
//测试环境
const ROOTPATH1 = "https://www.gomyorder.cn/tao";
//正式环境
const ROOTPATH = "https://www.gomyorder.cn";
// const ROOTPATH1 = "http://localhost:8888";
module.exports = {
    APIHOST: ROOTPATH,
    APIHOST1: ROOTPATH1,
    ROOTPATH: ROOTPATH
};

```

# 23.缓存封装

```js
/**
 * 缓存数据优化
 * var cache = require('utils/cache.js');
 * import cache from '../cache'
 * 使用方法 【
 *     一、设置缓存
 *         string    cache.put('k', 'string你好啊');
 *         json      cache.put('k', { "b": "3" }, 2);
 *         array     cache.put('k', [1, 2, 3]);
 *         boolean   cache.put('k', true);
 *     二、读取缓存
 *         默认值    cache.get('k')
 *         string    cache.get('k', '你好')
 *         json      cache.get('k', { "a": "1" })
 *     三、移除/清理  
 *         移除: cache.remove('k');
 *         清理：cache.clear(); 
 * 】
 * @type {String}
 */
var postfix = '_mallStore'; // 缓存前缀 
/**
 * 设置缓存 
 * @param  {[type]} k [键名]
 * @param  {[type]} v [键值]
 * @param  {[type]} t [时间、单位秒]
 */
function put(k, v, t) {
    uni.setStorageSync(k, v) 
    var seconds = parseInt(t);
    if (seconds > 0) {
        var timestamp = Date.parse(new Date());
        timestamp = timestamp / 1000 + seconds;
        uni.setStorageSync(k + postfix, timestamp + "")
    } else {
        uni.removeStorageSync(k + postfix)
    }
}


/**
 * 获取缓存 
 * @param  {[type]} k   [键名]
 * @param  {[type]} def [获取为空时默认]
 */
function get(k, def) {
    var deadtime = parseInt(uni.getStorageSync(k + postfix)) 
    if (deadtime) {
        if (parseInt(deadtime) < Date.parse(new Date()) / 1000) {
            if (def) {
                return def;
            } else {
                return false;
            }
        }
    }
    var res = uni.getStorageSync(k);
    if (res) {
        return res;
    } else {
        if (def == undefined  || def == "") {
            def = false; 
        }
        return def;
    }
}

function remove(k) {
    uni.removeStorageSync(k);
    uni.removeStorageSync(k + postfix);
}

/**
 * 清理所有缓存
 * @return {[type]} [description]
 */
function clear() {
    uni.clearStorageSync();
}


module.exports = {
    put: put,
    get: get,
    remove: remove,
    clear: clear,
}
```

# 24.轮播图渲染列表

```js
swiperpage(){
				var pageList = [];
				var arr = []
				this.swiper2List.forEach((item,index)=>{
					var length = pageList.length + 1
					//判断是否大于8
					if((index+1)/8 < length){
						arr.push(item)
						if((index+1) == this.swiper2List.length){
							var arr1 = JSON.parse(JSON.stringify(arr))
							pageList.push(arr1)
						}
					}else if((index+1)/8 == length){
						arr.push(item)
						var arr1 = JSON.parse(JSON.stringify(arr))
						pageList.push(arr1)
						arr = []
					}
				})
				console.log(pageList)
				return pageList
			},
```

