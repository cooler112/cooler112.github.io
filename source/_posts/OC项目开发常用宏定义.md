---
title: OC项目开发常用宏定义
date: 2019-03-06 17:40:09
tags: iOS
---

---
title: OC项目开发常用宏定义
date: 2017-02-25 15:40:37
tags:
---

```
#define WS(weakSelf)  __weak __typeof(self)weakSelf = self; //__typeof() 声明数据类型
#define DEF [NSUserDefaults standardUserDefaults]

//屏幕适配 间距设置
#define HORIZ_5 AUTO_WIDTH(5)
#define HORIZ_10 AUTO_WIDTH(10)
#define VERTICAL_5  AUTO_HIGHT(5)
#define VERTICAL_10  AUTO_HIGHT(10)

//指定某设计图尺寸确定高度或指按屏幕比例放缩
#define IMGHEIGHT_720(x) (x/720.0f*Main_Screen_Width)
//#deine IMGHEIGHT(x)(y) (y/x*AUTO_WIDTH(x))

//设备尺寸
#define iphone4x_3_5 ([UIScreen mainScreen].bounds.size.height==480.0f)
#define iphone5x_4_0 ([UIScreen mainScreen].bounds.size.height==568.0f)
#define iphone6_4_7 ([UIScreen mainScreen].bounds.size.height==667.0f)
#define iphone6Plus_5_5 ([UIScreen mainScreen].bounds.size.height==736.0f || [UIScreen mainScreen].bounds.size.height==414.0f)
#define IMAGEINDEX Main_Screen_Width / 720.0f

//应用框架尺寸
#define  NAVHEIGHT 64
#define TABBARHEIGHT 40

//app 尺寸宏定义
#define Main_Screen_Height [[UIScreen mainScreen] bounds].size.height //主屏幕的高度
#define Main_Screen_Width  [[UIScreen mainScreen] bounds].size.width  //主屏幕的宽度
/*** KeyWindow Height Width */
#define KeyWindow_Height [[[UIApplication sharedApplication] keyWindow] frame].size.height //KeyWindow的高度
#define KeyWindow_Width  [[[[UIApplication sharedApplication] keyWindow] frame].size..width  //KeyWindow的宽度
#define AUTO_WIDTH(number)   (number) / 375.0 *  CGRectGetWidth([UIScreen mainScreen].bounds)
#define AUTO_HIGHT(number)   (number) / 667.0 *  CGRectGetHeight([UIScreen mainScreen].bounds)

#define AUTO_WIDTH1080(number)   (number) / 540.0 *  CGRectGetWidth([UIScreen mainScreen].bounds)
#define AUTO_HIGHT1920(number)   (number) / 960.0 *  CGRectGetHeight([UIScreen mainScreen].bounds)
//当前版本
#define FSystenVersion            ([[[UIDevice currentDevice] systemVersion] floatValue])
#define AppVersion              ([[[NSBundle mainBundle] objectForInfoDictionaryKey:@"CFBundleShortVersionString"] floatValue])

// 字符串去空格
#define strTrimming(x) [x stringByTrimmingCharactersInSet:[NSCharacterSet whitespaceCharacterSet]]
```

#颜色字号定义
```
#define COLORWITHRGB(r,g,b,a) [UIColor colorWithRed:r/255.0 green:g/255.0 blue:b/255.0 alpha:a]
//主题色
#define STATUS_BAR_COLOR [UIColor colorWithRed:255/255.0 green:56/255.0 blue:61/255.0 alpha:1]
//#define TINY_COCLOR [UIColor colorWithRed:244/255.0 green:120/255.0 blue:0/255.0 alpha:1]
#define TINY_COCLOR [UIColor colorWithRed:255/255.0 green:56/255.0 blue:61/255.0 alpha:1]
#define TINY_LIGHT_COLOR UIColorFromRGB(0xff9b9e)

#define BACKGROUNDCOLOR [UIColor colorWithRed:243/255.0 green:243/255.0 blue:243/255.0 alpha:1]

#define RGBCOLOR(r,g,b) [UIColor colorWithRed:(r)/255.0 green:(g)/255.0 blue:(b)/255.0 alpha:1]
#define RGBACOLOR(r,g,b,a) [UIColor colorWithRed:(r)/255.0 green:(g)/255.0 blue:(b)/255.0 alpha:(a)]
#define ARC_COLOR RGBCOLOR(arc4random()%255, arc4random()%255, arc4random()%255)
#define KdarkGayColor RGBCOLOR(50, 50, 50)//深灰
#define KlightGayColor  RGBCOLOR(220, 220,220)//浅灰
#define KtextGayColor UIColorFromRGB(0x616161)
#define darkf4 UIColorFromRGB(0xf4f4f4)
#define dark444 UIColorFromRGB(0x444444)
#define dark999 UIColorFromRGB(0x999999)
#define dark666 UIColorFromRGB(0x666666)
#define darkf3f UIColorFromRGB(0xf3f3f3)

#define FONT(x) [UIFont systemFontOfSize:x]
#define FONT_B(x) [UIFont boldSystemFontOfSize:x]

#define FONT_10   [UIFont systemFontOfSize:10]
#define FONT_10_B [UIFont boldSystemFontOfSize:10]

#define FONT_12   [UIFont systemFontOfSize:12]
#define FONT_12_B [UIFont boldSystemFontOfSize:12]

#define FONT_14   [UIFont systemFontOfSize:14]
#define FONT_14_B [UIFont boldSystemFontOfSize:14]

#define FONT_16   [UIFont systemFontOfSize:16]
#define FONT_16_B [UIFont boldSystemFontOfSize:16]

#define FONT_18   [UIFont systemFontOfSize:18]
#define FONT_18_B [UIFont boldSystemFontOfSize:18]
//适配字体
#define SizeScale ((KeyWindow_Height > 568) ? KeyWindow_Height/568 : 1)
#define FONTNEW(x) [UIFont systemFontOfSize:x * SizeScale]
#define FONTNEW_B(x) [UIFont boldSystemFontOfSize:x *SizeScale]

#define FONTNEW_10   FONTNEW(10)
#define FONTNEW_10_B FONTNEW_B(10)

#define FONTNEW_12   FONTNEW(12)
#define FONTNEW_12_B FONTNEW_B(12)

#define FONTNEW_14   FONTNEW(14)
#define FONTNEW_14_B FONTNEW_B(14)

#define FONTNEW_16   FONTNEW(16)
#define FONTNEW_16_B FONTNEW_B(16)

#define FONTNEW_18   FONTNEW(18)
#define FONTNEW_18_B FONTNEW_B(18)

#define SizeScale1920 ((KeyWindow_Height > 960) ? KeyWindow_Height/960 : 1)
#define FONTNEW1080(x) if(iphone6Plus_5_5){return [UIFont systemFontOfSize:x * 1.15 / 3];}
#define FONTNEW_B1920(x) [UIFont boldSystemFontOfSize:x *SizeScale]

//RGB颜色转换（16进制->10进制）
#define UIColorFromRGB(rgbValue)    [UIColor colorWithRed:((float)((rgbValue & 0xFF0000) >> 16))/255.0 green:((float)((rgbValue & 0xFF00) >> 8))/255.0 blue:((float)(rgbValue & 0xFF))/255.0 alpha:1.0]

#define lightgrayColor  UIColorFromRGB(0xe8e8e8)
#define mostlightgrayColor  UIColorFromRGB(0xf3f3f3)
#define slivergrayColor  UIColorFromRGB(0xc0c0c0)
#define darkgrayColor  UIColorFromRGB(0x444444)
#define mostdarkgrayColor  UIColorFromRGB(0x999999)
#define darkmiddleColor UIColorFromRGB(0x666666)
#define bluemiddleColor UIColorFromRGB(0x00a0ec)
#define grayCCCCC UIColorFromRGB(0xcccccc)

#define LOADIMAGE(file) [[UIImage imageWithContentsOfFile:[[NSBundle mainBundle]pathForResource:file ofType:@"png"]] imageWithRenderingMode:UIImageRenderingModeAlwaysOriginal]
#define LOADIMAGECACHES(file) [UIImage imageNamed:file]
#define PLACEHOLDER_IMAGE    LOADIMAGECACHES(@"duoduo_gray")

#endif

```