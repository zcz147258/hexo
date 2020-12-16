---
title: nodejs文件图片服务器
date:
updated:
type: "tags"
categories: Node
comments:
description: nodejs文件图片服务器
keywords: nodejs文件图片服务器
cover: https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=4068303333,250769197&fm=11&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---

io.js
```js
const fs = require('fs')
const io = {
     ExitsFile : async function(path){
        //判断文件是否存在
         await fs.exists(path, function(exists) {
            if(exists){
                return 1
            }else{
                //创建目录
                fs.mkdir(path,(err)=>{
                    if(err){
                        throw err;
                    }
                    return 2
                })
            }
        });
    },
    ReadFile :function(){

    },
    WriteFile :function(data){
        var writeStream = fs.createWriteStream(data)
        writeStream.write(str)
         //监听写入完成
         writeStream.on('finish',()=>{
            console.log('写入完成')
        })
    }

}
module.exports = io;
```

上传配置 multer
```js
/*
 * @Descripttion:
 * @Author: sueRimn
 * @Date: 2020-07-24 18:56:24
 */

const io = require("../utils/io");
const multer = require("multer");
const path = require("path");
const uuid = require('uuid')

let uploadUtils = {
  multer() {
    //保存规则
    var storage = multer.diskStorage({
      //目录
      destination: function (req, res, cb) {
        const length = req.files.length - 1
         io.ExitsFile('/root/upload/'+req.files[length].fieldname);
        cb(null, '/root/upload/'+req.files[length].fieldname);
      },
      //文件名
      filename: function (req, file, cb) {
        let extname = path.extname(file.originalname);
        let fileid = uuid.v4()
        global.fileid = fileid
        cb(null, fileid + extname);
      },
    });
    //设置过滤规则（可选）
    // var imageFilter = function (req, file, cb) {
    //   var acceptableMime = [
    //     "image/jpeg",
    //     "image/png",
    //     "image/jpg",
    //     "image/gif",
    //   ];
    //   //微信公众号只接收上述四种类型的图片
    //   if (acceptableMime.indexOf(file.mimetype) !== -1) {
    //     cb(null, true);
    //   } else {
    //     cb(null, false);
    //   }
    // };
    //设置限制（可选）
    // var imageLimit = {
    //   fieldSize: "2MB",
    // };
    //配置上传文件的中间件
    var upload = multer({
      storage: storage,
      // fileFilter: imageFilter,
      // limits: imageLimit,
    });
    return upload;
  },
};
module.exports = uploadUtils;
```


使用multer
```js
const uploadUtils = require("../utils/multer");
router.post("/uploadnote", uploadUtils.multer().any(), (req, res) => {
  var uid = mongoose.Types.ObjectId(global.token);
  //保存到本地
  //存储到数据库
  let obj = {
    uid: uid,
    imgid: req.files[0].filename,
    imgname: req.files[0].originalname,
    fileid: req.files[1].filename,
    filename: req.files[1].originalname,
    description: req.body.description,
  };
  const arr = new NoteModel(obj);
  arr.save(function (err, docs) {
    if (err) {
      return res.send(err._message);
    }
    return res.send(docs);
  });
});
```

pipe读取文件
```js
app.get('/image/:imgid',(req,res)=>{

  let imgid = req.params.imgid;
  console.log(imgid)
  const cr = fs.createReadStream(`/root/upload/img/${imgid}`,{
    // highWaterMark:3, //文件一次读多少字节,默认 64*1024
    flags:'r', //默认 'r'
    autoClose:true, //默认读取完毕后自动关闭
    // start:0, //读取文件开始位置
    // end:3, //流是闭合区间 包含start也含end
    // encoding:'utf8' //默认null
  })
  cr.on('error',(err)=>{
    res.send(err)
  })
  cr.pipe(res);
})
```
