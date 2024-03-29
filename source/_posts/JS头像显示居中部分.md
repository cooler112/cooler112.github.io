---
title: JS头像显示居中部分
date: 2021-01-09 18:38:28
tags: JS
categories: 前端开发
---



在图片全屏轮播时，为了兼容更大的屏幕，我们常常把图片设置为很大，但是在显示的过程中，如果让图片随浏览器自动变化的话，常常会把图片压缩变形，影响显示，在不压缩图片的情况下，如何只显示图片的中间部分呢？
目前提供两种解决方案：

方案一：引入css

```
.parent {
    position: relative;
    overflow: hidden;
 　　width:400px;
　 　height:300px;
}

.child {
    position: absolute;
    top: -9999px;
    bottom: -9999px;
    left: -9999px;
    right: -9999px;
    margin: auto;

}


相应的html代码为：
<!DOCTYPE html>
<html lang="en">
　　<head>
　　<meta charset="UTF-8">
　　<title>Document</title>
　　<style type="text/css">
　　　　.parent {
　　　　　　position: relative;
　　　　　　overflow: hidden;
　　　　　　height: 300px;
　　　　　　width: 400px;
　　　　}
　　　　.child {
　　　　　　position: absolute;
　　　　　　top: -9999px;
　　　　　　bottom: -9999px;
　　　　　　left: -9999px;
　　　　　　right: -9999px;
　　　　　　margin: auto;
　　　　}
　　</style>
</head>
<body>
<div class="parent">
　　<img class="child" src="http://c11.eoemarket.com/upload/apps/2013/0420/131329/screenshots/21bf3021-aeef-4dbf-fd5c-6dd7c24cb1f3.jpg">
</div>
</body>
</html>
```

方案二：

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        body{
            text-align: center;
        }
        .container{
            width: 100%;
            height: 400px;
            margin: 0 auto;
            overflow: hidden;
        }
        .container img{
            margin: 0 -100% 0 -100%;
            vertical-align: top;
        }
    </style>
</head>
<body>
    <!-- 屏幕的放大或缩小都不会压缩里面的图片，里面的图片一直会在内容区域居中显示 -->
    <div class="container">
        <img src="http://a.hiphotos.baidu.com/zhidao/pic/item/72f082025aafa40fa38bfc55a964034f79f019ec.jpg" alt="">
    </div>
</body>
</html>
```

