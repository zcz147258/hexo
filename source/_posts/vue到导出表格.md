---
title: Vue导出表格
date:
updated:
type: "tags"
comments:
categories: Vue
description: Vue导出表格
keywords: Vue导出表格
cover: https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=22130535,2850036426&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---

```js
//main.js
import JsonExcel from 'vue-json-excel'
Vue.component('downloadExcel', JsonExcel)

 <download-excel
          class="export-excel-wrapper"
          :fields="json_fields"
          :fetch= "fetchData"
          :before-generate = "startDownload"
        :before-finish = "finishDownload"
          name="提现申请.xls"
        >
          <!-- 上面可以自定义自己的样式，还可以引用其他组件button -->
          <el-button type="primary" size="small" >导出EXCEL</el-button>
        </download-excel>


json_fields: {
        "序号(必填)": "id", // 支持嵌套属性
        "收款方姓名(必填)": "accountName", // 常规字段
        "收款方支付宝账号(必填)": "accountNo", // 支持嵌套属性
        "金额(必填，单位：元)": "actualAmount", // 支持嵌套属性
        "备注(选填)":{
            callback: value => {
            return ` `
          }
        }
      },


async fetchData(){
        this.filters.startTime = moment(this.filters.startTime)
        .utc(8)
        .format("YYYY-MM-DD HH:mm:ss");
      this.filters.endTime = moment(this.filters.endTime)
        .utc(8)
        .format("YYYY-MM-DD HH:mm:ss");
        //下载数据
      var result = await DownloadWithdraws({ "startTime":this.filters.startTime, "endTime":this.filters.endTime })
      console.log(result)
      if(result.code === 0){
          return result.data
      }
        console.log('请求数据')
    },
    startDownload(){
        console.log('开始下载')
    },
    finishDownload(){
        console.log('下载完成') 
    },
```