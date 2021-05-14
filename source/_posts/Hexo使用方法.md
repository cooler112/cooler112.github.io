---
title: Hexo使用方法
date: 2019-03-06 15:25:21
tags: 项目
categories: 博客建站
---


Hexo静态博客工具基于先安装node.js  
什么是Node.js:  
Node.js® is a JavaScript runtime built on Chrome's V8 JavaScript engine. Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient. Node.js' package ecosystem, npm, is the largest ecosystem of open source libraries in the world.
![Node.js是一个Javascript运行环境(runtime)。实际上它是对Google V8引擎进行了封装。V8引 擎执行Javascript的速度非常快，性能非常好。](http://baike.baidu.com/link?url=SyWoc-jV1q9IBR9lG6X1vII3xPpd0MGrorW2H5Y_I-Hy0Ba-DEIIuPaMk1WTLrpjyfdrUhP_27Ulhl72mLNd__)
使用brew快速安装  
brew install node.js  

安装Hexo工具(NPM是随同NodeJS一起安装的包管理工具)  

```
npm install -g hexo-cli --no-optional  
```
创建hexo博客位置 
```
Mkdir  ~/Document/blog
```
进行初始化
Hexo init 

## Praperation
Install [Nodejs](https://nodejs.org/en/) or Use Command 
###安装主题

```
git clone https://github.com/wizardforcel/hexo-theme-cyanstyle.git themes/cyanstyle
```
修改 Hexo 的 _config.yml 中的 theme 为 cyanstyle。

```dzh
$ brew install nodejs
```
Welcome to [Hexo](https://hexo.io/)! This is your very first post. Check [documentation](https://hexo.io/docs/) for more info. If you get any problems when using Hexo, you can find the answer in [troubleshooting](https://hexo.io/docs/troubleshooting.html) or you can ask me on [GitHub](https://github.com/hexojs/hexo/issues).

## Quick Start

### Command for Hexo
```dzh
Usage: hexo <command>

Commands:
clean     Removed generated files and cache.
config    Get or set configurations.
deploy    Deploy your website.
generate  Generate static files.
help      Get help on a command.
init      Create a new Hexo folder.
list      List the information of the site
migrate   Migrate your site from other system to Hexo.
new       Create a new post.
publish   Moves a draft post from _drafts to _posts folder.
render    Render files with renderer plugins.
server    Start the server.
version   Display version information.

Global Options:
--config  Specify config file instead of using _config.yml
--cwd     Specify the CWD
--debug   Display all verbose messages in the terminal
--draft   Display draft posts
--safe    Disable all plugins and scripts
--silent  Hide output on console

For more help, you can use 'hexo help [command]' for the detailed information
or you can check the docs: http://hexo.io/docs/
```

For more help, you can use 'hexo help [command]' for the detailed information
or you can check the docs: http://hexo.io/docs/

### Create a new post

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

### Run server

``` bash
$ hexo server
```

More info: [Server](https://hexo.io/docs/server.html)

### Generate static files

``` bash
$ hexo generate
```

More info: [Generating](https://hexo.io/docs/generating.html)

### Deploy to remote sites

``` bash
$ hexo deploy
```

More info: [Deployment](https://hexo.io/docs/deployment.html)



Welcome to [Hexo](https://hexo.io/)! This is your very first post. Check [documentation](https://hexo.io/docs/) for more info. If you get any problems when using Hexo, you can find the answer in [troubleshooting](https://hexo.io/docs/troubleshooting.html) or you can ask me on [GitHub](https://github.com/hexojs/hexo/issues).

## Quick Start

### Create a new post

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

### Run server

``` bash
$ hexo server
```

More info: [Server](https://hexo.io/docs/server.html)

### Generate static files

``` bash
$ hexo generate
```

More info: [Generating](https://hexo.io/docs/generating.html)

### Deploy to remote sites

``` bash
$ hexo deploy
```

More info: [Deployment](https://hexo.io/docs/deployment.html)
