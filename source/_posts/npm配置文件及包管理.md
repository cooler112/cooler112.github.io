---
title: npm配置文件及包管理
date: 2021-01-09 18:32:00
tags:
---

npm全局配置文件可以通过以下命令进行查找

```
npm config get userconfig  *## 查看配置文件路径
```

作为全局配置

还可以在Node项目中添加.npmrc作为项目配置

**config常用命令**

```
npm config ls -l  *##　查看所有配置项* npm config get cache  *## 查看缓存配置，get后面可以跟任意配置项* npm config edit  *## 直接编辑config文件，这个会打开文本*
```

**配置文件内容**

```
registry=https://registry.npm.taobao.org/    //下载源

@yh:registry=http://*****										//私有仓库
	
home=https://www.npmjs.org

ELECTRON_MIRROR=https://npm.taobao.org/mirrors/electron/

//registry.npm.taobao.org/:_password="bnBtUEBzc3cwcmQxMjM="

//registry.npm.taobao.org/:username=cooler112

//registry.npm.taobao.org/:email=971656743@qq.com

//registry.npm.taobao.org/:always-auth=false

//registry.npmjs.org/:_authToken=7cbacf76-47c5-480d-aaba-7d26d75e356f

prefix=/Users/smithcool/.nvm/versions/node/v10.15.3		//npm下载包保存路径
```



npm查看本地包版本号和远程包的版本号
npm 查看远程包
第一种方法:
```
npm info <packageName>
```

第二种方法:
```
npm view <packageName> versions --json
```
npm查看本地安装的包版本号
```
npm ls <packageName>        // 本地包
npm ls <packageName> -g     // 全局安装包
```
npm语义化版本号

npm使用 a.b.c 的版本号来管理安装包，a为达版本号，有重大api改变，一般不向下兼容，b为小版本号，新增功能，向下兼容，c为补丁号，通常修复一些bug。npm安装包的时候允许使用一些特殊符号表示安装的版本范围，如：
```
~a.b.c :    取最新的c的版本号值，a与b保持不变
^a.b.c :    取b和c均为最新版本号，a保持不变
```