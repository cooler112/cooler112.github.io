---
title: hexi_assist
date: 2019-03-06 15:24:06
tags: 项目经历
---

# 和商助手开发记录

{% asset_img 1.png 产品图片 %}

### 项目概况：

和商助手是和系的商家端，和系是个类似小京东的平台，助手是为了帮助商家进行发货，与买家互动、提现等一系列操作。功能相对简单，但是比较实用。个人负责和商助手新模块的开发与对现有模块进行功能优化，负责实现美工设计界面，负责与后台沟通接收网络数据，按进度完成开发任务。

主要包括了下面一系列功能：

1、免费开店，操作简单，只要两步就能开店。

2、管理方便，随时随地添加商品、查看并处理订单。

3、提现周期短，申请提现后1-2个工作日到账。

4、快捷分享，一键分享商品到微信、QQ等多个平台

 

### 项目难点：

商品上传模块过于复杂，技术不成熟代码也写得最复杂。这是我写过的最艰难的代码，可能确定内功不够，模块的设计也是不成功，技术上受限制，想采用Masonry的技术来实现。

1、实现商品上传，有图有没有图是两种不一样的显示状态，自己还运用了Masonry的动态进行实现。

2、要实现类别联动，也就是选择一个父类后要显示对应的子类，如果没有父类则显示默认，选择还需要选择变动请求网络，所以独立出来了一个模块

3、标签多种选择，一个类别有几个规格，比如尺寸有：大中小，颜色有红黄绿，最开始产品设计不能满足产品多样规格的需求，后面我们虽然即时想去了列表显示的方式解决问题，但是所有商品使用同一个规格表，导致哪怕是新加一个商品，都要做选择，只有一两个属性还好，想想20多个属性去选择是什么概念，每点一个要显示出来，每个列表的规格值还可以动态添加或者删除，另外提交的时候要去判断是不是该商品所有的规格选中了，没有选择还要提示，另外如果商品没有设置规格那么使用另外一种方式显示。总之逻辑上就够你确定半天了。技术上当时最让我头痛的就是不断增加的属性列表，以及最后的提交计算，你可能觉得可能没那么复杂。但是涉及到TableViewCell不动态刷新，Masonry动态添加删除控件，以及20多个属性的组合，就有点让人觉得疯狂了，最好还是做出来了，但是不想再去看第二眼，大大小小的各类模块和不规范的代码让自己读起来都有点吃力。程序设计一定要严谨。

 

### 二：动态图文列表

要做到图文混排，很多人觉得可能TableView就可以了，但是TableView不好处理单位Cell的长度增长，就是我在中间的文字区域编辑，内容增加或减少引起的行变化。TableView每次都得去刷新，非常麻烦，而且刷新你是不能编辑的，也就是刷新的时候没有输入焦点，无法输入。图片好处理，文字的动态变化非常伤脑筋。幸好当时深入研究了Masonry的约束规则，采用了约束的办法动态调整TextView的高度变化，还可以在文字删除完毕时把对应的TextView也干掉，比较合适的解决了这个问题。后面我发现这方面处理的最好的是wordpress的App版本，采用JS与html交互的方式，可能对文字加粗变长斜之类的，非常方便。功能非常强大，关系是完成后直接生成html代码，方便Web直接使用。非常完善的解决了这个需求。后面自己的项目也想接入这个模块用于发布文章，无奈老是有那么几个链接错误找不到原因解决。后面要尝试解决。

### 三：没有做本地缓存和缺少有效通知机制

虽然有WebImageChache这个类别减少图片的请求，但每次进入首页都要请求一次各种消息：比如商户帮助文字、用户是否有某个状态更改了，非常的消耗流量，特别是帮助，并不是经常更新的东西，安全可以采用本地缓存加通知更新的方式解决，特别是把推送和本地数据库的功能用好，采用Version判断是不是要更新某个信息，重新请求。包括和系在内都可以采用这种方式减少不必要的流量消耗，当时提出来了，可惜由于各种原因，最终没有实现。

总的来说和商助手基本满足用户使用需求，但是技术和设计上还有许多要改进优化的地方。

{% asset_img 2.jpg 产品图片 %}

{% asset_img 3.jpg 产品图片 %}

{% asset_img 4.jpg 产品图片 %}

