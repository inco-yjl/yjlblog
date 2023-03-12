---
title: "前端笔试题练习（一）"
date: 2023-03-11T16:00:00+08:00
author: ["yjlintp"]
tags:
- 前端
# summary->在列表页展现的摘要内容，自动生成，内容默认前70个字符，可通过此参数自定义，一般无需专门设置
summary: "练习百度的前端笔试题"
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
    setTimeout(function(){
        console.log(1);
    }, 0)
    new Promise(function(resolve){
        console.log(2);
        resolve();
        console.log(3);
    }).then(function(){
        console.log(4);
    })
    console.log(5);
```

Promise 构造函数接受一个函数作为参数，该函数是**同步的**并且会被<strong>立即执行</strong>，所以我们称之为起始函数。起始函数包含两个参数 resolve 和 reject，分别表示 Promise 成功和失败的状态。起始函数执行成功时，它应该调用 resolve 函数并传递成功的结果。当起始函数执行失败时，它应该调用 reject 函数并传递失败的原因。

Promise 构造函数返回一个 Promise 对象，该对象具有then方法，用于处理 Promise 成功状态的回调函数。then方法指定的回调函数将在**当前脚本所有同步任务**执行完后才会执行。所以3在4之前执行，4在5之后执行。

Promise属于JavaScript引擎内部任务，而setTimeout则是浏览器API，而引擎内部任务优先级高于浏览器API任务，所以1最后输出。

**答案：2 3 5 4 1**

<br/>
<h3>
2.下列布局在页面上的宽度比是多少？
</h3>

```css
    .flex {
        display: flex;
        width: 200px;
        height: 100px;
    }
    .left {
        flex: 3 2 50px;
        background: red;
    }
    .right {
        flex: 2 1 200px;
        background: blue;
    }
```
```html
    <div class="flex">
        <div class="left"></div>
        <div class="right"></div>
    </div>
```

flex: flex-grow flex-shrink flex-basis

flex-shrink × flex-basis 得出的是子元素总宽度超过父元素宽度时的收缩权重。

**答案：1:5**

<br/>
<h3>
3.下列代码的执行结果
</h3>

```javascript
    function sayHello() {
        console.log(name);
        console.log(age);
        var name = "Tom";
        let age = 18;
    } 
    sayHello();
```
**答案：undefined，ReferenceError**

**var和let的区别：**

**变量提升：**
当浏览器开辟出供代码执行的栈内存后，代码并没有自上而下立即执行，而是继续做了一些事情：把当前作用域中所有带var/function关键字的进行提前的声明和定义 => 变量提升机制。let不存在该机制

**默认值：**
var如果只声明没有赋值，默认值是undefined。而如果let的值在定义前使用，会报ReferenceError

**重复声明：**
var允许重复声明，而let声明的变量（在同一作用域中）不允许**任何关键词的**重复声明。重复声明被视作语法错误，代码一步都不会执行。

**暂时性死区：**

一个未声明的值a
```javascript
console.log(a)
// => ReferenceError: a is not defined
```

**但是**typeof一个未声明的值a
```javascript
console.log(typeof a)
// =>  'undefined' 这是浏览器的bug，本应报错，因为没有a（暂时性死区）
```

typeof一个let声明的值a
```javascript
console.log(typeof a)
// => ReferenceError: Cannot access 'a' before initialization
let a
```
<br/>

**执行顺序**
```javascript
for (var i = 0; i < 3; i++) {
setTimeout(_ => {
    console.log(i)
  })
}
```
**输出：333**

setTimeout和循环内部的执行是异步的，其优先执行完后再执行setTimeout内容。var声明的变量会覆盖之前的声明
```javascript
for (let i = 0; i < 3; i++) {
  setTimeout(_ => {
    console.log(i)
  })
}
```
**输出：012**

let在此定义的作用域是在函数的块内 (这里的 i 是函数局部变量)，每一次循环的 i 是相互独立的(属于不同作用域)

<br/>
<h3>
4.关于html语义化，以下说法错误的是？
</h3>

A.对表单分组的标题需要使用 `label` 标签包裹

B.对生僻字标注拼音需要使用 `ruby` 标签包裹

C.对引用文献需要使用 `cite` 标签包裹

D.`fieldset` 标签用来对表单进行分组

**html语义化**

将 `<label>` 和一个 `<input>` 元素相关联，为input元素定义标注，改进了表单控件的可用性；当你点击到label标签时，会自动聚焦到对应控件上

`<ruby>`被用来展示东亚文字注音或字符注释

`<cite>`表示一个作品的引用，且必须包含作品的标题

`<fieldset>`元素将一个 HTML 表单的一部分组成一组，内置了一个`<legend>`元素作为 fieldset 的标题。即A应是`<legend>`。以下是一个实例

<form action="#">
  <fieldset>
    <legend>Simple fieldset</legend>
    <input type="radio" id="radio">
    <label for="radio">Spirit of radio</label>
    <br/>
    <input type="radio" id="radio">
    <label for="radio">Music Type</label>
  </fieldset>
</form>

**答案：A**

<br/>
<h3>
5.linux下可以查看网卡流量情况的是
</h3>

<ol>
<li>sar</li>
<li>/proc/net/dev</li>
<li>ifstat</li>
<li>iftop</li>
<li><strong>nload</strong></li>
<li>iptraf-ng</li>
<li>nethogs</li>
</ol>

<br/>
<h3>
6.那么对于文件上传漏洞，有效防御手段有哪些？
</h3>

A.浏览器端限制文件扩展名

B.服务器端限制文件扩展名

C.将上传的文件存储在静态文件服务器中

D.验证Content-Type

文件上传漏洞是web安全中经常用到的一种漏洞形式。是对数据与代码分离原则的一种攻击。上传漏洞顾名思义，就是攻击者上传了一个可执行文件如木马、病毒、恶意脚本如PHP、ASP等执行文件等到服务器执行，并最终获得网站控制权限的高危漏洞。

一般来说文件上传过程中检测部分由客户端javascript检测、服务端Content-Type类型检测、服务端path参数检测、服务端文件扩展名检测、服务端内容检测组成。但这些检测并不完善，且都有绕过方法。

A:可以把木马php伪造成jpg绕过，制作一句话图片木马

D:服务端MIME检测绕过（Content-Type检测）：使用burp代理，修改Content-Type的参数

B貌似也不行

**答案：BC**

<br/>
<h3>
7.
关于以下代码，说法正确的有哪些？
</h3>

```javascript
function Person() { }
var person = new Person();
```

A.每一个原型都有一个constructor属性指向关联的构造函数。

B.
每一个对象都有一个prototype属性。

C.
Object.getPrototypeOf(person) === Person.prototype

D.
person.constructor === Person

**js原型**

```javascript
function Person(age) {
    this.age = age       
}
Person.prototype.name = 'kavin'
var person1 = new Person()
var person2 = new Person()
console.log(person1.name) //kavin
console.log(person2.name)  //kavin
```

在JavaScript中，每个**函数**都有一个prototype属性，这个属性指向函数的原型对象。上述例子中，函数的prototype指向了一个对象，而这个对象正是调用构造函数时创建的实例的**原型**，也就是person1和person2的原型。

每一个**javascript对象**(除null外)创建的时候，就会与之关联原型，每一个对象都会从原型中“继承”属性。

<img src='https://imgconvert.csdnimg.cn/aHR0cHM6Ly9pbWcyMDE4LmNuYmxvZ3MuY29tL2Jsb2cvODUwMzc1LzIwMTkwNy84NTAzNzUtMjAxOTA3MDgxNTEwMjQxMzQtNTEyNTU4MDA3LnBuZw?x-oss-process=image/format,png'/>

```javascript
function Person() {
}
var person = new Person();
console.log(person.__proto__ === Person.prototype);//true
//Object.getPrototypeOf(person)
```
每个对象(除null外)都会有的属性，叫做__proto__，这个属性会指向该对象的原型。
<img src='https://imgconvert.csdnimg.cn/aHR0cHM6Ly9pbWcyMDE4LmNuYmxvZ3MuY29tL2Jsb2cvODUwMzc1LzIwMTkwNy84NTAzNzUtMjAxOTA3MDgxNTEzMjI1MzAtMTYwODE1Nzk3My5wbmc?x-oss-process=image/format,png'/>

**构造函数**
```javascript
function Person() {
}
console.log(Person===Person.prototype.constructor)  //true
//person.constructor === Person.prototype.constructor
```
每个原型都有一个constructor属性，指向该关联的构造函数
<img src='https://imgconvert.csdnimg.cn/aHR0cHM6Ly9pbWcyMDE4LmNuYmxvZ3MuY29tL2Jsb2cvODUwMzc1LzIwMTkwNy84NTAzNzUtMjAxOTA3MDgxNTE2MTU2OTEtMTAxNzYxMTE5MC5wbmc?x-oss-process=image/format,png'/>

**原型链**

```javascript
console.log(Object.prototype.__proto__ === null) // true
```

每个构造函数都有一个原型对象，原型对象都包含一个指向构造函数的指针，而实例都包含一个指向原型对象的内部指针。那么假如我们让原型对象等于另一个类型的实例，结果会怎样？显然，此时的原型对象将包含一个指向另一个原型的指针，相应地，另一个原型中也包含着一个指向另一个构造函数的指针。假如另一个原型又是另一个类型的实例，那么上述关系依然成立。如此层层递进，就构成了实例与原型的链条。这就是所谓的原型链的基本概念。

<img src='https://imgconvert.csdnimg.cn/aHR0cHM6Ly9pbWcyMDE4LmNuYmxvZ3MuY29tL2Jsb2cvODUwMzc1LzIwMTkwNy84NTAzNzUtMjAxOTA3MDgxNTMxMzk1NzctMjEwNTY1MjU1NC5wbmc?x-oss-process=image/format,png'/>
(因为原型也是对象，所以是Object的实例)

**答案：ACD**

<br/>
<h3>
8.关于同源策略和跨域的问题，以下说法正确的有？
</h3>

A.`http://store.company.com/dir/page.html` 和 `http://store.company.com/dir/other.html` 不同源。

B.
node设置res.header("Access-Control-Allow-Origin", "*") 去解决跨域问题，会有安全问题。

C.
JSONP的原理是利用引入script不限制源的特点，把处理函数名作为参数传入，然后返回执行语句。

D.
document.domain的原理是将两个页面的document.domain设置成一致，只能解决主域相同的跨域问题。

**同源**

协议/主机/端口元组相同。

**跨域**

跨域的安全限制都是对浏览器端来说的，服务器端是不存在跨域安全限制的。浏览器的同源策略限制从一个源加载的文档或**脚本**与来自另一个源的资源进行**交互**。

**跨源资源共享（CORS）**

CORS是一种基于 HTTP Headers的机制。跨域的目标服务器返回的响应报文包含了正确 CORS 响应头，则允许 Web 应用服务器进行跨源访问控制，从而使跨源数据传输得以安全进行。

其中最敏感的就是 Access-Control-Allow-Origin 这个 Header, 他是W3C标准里用来检查该跨域请求是否可以被通过。 (Access Control Check)
跨域实现的过程大致如：

<blockquote>
从http://www.a.com/test.html 发起一个跨域请求，请求的地址为： http://www.b.com/test.php，如果 服务器B返回一个如下的header

<code>Access-Control-Allow-Origin: http://www.a.com</code>

那么，这个来自http://www.a.com/test.html 的跨域请求就会被通过。
在这个过程中， request 还会带上这个header：<code>Origin: http://www.a.com</code>
</blockquote>

**JSONP**

JSONP是一种非正式传输协议，该协议的一个要点就是允许用户传递一个callback(或者一开始就定义一个回调方法)参数给服务端，然后服务端返回数据时会将这个callback参数作为函数名来包裹住JSON数据，这样客户端就可以随意定制自己的函数来自动处理返回数据了。

可以发现，在web页面调用js文件是不受是否跨域问题的影响的。而且凡是拥有src/href这类属性的标签都拥有跨域的能力，比如img和script。这本质上就是一个GET请求。jsonp的实现原理其实就是利用了这个。

**实现方法**

```javascript
// 前端部分
<script>
    //callback
    function onResponse(posts) {
        console.log(posts);
    }
</script>

<script src="http://localhost:9090/api"></script>

//后端部分
const http = require('http');
http.createServer((req, res) => {
    if (req.url === '/api') {
        let posts = ['js', 'php'];
        res.end(`onResponse(${JSON.stringify(posts)})`);
    }
})
.listen(9090, () => {
    console.log(9090)
})
```
前端script中的src请求完毕以后，后端会给前端返回一个字符串`onResponse(["js","php"])`，因为script标签的原因，浏览器会把这一段字符串当做js来执行。这样我们一开始在前端定义好了的回调就会执行，我们就拿到数据了。

**利用document.domain实现跨域**

前提条件：这两个域名必须属于同一个基础域名!而且所用的协议，端口都要一致，否则无法利用document.domain进行跨域。
document.domain属性赋值是有限制的，只能赋成当前的域名或者**基础域名**。

两个子域名：

aaa.xxx.com

bbb.xxx.com

aaa里的一个网页（a.html）引入了bbb 里的一个网页（b.html），这时a.html里同样是不能操作b.html里面的内容的。因为document.domain不一样，一个是aaa.xxx.com，另一个是bbb.xxx.com。

这时就可以通过Javascript，将两个页面的domain改成一样的，需要在a.html里与b.html里都加入：

document.domain = "xxx.com";

这样这两个页面就可以互相操作了。也就是实现了同一基础域名之间的"跨域"。

**答案：BCD**

<br/>
<h3>
9.以下关于CSS盒模型，说法正确的是：
</h3>

A.
盒模型相关CSS属性包含：宽高、内边距、边框和外边距。

B.
如果`<p>`的纵向margin是12px，那么两个`<p>`之间纵向的距离是12px。

C.
在CSS中，增加内边距、边框和外边距不会影响内容区域的尺寸，但是会增加元素框的总尺寸。

D.
盒子的实际宽度=宽度+左填充+右填充+左边框+右边框+左边界+右边界。

**A**???

**B:** margin纵向塌陷现象：小的margin会塌陷到大的margin中，从而margin不叠加，只以大值为准。相邻元素的margin-top和margin-bottom 会发生重叠；空白内容的P标签、div标签等也会重叠。

**C:**
<img src='https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model/box-model.png'/>

**D:** 盒子的实际宽度不包含margin

**答案：BC**

<br/>
<h3>
10.下列在 JS 事件循环机制中属于微任务（microTask）的是？
</h3>

A.
process.nextTick

B.
promise

C.
setTimeout

D.
setInterval

**js事件循环**

js是单线程执行的，所谓异步任务也是用同步的方式去模拟的。Event Loop是js的执行机制，就是先确定事件的执行规则，然后按照这个规则循环执行。
<ul>
<li>任务和异步任务会分别进入不同的执行空间，同步任务进入主线程优先执行，异步的进入Event table，并注册该异步动作的回调函数。</li>
<li>当异步动作中指定的事情完成之后（比如发送请求给服务端），Event Table会将这个函数移入Event Queue（事件队列）</li>
<li>主线程内的任务执行完成之后，会有一段空置时间（很短），这个时候会去看Event Queue（事件队列）中找函数，如果有Event Queue中有需要执行的函数，那么就会把这个函数放入主线程进行执行。</li>
<li>以上的过程不断重复，形成了我们常说的Event loop（事件循环）</li>
</ul>

**微任务/宏任务**

微任务和宏任务皆为异步任务，它们都属于一个队列，主要区别在于他们的执行顺序。js线程在执行代码时正确的顺序是：同步任务--> 微任务--> 宏任务。每次**单个宏任务**执行完毕后，检查微任务(microTask)队列是否为空，如果不为空的话，会按照先入先出的规则全部执行完微任务。

macro-task(宏任务)：包括整体代码script，setTimeout，setInterval，setImmediate

micro-task(微任务)：Promise，process.nextTick

**nextTick**

process.nextTick() 是 Node 的一个定时器，让任务可以在指定的时间运行。其中 Node 一共提供了 4 个定时器，它们分别是 setTimeout()、setInterval()、setImmediate()、process.nextTick()。

process.nextTick() 这个名字有点误导，它是在本轮循环执行的，而且是所有异步任务里面最快执行的。

Node 执行完所有同步任务，接下来就会执行process.nextTick的任务队列。基本上，如果你希望异步任务尽可能快地执行，那就使用 process.nextTick。

```javascript
process.nextTick(() => console.log(3));
Promise.resolve().then(() => console.log(4)); // 3 // 4
```
(都属于微任务，nextTick优先执行)

```javascript
process.nextTick(() => console.log(1));
Promise.resolve().then(() => console.log(2));
process.nextTick(() => console.log(3));
Promise.resolve().then(() => console.log(4)); // 1 // 3 // 2 // 4
```
上面代码中，全部 process.nextTick 的回调函数，执行都会早于 Promise 的。

**答案：AB**

<br/>
<h3>
11.如图片的地址为imgUrl,下面哪行代码在网页中打开可以直接看到的是文字“hello”？
</h3>

A.`<img src=“imgUrl” title=“hello”>`

B.`<img src=“” title=“hello”>`

C.`<img src=“” alt=“hello”>`

D.`<img src=“imgUrl” alt=“hello”>`

title原本是悬浮显示的，但是图片出现错误显示不出来时也会显示（和alt一样）。但是alt优先级高

**答案：BC**

<br/>
<h3>
12.下列选项中，关于HTTP与HTTPS的区别的描述中，正确的是？
</h3>

A.http是超文本传输协议，信息是明文传输。https则是具有安全性的ssl加密传输协议。

B.http和https使用的是完全不同的连接方式，用的端口也不一样。

C.http的连接很简单，是无状态的。HTTPS协议是由SSL+HTTP协议构建的可进行加密传输、身份认证的网络协议，比http协议安全。

D.
http默认使用80端口，https默认使用403端口。

**A:** HTTP 明文传输，数据都是未加密的，安全性较差，HTTPS（SSL+HTTP） 数据传输过程是加密的，安全性较好

**B:** http 和 https 使用的是完全不同的连接方式，用的端口也不一样。HTTP 使用 TCP 三次握手建立连接，客户端和服务器需要交换 3 个包，而 HTTPS除了 TCP 的三个包，还要加上 ssl 握手需要的 9 个包，所以一共是 12 个包。

**C:** HTTPS 开发的主要目的，是提供对网站服务器的身份认证，保护交换数据的隐私与完整性。

**D:** HTTP 默认工作在 TCP 协议 80 端口,HTTPS 默认工作在 TCP 协议443端口

**答案：ABC**


<br/>
<h3>
13.下列关于 React 的生命周期的描述，正确的有哪些？
</h3>

A.
组件的生命周期包括实例化、运行态和销毁期；

B.
允许在 render 函数中执行 this.setState；

C.
componentDidMount 函数中可以获取到该组件的 dom 节点；

D.
React 16 提供的 componentDidCatch 方法，可以捕获构造函数、渲染和生命周期函数的异常；

**答案：ACD**
