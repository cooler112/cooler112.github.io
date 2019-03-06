---
title: Chrom+Vimium实现全键盘操作
date: 2019-03-06 17:35:33
tags:
---

不用移动，确定，点击，全键盘搞定，不过部分文本选中这块要使用鼠标进行选中，当习惯键盘操作后会发现非常的快捷 
####Tab and window shortcuts窗口标签快捷键
| 快捷键组合                                                   | 功能                     | 说明               |      |
| ------------------------------------------------------------ | ------------------------ | ------------------ | ---- |
| Open a new window                                            | ⌘ + n                    | 新开窗口           |      |
| Open a new window in Incognito mode                          | ⌘ + Shift + n            | 新建窗口匿名模式   |      |
| Open a new tab, and jump to it                               | ⌘ + t                    | 进入新建标签       |      |
| Reopen the last closed tab, and jump to it                   | ⌘ + Shift + t            | 进入上次关闭标签   |      |
| Jump to the next open tab                                    | ⌘ + Option + Right arrow | 标签切换向后       |      |
| Jump to the previous open tab                                | ⌘ + Option + Left arrow  | 标签切换向前       |      |
| Jump to a specific tab                                       | ⌘ + 1 through ⌘ + 8      | 进入指定标签       |      |
| Jump to the last tab                                         | ⌘ + 9                    | 进入最后一个标签   |      |
| Open the previous page in your browsing history for the current tab | ⌘ + [ or ⌘ + Left arrow  | 向前               |      |
| Open the next page in your browsing history for the current tab | ⌘ + ] or ⌘ + Right arrow | 向后               |      |
| Closes the current tab or pop-up                             | ⌘ + w                    | 关闭标签或弹出     |      |
| Closes the current window                                    | ⌘ + Shift + w            | 关闭当前窗口       |      |
| Minimize the window                                          | ⌘ + m                    | 最小化Chrome       |      |
| Hide Google Chrome                                           | ⌘ + h                    | 隐藏               |      |
| Quit Google Chrome                                           | ⌘ + q                    | 关闭所有Chrome窗口 |      |

####Google Chrome feature shortcuts工具快捷键
| 功能                                               | 快捷键组合         | 说明           |      |
| -------------------------------------------------- | ------------------ | -------------- | ---- |
| Show or hide the Bookmarks Bar                     | ⌘ + Shift + b      | 显示隐藏书签   |      |
| Open the Bookmark Manager                          | ⌘ + Option + b     | 书签栏管理     |      |
| Open the Settings page in a new tab                | ⌘ + ,              | 打开设置页面   |      |
| Open the History page in a new tab                 | ⌘ + y              | 打开历史页面   |      |
| Open the Downloads page in a new tab               | ⌘ + Shift + j      | 打开下载页面   |      |
| Open the Find Bar to search the current page       | ⌘ + f              | 当前查找       |      |
| Jump to the next match to your Find Bar search     | ⌘ + g              | 查找下一个     |      |
| Jump to the previous match to your Find Bar search | ⌘ + Shift + g      | 想找前一个     |      |
| When Find Bar is open, search for selected text    | ⌘ + e              | 查找选中字段   |      |
| Open Developer Tools                               | ⌘ + Option + i     | 打开开发者工具 |      |
| Open the Clear Browsing Data options               | ⌘ + Shift + Delete | 清除记录       |      |
| Log in as a different user or browse as a Guest    | ⌘ + Shift + m      | 登录           |      |

####Address bar shortcuts
| 功能                    | 快捷键组合 | 说明         |      |
| ----------------------- | ---------- | ------------ | ---- |
| Jump to the Address Bar | ⌘ + l      | 跳转到地址栏 |      |

###Webpage shortcuts
| 功能                                                       | 快捷键组合            | 说明                   |      |
| ---------------------------------------------------------- | --------------------- | ---------------------- | ---- |
| Open options to print the current page                     | ⌘ + p                 | 打印                   |      |
| Open options to save the current page                      | ⌘ + s                 | 保存                   |      |
| Reload your current page			⌘ + r                  | 重新加载              |                        |      |
| Reload your current page, ignoring cached content          | ⌘ + Shift + r         | 忽略缓存重新加载       |      |
| Stop the page loading                                      | Esc                   | 停止加载               |      |
| Browse clickable items moving forward                      | Tab                   | 切换                   |      |
| Browse clickable items moving backward                     | Shift + Tab           | 向后切换               |      |
| Open a file from your computer in Google Chrome            | ⌘ + o + Select a file | 浏览器打开             |      |
| Display non-editable HTML source code for the current page | ⌘ + Option + u        | 显示源码               |      |
| Open the JavaScript Console                                | ⌘ + Option + j        | 打开脚本编辑器         |      |
| Save your current webpage as a bookmark                    | ⌘ + d                 | 保存为书签             |      |
| Save all open tabs as bookmarks in a new folder            | ⌘ + Shift + d         | 保存所有打开页面为书签 |      |
| Turn full-screen mode on or off                            | ⌘ + Ctrl + f          | 全屏                   |      |
| Make everything on the page bigger                         | ⌘ and +               | 放大                   |      |
| Make everything on the page smaller                        | ⌘ and -               | 缩小                   |      |
| Return everything on the page to the default size          | ⌘ + 0                 | 还原                   |      |
| Scroll down a webpage, a screen at a time                  | Space                 | 向下                   |      |
| Scroll up a webpage, a screen at a time                    | Shift + Space         | 向上                   |      |
| Search the web                                             | ⌘ + Option + f        | 搜索                   |      |
| Open your home page in the current tab                     | ⌘ + Shift + h         | 打开首页               |      |

##Vimnum
作为Chrome的强大快捷器插件，实现快速浏览访问

![Screen Shot 2017-03-22 at 15.13.40.png](http://upload-images.jianshu.io/upload_images/4767765-f7b06159d95572d4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)