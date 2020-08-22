---
layout:     post
title:      "SnackBar"
date:       2020-8-22 14:12:12
author:     "Chen"
header-img: "img/post-bg-miui6.jpg"
tags:
    - 原创
    - js
---
> snackbar 简明介绍

## 什么是snackbar

Toast，相信大家都不陌生。而最近出来的snackbar可以说是Toast的升级版。
snackbar特点：
> 一小段时间之后、或者用户与屏幕触发交互，Snackbar 会自动消失。

而更强大的是，js也行的通：
我们可以通过一个小实例来学习：
```js
function myFunction() {
    var x = document.getElementById("snackbar")
    x.className = "show";
    setTimeout(function(){ x.className = x.className.replace("show", ""); }, 3000);
}
```

下面是h5与css：
```html
//html
<button onclick="myFunction()">显示 Snackbar</button>
<div id="snackbar">一些文本..</div>
```

</br>

```css
//css
#snackbar {
    visibility: hidden;
    min-width: 250px;
    margin-left: -125px;
    background-color: #333;
    color: #fff;
    text-align: center;
    border-radius: 2px;
    padding: 16px;
    position: fixed;
    z-index: 1;
    left: 50%;
    bottom: 30px;
    font-size: 17px;
}

#snackbar.show {
    visibility: visible;
    -webkit-animation: fadein 0.5s, fadeout 0.5s 2.5s;
    animation: fadein 0.5s, fadeout 0.5s 2.5s;
}

@-webkit-keyframes fadein {
    from {bottom: 0; opacity: 0;} 
    to {bottom: 30px; opacity: 1;}
}

@keyframes fadein {
    from {bottom: 0; opacity: 0;}
    to {bottom: 30px; opacity: 1;}
}

@-webkit-keyframes fadeout {
    from {bottom: 30px; opacity: 1;} 
    to {bottom: 0; opacity: 0;}
}

@keyframes fadeout {
    from {bottom: 30px; opacity: 1;}
    to {bottom: 0; opacity: 0;}
}
```
