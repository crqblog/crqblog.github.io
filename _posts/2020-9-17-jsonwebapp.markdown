---
layout:     post
title:      "Web App构建"
subtitle:      "App而非A-P-P"
date:       2020-9-17 14:12:12
author:     "Chen"
header-img: "img/post-bg-miui6.jpg"
tags:
    - 原创
    - Web
---
> Web App构建

## Json
在GitHub Pages制作Web App十分简单，可是首先，你要先建立文件/pwa/manifest.json

**note：你可以更改文件名称，但是随后步骤也需更改！**

实例代码：
```json
{
  "name": "Name",
  "short_name": "Name",
  "description": "My first web app",
  "icons": [{
    "src": "imgs/example.png",
    "sizes": "128x128",
    "type": "image/png"
  }, {
    "src": "imgs/example2.png",
    "sizes": "512x512",
    "type": "image/png"
  }],
  "background_color": "#fff",
  "theme_color": "#000",
  "start_url": "/",
  "display": "standalone",
  "orientation": "portrait"
}
```

## 引入文件
最重要的一点来了

请在你的html页面的head标签中加入这句语句：

```js
<link rel="manifest" href="{{ site.baseurl }}/pwa/manifest.json"> // 如果你没有使用liquid（大括号使用的语句），请把site指令替换为你网站主页的URL（根域名）example：https//crq.js.org 不要使用https//crq.js.org/example类型的URL
```

## 收工
进入自己的页面刷新首页，当你再次试图添加书签到主屏幕时，即可创建Web App！
