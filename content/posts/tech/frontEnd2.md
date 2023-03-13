---
title: "前端笔试题练习（二）"
date: 2023-03-12T15:48:21+08:00
author: ["yjlintp"]
tags:
- 前端
# summary->在列表页展现的摘要内容，自动生成，内容默认前70个字符，可通过此参数自定义，一般无需专门设置
summary: "练习百度的前端笔试题2"
# description->需要自己编写的文章描述，是搜索引擎呈现在搜索结果链接下方的网页简介，建议设置
description: "不会写，好想死"
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

<h3>
1.下列程序的运行结果是什么？
</h3>

```javascript
function getPersonInfo (one, two, three) {
console.log(one)
console.log(two)
console.log(three)
}
const person = 'Lydia'
const age = 21
getPersonInfo `${person} is ${age} years old`
```
A.
“Lydia” 21 [“”,  “ is ”,  “ years old”]

B.
[“”, “ is ”, “ years old”] “Lydia” 21

C.
“Lydia” [“”, “ is ”, “ years old”] 21

D.
Reference Error

**模板字符串**

模板字符串可以包含特定语法（`${expression}`）的占位符。占位符中的表达式和周围的文本会一起传递给一个默认函数，该函数负责将所有的部分连接起来。如果一个模板字符串由**表达式**开头，则该字符串被称为带标签的模板字符串，该表达式通常是一个**函数**，它会在模板字符串处理后被调用。

标签使您可以用函数解析模板字符串。标签函数的第一个参数包含一个**字符串值的数组**。其余的参数与表达式相关。

**答案：B**


<br/>
<h3>
2.关于将 Promise.all 和 Promise.race 传入空数组的两段代码的输出结果说法正确的是
</h3>

```javascript
Promise.all([]).then((res) => {
    console.log('all');
});
Promise.race([]).then((res) => {
    console.log('race');
});
```

A.all 和 race 都会被输出

B.all 和 race 都不会被输出

C.all 会被输出，而 race 不会被输出

D.all 不会被输出，race 会被输出

**Promise.all:** 将多个Promise实例包装成一个Promise实例。

<ul>
<li>如果传入的参数是一个空的可迭代对象，则返回一个已完成（already resolved）状态的 Promise。</li>
<li>如果传入的参数不包含任何 promise，则返回一个异步完成（asynchronously resolved）Promise。注意：Google Chrome 58 在这种情况下返回一个已完成（already resolved）状态的 Promise。</li>
<li>其他情况下返回一个处理中（pending）的Promise。这个返回的 promise 之后会在所有的 promise <strong>都完成</strong>或有一个 promise 失败时异步地变为完成或失败。返回值将会按照参数内的 promise 顺序排列，而不是由调用 promise 的完成顺序决定。</li>
</ul>

**Promise.all:** 赛跑。一旦迭代器中的某个 promise 解决或拒绝，返回的 promise 就会解决或拒绝。如果传的迭代是空的，则返回的 promise 将永远等待。

**答案：C**

<br/>
<h3>
3.以下使用 typeof 操作符的代码的输出结果是？
</h3>

```javascript
var x = typeof x
console.log(x)
var res = typeof typeof x;
console.log(res)
```

typeof的返回值是字符串类型，所以是string

<br/>
<h3>
4.关于html的canvas的绘制、缩放，下列说法正确的是？
</h3>

A.
图像绘制在canvas元素之外也可见

B。
使用 drawImage方法绘制的图片可以用css3的tramsform:scale的属性实现缩放

C.
默认情况下，canvas是一个可以获取焦点的元素

D.
其他3个选项都不正确

**A:** 好像是对的？

**B:** 不是css，而是js的context.transform方法。context：渲染上下文对象

**C:** 不能直接获得，可以通过以下代码获得：
```javascript
canvas.setAttribute('tabindex', '0'); // tabindex指示元素是否可以聚焦
canvas.addEventListener('click', function() {
    canvas.focus();
});
canvas.focus();
```

注意canvas如果在css中设置宽高，可能导致图案变形，这时就使用canvas本身的宽高属性

**答案：D**


<br/>
<h3>
5.下面这段代码在浏览器中渲染出来的div高度是多少
</h3>

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta http-equiv="X-UA-Compatible" content="ie=edge">
<title>Document</title>
<style>
.heightTest {
height: 1000px;
min-height: 500px;
max-height: 300px;
}
</style>
</head>
 
<body>
<div class="heightTest"></div>
</body>
 
</html>
```

max-height会覆盖height，而min-height会覆盖max-height

=>max-height和height取小值，min-height和height取大值

**答案：500px**

<br/>
<h3>
6.如何仅获得下述值为3的DOM节点引用(不包含其他元素)
</h3>

```html
<ul class='aaa'>
    <li class='bbb'>1</li>
    <li class='ccc'>2</li>
    <li>3</li>
    <li>4</li>
</ul>
```

A .aaa > li

B .bbb ~ li

C .ccc ~ li

D .ccc + li

**css选择器:**

**组合器**

后代选择器：所有后代节点 `A B`

直接子代组合器：`A B`

一般兄弟组合器：后一个节点在前一个节点**后面**的**任意**位置，且共享同一个父节点 `A ~ B`

紧邻兄弟组合器：A节点后紧跟的兄弟节点B `A + B`

列组合器：`col || td`,匹配表格列内所有`<td>`

**分组选择器**

选择器列表：`,`将不同的选择器结合起来

**伪选择器**

`:`按状态信息来选择元素

`::`用于表示无法用 HTML 语义表达的实体。`p::first-line`匹配所有`<p>`元素的第一行。

**答案：D**

<br/>
<h3>
7.下面哪个选项不能实现除第一个<li>标签外的<li>标签字体都为红色，即如下注释效果
</h3>

```html
<ul class="word">
    <li class="text">1</li>       //字体为黑色
    <li class="text">2</li>       //字体为红色
    <li class="text">3</li>       //字体为红色
</ul>
```

A
`
.text ~ .text {
    color: red;
}
`

B
`
.word:not(:first-child) {
    color: red;
}
`

`
C
.text:nth-last-child(2){
    color: red;
}
`

`
D
.text + .text {
    color: red;
}
`

**A:** 对第一个标签应用，即可使后面两个标签均为红色

**B:** 可匹配除第一个元素之外的元素

**C:** 仅匹配倒数第二个元素，即只有第一个标签为红色

**D:** 匹配每个.text后的紧邻元素，则除了第一个都为红色

答案：C

<br/>
<h3>
8.内存泄漏是 javascript 代码中必须尽量避免的，以下几段代码可能会引起内存泄漏的有（）
</h3>

(1)
```javascript
function getName() {
    name = 'javascript'
}
getName()
 ```
    
(2)
```javascript
const elements = {
    button: document.getElementById('button')
};
function removeButton() {
    document.body.removeChild(elements.button);
}
removeButton()
```

(3)
```javascript
let timer = setInterval(() => {
    const node = document.querySelector('#node') 
    if(node) {
        clearInterval(timer)
    }
}, 1000);
```

A.
(1)、（2）、（3）

B.
(2)、（3）

C.
(1)、（3）

D.
(1)、（2）


**js内存泄漏：**

内存泄漏：程序不再使用或不需要的一块内存，但是由于某种原因没有被释放仍然被不必要的占有。在代码中创建对象和变量会占用内存，但是javaScript是有自己的内存回收机制，可以确定那些变量不再需要，并将其清除。但是代码中存在逻辑缺陷的时候，一些已经不需要的变量在程序中还存在着引用。

**常见情况**

**1.全局变量：** 在非严格模式下当引用未声明的变量时，会在全局对象中创建一个新变量。在浏览器中，全局对象将是window。全局变量无法被垃圾回收机制回收。所以（1）中情况会造成内存泄漏。

**2.DOM引用：** 如（2）中情况，删除了DMO节点，但保留了引用，导致DOM元素没有被回收。值得注意的是子节点的引用问题，如果删除父节点但仍有子元素的引用在，可能导致整个父元素仍保留在内存中。

**3.被遗忘的定时器和回调函数：** setInterval不会清除定时器队列，需要在定时器完成工作时，手动清楚定时器，否则回调函数及其内部引用对应的数据不会被回收。

**4.闭包：**

```javascript
        var fn  =function(){
            var sum = 0
            return function(){
                sum++
                console.log(sum);
            }
        }
        fn1=fn() 
        fn1()   //1
        fn1()   //2
        fn1()   //无法被回收
        fn1 = null //手动释放
```

**答案：D**

<br/>
<h3>
9.对于一个数字组成的数组 nums，现在需要执行在不改动 nums 的基础上去重操作，返回一个新的无重复元素的数组，以下几段代码能完成这一操作的是?
</h3>

```javascript
(1)
const newNums = Array.from(new Set(nums))
(2)
const newNums = nums.filter((n, i) => {
    return nums.indexOf(n) === i
})
(3)
const newNums = nums.forEach((n, i) => {
    return nums.indexOf(n) === i
})
(4)
const newNums = nums.reduce((acc, n, i) => {
    return [].concat(acc, nums.indexOf(n) === i ? n : []
)
})
```

A.
(1)、（2）、（3）、（4）

B.
(1)、（3）、（4）

C.
(1)、（2）、（4）

D.
(1)、（4）

**js数组去重：**

<ol>
<li>
利用Set()+Array.from():

Set对象：是值的集合，你以按照插入的顺序迭代它的元素。Set中的元素是唯一的。

Array.from() 方法：对一个类似数组或可迭代对象创建一个新的，浅拷贝的数组实例。
</li>

<li>
filter+indexOf
filter() 方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素。

利用数组的indexOf方法:返回第一次出现指定值的索引。

（forEach() 方法按顺序为数组中的每个元素调用一次函数。）
</li>
<li>
reduce() 方法接收一个函数作为累加器,reduce 为数组中的每一个元素依次执行回调函数，不包括数组中被删除或从未被赋值的元素，接受四个参数：初始值（上一次回调的返回值），当前元素值，当前索引，原数组。(4)中利用数组作为每次回调的返回值，indexOf作为判断方法
</li>
</ol>

**答案：C**

<br/>
<h3>
10.利用 sourcemap 定位线上 js 问题是必须掌握的技能，以下关于 sourcemap 文件说法不正确的是（）
</h3>

A.
利用 sourcemap 可以定位到具体的出错代码文件的行、列信息

B.
sourcemap 文件通过记录列号的相对位置来提高性能

C.
在 chrome 渲染过程中，请求完 js 文件后会立即尝试请求对应的 sourcemap 文件并解析

D.
sourcemap 文件使用了 VLQ 编码做映射表

**sourcemap**

Source Map 就是一个信息文件，里面存储了代码打包转换后的位置信息，实质是一个 json 描述文件，维护了打包前后的代码映射关系。在Webpack（或其他打包工具）构建代码中，开启 Source Map 重新构建，就可以使用相关功能。

打包编译后的 bundle.js.map 文件中，mappings（映射）属性的值是：AAAA; AACA, c。这是一个字符串，它分成三层：

第一层是行对应，以分号（; ）表示，每个分号对应转换后**源码的一行**。

第二层是位置对应，以逗号（, ）表示，每个逗号对应转换后**源码的一个位置**。

第三层是位置转换，以**VLQ** 编码表示，代表该位置对应的**转换前的源码位置**。

所以该字符串表示转换后的源码分成两行，第一行有一个位置，第二行有两个位置。

以AAAA 举例，转换后得到 [0, 0, 0, 0] ，所以代表的含义分别是；压缩代码的第一列、第一个源代码文件，即index.js、
源代码的第一行、
源代码第一列

**C：** 需要使用开发者工具，勾选"Enable source maps"。

**答案：C**

<br/>
<h3>
11.对一网站做渗透测试，目标站点由wordpress搭建，请问下面操作最为合适的是?
</h3>

A.
访问robots.txt，查看站点结构及敏感目录

B.
使用wpscan对网站进行扫描

C.
使用appscan或awvs对网站进行漏洞扫描

D.
寻找网站后台，进行暴力破解登录账号密码

**渗透测试**

渗透测试就是通过一些手段来找到网站，APP，网络服务，软件，服务器等网络设备和应用的漏洞，告诉管理员有哪些漏洞，怎么填补，从而防止黑客的入侵。

**网站敏感目录**

robots.txt 文件是专门针对搜索引擎机器人robot 编写的一个纯文本文件。我们可以在这个文件中指定网站中不想被robot访问的目录。这样，我们网站的部分或全部内容就可以不被搜索引擎收录了，或者让搜索引擎只收录指定的内容。

wpscan为wordpress站点专用扫描工具，可扫描wordpress版本、插件及漏洞、用户名泄露、暴力破解接口等。

**答案：B**

<br/>
<h3>
12.关于网络请求延迟增大的问题，以下哪些描述是正确的()
</h3>

A.
使用ping来测试 TCP 端口是不是可以正常连接

B.
使用tcpdump 抓包分析网络请求

C.
使用strace观察进程的网络系统调用

D.
使用Wireshark分析网络报文的收发情况

ping是基于ICMP协议不能测试TCP

**答案：BCD**

<br/>
<h3>
13.
下面可以按照从小到大顺序排列显示磁盘中各个分区利用率的命令是
</h3>

A.
`du | grep -o "\<[0-9]*%.*" -o | sort -n`

B.
`df | grep -o "\<[0-9]*%.*" -o | sort -r`

C.
`df | grep -o "\<[0-9]*%.*" -o | sort -n`

D.
`du | grep -o "\<[0-9]*%.*" -o | sort -m`

df:显示目前在 Linux 系统上的文件系统磁盘使用情况统计
du:前所在文件夹的总磁盘占用量

sort -r降序， -n升序

**答案：C**

<br/>
<h3>

14.如下伪码实现了简单的消费者的功能
</h3>

```C
void consumption() {
    while(____){
         ____;
    }
    P(mutex);
    队列里面取一个元素;
    V(mutex);
    ————————;
}
```

里面的P,V就是指PV操作，mutex是互斥信号量；现有如下方法：
<ul>
<li>isFull() : 表示队列元素满了</li>
<li>isEmpty(): 表示队列元素为空</li>
<li>m_notFull.wait(): 阻塞当前进程，直到队列元素不满</li>
<li>m_notFull.notify(): 队列元素不满了，唤醒某个进程</li>
<li>m_notEmpty.wait()：阻塞当前进程，直到队列元素不为空</li>
<li>m_notEmpty.notify():队列元素不为空了，唤醒某个进程</li>
</ul>
请你按选好方法，填到上面空行，完成消费者的功能

让生产者在缓冲区满时休眠，等到下次消费者消耗缓冲区中的数据的时候，生产者才能被唤醒，开始往缓冲区添加数据。让消费者在缓冲区空时进入休眠，等到生产者往缓冲区添加数据之后，再唤醒消费者。

mutex是互斥信号量，一般为1，实现对缓冲区的互斥访问

**答案：isEmpty(),m_notEmpty.wait(),m_not_Full.notify()**