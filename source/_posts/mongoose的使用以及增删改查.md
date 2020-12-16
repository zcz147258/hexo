---
title: Mongoose的使用以及增删改查
date:
updated:
type: "tags"
comments:
categories: DataBase
description: Mongoose的使用以及增删改查
keywords: Mongoose的使用以及增删改查
cover: https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=1139235225,3544810372&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---

```js
//准备 Mongoose db类  可以看历史博客找到
//书写 Model
/*
 * @Descripttion: 
 * @Author: mikasa
 * @Date: 2020-07-12 15:10:04
 */ 
var mongoose  = require('./db')
var BlogSchema = mongoose.Schema({
    uid:{
        type:mongoose.Schema.Types.ObjectId,
        required:true,
    },
    title:{
        type:String,
        required:true
    },
    content:{
        type:String,
        required:true,
        max:50000
    },
    commets:{ 
        type:Number,
        default:0 
    },
    view:{
        type:Number,
        default:0
    },
    create_time:{
        type: Date,
        default: Date.now
    },
    update_time:{
        type: Date,
        default: Date.now
    },
    tag:{
        type:String,
        required:true
    }
},{versionKey: false,timestamps: { createdAt: 'create_time', updatedAt: 'update_time' }})
BlogSchema.statics.findAll = function(uid,cb){
    this.find({"uid":uid},{uid:0},function(err,docs){
        cb(err,docs)
    })
}
BlogSchema.statics.findHot = function(uid,cb){
    this.find({"uid":uid},{uid:0,content:0,update_time:0},function(err,docs){
        cb(err,docs)
    }).sort({view:-1}).limit(10)
}
BlogSchema.statics.findHotAll = function(uid,cb){
    this.find({},{content:0,update_time:0},function(err,docs){
        cb(err,docs)
    }).sort({view:-1}).limit(10)
}
BlogSchema.statics.findById = function(id,cb){
    this.find({"_id":id},function(err,docs){
        cb(err,docs)
    })
}
BlogSchema.statics.deleteById = function(id,cb){
    this.remove({"_id":id},function(err,docs){
        cb(err,docs)
    })
}
BlogSchema.statics.updateById = function(id,title,content,tag,cb){
    this.updateOne({"_id":id},{"title":title,"content":content,"tag":tag},function(err,docs){
        cb(err,docs)
    })
}
BlogSchema.statics.updateView = function(id,cb){
    this.updateOne({"_id":id},{$inc:{view:1}},function(err,docs){
        cb(err,docs)
    })
}
BlogSchema.statics.updateCommets = function(bid,cb){
    this.updateOne({"_id":id},{$inc:{commets:1}},function(err,docs){
        cb(err,docs)
    })
}
BlogSchema.statics.findTag = function(uid,tagname,cb){
    this.find({"uid":uid,"tag":decodeURI(tagname)},{content:0,update_time:0},function(err,docs){
        cb(err,docs)
    }).sort({view:-1})
}
var BlogModel  = mongoose.model('Blog',BlogSchema,'blog')

module.exports = BlogModel 

//书写 router操作model
const express = require("express");
const BlogModel = require("../model/blog");
var mongoose = require("../model/db");
const router = express.Router();

router.get('/hot',(req,res)=>{
  var uid = req.param('uid')
  BlogModel.findHot(uid,function(err,docs){
      if(err){
          return res.send(err)
      }
      return res.send(docs)
  })
})
```