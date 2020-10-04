---
title: Markdown方法
date: 2019-08-09 20:31:16
tags: [markdown]
typora-root-url: ..
---
heiheihei 
<!--more-->


## 文字格式  
**文字** ， __文字__ ， _文字_ ， *文字*  
```
**文字** ， __文字__ ， _文字_ ， *文字*  
```
*斜体文本*    _斜体文本_
**粗体文本**    __粗体文本__
***粗斜体文本***    ___粗斜体文本___
```
*斜体文本*    _斜体文本_
**粗体文本**    __粗体文本__
***粗斜体文本***    ___粗斜体文本___
```

## 常见的特殊符号
```{code}
! &#33; — 惊叹号Exclamation mark 
” &#34; &quot; 双引号Quotation mark 
# &#35; — 数字标志Number sign 
$ &#36; — 美元标志Dollar sign 
% &#37; — 百分号Percent sign 
& &#38; &amp; Ampersand 
‘ &#39; — 单引号Apostrophe 
( &#40; — 小括号左边部分Left parenthesis 
) &#41; — 小括号右边部分Right parenthesis 
* &#42; — 星号Asterisk 
+ &#43; — 加号Plus sign 
< &#60; &lt; 小于号Less than 
= &#61; — 等于符号Equals sign 
> &#62; &gt; 大于号Greater than 
? &#63; — 问号Question mark 
@ &#64; — Commercial at 
[ &#91; --- 中括号左边部分Left square bracket 
\ &#92; --- 反斜杠Reverse solidus (backslash) 
] &#93; — 中括号右边部分Right square bracket 
{ &#123; — 大括号左边部分Left curly brace 
| &#124; — 竖线Vertical bar 
} &#125; — 大括号右边部分Right curly brace 
```
## 链接方法
#### 常用链接方法
文字链接 [链接名称](https://chwshuang.github.io)
网址链接 <https://chwshuang.github.io>

#### 高级链接技巧
这个链接用 1 作为网址变量 [Google][1].
这个链接用 yahoo 作为网址变量 [Yahoo!][yahoo].
然后在文档的结尾为变量赋值（网址）
[1]: http://www.google.com/
[yahoo]: http://www.yahoo.com/


 ## 列表  

 #### 普通无序列表

- 列表文本前使用 [减号+空格]
+ 列表文本前使用 [加号+空格]
* 列表文本前使用 [星号+空格]

#### 普通有序列表
1. 列表前使用 [数字+空格]
2. 我们会自动帮你添加数字
7. 不用担心数字不对，显示的时候我们会自动把这行的 7 纠正为 3

#### 列表嵌套

1. 列出所有元素：
    - 无序列表元素 A
        1. 元素 A 的有序子列表
    - 前面加四个空格
2. 列表里的多段换行：
    前面必须加四个空格，
    这样换行，整体的格式不会乱
3. 列表里引用：

    > 前面空一行
    > 仍然需要在 >  前面加四个空格
	
```{code}

1. 列出所有元素：
    - 无序列表元素 A
        1. 元素 A 的有序子列表
    - 前面加四个空格
2. 列表里的多段换行：
    前面必须加四个空格，
    这样换行，整体的格式不会乱
3. 列表里引用：

    > 前面空一行
    > 仍然需要在 >  前面加四个空格
	
	
```

## 图片
```
![图片名称](http: //图片地址)
当然，你也可以像网址那样对图片网址使用变量

这个链接用 1 作为网址变量 [ Google] [ 1].
然后在文档的结尾位变量赋值(网址)

[1]: http: //www.google.com/logo.png
也可以使用 HTML 的图片语法来自定义图片的宽高大小

<img src="/images/headpic.jpg" class="full-image"  />  
```

<img src="/images/headpic.jpg" class="full-image"  />  

## 换行  
如果另起一行，只需在当前行结尾加 2 个空格
```
在当前行的结尾加 2 个空格  
这行就会新起一行
如果是要起一个新段落，只需要空出一行即可。
```
## 分隔符  
如果你有写分割线的习惯，可以新起一行输入三个减号-。当前后都有段落时，请空出一行：

前面的段落

---

后面的段落

## 小型文本  
```
<small>文本内容</small>
```

预览效果： 
我是正常文字 
<small>我是小型文字</small>

## 表格
Markdown的扩展语法，hexo已经支持

```
| 参数           | 说明                 |   默认值            |
| ------------- |:-------------------:|:------------------:|
| host          | 远程主机的地址         |                    |
| user          | 使用者名称            |                    |
| root          |  远程主机的根目录      |                    |
| port          | 端口                 |       22           |
| delete        | 删除远程主机上的旧文件   |  true              |
| verbose       | 显示调试信息           |   true             |
| ignore_errors | 忽略错误              |     false          |
```

| 参数           | 说明                 |   默认值            |
| ------------- |:-------------------:|:------------------:|
| host          | 远程主机的地址         |                    |
| user          | 使用者名称            |                    |
| root          |  远程主机的根目录      |                    |
| port          | 端口                 |       22           |
| delete        | 删除远程主机上的旧文件   |  true              |
| verbose       | 显示调试信息           |   true             |
| ignore_errors | 忽略错误              |     false          |

