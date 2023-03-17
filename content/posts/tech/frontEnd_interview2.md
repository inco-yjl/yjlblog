---
title: "前端知识点Js"
date: 2023-03-17T22:45:47+08:00
author: ["yjlintp"]
tags:
- 前端
# summary->在列表页展现的摘要内容，自动生成，内容默认前70个字符，可通过此参数自定义，一般无需专门设置
summary: "准备百度面试"
# description->需要自己编写的文章描述，是搜索引擎呈现在搜索结果链接下方的网页简介，建议设置
description: "不会"
weight: # 输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
slug: ""
draft: false # 是否为草稿
comments: true
showToc: true # 显示目录
TocOpen: true # 自动展开目录
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: true # 底部不显示分享栏
showbreadcrumbs: true # 顶部显示当前路径
---

# javascript
## 数组
### API

#### 数组API中的纯函数

**纯函数**：

- 不改变源数组（没有副作用）
- 返回一个数组

- concat 
- map 逐个映射 `arr.map(num => num * 2)`/`arr.map(function(num){ return num*2 })`
- filter 对数组中每个元素进行检查 `arr.filter(num => num>15)`/`arr.map(function(num){ return num>15})`
- slice 返回数组切片，包含start不包含end，如果end不指定，则一直到结尾；如果都不指定，则返回全部

**splice与slice区别：**

slice是切片，splice是剪接。改变原数组，返回值是剪接后的数组。传参：开始索引、剪掉的元素个数、要加入的元素、……