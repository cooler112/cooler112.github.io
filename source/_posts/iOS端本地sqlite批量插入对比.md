---
title: iOS端本地sqlite批量插入对比
date: 2019-03-06 17:42:54
tags: iOS
categories: 苹果开发
---

###1、Sqlite优势明显
iOS端本地数据库一般用sqlite,而且相对于plist、userdefault、文本存储等，使用数据库方便大量数据的操作，而且与后台数据库具有一致性，减少中间不必要的转换，适应能力强。配合FMDB来使用，非常的方便，有一点需要在App内部空间创建.sqlite文件，如果去包含资源文件是可读不可写的。
###2、什么文件适合数据库
对于常见的行政区域，由于可能会出现数据相应的调整，虽然不是很频繁，但是如果保存在本地会影响相关的业务。比如成都这几年分出了天府新区，郫县改为了区，谁能保证以后会不会还有大动作，所以从后台获取较妥，为了避免不必要的数据请求，App启动前可以进行版本检查，判断是否对某些文件进行更新。
###3、放在数据库要注意的事情 
  . 数据库句柄的引用和关闭，每次打开是要判断是否数据库可用，用完后即时关闭，避免资源占用
  . 可以独立出来统一管理，比如通知消息一般会存数据库，那么通知的增删查改可以放数据库，地址查对应省市区也可以，可以采用一个单例来统一管理.
  . 性能和效率

      dispatch_queue_t queue = dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0);
            dispatch_sync(queue, ^{
                [dataBase open];
                for (NSInteger index = 0; index < contentArr.count; index++) {
                    NSDictionary *dic = [contentArr objectAtIndex:index];
                    BOOL resulat = [dataBase executeUpdate:@"INSERT INTO address(L0_CMT,L0_ID,L1_CMT,L1_ID,L2_CMT,L2_ID,L3_CMT,L3_ID,P_ID) VALUES(?,?,?,?,?,?,?,?,?);",[dic objectForKey:@"L0_CMT"]
                                    ,[dic objectForKey:@"L0_ID"]
                                    ,[dic objectForKey:@"L1_CMT"]
                                    ,[dic objectForKey:@"L1_ID"]
                                    ,[dic objectForKey:@"L2_CMT"]
                                    ,[dic objectForKey:@"L2_ID"]
                                    ,[dic objectForKey:@"L3_CMT"]
                                    ,[dic objectForKey:@"L3_ID"]
                                    ,[dic objectForKey:@"P_ID"]];
                    if (resulat) {
                    }
                }
                [dataBase close];
      );
如上图所示看似没有问题，实际上暗茂杀机。之前使用dispatch_async来进行异步数据操作完成批量数据写入，但是运行时报错无法打开数据库句柄，推断数据库是线程安全，不允许多个线程同时对其进行操作，所以对数据库的操作应该放在主线程中。

问题又来了，放在主线程通过全局串行队列进行的时候，可能会导致操作卡顿，因为省市区几千条数据，我是循环插入的，那该怎么办，于是有了后面的批量插入，效率快多了

             [dataBase setShouldCacheStatements:YES];//是否应该缓存插入描述
                static NSString *insertSQLStatment = @"INSERT INTO address(L0_CMT,L0_ID,L1_CMT,L1_ID,L2_CMT,L2_ID,L3_CMT,L3_ID,P_ID) VALUES(?,?,?,?,?,?,?,?,?);";
                [dataBase beginTransaction]; //启动事务
                for (NSDictionary *dic in contentArr)
                {
                    [dataBase executeUpdate:insertSQLStatment withArgumentsInArray:@[
                                                                                     [dic objectForKey:@"L0_CMT"]
                                                                                     ,[dic objectForKey:@"L0_ID"]
                                                                                      ,[dic objectForKey:@"L1_CMT"]
                                                                                     ,[dic objectForKey:@"L1_ID"]
                                                                                     ,[dic objectForKey:@"L2_CMT"]
                                                                                     ,[dic objectForKey:@"L2_ID"]
                                                                                     ,[dic objectForKey:@"L3_CMT"]
                                                                                     ,[dic objectForKey:@"L3_ID"]
                                                                                    ,[dic objectForKey:@"P_ID"]]
                                                                                     ];
                }
                [dataBase commit]; //开始执行
                [dataBase close];

事务对于大批量操作太管用了，主要是快，这样就算有阻塞，时间短得可怜，用户无法察觉。

欢迎讨论交流