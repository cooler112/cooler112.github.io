---
title: iOS_AlertController使用方法
date: 2019-03-06 17:39:50
tags: iOS
---

###UIAlertController是iOS8引入的新特性，可以使用它代替AlertView或ActionSheet，主要方法如下：
```
#import <UIKit/UIViewController.h>

NS_ASSUME_NONNULL_BEGIN
//定义每个选项的特性（默认、取消、红色标记按钮）
typedef NS_ENUM(NSInteger, UIAlertActionStyle) {
    UIAlertActionStyleDefault = 0,
    UIAlertActionStyleCancel,	
    UIAlertActionStyleDestructive
} NS_ENUM_AVAILABLE_IOS(8_0);
//定义弹出框样式
typedef NS_ENUM(NSInteger, UIAlertControllerStyle) {
    UIAlertControllerStyleActionSheet = 0,
    UIAlertControllerStyleAlert
} NS_ENUM_AVAILABLE_IOS(8_0);

NS_CLASS_AVAILABLE_IOS(8_0) @interface UIAlertAction : NSObject <NSCopying>
//初始化每个按钮选项
+ (instancetype)actionWithTitle:(nullable NSString *)title style:(UIAlertActionStyle)style handler:(void (^ __nullable)(UIAlertAction *action))handler;

@property (nullable, nonatomic, readonly) NSString *title;
@property (nonatomic, readonly) UIAlertActionStyle style;
@property (nonatomic, getter=isEnabled) BOOL enabled;

@end

NS_CLASS_AVAILABLE_IOS(8_0) @interface UIAlertController : UIViewController
//初始化弹出框
+ (instancetype)alertControllerWithTitle:(nullable NSString *)title message:(nullable NSString *)message preferredStyle:(UIAlertControllerStyle)preferredStyle;

- (void)addAction:(UIAlertAction *)action;
@property (nonatomic, readonly) NSArray<UIAlertAction *> *actions;

@property (nonatomic, strong, nullable) UIAlertAction *preferredAction NS_AVAILABLE_IOS(9_0);
- (void)addTextFieldWithConfigurationHandler:(void (^ __nullable)(UITextField *textField))configurationHandler;
@property (nullable, nonatomic, readonly) NSArray<UITextField *> *textFields;

@property (nullable, nonatomic, copy) NSString *title;
@property (nullable, nonatomic, copy) NSString *message;

@property (nonatomic, readonly) UIAlertControllerStyle preferredStyle;

@end

NS_ASSUME_NONNULL_END
```
添加方法：

```
-(void)alertControllerShow{
    UIAlertController *alertController = [UIAlertController alertControllerWithTitle:@"好分期" message:@"非常好的投资平台" preferredStyle:UIAlertControllerStyleAlert];
    [alertController addTextFieldWithConfigurationHandler:^(UITextField * _Nonnull textField) {
        NSLog(@"%@",textField.text);
        textField.placeholder = @"addSomeText";
    }];
    
    UIAlertAction *cancelAction = [UIAlertAction actionWithTitle:@"取消" style:UIAlertActionStyleCancel handler:nil];
    [alertController addAction:cancelAction];
    
    UIAlertAction *signAction = [UIAlertAction actionWithTitle:@"签到" style:UIAlertActionStyleDefault handler:^(UIAlertAction * _Nonnull action) {

    }];
    [alertController addAction:signAction];
    
    UIAlertAction *changePasswordAction = [UIAlertAction actionWithTitle:@"修改密码" style:UIAlertActionStyleDefault handler:^(UIAlertAction * _Nonnull action) {
    }];
    [alertController addAction:changePasswordAction];
    
    NSString *cachesPath = [CacheOperation getCachesPath];///获得缓存路径
    float cacheSize = [CacheOperation getCacheSizeAtPath:cachesPath];///获得缓存大小
    if (cacheSize > 10.0) {///如果缓存大于10M则显示清除缓存按钮
        UIAlertAction *clearCacheAction = [UIAlertAction actionWithTitle:[NSString stringWithFormat:@"清除缓存 - %.2fM", cacheSize] style:UIAlertActionStyleDefault handler:^(UIAlertAction * _Nonnull action) {
            [CacheOperation clearCacheAtPath:cachesPath];///清除缓存
        }];
        [alertController addAction:clearCacheAction];
    }
    
    UIAlertAction *exitLoginAction = [UIAlertAction actionWithTitle:@"退出登录" style:UIAlertActionStyleDestructive handler:^(UIAlertAction * _Nonnull action) {
        //UIAlertActionStyleDestructive：毁灭性按钮，红色标注

    }];
    [alertController addAction:exitLoginAction];
    
    [self presentViewController:alertController animated:YES completion:nil];
}
```


###不同于UIAlertView,ActionSheet要去设置委托，代码块方式直接使用，非常方便