---
title: antd表单验证
date:
updated:
type: "tags"
comments:
categories: React
description: antd表单验证
keywords: antd表单验证
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
 * @Author: mikasa
 * @Date: 2020-07-28 16:18:27
 */
import ReactCanvasNest from 'react-canvas-nest';
import React, { useState, Component } from "react";
import "./regist.less";
import { Form, Input, Select, Button, message } from "antd";
import { SendEmail,AddUser } from '../../api'
import { withRouter } from 'react-router-dom'
const RegistrationForm = (props) => {
  const [form] = Form.useForm();
  const onFinish = (values) => {
    props.registing(values)

  };
  const sendmessage = ()=>{
    props.sendmessage(form.getFieldValue('email'))
  }
  return (
    <Form form={form} name="register" onFinish={onFinish} scrollToFirstError>
      <Form.Item
        name="username"
        label="用户名"
        hasFeedback
        rules={[
          {
            required: true,
            message: "请输入你的用户名",
          },
          ({ getFieldValue }) => ({
            validator(rule, value) {
              if (value.length > 5 && value.length < 13) {
                return Promise.resolve();
              } else {
                return Promise.reject("请输入6至12个字符");
              }
            },
          }),
        ]}
      >
        <Input />
      </Form.Item>

      <Form.Item
        name="password"
        label="密码"
        rules={[
          {
            required: true,
            message: "请输入你的密码",
          },
          {
            pattern: /^[a-zA-Z0-9]{6,12}$/,
            message: "数字和字母大于6位,小于12位",
          },
        ]}
        hasFeedback
      >
        <Input.Password />
      </Form.Item>

      <Form.Item
        name="confirm"
        label="确认密码"
        dependencies={["password"]}
        hasFeedback
        rules={[
          {
            required: true,
            message: "请输入你的密码",
          },
          ({ getFieldValue }) => ({
            validator(rule, value) {
              if (!value || getFieldValue("password") === value) {
                return Promise.resolve();
              }
              return Promise.reject("两次输入的密码不一致");
            },
          }),
        ]}
      >
        <Input.Password />
      </Form.Item>
      <Form.Item
        name="email"
        label="邮箱"
        hasFeedback
        rules={[
          {
            type: "email",
            message: "请输入正确的邮箱",
          },
          {
            required: true,
            message: "请输入你的邮箱",
          },
        ]}
      >
        <Input />
      </Form.Item>
      <div style={{ display:'flex' }}>
        <Form.Item
          name="code"
          label="验证码"
          rules={[
            {
              required: true,
              message: "请输入验证码",
            },
          ]}
        >
          <Input />

        </Form.Item>
        <Button type="primary" style={{ marginLeft:'15px' }} onClick={ sendmessage } disabled={ props.send }>
            { props.sendinfo }
        </Button>
      </div>
      <Form.Item style={{ textAlign:'center' }}>
        <Button type="primary" htmlType="submit" size="large" danger>
          注册
        </Button>
      </Form.Item>
    </Form>
  );
};

 class Regist extends Component {
  constructor(props) {
    super(props);
    document.title = "注册页面";
    this.state = {
      control: false,
      send:false,
      sendinfo:'发送'
    };
  }
  sendmessage = (email)=>{
    SendEmail({email}).then(res=>{
      if(res.accepted){
        this.setState({
          send:true
        })
        var sencond = 60;
        var time1 = setInterval(() => {
          this.setState({
            sendinfo:`${--sencond}s后再试`
          },function(){
            if(sencond == 0){
              clearInterval(time1)
              this.setState({
                send:false,
                sendinfo:'发送'
              })
            }
          })
        }, 1000);
        message.info('邮件已发送请输入验证码')
      }else{
        message.error('邮件发送错误')
      }
    })
  }

  registing = (values)=>{
    AddUser(values).then(res=>{
      if(res === '添加成功'){
        message.success('注册用户成功！正在返回登陆页面')
        this.props.history.push('/login')

      }else{
        if(res === '验证码错误'){
            message.error('验证码错误')
        }else{
          message.error('用户名已被使用')
        }
      }
    })
  }
  render() {
    return (
      <div className="regist">
                <ReactCanvasNest config = {{ pointColor: ' 236, 131, 10 ',lineColor:'236, 131, 10',lineWidth:3,count:50 ,dist:1000,pointR:2}} style={{ background:'#FFEFD5' }} />
        <div className="container_regist">
          <h1 style={{ fontSize:'25px',textAlign:'center',fontWeight:'bolder',marginTop:'10px' }}>注册</h1>  
          <RegistrationForm sendmessage={this.sendmessage} registing={this.registing}  {...this.state} />
        </div>
      </div>
    );
  }
}
export default withRouter(Regist,RegistrationForm)
```

