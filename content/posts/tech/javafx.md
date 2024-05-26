---
title: "Javafx"
date: 2023-03-07T22:30:25+08:00
author: ["Inco"]
tags:
- javafx
# summary->在列表页展现的摘要内容，自动生成，内容默认前70个字符，可通过此参数自定义，一般无需专门设置
summary: "做javafx的一些过程记录"
# description->需要自己编写的文章描述，是搜索引擎呈现在搜索结果链接下方的网页简介，建议设置
description: "javafx GUI框架学习"
weight: # 输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
slug: ""
draft: false # 是否为草稿
comments: true
showToc: true # 显示目录
TocOpen: false # 自动展开目录
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: true # 底部不显示分享栏
showbreadcrumbs: true # 顶部显示当前路径
---
<h2>自定义加载</h2>
<h3>
加载自定义字体
</h3>
&ensp;&ensp;&ensp;&ensp;在Application中使用Font的loadFont方法，字体的ttf（或其他）文件放在resources目录下。

<code> font=Font.loadFont(getClass().getResource("xxx.ttf").toExternalForm(), 10);</code>

第二个参数是字体大小

<h3>
加载预设置样式
</h3>
<code>Node.getStylesheets().addAll((getClass().getResource("xxx.css").toExternalForm()));</code>
<h4>
坑
</h4>
<ul>
<li>
application文件放在父文件夹下,避免加载资源的麻烦
</li>
</ul>

<h2>UI</h2>
&ensp;&ensp;&ensp;&ensp;虽然SceneBuilder好用，但是对于复杂布局以及动态元素过多的布局，仍需要手动写代码，用Java进行布局。

<h2>字体</h2>
<h3>字体特效</h3>
&ensp;&ensp;&ensp;&ensp;使用Effect库，可以使用一些常见的字体特效，如阴影DropShadow

<h3>对齐</h3>
&ensp;&ensp;&ensp;&ensp;通过设置节点的对齐方式<code>setAlignment</code>

<h2>节点</h2>
<h3>坐标</h3>
&ensp;&ensp;&ensp;&ensp;在设置坐标的时候使用其他节点的preHeight等数值，无反应。似乎没有显式设定尺寸和坐标的话也无法获取对应数据，只能用一些近似计算。（比如Label利用字体和字符长度来计算等）

<h2>应用</h2>
<h3>最小化</h3>
&ensp;&ensp;&ensp;&ensp;首先将应用图标从任务栏去掉，方法是在stage外再套一个透明stage（因为该设置默认是有关闭按钮的，所以套在外边）。

<code>

        transparentStage.initStyle(StageStyle.UTILITY);
        //将stage的透明度设置为0
        transparentStage.setOpacity(0);
        //stage展示出来
        transparentStage.show();
        stage.initOwner(transparentStage);
</code>

&ensp;&ensp;&ensp;&ensp;然后将应用最小化到系统托盘，利用java.awt.SystemTray来实现。

<h3>多次启动</h3>
&ensp;&ensp;&ensp;&ensp;为了防止将一种应用lauch太多个实例，而将application子类写作单例类。application若多次新建stage，虽然属于一个应用，但是都调用show方法的话都会显示出来，如果从一个应用调用另一个应用需要注意这两点。可以在每次调用前stage.close()保证只有一个stage在展示，也可以使stage不变而改变scene和其中节点。

<h3>生命周期</h3>
&ensp;&ensp;&ensp;&ensp;application的生命周期是从launch到stop，在实现最小化时将stop改为hide，使得程序可以继续运行。值得一提的是，在本设计中（一种常用设计），从系统托盘打开的是设置窗口而不是ui窗口，所以系统托盘也应采用如上调整，防止打开多个应用。

<h2>IDEA+javafx+gradle项目bug记录</h2>
<font color=#333333 size=2>和javafx不一定有关系，顺便记一下</font>

<br></br>
<ul>
<li>
<code>Invalid gradle jdk configuration found</code>
和项目的java jdk版本不匹配
</li>
</ul>
