---
title: Mongoose的aggregate
date:
updated:
type: "tags"
comments:
categories: DataBase
description: Mongoose的aggregate
keywords: Mongoose的aggregate
cover: https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=1139235225,3544810372&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---
# 1.分类统计数量个数
```js
BlogModel.aggregate(
    [
      {
        $project: {
          tag: 1,
          uid:1,
          sum:1
        },
      },
      {
          $match:{
              uid:mongoose.Types.ObjectId(uid)
          }
      },
      {
          $group:{
              _id:"$tag",
              sum:{$sum: 1}, 
          }
      },
    ],function (err, docs) {
      if(err){
        return res.send(err)
      }
      res.send(docs);
    }
  )
})
```

# 2.分类统计总和 总价值
```js
router.get("/allscan", (req, res) => {
    var uid = mongoose.Types.ObjectId(global.token);
    BlogModel.aggregate(
      [
        {
          $project: {
              //只有被设置进去的字段才会显示出来，其他列就不会被显示。
            // day : {$substr: [{"$add":["$create_time", 28800000]}, 0, 7] },
            view: 1,
            commets:1,
            uid:1
          },
        },
        {
            $match:{
                uid:uid
            }
        },
        {
            $group:{
                _id:"$uid",
                totalViews:{$sum: "$view"},
                totalComments:{$sum: "$commets"},
            }
        },
      ],
      function (err, docs) {
        res.send(docs);
      }
    );
  });router.get("/allscan", (req, res) => {
    var uid = mongoose.Types.ObjectId(global.token);
    BlogModel.aggregate(
      [
        {
          $project: {
              //只有被设置进去的字段才会显示出来，其他列就不会被显示。
            // day : {$substr: [{"$add":["$create_time", 28800000]}, 0, 7] },
            view: 1,
            commets:1,
            uid:1
          },
        },
        {
            $match:{
                uid:uid
            }
        },
        {
            $group:{
                _id:"$uid",
                totalViews:{$sum: "$view"},
                totalComments:{$sum: "$commets"},
            }
        },
      ],
      function (err, docs) {
        res.send(docs);
      }
    );
  });
```

# 3.多表查询
```js
 User.aggregate([
      {
        $lookup: {
          from: "resource",
          localField: "resource",
          foreignField: "_id",
          as: "items",
        },
      },
      {
        $project:{ password:0,username:0,emial:0,resource:0}
      },
      {
        $match: {
          "_id": mongoose.Types.ObjectId(uid),
        },
      },
    ],(err,docs)=>{
      return res.send(docs)
    });

```
