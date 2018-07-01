---
title: "使用ng-animate为网页增加动画效果"
slug: 'test-slug'
date: 2018-06-24T15:50:06+08:00
draft: false
author: 'allen'
disqusIdentifier: 123
---

AngularJS 中提供了ngAnimate模块，可以为网页提供动画效果。

典型的应用就是视图切换和元素添加与移除。

这里以ui-view 和 ng-repeat指令作为展示。
<!--more-->
首先需要引入我们需要的js文件

```js
<script src="../angular.js"></script>
<script src="../angular-ui-router.js"></script>
<script src="../angular-animate.js"></script>
```

再引入我们需要的模块：`ui.router`和`ngAnimate`。

```js
angular.module("app", ['ui.router', 'ngAnimate'])
```

然后我们可以正常编写我们的应用，我们这里做的额外工作只是编写css文件。

只编写样式就可以了？实际上，$animate服务本身支持几个内置的指令，比如ng-repeat, ng-show, ng-view等。而它的本质只是为其在视图变化期间添加了额外的CSS样式。

对于添加元素事件会添加`ng-enter`和`ng-enter-active`样式类，对于移除元素会添加`ng-leave`和`ng-leave-active`样式。其中前者样式相当于初始化元素样式，后者则对应实际的动画样式。

举个例子：
```
<div>
  <h1>Nihao</h1>
</div>
```

{{< codeblock "archives.css" "css" "http://underscorejs.org/#compact" "archives.css" >}}
li{
    transition: all 5.3s ease-in-out;
}

li.ng-enter{
    opacity: 0;
    transform:translateY(100%);
}
li.ng-enter.ng-enter-active{
    opacity: 1;
    transform:translateY(0);
}
li.ng-leave{
    opacity: 1;
    transform:translateY(0);
}
li.ng-leave.ng-leave-active{
    opacity: 0;
    transform:translateY(100%);
}
{{< /codeblock >}}
对应的效果就是：
![这里写图片描述](/images/201806/1.gif)

ui-view也是一样，实际上它保留了2个ui-view元素，一个对应将展示的节点，一个对应将移除的节点。

```css
[ui-view].ng-enter,
[ui-view].ng-leave {
    box-sizing: border-box;
    position: absolute;
    width: 100%;
    transition: all .3s ease-in-out;
}

[ui-view].ng-enter {
    opacity: 0;
    transform: scale3d(.6, .6, .6);
}

[ui-view].ng-enter-active {
    opacity: 1;
    transform: scale3d(1, 1, 1);
}

[ui-view].ng-leave {
    opacity: 1;
    transform: scale3d(1, 1, 1);
}

[ui-view].ng-leave-active {
    opacity: 0;
    transform: scale3d(.6, .6, .6);
}
```
效果就是这样的
![这里写图片描述](/images/201806/2.gif)

审查元素会发现以上4种样式。
![这里写图片描述](/images/201806/3.png)

以上。
掌握这些技巧我们就可以为应用添加简单实用的网页动画效果。