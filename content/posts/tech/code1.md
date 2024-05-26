---
title: "编程题练习（一）"
date: 2023-03-12T14:45:56+08:00
author: ["Inco"]
tags:
- 算法
# summary->在列表页展现的摘要内容，自动生成，内容默认前70个字符，可通过此参数自定义，一般无需专门设置
summary: "练习百度的前端笔试题"
# description->需要自己编写的文章描述，是搜索引擎呈现在搜索结果链接下方的网页简介，建议设置
description: "欸"
weight: # 输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
slug: ""
draft: false # 是否为草稿
comments: true
showToc: false # 显示目录
TocOpen: true # 自动展开目录
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: true # 底部不显示分享栏
showbreadcrumbs: true # 顶部显示当前路径
---

<h3>求从l到r中所有数字的异或和</h3>

`f(b)=1 xor 2 xor …… xor b`
当b%4=0时：f(b)=b
当b%4=1时：f(b)=1
当b%4=2时：f(b)=b+1
当b%4=3时：f(b)=0

`cal(l,r)=cal(1,r) xor cal(1,l);`


<h3>
保存class为js-input的输入框的dom元素引用
</h3>

`this.input = document.querySelector('.js-input');`或`document.getElementsByClassName("js-input")[0];`

```javascript
input.addEventListener('keydown', function (event) {
        // 请修改这一行代码，判断用户是否按了回车键
        var isEnter = event.keyCode === 13;//通过keyCode
        // 请修改这一行代码，判断用户是否按了删除键
        var isDelete = event.keyCode === 8;
 
        ……
    });
```
