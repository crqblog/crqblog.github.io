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
