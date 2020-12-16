---
title: React父子方法调用
date:
updated:
type: "tags"
comments:
categories: React
description: React父子方法调用
keywords: React父子方法调用
cover: https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=2431606259,2554064138&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---

```js
//React父组件调用子组件方法
var HelloMessage = React.createClass({
    childMethod: function(){
        alert("组件之间通信成功");
    },
    render: function() {
        return <div> <h1>Hello {this.props.name}</h1>  <button onClick={this.childMethod}>子组件</button></div>
    }
});

// 父组件
var ImDaddyComponent = React.createClass({
    getDS: function(){
        // 调用组件进行通信
        this.refs.getSwordButton.childMethod();
    },
    render: function(){
        return (
                <div>
                    <HelloMessage name="John" ref="getSwordButton" />
                    <button onClick={this.getDS}>父组件</button>
                </div>
        );
    }
});

ReactDOM.render(
        <ImDaddyComponent  />,
        document.getElementById('correspond')
);

//React子组件调用父组件方法
this.props.MakeMoney();
```