---
title: git操作
date: 2019-03-06 17:29:56
tags: 编程工具
---



#重要性说明
Git作为目前项目版本管理的工具，其先进性和便捷性不言而喻，所以一定要深入掌握才行，这样对以后的管理非常方便。主要实现的功能
* 个人或团队开发项目管理
* 项目版本恢复或指定版本打包
* 最近才经历过的用cocopod打包自己的插件作为私有库要用到tag标记版本号
* 目前Jenkins通过git源代码提取来进行打包
* iOS个人开发的各种第三方库的引入

#重要性补充说明
* 使用码云进行私有库管理，可以创建组织和公司
* 复制Github上优秀的项目
* 公司GitLab项目维护管理

#Git的通用操作
##Git工具命令安装下载

    brew install git //Mac安装    
    yum install git-core//CentOS
    apt-get install git//Ubuntu
##Git克隆Git库的办法是

    git clone <#库地址>     
    库地址包括有HTTPS的和SSH的
    ssh://diaoyu@120.40.160.80:2222/home/Product/fishing.git
    https://github.com/cooler112/Cooler

##自建Git库

    git init  <仓库名称,以.git结尾规范>
    git init -bare <仓库名称> //创建裸仓库，没有工作区间，防止有人登录服务器去改文件

##忽略提交的部分文件

    ##以JAVA项目为例
    target/
    !.mvn/wrapper/maven-wrapper.jar
    ### STS ###
    .apt_generated
    .classpath
    .factorypath
    .project
    .settings
    .springBeans
    .sts4-cache
    ### IntelliJ IDEA ###
    .idea
    *.iws
    *.iml
    *.ipr
    ### NetBeans ###
    nbproject/private/
    build/
    nbbuild/
    dist/
    nbdist/
    .nb-gradle/
***以下为忽略规则***

    # 此为注释 – 将被 Git 忽略
    # 忽略所有 .a 结尾的文件
    *.a
    # 但 lib.a 除外
    !lib.a
    # 仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
    /TODO
    # 忽略 build/ 目录下的所有文件
    build/
    # 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
    doc/*.txt
    # 忽略 doc/ 目录下所有扩展名为 txt 的文件
    doc/**/*.txt

##从拷贝到提交单人简单操作

    git add *  git add *  添加到缓存区
    git commit -m “”  提交
    git remote add origin <仓库名称>
    git push --set-upstream origin master  //直接提交到远程仓库或
    git push -u origin master //功能同上

##撤消功能的使用：reset,checkout,--amend

    ##已经commit 添加备注后发现还需要更改，更改完成后调用可以修改备注内容，push时只算作一次
    git commit —amend
    ##将Add的文件从暂存区撤回到工作区
    git reset filename
    ##将工作区的文件恢复到初始状态
    git checkout filename
    ##回恢到某次提交
    git reset --hard ******//操作之前先处理好未提交文件
    git fsck --lost-found //在.git/lost-found找到只添加未提交的文件集
    git reflog//查看提交记录

##远端仓库的操作git remote
    git remote //列出所有
    git remote show <分支名>//查看状态
    git remote add <分支名称>  <分支地址>
    git remove rename //改名，本地也会一一对应
    git remote rm <分支名>  //某个分支不再维护或不再贡献
    git pull   <分支名,默认master>//自动合并远端与目前的对应分支

  ##标签操作
标签是在commit 过后才进行的操作，在提交的时候需要指定分支和标签号才后有作用，标签相当于某一提交操作的快照

    git tag //简单标签
    git tag -a "0.0.1" -m " <标签内容>
    git tag -a 0.0.1 <某次提交编号>
    git push origin 0.0.1  //标签生效

 ##分支操作
分支主要用于开发新版本而保证正式版本不受干扰或者Bug修复，主要操作是合并,在分支合并前清空暂存区

    git branch //查看所有，-v 查看详情 --merged 查看合并分支 --unmerged查看未合并
    git branch <新分支名>
    git checkout <分支名>切换分支
    git checkout -b <新分支名>//分支并切换
    git merge <分支名>//进行合并 
    git branch -d //删除分支
    git checkout -b awesomeBranch origin/awesomebranch   //将远程分支拷贝到本地新建分支
    git checkout --track origin/awesomebranch//同上
   git push origin :awesomebranch//删除远程分支，比如已经合并到master   