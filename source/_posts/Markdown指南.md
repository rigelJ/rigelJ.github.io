---
title: Markdown使用指南
date: 2021-04-11 10:31:39
tags:
- Markdown
categories:
- 软件文档
mathjax: true
cover: /myimage/doc/markdown_cover.png
---

# **Markdown使用 指南**

*********

## Markdown 标题

*****

### 使用#标记多级标题

> 一级标题用#号来标记
>
> 二级标题用##号来标记
>
> ..... 依次类推

### 使用=和-标记一级和二级标题（部分支持）

> 一级标题用=======来标注
>
> 二级标题用------------来标注

***********

## Markdown段落格式

### 字体

>*斜体*   * *
>
>**粗体**  ** **
>
>***斜粗体***   * * *  * * *

### 线条

>分割线 *********
>
>~~删除线~~  ~~ ~~
>
><u>下划线</u>  <u> </u>
>
>脚注  [^脚注]

**********

## Markdown列表

* 第一项

  - 第一个元素

    * 第二个元素

* 第二项

    * 第一个元素
    * 第二个元素 

**********

## Markdown 区块

### 区块嵌套

> 区块引用符 >
>
> > 第一层嵌套 >>
>
> > > 第二层嵌套 >>>
> > >
> > > 
>

### 区块中使用列表

> * 第一项
>   * 1.1
>   * 1.2
> * 第二项
>   * 2.1
>   * 2.2
> * 第三项

### 列表中使用区块

* 第一项

  > 学技术不仅是技术，而是梦想

* 第二项 

  > 我们的目标是星辰大海。

*******

## Markdown 代码 

### 单个片段代码

> `printf()`函数

### 代码区块

代码块使用三个反引号建立，以下是部分语言的实例代码：

> **Python实例**
>
> ```python
> import os
> import sys
> print("hello world!")
> ```
>
> **Javascript实例**
>
> ```javascript
> $(document).ready(function(){
> alert('RUNO')
> })
> ```
>
> **PHP实例**
>
> ```php
> <?php
> echo 1
> ?>
> ```

******

## Markdown 链接

链接使用[链接名称](http://www.baidu.com)建立，格式为[]() ，也可以用变量设置来建立一个链接，赋值在文档末尾进行

>这个链接用 1 作为网址变量 [Google][1]

******

## Markdown 图片

### 通过markdown语法插入图片

Markdown 插入图片的语法格式如下：

> ![属性文本]()

### 通过Typora直接插入图片 (编辑器必须是Typora编辑器)

>格式-->图像-->插入图片

*****

## Markdown 表格

Markdown表格格式如下：

> | |为分割单元格，-表示长度，：：为中央对齐

| 数据统计表 |  A   |  B   |  C   |  D   |  E   |
| :--------: | :--: | :--: | :--: | :--: | :--: |
|    文字    |  1   |  4   |  5   |  8   |  9   |
|    图标    |  2   |  3   |  6   |  7   |  0   |

******

## Markdown 拓展技巧

### HTML元素

不在 Markdown 涵盖范围之内的标签，都可以直接在文档里面用 HTML 撰写。目前支持的HTML元素有：

> \<kbd>元素：使用<kbd>Shift</kbd> +<kbd>W</kbd> 执行操作
>
> \<b>元素：<b>123</b>    
>
> \<i>元素：<i>admin</i>
>
> \<em>元素：<em>admin</em>
>
> \<sup>元素：A<sup>1</sup>
>
> \<br> 元素：换行

### 转义字符

Markdown 使用了很多特殊符号来表示特定的意义，如果需要显示特定的符号则需要使用转义字，Markdown 使用反斜杠转义特殊字符：

> \ * \ * 转义文本加粗

### 公式

当你需要在编辑器中插入数学公式时，可以使用两个美元符 $$ 包裹 TeX 或 LaTeX 格式的数学公式来实现。提交后，问答和文章页会根据需要加载 Mathjax 对数学公式进行渲染。如输入：

> ```nginx
> \mathbf{V}_1 \times \mathbf{V}_2 =  \begin{vmatrix} 
> \mathbf{i} & \mathbf{j} & \mathbf{k} \\
> \frac{\partial X}{\partial u} &  \frac{\partial Y}{\partial u} & 0 \\
> \frac{\partial X}{\partial v} &  \frac{\partial Y}{\partial v} & 0 \\
> \end{vmatrix}
> ${$tep1}{\style{visibility:hidden}{(x+1)(x+1)}}
> ```

会显示如下公式：

$$
\mathbf{V}_1 \times \mathbf{V}_2 =  \begin{vmatrix} 
\mathbf{i} & \mathbf{j} & \mathbf{k} \\
\frac{\partial X}{\partial u} &  \frac{\partial Y}{\partial u} & 0 \\
\frac{\partial X}{\partial v} &  \frac{\partial Y}{\partial v} & 0 \\
\end{vmatrix}
${$tep1}{\style{visibility:hidden}{(x+1)(x+1)}}
$$



## **参考**

1.菜鸟教程 <u>https://www.runoob.com/markdown/md-tutorial.html</u>

2.知乎专栏 <u>https://zhuanlan.zhihu.com/p/67153848</u>




[^脚注]: 这是一个脚注

[1] : http://www.google.com