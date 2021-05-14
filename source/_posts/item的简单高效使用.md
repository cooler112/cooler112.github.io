---
title: item的简单高效使用
date: 2019-03-06 17:35:46
tags: item
categories: 编程工具
---

在项目开发中我们往往需要进行模型设计，为一个对象配置多个属性，以前的方法前后端都需要分别进行设置，往往还容易出错，重复编写，实际上谷歌早就提供了一套成熟可行的方法可以统一开发中的模型，那就是：
[Protobuf](https://developers.google.com/protocol-buffers/docs/proto?hl=zh-cn)

先在Github下载[源代码](https://github.com/protocolbuffers/protobuf)
下载后通过命令行进行安装：
    
     1 $ ./autogen.sh
      2 $ ./configure
      3 $ make
      4 $ make check
      5 $ sudo make install

安装耗时较多，完成最后一步后可以看到命令行中多了protoc这个命令，主要的作用是把proto源文件转化为目标文件（包括Java\python\oc\go）中的类型定义文件。
主要命令示例：
    
    //DIR为路径
    protoc --proto_path=$DIR --objc_out=$DIR  Define.proto
    
     --cpp_out=OUT_DIR           Generate C++ header and source.
     --csharp_out=OUT_DIR        Generate C# source file.
     --java_out=OUT_DIR          Generate Java source file.
     --js_out=OUT_DIR            Generate JavaScript source.
     --objc_out=OUT_DIR          Generate Objective C header and source.
     --php_out=OUT_DIR           Generate PHP source file.
     --python_out=OUT_DIR        Generate Python source file.
     --ruby_out=OUT_DIR          Generate Ruby source file.

以OC为例，转换成功后会生成.h和.m文件，把生成后的放入项目中，在项目Pod中引入：
  pod 'Protobuf', '~> 3.4.0'

如果手动加入需要添加:-fno-objc-arc  因为该类不支https://blog.csdn.net/u010019717/article/details/44830601持ARC
配置好会在项目中就可以直接使用该类了，特别方便。

关于proto书写格式
    
    syntax = "proto2";
    
    package XHR.Group;
    import "XHR.BaseDefine.proto";
    option optimize_for = LITE_RUNTIME;
    
    // CID_GROUP_REQ_GROUP_LIST             0x0301      获取群列表
    message XHRGroupListReq{
        	required string uid = 1;
        	required uint64 latest_update_time = 2;
    }
    
    // CID_GROUP_RSP_GROUP_LIST             0x0302   
    message XHRGroupListRsp{
    	    required XHR.BaseDefine.ResultType result_code = 1;
        required string result_string = 2;
        required string uid = 3;
        repeated XHR.BaseDefine.GroupInfo group_list = 4;
        required uint64 latest_update_time = 5;
    }

参考文章：
[Protocol Buffers(Protobuf)开发者指南---概览](https://blog.csdn.net/u010019717/article/details/44830573)
[Protobuf3语言指南](https://blog.csdn.net/u011518120/article/details/54604615#JSONMapping)
 [Protobuf 从入门到实战](https://www.cnblogs.com/NeilZhang/p/8410589.html)