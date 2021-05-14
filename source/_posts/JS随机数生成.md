---
title: JS随机数生成
date: 2021-01-09 18:11:51
tags: js
categories: 前端开发
---

在前端调试时、有时需要判断是否同时收到两条相同通知，除了用毫秒及时间判断，还可以用随机数

使用Math函数解决

```
//Math 对象方法：
Math.ceil();  //向上取整。
Math.floor();  //向下取整。
Math.round();  //四舍五入。
Math.random();  //0.0 ~ 1.0 之间的一个伪随机数。【包含0不包含1】 //比如0.8647578968666494
//实例说明：
Math.ceil(Math.random()*10);      // 获取从1到10的随机整数 ，取0的概率极小。
Math.round(Math.random());   //可均衡获取0到1的随机整数。
Math.floor(Math.random()*10);  //可均衡获取0到9的随机整数。
Math.round(Math.random()*10);  //基本均衡获取0到10的随机整数
生成[n,m]的随机整数的函数

//生成从minNum到maxNum的随机数
function randomNum(minNum, maxNum) {
  switch (arguments.length) {
    case 1:
      return parseInt(Math.random() * minNum + 1, 10);
      break;
    case 2:
      return parseInt(Math.random() * ( maxNum - minNum + 1 ) + minNum, 10);
      //或者 Math.floor(Math.random()*( maxNum - minNum + 1 ) + minNum );
      break;
    default:
      return 0;
      break;
  }
} 
Math.random() 生成 [0,1) 的数，所以 Math.random()*5 生成 {0,5) 的数。
parseInt() 可以简单理解成返回舍去参数的小数部分后的整数，所以 parseInt(Math.random()*5) 生成的是 [0,4] 的随机整数。
```

