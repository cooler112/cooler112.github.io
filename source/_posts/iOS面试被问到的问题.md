---
title: iOS面试被问到的问题
date: 2019-03-06 17:39:39
tags: iOS
categories: 苹果开发
---

近期面试问答汇总

###@property(nonatomic,getter=isOn) BOOL on; 中的getter = isOn的含义？
答：
如果这个property是 BOOL on， 那么Objc默认创建的 setter 为： - (void)on:(BOOL)setOn { } getter 为： - (BOOL)on { return on; } 但是你可以手动更改 setter 和 getter 方法，就像上面的： getter = xxxOn 的话， getter 就变为： - (BOOL)xxxOn { return on; }
同样setter也是一样的道理

###什么是内存管理机制
所谓内存管理就是所有权机制，对象被拥有的计算量不为0，才得以存在，不然被销毁。
alloc:分配内存，引用计算数为1
Copy:创造该对象复本，对该副本拥有并计数为1
Retain:对持有对象计数+1，当进行setter时会先判断该对象是否与原来一致
Release:销毁对象
autoRealease:系统自动在未来某个时段计数器-1
Strong:ARC引入属性，与retain一样，对对象持有，也就是在自身销毁同时，所持有对象也会销毁，可能会造成死锁。
Weak:ARC引入属性，只是引用对象并不将计数加1，前该对象被销毁后指针为空。

###比较WebView与UKWebView之间的区别
1. 在性能、稳定性、功能方面有很大提升（最直观的体现就是加载网页是占用的内存，模拟器加载百度与开源中国网站时，WKWebView占用23M，而UIWebView占用85M）；
2. 允许JavaScript的Nitro库加载并使用（UIWebView中限制）；
3. 支持了更多的HTML5特性；
4. 高达60fps的滚动刷新率以及内置手势；
5. 将UIWebViewDelegate与UIWebView重构成了14类与3个协议（查看苹果官方文档）
  window.webkit.messageHandlers.closeMe.postMessage(null);
  //OC注册供JS调用的方法
  [[_webView configuration].userContentController addScriptMessageHandler:self name:@"closeMe"];
  //OC在JS调用方法做的处理
- (void)userContentController:(WKUserContentController *)userContentController didReceiveScriptMessage:(WKScriptMessage *)message
  {
  NSLog(@"JS 调用了 %@ 方法，传回参数 %@",message.name,message.body);
  }
  //javaScriptString是JS方法名，completionHandler是异步回调block
  [self.webView evaluateJavaScript:javaScriptString completionHandler:completionHandler];

###数据库操作知道吗，你使用了哪些第三方的，有什么优势
苹果自带有coreData:CoreData是一个模型层的技术，也是一种持久化技术（数据库），它能将模型对象的状态持久化到磁盘里,其底层也是数据库sqlite的存储。
一般用第三方FMDB来自己sqlite的操作，为了保证线程安全，FMDB提供方便快捷的FMDatabaseQueue类
FMDatabaseQueue的创建 FMDatabaseQueue *queue = [FMDatabaseQueue databaseQueueWithPath:path];
简单使用 [queue inDatabase:^(FMDatabase *db) { [db executeUpdate:@"INSERT INTO t_student(name) VALUES (?)", @"Jack"]; [db executeUpdate:@"INSERT INTO t_student(name) VALUES (?)", @"Rose"]; [db executeUpdate:@"INSERT INTO t_student(name) VALUES (?)", @"Jim"];
以队列的方法添加操作，保证对数据库的操作不会出错。

###在OC中这些声明的作用，对对应的成员变量进行权限声明
@protected 该类和所有子类中的方法可以直接访问这样的变量。
@private 该类中的方法可以访问，子类不可以访问。
@public   可以被所有的类访问
@package 对framework而言内部使用，对外private，适合第三方静态库类

###为什么Block 要用Copy属性
Block一开始放在栈上的，而代码块内的数据会用到本地变量，只有Copy会才能放到堆上，而且本地变量要使用弱引用，retail不加1 

###为什么Delegate 不能用Strong,可以用weak,assign？
如果使用Strong,当两个对像互相把对方作为代理时，项目一个释放会引起另一个的释放，造成列循环。ARC引入strong和weak两个内存管理属性（以及__strong, __weak, __unsafe_unretained, __autoreleasing四个变量生命期qualifier）之后，对象的delegate成员变量就面临着对内存管理属性的选择：weak or assign
众所周知，weak属性的变量是不为其所属对象持有的，并且在该变量被销毁之后，此weak变量的值会自动被赋值为nil。而assign属性一般是对C基本数据类型成员变量的声明，当然也可以用在对象类型成员变量上，只是其代表的意义只是单纯地拷贝所赋值变量的值。即如果对某assign成员变量B赋值某对象A的指针，则此B只是简单地保存此指针的值，且并不持有对象A，也就意味着如果A被销毁，则B就指向了一个已经被销毁的对象，如果再对其发送消息会引发崩溃。
但在delegate成员变量这个细分领域，我们即可以用weak，又可以用assign。因为在几乎所有场景下，delegate所指向的对象C的生存期都是覆盖了delegate成员变量本身所在的对象D的生存期的，所以，在D的生存期内，C所使用的D的指针都是有效的，所以这个时候使用assign是没有关系的。

###什么是NSLoop?用在哪些地方
* RunLoop，是多线程的法宝，即一个线程一次只能执行一个任务，执行完任务后就会退出线程。主线程执行完即时任务时会继续等待接收事件而不退出。非主线程通常来说就是为了执行某一任务的，执行完毕就需要归还资源，因此默认是不运行RunLoop的；

* 每一个线程都有其对应的RunLoop，只是默认只有主线程的RunLoop是启动的，其它子线程的RunLoop默认是不启动的，若要启动则需要手动启动；

* 在一个单独的线程中，如果需要在处理完某个任务后不退出，继续等待接收事件，则需要启用RunLoop；

* NSRunLoop提供了一个添加NSTimer的方法，可以指定Mode，如果要让任何情况下都回调，则需要设置Mode为Common模式；

* 实质上，对于子线程的runloop默认是不存在的，因为苹果采用了懒加载的方式。如果我们没有手动调用[NSRunLoop currentRunLoop]的话，就不会去查询是否存在当前线程的RunLoop，也就不会去加载，更不会创建。

###说一说你项目用到的混合加密及信息通信安全机制 
每次App启动先生成一个随机的DES密钥A，然后加密要传输的字段后保存在字典中，将DES密钥用AES公钥加密B后保存在字典中。后台用私钥解密出DES密钥后再用来解密传输字段，最后得出原始数据并保存该加密B与对应的DES密钥A
后面使用HTTPS进行通信加密，使用公证的证书最为安全。

###如何保证在数据传输中不被重放攻击
以时间戳作为传参，后台协商响应时间差范围，参考三次握手协议两边商量序列号，当发过来的序列号为服务器也存在的序列号则丢弃。

###四种设计模式：单例模式，MVC，委托和观察者模式
单例：UIApplication，UserDefault,UIAccelerometer,NSNotification,NSFileManager,NSBundle
委托：委托对象主要对控件对象的操作和状态作出响应，数据源委托是必须实现的
观察者模式四个组成部分：
抽象主题：观察者容器，添加移除及向观察者发送通知
抽象观察者：是一个协议，可以更新对象
具体观察者：具体实现
具体主题：SubScript协议实现
具体应用:通知与KVO（对象属性发生变化时通知给观察者对象）

###MVC模式：
Model:保存应用数据状态，回应视图状态查询，处理应用业务逻辑，完成应用功能，将状态变化通知视图
View:为用户展示信息提供接口，通过视图向控制器发出请求，向模型发出数据查询
Controller:接收用户请求，更新模型数据，更新所对应视图状态响应用户请求，作为视图和模型的媒介，降低耦合度，权责清晰提高开发效率

###Iphone 与iPad区别控件：iPad独有UIPoperViewController UISpiltController

###分层架构设计：
表示层：界面显示
业务逻辑层：处理表示层提供数据并返回结果到表示层进行显示
数据持久层：进行本地或网络访问
信息系统层，存在本地或网络的信息

###Textkit为程序员提供文字排版和渲染功能，主要实现图文混排的功能

###数据持久化方式
沙箱目录 
属性列表
对象归档(将对象进行序列化成为文件)
sqlite
CoreData(对象关系映射技术，也是SQLite)

###
XML是一种自描述的数据交换格式，两种读取方式：SAX（从上到下，只读，速度快）和DOM （节点方式可更改，要先读完后才能操作）系统自带NSXMLParse,第三方GDataXML
Json:轻量级数据交换格式，自带NSJsonSerliazation，最快，处理相当麻烦，第三方JsonKit，SBJson

###HTTP与HTTPS的区别
HTTP:80  
HTTPS:超文本文件传输安全协议：443   SSL：40位关键字 RC4流加密算法

###Git操作
Git添加到工作区：git add
Git提交到master:  git commit -m “”
Git上传到目标库：git push --set-upstream iOSMVCTemple master
Git添加远程目标：git remote add name gitAddress

###封装，继承，多态的意义
封装：对名隐藏细节，保证数据不被破坏，使代码模块化
继承：代码重用，方便子类扩展
多态：允许用父类指针指向子类，因为子类实现对父类方法的重写，所以对同一消息有不同响应
前两者实现对代码的重用，最后个实现对接口的重用。

###浅复制和深复制的区别？
浅层复制：只复制指向对象的指针，而不复制引用对象本身。对于要进行拷贝的对象，自身要实现NSCoding协议 -initWithZone:(NSZone)Zone

###类别优劣？
category 可以在不获悉，不改变原来代码的情况下往里面添加新的方法，只能添加，不能删除修改。
并且如果类别和原来类中的方法产生名称冲突，则类别将覆盖原来的方法，因为类别具有更高的优先级。

### KVO与 KVC
kvc:键 - 值编码是一种间接访问对象的属性使用字符串来标识属性，而不是通过调用存取方法，直接或通过实例变量访问的机制。
很多情况下可以简化程序代码。apple文档其实给了一个很好的例子。
kvo:键值观察机制，当被观察的某一属性变化可进行响应

###为什么说oc是动态运行时语言？
答案：多态。 主要是将数据类型的确定由编译时，推迟到了运行时。
简单来说，运行时机制使我们直到运行时才去决定一个对象的类别，以及调用该类别对象指定方法。

###说说推送的实现原理
当我们选择接收远程远程推送的时候，系统将应用BundleId和UUID发送到苹果自己的APNS服务器进行唯一设备和唯一App的注册，服务器进行注册后返回Tocken作为访问令牌，用户服务器通过推送证书和得到的Tocken向APNS请求发送推送消息，APNS服务器收到请求后进行列表查找然后向指定设备发送消息。

###单例的核心是什么 
保证实例对象只被初始化一次，并在整个程序周期中反复使用

###讲讲网络接口编程是什么 
好好学习后再写

###什么是多线程
针对计算机多核设计的一套并发操作，多个任务同时进行，目前iOS上的多线程操作包括:NSThread,NSOperation,GCD,其中苹果推荐使用GCD
###App的性能优化可以从哪方面入手
正确重用Cell，图片缓存，避免加载大的Xib文件，不要把主线程放到block里面，用好多线程，选择合理的方式进行数据的持久化，使用ARC,autoPool
View尽量使用不透明的，使用gzip获取大量数据，解压工作放在后台，尽量避免格式转换一定要用可以使用单例，重用大开销对象，，使用好Cache,重用延时加载Views,处理内存警告，避免反复使用或处理数据，使用wkWeb加载数据
###SDWebImage的实现原理
主要运用来加载网络图片，根据网络请求先去内存查找对应的图片，然后去硬盘（如果设置的话），如果都没有去网络下载放到缓存，下次直接本地加载,使用NSCache作为缓存，异步操作，在回调中处理结果，使用NSOperation回调结果。

Jsonkit(Json格式转换器)
MJRefresh:刷新工具
MJExtention:数模转换
Masonry：约束布局
FMDB:sqlite数据器操作封闭
UShare:友盟第三方分享工具
ShareSDK:Mob第三方分享
JPush:极光推送
Open SSl:加密库
微信支付SDK
支付宝SDK
SVProgressAssistant:加载框
MBProgressAssistant:加载框
ImageBrowerVC:图片展示器
IQKeyboardManager:文本输入自己调整屏幕
DQAlertView:应用Model弹框
BlocksKit:代码块方式实现控件消息响应
KYVedioPlayer:第三方播放器
UIView+RSAdditions：视图定位器
UITableView+FDTemplateLayoutCell：TableViewCell高度自动计算器
KAlertView:弹框
AFNetworking:第三方网络库
BaiduMap:百度地图库
SDScrollView：图片轮播
LBXScanView:二维码扫描
RongIMKit:融云通信
AliyunOSSiOS:阿里云数据上传库