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

而更强大的是，js也行的通！
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
<button onclick="myFunction()">显示 Snackbar</button>
<div id="snackbar">一些文本..</div>
```


```css
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

## 应用
我的博客开始添加了snackbar来显示更新提醒，但由于添加了看版娘组件但是又懒得修改，只得狠心删除。给大家贴一下源码吧
```js
var createSnackbar = (function() {
  var previous = null;
  return function(config) {
    var message = config.message,
      actionText = config.actionText,
      action = config.action,
      duration = config.duration;

    if (previous) {
      previous.dismiss();
    }
    var snackbar = document.createElement('div');
    snackbar.className = 'paper-snackbar';
    snackbar.dismiss = function() {
      this.style.opacity = 0;
    };
    var text = document.createTextNode(message);
    snackbar.appendChild(text);
    if (actionText) {
      if (!action) {
        action = snackbar.dismiss.bind(snackbar);
      }
      var actionButton = document.createElement('button');
      actionButton.className = 'action';
      actionButton.innerHTML = actionText;
      actionButton.addEventListener('click', action);
      snackbar.appendChild(actionButton);
    }
    setTimeout(function() {
      if (previous === this) {
        previous.dismiss();
      }
    }.bind(snackbar), duration || 5000);
    
    snackbar.addEventListener('transitionend', function(event, elapsed) {
      if (event.propertyName === 'opacity' && this.style.opacity == 0) {
        this.parentElement.removeChild(this);
        if (previous === this) {
          previous = null;
        }
      }
    }.bind(snackbar));


    
    previous = snackbar;
    document.body.appendChild(snackbar);
getComputedStyle(snackbar).bottom;
    snackbar.style.bottom = '0px';
    snackbar.style.opacity = 1;
  };
})();
```
【ps：这段代码源于codepen.io,也希望大家支持一下他们哟！】
## Android
**既然Web上行得通，那么，在其它环境呢？**
我们就拿安卓系统来举例吧

```js
Snackbar.make(view, message, duration)
        .setAction(action message, click listener)
        .show();
```

这是一个标准的snackbar，但是
首先，你要准备XML于Java文件：

```js
<android.support.design.widget.CoordinatorLayout
      android:id="@+id/layout"
      android:layout_width="match_parent"
      android:layout_height="match_parent">
  </android.support.design.widget.CoordinatorLayout>
```



```js
Snackbar.make(mLayout, "Message", Snackbar.LENGTH_LONG).setAction("按钮", new View.OnClickListener() {
                    @Override
                    public void onClick(View v) {
                    }
                }).show();

```

【ps：在编写前，别忘记找到你app的build gradle文件，并加入 **compile 'com.android.support:design:23.4.0'** 这一串compile语句】

## 总结
snackbar在编程领域可以说是一个分界点，标志着技术的进步，也相信通过我们各个开发者的努力，会做的更好。我也会持续为大家更新技术博文哦，谢谢大家！

