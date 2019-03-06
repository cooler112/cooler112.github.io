---
title: 好分期
date: 2019-03-06 15:25:30
tags: 项目经历
---



# 好分期后台管理iOS端维护要点总结：



{% asset_img 1.png  %}

项目概况：主要为后台审核人员操作手机端操作，已经有人开发得差不多了，所以我的工作主要是维护，在维护中学到了些新东西，总结下

好分期后台管理iOS端开发总结：
**标准化开发，明确你每句代码的意图**

在前人做了详细备注的基础下，代码一看就懂，没有丝毫入坑的感觉，数据的收发非常的规范，而且后期的扩展相对轻松，不经感叹做好项目代码记录是规范化备注是多么重要的一件事情，不过也不一定是每句代码都 要说明 点什么，除非你是新手第一次接手项目。另外发现几个稍微有点欠妥的地方，一是把网络请求接口直接写在项目代码里面不分层虽然方便了，但是后台如果要统一改接口名称 要一个个去找，不是很方便 。二是搜索这个控件在取消的时候并没进行重新请求（已经修改）。界面全部采用TableView作为基础在Cell上布局控件，这种做法让我耳目一新，但是模块化的效果好很明显。不过重复控件太多，有些可以通过Cell重用实现的。还有就是在加载的时候如果网络出现问题，用户只能等待，这样的体验不是很好，这点也是我以后写代码要注意的地方。这款App主要的功能作用是显示数据，复杂的计算和操作后台都处理好了，所以项目并不算大。维护起来也很轻松

**键盘弹出界面自动移动防止遮挡**

		///IQKeyboardManager:自动处理键盘事件的第三方库
		
		​    IQKeyboardManager *manager = [IQKeyboardManager sharedManager];
		
		​    manager.enable = YES;//控制整个功能是否启用
		
		​    manager.shouldResignOnTouchOutside = YES;//控制点击背景是否收起键盘
		
		​    manager.shouldToolbarUsesTextFieldTintColor = YES;//控制键盘上的工具条文字颜色是否用户自定义
		
		​    manager.enableAutoToolbar = NO;//控制是否显示键盘上的工具条
		
		​    manager.preventShowingBottomBlankSpace = NO;//防止IQKeyboardManager让rootview上滑过度,默认是YES

**IPS****不用第三方可以手动进行采取上传到服务器，用于点对点推送：** 

  //注册UserNotification,以获取推送通知的权限

		​    UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound | UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
		
		​    [application registerUserNotificationSettings:settings];
		
		​    //注册远程推送
		
		​    [application registerForRemoteNotifications];
		
		​    
		
		​    // Override point for customization after application launch.
		
		​    return YES;
		
		}
		
		– (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {//处理推送消息
		
		​    NSLog(@”userinfo：%@”, userInfo);
		
		​    NSLog(@”收到推送消息：%@”, [[userInfo objectForKey:@”aps”] objectForKey:@”alert”]);
		
		}
		
		///如果注册失败，比如没有证书等等调用
		
		– (void)application:(UIApplication *)application didFailToRegisterForRemoteNotificationsWithError:(NSError *)error {
		
		​    NSLog(@”远程通知注册失败：%@”, error);
		
		}
		
		///用户同意后，会调用此程序，获取系统的deviceToken，应把deviceToken传给服务器保存，此函数会在程序每次启动时调用(前提是用户允许通知)
		
		– (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
		
		​    //NSLog(@”获取到的Token值为：%@”, deviceToken);
		
		​    [Defaults setObject:deviceToken forKey:@”deviceToken”];//Token值，用于登录的时候向后台发送用户对应的设备，方便针对进行推送
	
			}	

**强制更新模块：本地调用 版本号与服务器返回版本号对比大小进行控制** 

		– (void)versionUpdate:(double)versionInfo {
		
		​    ///系统版本更新
		
		​    NSDictionary *infoDictionary = [[NSBundle mainBundle] infoDictionary];
		
		​    NSString *app_Version = [infoDictionary objectForKey:@”CFBundleShortVersionString”];//app版本
		
		​    
		
		​    if (versionInfo > [app_Version doubleValue]) {
		
		​        UIAlertController *alert = [UIAlertController alertControllerWithTitle:@”提示” message:@”有新版本请立即更新” preferredStyle:UIAlertControllerStyleAlert];
		
		​        UIAlertAction *firstAction = [UIAlertAction actionWithTitle:@”立即更新” style:UIAlertActionStyleDefault handler:^(UIAlertAction *action) {
		
		​            [[UIApplication sharedApplication] openURL:[NSURL URLWithString:@”https://www.pgyer.com/obUA”]];
		
		​        }];
		
		​        [alert addAction:firstAction];
		
		​        [self presentViewController:alert animated:YES completion:nil];
		
	​    }
	
	}

**关于列表的动态添加或删除**

对于TableView或CollectionView 的操作，从网络获取列表数据后，可以直接在本地列表进行操作，后台只需要返回成都或失败即可，没有必要去重新请求，刷新列表

**将上传图片加入主线程队列进行，防止阻断，界面更新放到放线程进行**

​		项目概况：主要为后台审核人员操作手机端操作，已经有人开发得差不多了，所以我的工作主要是维护，在维护中学到了些新东西，总结下

好分期后台管理iOS端开发总结：
**标准化开发，明确你每句代码的意图**

在前人做了详细备注的基础下，代码一看就懂，没有丝毫入坑的感觉，数据的收发非常的规范，而且后期的扩展相对轻松，不经感叹做好项目代码记录是规范化备注是多么重要的一件事情，不过也不一定是每句代码都 要说明 点什么，除非你是新手第一次接手项目。另外发现几个稍微有点欠妥的地方，一是把网络请求接口直接写在项目代码里面不分层虽然方便了，但是后台如果要统一改接口名称 要一个个去找，不是很方便 。二是搜索这个控件在取消的时候并没进行重新请求（已经修改）。界面全部采用TableView作为基础在Cell上布局控件，这种做法让我耳目一新，但是模块化的效果好很明显。不过重复控件太多，有些可以通过Cell重用实现的。还有就是在加载的时候如果网络出现问题，用户只能等待，这样的体验不是很好，这点也是我以后写代码要注意的地方。这款App主要的功能作用是显示数据，复杂的计算和操作后台都处理好了，所以项目并不算大。维护起来也很轻松

**键盘弹出界面自动移动防止遮挡**

		///IQKeyboardManager:自动处理键盘事件的第三方库
		
		​    IQKeyboardManager *manager = [IQKeyboardManager sharedManager];
		
		​    manager.enable = YES;//控制整个功能是否启用
		
		​    manager.shouldResignOnTouchOutside = YES;//控制点击背景是否收起键盘
		
		​    manager.shouldToolbarUsesTextFieldTintColor = YES;//控制键盘上的工具条文字颜色是否用户自定义
		
		​    manager.enableAutoToolbar = NO;//控制是否显示键盘上的工具条
		
		​    manager.preventShowingBottomBlankSpace = NO;//防止IQKeyboardManager让rootview上滑过度,默认是YES

**IPS****不用第三方可以手动进行采取上传到服务器，用于点对点推送：** 

		  //注册UserNotification,以获取推送通知的权限
		
		​    UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound | UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
		
		​    [application registerUserNotificationSettings:settings];
		
		​    //注册远程推送
		
		​    [application registerForRemoteNotifications];
		
		​    
		
		​    // Override point for customization after application launch.
		
		​    return YES;
		
		}
		
		– (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {//处理推送消息
		
		​    NSLog(@”userinfo：%@”, userInfo);
		
		​    NSLog(@”收到推送消息：%@”, [[userInfo objectForKey:@”aps”] objectForKey:@”alert”]);
		
		}
		
		///如果注册失败，比如没有证书等等调用
		
		– (void)application:(UIApplication *)application didFailToRegisterForRemoteNotificationsWithError:(NSError *)error {
		
		​    NSLog(@”远程通知注册失败：%@”, error);
		
		}
		
		///用户同意后，会调用此程序，获取系统的deviceToken，应把deviceToken传给服务器保存，此函数会在程序每次启动时调用(前提是用户允许通知)
		
		– (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
		
		​    //NSLog(@”获取到的Token值为：%@”, deviceToken);
		
		​    [Defaults setObject:deviceToken forKey:@”deviceToken”];//Token值，用于登录的时候向后台发送用户对应的设备，方便针对进行推送
		
		}
		
		**强制更新模块：本地调用 版本号与服务器返回版本号对比大小进行控制** 
		
		– (void)versionUpdate:(double)versionInfo {
		
		​    ///系统版本更新
		
		​    NSDictionary *infoDictionary = [[NSBundle mainBundle] infoDictionary];
		
		​    NSString *app_Version = [infoDictionary objectForKey:@”CFBundleShortVersionString”];//app版本
		
		​    
		
		​    if (versionInfo > [app_Version doubleValue]) {
		
		​        UIAlertController *alert = [UIAlertController alertControllerWithTitle:@”提示” message:@”有新版本请立即更新” preferredStyle:UIAlertControllerStyleAlert];
		
		​        UIAlertAction *firstAction = [UIAlertAction actionWithTitle:@”立即更新” style:UIAlertActionStyleDefault handler:^(UIAlertAction *action) {
		
		​            [[UIApplication sharedApplication] openURL:[NSURL URLWithString:@”https://www.pgyer.com/obUA”]];
		
		​        }];
		
		​        [alert addAction:firstAction];
		
		​        [self presentViewController:alert animated:YES completion:nil];
	
	​    }
	
	}

**关于列表的动态添加或删除**

对于TableView或CollectionView 的操作，从网络获取列表数据后，可以直接在本地列表进行操作，后台只需要返回成都或失败即可，没有必要去重新请求，刷新列表

**将上传图片加入主线程队列进行，防止阻断，界面更新放到放线程进行**

		  dispatch_async(dispatch_get_global_queue(0, 0), ^{
		
		   队列操作。。。        
		
		​        [Service serviceWithJAVAUrl:@”” params:params images:imgArr message:@”” controller:self succeedBlock:^(id response) {
		
		​            dispatch_async(dispatch_get_main_queue(), ^{
		
		​             
		
		​            });
		
		​        } failBlock:^{
		
		​            dispatch_async(dispatch_get_main_queue(), ^{
		
		​            });
		
		​        }];
		
		​    });
		
		带图片带参数AFNetworking上传:
		
		\+ (void)serviceWithUrl:(NSString *)url
		
		​                params:(NSDictionary *)params
		
		​                images:(NSArray *)images
		
		​               message:(NSString *)message
		
		​            controller:(id)controller
		
		​          succeedBlock:(void (^) (id response))succeedBlock
		
		​             failBlock:(void (^) (void))failBlock
		
		{
		
		​    AFHTTPRequestOperationManager *manager = [AFHTTPRequestOperationManager manager];
		
		//设置可以接收的数据类型
		
		​    manager.responseSerializer.acceptableContentTypes = [NSSet setWithObjects:@”application/json”, @”text/json”, @”text/javascript”, @”text/html”, nil];
		
		//设置是否对发送数据进行Json格式化
		
		​      //manager.requestSerializer=[AFJSONRequestSerializer serializer];
		
		//报头标记，只是作为双方识别的记号而已
		
		​    [manager.requestSerializer setAuthorizationHeaderFieldWithUsername:@”RqPs” password:@“***********”];
		
		​    
		
		​    if (![message isEqualToString:@””]) {
		
		​        [SVProgressHUD showWithStatus:message maskType:SVProgressHUDMaskTypeBlack];
		
		​    }
		
		​    
		
		​    NSString *URL = [NSString stringWithFormat:@”%@%@”,BASEURL,url];
		
		​    [manager POST:URL parameters:params constructingBodyWithBlock:^(id<AFMultipartFormData> formData) {
		
		​        //[SVProgressHUD dismiss];
		
		​        
		
		​        NSMutableArray *arr = [[NSMutableArray alloc] init];
		
		​        for (int i = 0; i < images.count; i++) {
		
		​            NSDictionary *image = images[i];
		
		​            NSString *fileName = image.allKeys[0];
		
		​            int nameCount = 0;
		
		​            for (NSString *str in arr) {
		
		​                if ([str containsString:image.allKeys[0]]) {
		
		​                    nameCount++;
		
		​                    ///图片等比例压缩
		
		​                }
		
		​            }
		
		​            
		
		​            ///重名 添加后缀
		
		​            if (nameCount != 0) {
		
		​                fileName = [NSString stringWithFormat:@”%@%d”, image.allKeys[0], nameCount+1];
		
		​            }
		
		​            
		
		​            NSDateFormatter *formatter = [[NSDateFormatter alloc] init];
		
		​            [formatter setDateFormat:@”yyyyMMddHHmmssSSS”];
		
		​            NSString *dateTime = [formatter stringFromDate:[NSDate date]];
		
		​            [arr addObject:[NSString stringWithFormat:@”%@_%@”, fileName, dateTime]];
		
		​        }
		
		​        
		
		​       for (int i = 0; i < images.count; i++) {
		
		​           NSDictionary *image = images[i];
		
		​           [formData appendPartWithFileData: UIImageJPEGRepresentation(image.allValues[0], 0.0) name:arr[i] fileName:[arr[i] stringByAppendingFormat:@”.png”] mimeType:@”image/png”];
		
		​       }
		
		​        
		
		​    } success:^(AFHTTPRequestOperation *operation, id responseObject) {
		
		​        [SVProgressHUD dismiss];
		
		​        NSLog(@”%@”, responseObject);
		
		​        
		
		​        NSDictionary *result = responseObject;
		
		​        if (![[NSString stringWithFormat:@”%@”, result[@”Flag”]] isEqualToString:@”1″]) {
		
		​            [ExtensionMethod simpleAlertWithMessage:responseObject[@”Message”] controller:controller handler:^{
		
		​                if (failBlock == NULL) {
		
		​                    return;
		
		​                }
		
		​                failBlock();
		
		​            }];
		
		​            return;
		
		​        } else if (result == nil) {
		
		​            [ExtensionMethod simpleAlertWithMessage:@”后台服务异常，请稍后再试” controller:controller handler:nil];
		
		​            return;
		
		​        }
		
		​        
		
		​        succeedBlock(responseObject);
		
		​    } failure:^(AFHTTPRequestOperation *operation, NSError *error) {
		
		​        [SVProgressHUD dismiss];
		
		​        if (failBlock) {
		
		​            [ExtensionMethod simpleAlertWithMessage:@”网络异常，请稍后再试” controller:controller handler:^{
		
		​                if (failBlock == NULL) {
		
		​                    return;
		
		​                }
	
	​                failBlock();
	
	​            }];
	
	​        }
	
	​    }];
	
	}

​	

另外使用了比较好用的第三方控件：RMPickerViewController第三方选择器，UUID设备唯一标记方法