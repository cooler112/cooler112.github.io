---
title: npm npm link使用方法
date: 2021-01-16 14:10:57
tags: npm
categories: 前端开发
---

 初始链接模块修改main文件指向当前运行主文件，不是打包文件目录
 ```
 从dist/index.js改为src/main.js
 ```


1. 项目和模块在同一个目录下，可以使用相对路径
```
npm link ../module
```



2. 项目和模块不在同一个目录下

cd到模块目录，



```
npm link，进行全局link
```
cd到项目目录
```
npm link 模块名(package.json中的name)
```
3. 解除link

解除项目和模块link，项目目录下
```
npm unlink 模块名
```
解除模块全局link，模块目录下
```
npm unlink 模块名
```