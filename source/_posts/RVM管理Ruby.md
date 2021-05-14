---
title: RVM管理Ruby
date: 2019-03-06 17:31:03
tags: rvm
categories: 编程工具
---

---
title: RVM管理Ruby
date: 2017-03-20 16:03:50
tags: 命令
---

###安装RVM

```
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
\curl -sSL https://get.rvm.io | bash -s stable
```

###使用rvm管理Ruby 

列出已知的 Ruby 版本  

```
rvm list known  
```
安装一个 Ruby 版本

```  
rvm install 2.2.0 --disable-binary  
```
这里安装了最新的 2.2.0, rvm list known 列表里面的都可以拿来安装。  
切换 Ruby 版本  

```
rvm use 2.2.0  
```
如果想设置为默认版本，这样一来以后新打开的控制台默认的 Ruby 就是这个版本

```  
rvm use 2.2.0 --default   
```
查询已经安装的ruby  
rvm list  
卸载一个已安装版本  

```
rvm remove 1.8.7  
```
###gemset 的使用
RVM 不仅可以提供一个多 Ruby 版本共存的环境，还可以根据项目管理不同的 gemset.  
gemset 可以理解为是一个独立的虚拟 Gem 环境，每一个 gemset 都是相互独立的。  
比如你有两个项目，一个是 Rails 2.3 一个是 rails3. gemset 可以帮你便捷的建立两套 Gem 开发环境，并且方便的切换。  
gemset 是附加在 Ruby 语言版本下面的，例如你用了 1.9.2, 建立了一个叫 rails3 的 gemset,当切换到 1.8.7 的时候，rails3 这个 gemset 并不存在。  
建立 gemset  

```
rvm use 1.8.7  
rvm gemset create rails23  
```
然后可以设定已建立的 gemset 做为当前环境
use 可以用来切换语言或者 gemset
前提是他们已经被安装(或者建立)。并可以在 list 命令中看到。

```
rvm use 1.8.7
rvm use 1.8.7@rails23
```
然后所有安装的 Gem 都是安装在这个 gemset 之下。
列出当前 Ruby 的 gemset

```
rvm gemset list
```
清空 gemset 中的 Gem
如果你想清空一个 gemset 的所有 Gem, 想重新安装所有 Gem，可以这样

```
rvm gemset empty 1.8.7@rails23
```
删除一个 gemset

```
rvm gemset delete rails2-3
```
项目自动加载 gemset
RVM 还可以自动加载 gemset。 例如我们有一个 Rails 3.1.3 项目，需要 1.9.3 版本 Ruby，整个流程可以这样。

```
rvm install 1.9.3
rvm use 1.9.3
rvm gemset create rails313
rvm use 1.9.3@rails313
```
下面进入到项目目录，建立一个 .rvmrc 文件。
在这个文件里可以很简单的加一个命令：

```
rvm use 1.9.3@rails313
```
然后无论你当前 Ruby 设置是什么，cd 到这个项目的时候，RVM 会帮你加载 Ruby 1.9.3 和 rails313 gemset.