---
title: "前端知识点Js"
date: 2023-03-17T22:45:47+08:00
author: ["Inco"]
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

### 数组API中的纯函数

**纯函数**：

- 不改变源数组（没有副作用）
- 返回一个数组

- concat 
- map 逐个映射 `arr.map(num => num * 2)`/`arr.map(function(num){ return num*2 })`
- filter 对数组中每个元素进行检查 `arr.filter(num => num>15)`/`arr.map(function(num){ return num>15})`
- slice 返回数组切片，包含start不包含end，如果end不指定，则一直到结尾；如果都不指定，则返回全部

**splice与slice区别：**

slice是切片，splice是剪接。改变原数组，返回值是剪接后的数组。传参：开始索引、剪掉的元素个数、要加入的元素、……


**map(parseInt)**


    const res = [10, 20, 30].map(parseInt)
        console.log(res)
👇

👇
    
    const res2 = [10, 20, 30].map((num, index) => {
        return parseInt(num, index)
    })

map的传参：当前值 当前索引

parseInt传参：字符串 进制基数（2-36，取0相当于不指定，会自行推算进制）

- parseInt(10,0)=10 
- parseInt(20,1)=NaN(进制不能为1) 
- parseInt(30,2)=NaN(进制为2时不能有3)

        res2 = [10, NaN, NaN]

### 增删

pop、shift返回值是被删除的元素; push、unshift返回值是数组长度

## 函数

在 JavaScript 中，函数是**对象**的方法。

如果一个函数不是 JavaScript 对象的方法，那么它就是全局对象的函数。
### call / apply / bind

`call()` 允许为不同的对象分配和调用属于其他对象的函数/方法。第一个参数提供新的**this**值给当前调用的函数/方法。可以使用 call 来实现继承：写一个方法，然后让另外一个新的对象来继承它（而不是在新对象中再写一次这个方法）。

如果不指定第一个参数，`this`的值将会被绑定为全局对象。(在严格模式下，`this`的值将是`undefined`)

```javascript
    //call 调用父构造函数
    function Product(name, price) {
    this.name = name;
    this.price = price;
    }

    function Food(name, price) {
    Product.call(this, name, price);
    this.category = 'food';
    }

    function Toy(name, price) {
    Product.call(this, name, price);
    this.category = 'toy';
    }

    var cheese = new Food('feta', 5);
    var fun = new Toy('robot', 40);
```

apply和call类似，只是第二个参数是数组

### class实现继承

extends/super

```javascript
    // 父类
    class People {
        constructor(name) {
            this.name = name
        }
        eat() {
            console.log(`${this.name} eat food`);
        }
    }

    // 子类
    class Student extends People {
        constructor(name, number) {
            super(name)
            this.number = number
        }
        sayHi() {
            console.log(`姓名 ${this.name} 学号 ${this.number}`);
        }
    }
```

## DOM

一个 web 页面是一个**文档**。这个文档可以在浏览器窗口或作为 HTML 源码显示出来。**文档对象模型 (DOM)** 是 HTML 和 XML 文档的**编程接口**。它提供了对文档的结构化的表述，并定义了一种方式可以使从程序中对该结构进行**访问**，从而改变文档的结构，样式和内容。DOM 将文档解析为一个由节点和对象（包含属性和方法的对象）组成的结构集合。DOM 是 web 页面的完全的**面向对象**表述，它会将 web 页面和脚本连接起来。
DOM 被设计成与特定编程语言相独立，使文档的结构化表述可以通过单一，一致的 API 获得。

`window` 对象表示浏览器中的内容，而 `document` 对象是文档本身的根节点。`Element` 继承了通用的 `Node` 接口，将这两个接口结合后就提供了许多方法和属性可以供单个元素使用。

### 事件冒泡
一个事件触发后，会在子元素和父元素之间传播（propagation）。这种传播分为三个阶段.

- 捕获阶段：从window对象传导到目标节点（上层传到底层）称为“捕获阶段”（capture phase），捕获阶段不会响应任何事件；
- 目标阶段：在目标节点上触发，称为“目标阶段”
- 冒泡阶段：从目标节点传导回window对象（从底层传回上层），称为“冒泡阶段”（bubbling phase）。

在现代浏览器中，默认情况下，所有事件处理程序都在冒泡阶段进行注册。在冒泡阶段中，事件沿着路线寻找处理器，找到了即运行它。在不进行设置的情况下，该冒泡链上的所有对应处理器都会依次运行，想要阻止事件在冒泡链上进一步扩大，可以在处理器中使用事件的stopPropagation()方法。

preventDefault()方法可以取消事件的默认操作，但不会阻止事件通过 DOM 进一步传播，仍要使用stopPropagation()方法。
### 事件代理（委托）

事件代理即是利用事件让子节点上发生的事件冒泡到父节点上，让父元素担当事件监听的职务。一个例子是，如果想让每个列表项`<li>`被点击时弹出一条信息，您可以将click单击事件监听器设置在父元素`<ul>`上，这样事件就会从列表项冒泡到其父元素`<ul>`上。

其优点是：
- 可以大量节省内存占用
- 减少重复性操作（事件注册）
- 可以实现当新增子对象时无需再次对其绑定事件

### 如何减少DOM操作

DOM操作会导致浏览器重解析，引起重排和重绘，直接影响页面性能。对DOM的操作一般有两种：修改已存在页面上的DOM元素（更改样式），创建插入新的DOM元素。

- 如果插入一个元素，应把样式属性修改放在前，插入页面放最后。
- 如果插入多个元素，可以创建文档片段对象（DocumentFragment），将多个DOM元素的插入操作合并到一个

        const frag = document.createDocumentFragment()

        for(let i = 0; i < 10; i++) {
            const li = document.createElement('li')
            li.innerHTML = `List item ${i}`
            // 先插入文档片段中
            frag.appendChild(li)
        }
        // 都完成之后，再统一插入到 DOM 结构中
        list.appendChild(frag)

- 如果要修改DOM元素样式，不要一个个添加/修改，应直接对class进行修改，整体改变样式，防止多次重绘
- 缓存DOM对象：如果需要重复访问同一DOM对象（比如循环寻找子节点），就先将DOM对象赋值给一个对象进行缓存
- 移除元素：如果需要对元素进行复杂的操作（添加子节点等等），应当先将元素从页面中移除再进行操作

### document load和document ready

    //document load
    $(document).load(function(){
        ...code...
    })
    
当页面**所有资源**（DOM文档树、css文件、js文件、图片资源）全部加载完后，执行一个函数

    //document ready
    $(document).ready(function(){
        ...code...
    })
    //简写
    $(function(){
        ...code...
    })

当DOM文档树（不包含图片、css）加载完后执行一个函数。原生js并不包含这个方法，jquery才有。原生js onload事件即为load方法。

## 判等
- `==`两边值类型不同时，会尝试进行类型转换，再比较值是否相等。原始类型的数据会转化为数值类型再进行比较，对象会转化成原始类型的值再进行比较
- 
        '' == '0'          // false
        0 == ''            // true
        0 == '0'            // true
        false == 'false'    // false
        false == '0'        // true
        false == undefined  // false
        false == null      // false
        null == undefined  // true
        ' \t\r\n ' == 0    // true

- `===`严格相等。对于高级类型，如Object、Array，不是比较值相等，而是需要都指向同一对象（地址相同）
  
        undefined === null

## JSON
- JSON 是一种数据格式，本质是一段字符串
- JSON 格式和 JS 对象结构一致，对 JS 语言更友好
- window.JSON 是一个全局对象：JSON.stringify（JS 对象转为 JSON 格式） JSON.parse（JSON 格式转为 JS 对象）

## Object

### 手写深拷贝

```javascript
    function deepClone(obj = {}) {
        if (typeof obj !== 'object' || obj == null) {
            //  obj 是 null，或者不是对象和数组，直接返回
            return obj
        }

        // 初始化返回结果
        let result
        if (obj instanceof Array) {
            result = []
        } else {
            result = {}
        }

        for (let key in obj) {
            // 保证 key 不是原型的属性
            if (obj.hasOwnProperty(key)) {
                // 递归
                result[key] = deepClone(obj[key])
            }
        }

        // 返回结果 
        return result
    }

    const obj1 = {
        name: '张三',
        age: {
            realAge: 20
        },
        arr: ['a', 'b', 'c']
    }
    const obj2 = deepClone(obj1)
    obj2.name = '李四'
    obj2.age.realAge = 22
    obj2.arr[0] = 'x'
    console.log(obj1.name) // 张三
    console.log(obj1.age.realAge) // 20
    console.log(obj1.arr[0]) // a
```

### Object.assign()
- assign 的属性拷贝是浅拷贝
- 用于将源对象的所有可枚举属性复制到目标对象中
- 如果目标对象和源对象有同名属性，或者多个源对象有同名属性，则后面的属性会覆盖前面的属性
- 如果该函数只有一个参数，当参数为对象时，直接返回该对象；当参数不是对象时，会先将参数转为对象然后返回

```javascript
    let sourceObj = {
        a: {
            b: 1
        }
    }
    let targetObj = {
        c: 3
    }
    let res = Object.assign(targetObj, sourceObj)
    console.log(res) // {c: 3, a: {b: 2}}
    targetObj.a.b = 2
    console.log(sourceObj.a.b) // 2
```

### new Object() 和 Object.create() 
- new Object或 const object = {…} 原型为Object.prototype
- Object.create(null) 没有原型
- Object.create({…}) 可以指定原型

```javascript 
    const obj1 = {
        a: 10,
        b: 20,
        sum() {
            return this.a + this.b
        }
    }
    const obj2 = new Object ({
        a: 10,
        b: 20,
        sum() {
            return this.a + this.b
        }
    })
    obj1 === obj2 //false,原型不一样
```