---
title: Latex使用方式
top: false
cover: false
toc: true
mathjax: false
date: 2024-1-26 15:24:28
author:
img:
coverImg:
password:
summary:
tags:
- Latex
categories:

---

# Latex使用方式

##  1 Latex优势

-   使用固定模板，格式固定，只需套用模板即可生成文章

## 2 Latex图表

### 1. 表格

1.   **设定表格宽度**[^1]

```latex
\usepackage{graphicx} # 记得加宏包
\resizebox{\linewidth}{!}{  #此处！表示根据根据宽高比进行自适应缩放
\begin{tabular}...
....
....
\end{tabular}
} # 注意加的位置在\begin{tabular}和\end{tabular}前后
```

2.   文字自动换行

     还在研究中，相关链接[^2][^3]

### 2. 图片

1.   单栏与双栏图片[^4]

单栏

```latex
\begin{figure}
...
\end{figure}
```

双栏

```latex
\begin{figure*}
...
\end{figure*}
```





## 参考链接

[^1]:[Latex解决表格过宽问题，自适应调整宽度](https://zhuanlan.zhihu.com/p/337457317)

[^2]: [表格：字数太多时自动换行](https://blog.csdn.net/weixin_39278265/article/details/105623872)
[^3]: [latex表格中内容过多如何换行【已解决】](https://blog.csdn.net/qq_43604183/article/details/134739083?spm=1001.2101.3001.6650.2&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-2-134739083-blog-121678328.235%5Ev43%5Epc_blog_bottom_relevance_base3&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-2-134739083-blog-121678328.235%5Ev43%5Epc_blog_bottom_relevance_base3)
[^4]: [Latex写文章时插入单栏图片和双栏图片方法](https://blog.csdn.net/Time_Memory_cici/article/details/129381838)
