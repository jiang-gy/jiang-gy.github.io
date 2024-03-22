---
title: Markdown语法
top: false
cover: false
toc: true
mathjax: false
date: 2024-01-21 10:16:52
author:
img:
coverImg:
password:
summary:
tags:
- Hexo博客
- Markdown语法
categories:

---

# Markdown语法

##  1 Markdown优势

-   相对于word，操作方便，打开迅速
-   主题丰富，较为美观

## 2 Markdown语法

### 1 脚注，尾注

参考文章[^1]

**1.脚注，尾注**：主要用于注释说明内容 (参看[使用场景](https://link.zhihu.com/?target=https%3A//www.imooc.com/wiki/markdownlesson/markdownfootnote.html%23%3A~%3Atext%3D%E5%86%99%E5%88%B0%E6%96%87%E7%AB%A0%E6%9C%AB%E5%B0%BE%E3%80%82-%2C3.%20%E4%BD%BF%E7%94%A8%E5%9C%BA%E6%99%AF%E5%8F%8A%E5%AE%9E%E4%BE%8B%2C-%E5%AE%9E%E4%BE%8B%204%EF%BC%9A))。脚注/尾注的特点是可以在页面中来回跳转。

示例：


这是一个链接到谷歌的[^脚注]。

[^脚注]: http://www.google.com

源码：

```text
这是一个链接到谷歌的[^脚注]。

[^脚注]: http://www.google.com
```



![img](https://gitee.com/jgyong/blogimg/raw/master/img/202401211224018.webp)



### 2 引用链接

两部分：

-   引用文本
-   引用主体

引用文本格式：`[显示文字][引用标签]`

引用主体格式：`[引用标签]: <链接地址> (链接可选标题)`(参看主体格式说明[^1](https://zhuanlan.zhihu.com/p/499137261/以下示例格式对于**引用主体格式**效果相同：))

示例：

I get 10 times more traffic from [Google][1] than from [Yahoo][2] or [MSN][3].  

[1]: http://google.com/        "Google"
[2]: http://search.yahoo.com/  "Yahoo Search"
[3]: http://search.msn.com/    "MSN Search"
一般链接放置位置末尾，便于统一管理。

源码：

```text
I get 10 times more traffic from [Google][1] than from [Yahoo][2] or [MSN][3].  

[1]: http://google.com/        "Google" 
[2]: http://search.yahoo.com/  "Yahoo Search" 
[3]: http://search.msn.com/    "MSN Search"
```

## 参考链接

[^1]:[Markdown写作 | 尾注,脚注和引用链接的正确使用](https://zhuanlan.zhihu.com/p/499137261)

