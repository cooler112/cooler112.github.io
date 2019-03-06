---
title: OC常用格式检查
date: 2019-03-06 17:40:22
tags: iOS
---

---
title: OC常用格式检查
date: 2017-03-01 16:16:14
tags:
---
要点：

1. 在textField或者TextView进行输入时一般会进行输入时检查
2. 点击提交的时候会进行手机号之类的格式验证
3. 邮箱身份证验证
4. 数据类型判断
5. 小数判断
6. 时间格式转换

```
//
//  FormatAssistant.h
//  HexiShop
//
//  Created by Smith Cool on 16/8/18.
//  Copyright © 2016年 Xiaohr. All rights reserved.
//

#import <Foundation/Foundation.h>

@interface FormatAssistant : NSObject

//输入检查input开头
//类型检查is开头
#pragma mark ---------------------手机号phone--------------------------------

/**
 *  @author Xiao  Huarong, 16-08-18 16:08:42
 *
 *  针对手机号码输入的格式检查
 *
 *  @param BOOL number 逐步输入手机号
 *
 *  @return 正确返回yes，错误返回NO
 */
+ (BOOL)inputValidatePhoneNumber:(NSString*)number;

/**
 *  @author Xiao  Huarong, 16-08-18 16:08:40
 *
 *  手机号码是否合法格式检查
 *
 *  @param BOOL phoneNumber
 *
 *  @return 不合法返回YES，合法返回NO
 */
+(BOOL)phoneNumberisWrong:(NSString *)phoneNumber;

/**
 *  @brief 手机空格格式检查并返回值
 *
 *  @param phoneNumber 手机号
 *
 *  @return 是：有错
 */
+(BOOL)phoneNumberisWrongWithAll:(NSString *)phoneNumber;

/**
 *  @author Xiao  Huarong, 16-08-18 16:08:33
 *
 *  针对座机号码输入的格式检查
 *
 *  @param NSString zjNumber
 *
 *  @return BOOL
 */
+ (BOOL)inputZuoJiNumberisWrong:(NSString*)zjNumber;


#pragma mark -------------------------类型检查----------------------------------------
/**
 *  @author Xiao  Huarong, 16-08-18 16:08:29
 *
 *  是否为浮点型
 *
 *  @param string floatNumber
 *
 *  @return 为浮点型返回YES，否则返回NO
 */
+ (BOOL)isPureFloat:(NSString*)floatNumber;

/**
 *  @author Xiao  Huarong, 16-08-18 16:08:48
 *
 *  是否为整型
 *
 *  @param string intNumber
 *
 *  @return BOOL 是返回YES，否则返回NO
 */
+ (BOOL)isPureInt:(NSString*)intNumber;

/**
 *  @author Xiao  Huarong, 16-08-18 17:08:57
 *
 *  两位小数输入限制（必须与UITextFieldDelegate Change代理同用）
 *
 *  @param String xiaoshuStr 输入的数字
 *  @param NSRange  rang    输入的变化
 *  @return BOOL
 */
+(BOOL)inputXiaoshuValidate:(NSString *)xiaoshuStr stringConfig:(NSString *)string shouldChangeCharactersInRange:(NSRange)range weishuConfig:(NSInteger)weishu;

/**
 *  @author Xiao  Huarong, 16-08-18 16:08:49
 *
 *  针对输入金额的格式检查
 *
 *  @param NSString moneyStr
 *
 *  @return BOOL
 */
+ (BOOL)inputMoneyFormat:(NSString*)moneyStr;

#pragma mark -------------------------密码检查password----------------------------------------
/**
 *  @author Xiao  Huarong, 16-08-18 16:08:13
 *
 *  常规密码检查（6到20位大小数字）
 *
 *  @param BOOL passWordStr
 *
 *  @return BOOL
 */
+ (BOOL)passwordNormalisRight:(NSString *)passWordStr;
/**
 *  @author Xiao  Huarong, 16-08-18 16:08:20
 *
 *  密码输入格式检查 ^[a-zA-Z0-9|,|.|_|!|?]
 *
 *  @param String passwordInputStr
 *
 *  @return BOOL
 */
+ (BOOL)inputPasswordisRight:(NSString*)passwordInputStr;


#pragma mark -------------------------自定义格式检查----------------------------------------
/**
 *  @author Xiao  Huarong, 16-08-18 16:08:13
 *
 *  自定义符串类型检查 店铺名称检查（^[_|A-Za-z0-9\u4E00-\u9FA5_-]+$"）
 *
 *  @param String passWordStr
 *  @param String regix 匹配符
 *
 *  @return BOOL
 */
+ (BOOL)stringFormatisRight:(NSString *)string withRegix:(NSString *)regix;


/**
 *  @author Xiao  Huarong, 16-08-18 16:08:21
 *
 *  自定义输入格式检查
 *
 *  @param String inputString
 *  @param String regix 匹配符
 *  @return BOOL
 */
+ (BOOL) inputStringFormatRight:(NSString *)inputString withRegix:(NSString *)regix;

#pragma mark -------------------------其它格式检查----------------------------------------
/**
 *  @author Xiao  Huarong, 16-08-18 17:08:41
 *
 *  身份证号码格式检查
 *
 *  @param identityCard 身份证号串
 *
 *  @return BOOL
 */
+(BOOL)IDcardFormateCheck:(NSString *)identityCard;

/**
 *  @brief 邮箱格式检查
 *  @param String mailStr
 *
 *  @return BOOL
 */

+(BOOL)mailValidateIsRight:(NSString *)mailStr;

+(NSString *)DateWidthFormat:(NSString *)formatStr dateConfig:(NSDate *)date;
+(NSString *)DateWidthFormat:(NSString *)formatStr timeInterValeConfig:(double)timeTamp;
-(NSString *)DateStrFromDate:(NSDate *)date;

@end

```

```
//
//  FormatAssistant.m
//  HexiShop
//
//  Created by Smith Cool on 16/8/18.
//  Copyright © 2016年 Xiaohr. All rights reserved.
//

#import "FormatAssistant.h"

@implementation FormatAssistant

/**
 *  @author Xiao  Huarong, 16-08-18 16:08:42
 *
 *  针对手机号码输入的格式检查
 *
 *  @param BOOL number 逐步输入手机号
 *
 *  @return 正确返回yes，错误返回NO
 */
+ (BOOL)inputValidatePhoneNumber:(NSString*)number{
    BOOL res = YES;
    NSCharacterSet* tmpSet = [NSCharacterSet characterSetWithCharactersInString:@"0123456789"];
    int i = 0;
    while (i < number.length) {
        NSString * string = [number substringWithRange:NSMakeRange(i, 1)];
        NSRange range = [string rangeOfCharacterFromSet:tmpSet];
        if (range.length == 0) {
            res = NO;
            break;
        }
        i++;
    }
    return res;
}

/**
 *  @author Xiao  Huarong, 16-08-18 16:08:40
 *
 *  手机号码是否合法格式检查
 *
 *  @param BOOL phoneNumber
 *
 *  @return 不合法返回YES，合法返回NO
 */
+(BOOL)phoneNumberisWrong:(NSString *)phoneNumber{
    NSString *phoneNo = strTrimming(phoneNumber);
    NSString *regex = @"1[3|4|5|7|8|][0-9]{9}";
    NSPredicate *predicate = [NSPredicate predicateWithFormat:@"SELF MATCHES %@", regex];
    if (![predicate evaluateWithObject:phoneNo]) {
        return YES;
    }
    return NO;
}
/**
 *  @brief 手机空格格式检查并返回值
 *
 *  @param phoneNumber 手机号
 *
 *  @return 是：有错
 */
+(BOOL)phoneNumberisWrongWithAll:(NSString *)phoneNumber{
    if (![phoneNumber hasValue]) {
        [UserHelp showMessage:@"手机号不能为空"];
        return YES;
    }else{
        if([FormatAssistant phoneNumberisWrong:phoneNumber]){
            [UserHelp showMessage:@"手机号格式不正确"];
            return YES;
        }else{
            return NO;
        }
    }
}

/**
 *  @author Xiao  Huarong, 16-08-18 16:08:33
 *
 *  针对座机号码输入的格式检查
 *
 *  @param NSString zjNumber
 *
 *  @return BOOL
 */
+ (BOOL)inputZuoJiNumberisWrong:(NSString*)zjNumber{
    BOOL res = YES;
    NSCharacterSet* tmpSet = [NSCharacterSet characterSetWithCharactersInString:@"0123456789-"];
    int i = 0;
    while (i < zjNumber.length) {
        NSString * string = [zjNumber substringWithRange:NSMakeRange(i, 1)];
        NSRange range = [string rangeOfCharacterFromSet:tmpSet];
        if (range.length == 0) {
            res = NO;
            break;
        }
        i++;
    }
    return res;
}

#pragma mark -------------------------类型检查----------------------------------------
/**
 *  @author Xiao  Huarong, 16-08-18 16:08:29
 *
 *  是否为浮点型
 *
 *  @param string floatNumber
 *
 *  @return 为浮点型返回YES，否则返回NO
 */
+ (BOOL)isPureFloat:(NSString*)floatNumber{
    NSScanner* scan = [NSScanner scannerWithString:floatNumber];
    float val;
    return[scan scanFloat:&val] && [scan isAtEnd];
}

/**
 *  @author Xiao  Huarong, 16-08-18 16:08:48
 *
 *  是否为整型
 *
 *  @param string intNumber
 *
 *  @return BOOL 是返回YES，否则返回NO
 */
+ (BOOL)isPureInt:(NSString*)intNumber{
    NSScanner* scan = [NSScanner scannerWithString:intNumber];
    int val;
    return[scan scanInt:&val] && [scan isAtEnd];
}

/**
 *  @author Xiao  Huarong, 16-08-18 17:08:57
 *
 *  两位小数输入限制（必须与UITextFieldDelegate Change代理同用）
 *
 *  @param String xiaoshuStr 输入的数字
 *  @param String string 变化串
 *  @param NSRange  rang    输入的变化
 *  @param weishu
 *  @return BOOL
 */

+(BOOL)inputXiaoshuValidate:(NSString *)xiaoshuStr stringConfig:(NSString *)string shouldChangeCharactersInRange:(NSRange)range weishuConfig:(NSInteger)weishu{
    BOOL isHaveDian = YES;
    if ([xiaoshuStr rangeOfString:@"."].location == NSNotFound) {
        isHaveDian = NO;
    }
    
    if ([string length] > 0) {
        unichar single = [string characterAtIndex:0];//当前输入的字符
        if ((single >= '0' && single <= '9') || single == '.') {//数据格式正确
            
            //首字母不能为0和小数点
            if([xiaoshuStr length] == 0){
                if(single == '.') {
                    //                        [self showText:@"亲，第一个数字不能为小数点"];
                    [xiaoshuStr stringByReplacingCharactersInRange:range withString:@""];
                    return NO;
                }
                // if (single == '0') {
                //                        [self showText:@"亲，第一个数字不能为0"];
                //      [xiaoshuStr stringByReplacingCharactersInRange:range withString:@""];
                //    return NO;
                //}
            }
            
            //输入的字符是否是小数点
            if (single == '.') {
                if(!isHaveDian)//text中还没有小数点
                {
                    isHaveDian = YES;
                    return YES;
                    
                }else{
                    //                        [self showText:@"亲，您已经输入过小数点了"];
                    [xiaoshuStr stringByReplacingCharactersInRange:range withString:@""];
                    return NO;
                }
            }else{
                if (isHaveDian) {//存在小数点
                    
                    //判断小数点的位数
                    NSRange ran = [xiaoshuStr rangeOfString:@"."];
                    if (range.location - ran.location <= weishu) {
                        return YES;
                    }else{
                        //                            [self showText:@"亲，您最多输入两位小数"];
                        return NO;
                    }
                }else{
                    return YES;
                }
            }
        }else{//输入的数据格式不正确
            //                [self showText:@"亲，您输入的格式不正确"];
            [xiaoshuStr stringByReplacingCharactersInRange:range withString:@""];
            return NO;
        }
    }
    else
    {
        return YES;
    }
}


/**
 *  @author Xiao  Huarong, 16-08-18 16:08:49
 *
 *  针对输入金额的格式检查
 *
 *  @param NSString moneyStr
 *
 *  @return BOOL
 */
+ (BOOL)inputMoneyFormat:(NSString*)moneyStr{
    BOOL res = YES;
    NSCharacterSet* tmpSet = [NSCharacterSet characterSetWithCharactersInString:@"0123456789."];
    int i = 0;
    while (i < moneyStr.length) {
        NSString * string = [moneyStr substringWithRange:NSMakeRange(i, 1)];
        NSRange range = [string rangeOfCharacterFromSet:tmpSet];
        if (range.length == 0) {
            res = NO;
            break;
        }
        i++;
    }
    return res;
}

#pragma mark -------------------------密码检查----------------------------------------
/**
 *  @author Xiao  Huarong, 16-08-18 16:08:13
 *
 *  常规密码检查（6到20位大小数字）
 *
 *  @param BOOL passWordStr
 *
 *  @return BOOL
 */
+ (BOOL)passwordNormalisRight:(NSString *)passWordStr{
    NSString *passWordRegex = @"^[a-zA-Z0-9]{6,20}+$";
    NSPredicate *passWordPredicate = [NSPredicate predicateWithFormat:@"SELF MATCHES %@",passWordRegex];
    return [passWordPredicate evaluateWithObject:passWordStr];
}

/**
 *  @author Xiao  Huarong, 16-08-18 16:08:20
 *
 *  密码输入格式检查 ^[a-zA-Z0-9|,|.|_|!|?]"
 *
 *  @param String passwordInputStr
 *
 *  @return BOOL
 */
+ (BOOL)inputPasswordisRight:(NSString*)passwordInputStr{
    BOOL res = YES;
    NSString *passWordRegex = @"^[a-zA-Z0-9|,|.|_|!|?]";
    int i = 0;
    while (i < passwordInputStr.length) {
        NSString * stringsub = [passwordInputStr substringWithRange:NSMakeRange(i, 1)];
        NSPredicate *passWordPredicate = [NSPredicate predicateWithFormat:@"SELF MATCHES %@",passWordRegex];
        if (![passWordPredicate evaluateWithObject:stringsub]) {
            res = NO;
            break;
        }
        i++;
    }
    return res;
}

#pragma mark -------------------------自定义格式检查----------------------------------------
/**
 *  @author Xiao  Huarong, 16-08-18 16:08:13
 *
 *  自定义符串类型检查
 *
 *  @param String passWordStr
 *  @param String regix 匹配符
 *
 *  @return BOOL
 */
+ (BOOL)stringFormatisRight:(NSString *)string withRegix:(NSString *)regix{
    NSString *RegixFormat = regix;
    NSPredicate *passWordPredicate = [NSPredicate predicateWithFormat:@"SELF MATCHES %@",RegixFormat];
    return [passWordPredicate evaluateWithObject:string];
}

/**
 *  @author Xiao  Huarong, 16-08-18 16:08:21
 *
 *  自定义输入格式检查
 *
 *  @param String inputString
 *  @param String regix 匹配符
 *  @return BOOL
 */
+ (BOOL) inputStringFormatRight:(NSString *)inputString withRegix:(NSString *)regix{
    BOOL res = YES;
    int i = 0;
    while (i < inputString.length) {
        NSString * stringsub = [inputString substringWithRange:NSMakeRange(i, 1)];
        NSPredicate *passWordPredicate = [NSPredicate predicateWithFormat:@"SELF MATCHES %@",regix];
        if (![passWordPredicate evaluateWithObject:stringsub]) {
            res = NO;
            break;
        }
        i++;
    }
    return res;
}

#pragma mark -------------------------其它格式检查----------------------------------------
/**
 *  @author Xiao  Huarong, 16-08-18 17:08:41
 *
 *  身份证号码格式检查
 *
 *  @param identityCard 身份证号串
 *
 *  @return BOOL
 */
+ (BOOL)checkIDCard:(NSString *)value {
    value = [value stringByTrimmingCharactersInSet:[NSCharacterSet whitespaceAndNewlineCharacterSet]];
    NSInteger length =0;
    if (!value) {
        return NO;
    }else {
        length = [value length];
        if (length !=15 && length !=18) {
            return NO;
        }
    }
    // 省份代码
    
    
    
    NSArray *areasArray =@[@"11",@"12", @"13",@"14", @"15",@"21", @"22",@"23", @"31",@"32", @"33",@"34", @"35",@"36", @"37",@"41",@"42",@"43", @"44",@"45", @"46",@"50", @"51",@"52", @"53",@"54", @"61",@"62", @"63",@"64", @"65",@"71", @"81",@"82", @"91"];
    
    NSString *valueStart2 = [value substringToIndex:2];
    BOOL areaFlag =NO;
    for (NSString *areaCode in areasArray) {
        
        if ([areaCode isEqualToString:valueStart2]) {
            areaFlag =YES;
            break;
        }
    }
    
    if (!areaFlag) {
        return false;
    }
    
    NSRegularExpression *regularExpression;
    NSUInteger numberofMatch;
    int year =0;
    switch (length) {
        case 15:
            year = [value substringWithRange:NSMakeRange(6,2)].intValue +1900;
            if (year %4 ==0 || (year %100 ==0 && year %4 ==0)) {
                regularExpression = [[NSRegularExpression alloc]initWithPattern:@"^[1-9][0-9]{5}[0-9]{2}((01|03|05|07|08|10|12)(0[1-9]|[1-2][0-9]|3[0-1])|(04|06|09|11)(0[1-9]|[1-2][0-9]|30)|02(0[1-9]|[1-2][0-9]))[0-9]{3}$"
                                                                        options:NSRegularExpressionCaseInsensitive
                                                                          error:nil];//测试出生日期的合法性
            }else {
                regularExpression = [[NSRegularExpression alloc]initWithPattern:@"^[1-9][0-9]{5}[0-9]{2}((01|03|05|07|08|10|12)(0[1-9]|[1-2][0-9]|3[0-1])|(04|06|09|11)(0[1-9]|[1-2][0-9]|30)|02(0[1-9]|1[0-9]|2[0-8]))[0-9]{3}$"
                                                                        options:NSRegularExpressionCaseInsensitive
                                                                          error:nil];//测试出生日期的合法性
            }
            numberofMatch = [regularExpression numberOfMatchesInString:value
                                                               options:NSMatchingReportProgress
                                                                 range:NSMakeRange(0, value.length)];
            if(numberofMatch >0) {
                return YES;
            }else {
                return NO;
            }
        case 18:
            year = [value substringWithRange:NSMakeRange(6,4)].intValue;

            if (year %4 ==0 || (year %100 ==0 && year %4 ==0)) {
                
                regularExpression = [[NSRegularExpression alloc]initWithPattern:@"^[1-9][0-9]{5}19[0-9]{2}((01|03|05|07|08|10|12)(0[1-9]|[1-2][0-9]|3[0-1])|(04|06|09|11)(0[1-9]|[1-2][0-9]|30)|02(0[1-9]|[1-2][0-9]))[0-9]{3}[0-9Xx]$"
                                     
                                                                        options:NSRegularExpressionCaseInsensitive
                                     
                                     
                                     
                                                                          error:nil];//测试出生日期的合法性
                
                
                
            }else {
                
                
                
                regularExpression = [[NSRegularExpression alloc]initWithPattern:@"^[1-9][0-9]{5}19[0-9]{2}((01|03|05|07|08|10|12)(0[1-9]|[1-2][0-9]|3[0-1])|(04|06|09|11)(0[1-9]|[1-2][0-9]|30)|02(0[1-9]|1[0-9]|2[0-8]))[0-9]{3}[0-9Xx]$"
                                     
                                     
                                     
                                                                        options:NSRegularExpressionCaseInsensitive
                                     
                                     
                                     
                                                                          error:nil];//测试出生日期的合法性
                
                
                
            }
            
            
            
            numberofMatch = [regularExpression numberOfMatchesInString:value
                             
                             
                             
                                                               options:NSMatchingReportProgress
                             
                             
                             
                                                                 range:NSMakeRange(0, value.length)];
            
            if(numberofMatch >0) {
                
                
                
                int S = ([value substringWithRange:NSMakeRange(0,1)].intValue + [value substringWithRange:NSMakeRange(10,1)].intValue) *7 + ([value substringWithRange:NSMakeRange(1,1)].intValue + [value substringWithRange:NSMakeRange(11,1)].intValue) *9 + ([value substringWithRange:NSMakeRange(2,1)].intValue + [value substringWithRange:NSMakeRange(12,1)].intValue) *10 + ([value substringWithRange:NSMakeRange(3,1)].intValue + [value substringWithRange:NSMakeRange(13,1)].intValue) *5 + ([value substringWithRange:NSMakeRange(4,1)].intValue + [value substringWithRange:NSMakeRange(14,1)].intValue) *8 + ([value substringWithRange:NSMakeRange(5,1)].intValue + [value substringWithRange:NSMakeRange(15,1)].intValue) *4 + ([value substringWithRange:NSMakeRange(6,1)].intValue + [value substringWithRange:NSMakeRange(16,1)].intValue) *2 + [value substringWithRange:NSMakeRange(7,1)].intValue *1 + [value substringWithRange:NSMakeRange(8,1)].intValue *6 + [value substringWithRange:NSMakeRange(9,1)].intValue *3;

                int Y = S %11;

                NSString *M =@"F";

                NSString *JYM =@"10X98765432";

                M = [JYM substringWithRange:NSMakeRange(Y,1)];// 判断校验位

                if ([M isEqualToString:[value substringWithRange:NSMakeRange(17,1)]]) {

                    return YES;// 检测ID的校验位
 
                }else {

                    return NO;
 
                }
            }else {

                return NO;
            }

        default:

            return false;
    }
}
/**
 *  @brief 邮箱格式检查
 *  @param String mailStr
 *  
 *  return BOOL
 */

+(BOOL)mailValidateIsRight:(NSString *)mailStr{
    NSString *emailRegex = @"[A-Z0-9a-z._%+-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,4}";
    NSPredicate *emailTest = [NSPredicate predicateWithFormat:@"SELF MATCHES %@", emailRegex];
    return [emailTest evaluateWithObject:mailStr];
}

+(NSString *)DateWidthFormat:(NSString *)formatStr dateConfig:(NSDate *)date{
    NSDateFormatter *format = [[NSDateFormatter alloc]init];
    [format setDateFormat:formatStr];
    return [format stringFromDate:date];
}
+(NSString *)DateWidthFormat:(NSString *)formatStr timeInterValeConfig:(double)timeTamp{
    NSDate *date = [NSDate dateWithTimeIntervalSince1970:timeTamp];
    
    NSDateFormatter *format = [[NSDateFormatter alloc]init];
    [format setDateFormat:formatStr];
    return [format stringFromDate:date];
}

-(NSString *)DateStrFromDate:(NSDate *)date{
    NSTimeInterval interval = [date timeIntervalSince1970] * 1000;
    NSString *timeTramp = [NSString stringWithFormat:@"%ld",(long)interval];
    return timeTramp;
}

@end
```