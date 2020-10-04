---
title: MIPS指令集初识
date: 2020-05-20 18:12:53
tags: [计组]
typora-root-url: ..
---



http://www.360doc.com/content/10/0817/09/2415113_46631439.shtml

<!--more-->

#  MIP指令的一般性语法格式

一个操作符, 三个操作数

``op dst,  src1,  src2``

op: 指令的基本功能

dst: 保存结果的寄存器

src1: 第一个操作数

src2: 第二个操作数



# 指令格式与操作数

## 第1类操作数 寄存器

MIPS有32个寄存器, 每个寄存器的宽度都是32位。

根据指令的功能来解读寄存器值的正负，32位编码按有符号还是无符号解读取决于指令。

``$s0~$s7``是程序员变量寄存器

``$t0~$t9``是临时变量寄存器



![image-20200520193540275](/images/MIPS%E6%8C%87%E4%BB%A4%E9%9B%86%E5%88%9D%E8%AF%86/image-20200520193540275.png)





### 0号寄存器

![image-20200520193758456](/images/MIPS%E6%8C%87%E4%BB%A4%E9%9B%86%E5%88%9D%E8%AF%86/image-20200520193758456.png)







## 立即数

![image-20200520193815706](/images/MIPS%E6%8C%87%E4%BB%A4%E9%9B%86%E5%88%9D%E8%AF%86/image-20200520193815706.png)





## 主存单元

### 主存单元的颗粒度: 

字节: 是存储器最常用的存储单位

### 地址

主存单元的编号就是地址, 等同于数组下标.

### CPU字长

一般指CPU一条指令可以计算的数据的宽度.





### 主存的抽象模型

![image-20200520194048749](/images/MIPS%E6%8C%87%E4%BB%A4%E9%9B%86%E5%88%9D%E8%AF%86/image-20200520194048749.png)

### 主存地址的表示方式

绝对地址和相对地址.

![image-20200520194123976](/images/MIPS%E6%8C%87%E4%BB%A4%E9%9B%86%E5%88%9D%E8%AF%86/image-20200520194123976.png)





![image-20200520194159071](/images/MIPS%E6%8C%87%E4%BB%A4%E9%9B%86%E5%88%9D%E8%AF%86/image-20200520194159071.png)







### 注意:

MIPS只支持**寄存器与寄存器\ 寄存器与立即数的运算**



# 指令集与汇编程序

## 汇编程序的基本结构

代码段 `.text`    数据段`.data`    

本质是代表基地址的标号

![image-20200520194905386](/images/MIPS%E6%8C%87%E4%BB%A4%E9%9B%86%E5%88%9D%E8%AF%86/image-20200520194905386.png)







## 全局变量声明

全局变量位于`.data`关键字后

- 要素1: 变量名
  - 可以包含字母\数字\下划线等, 但是不能有空格\或 + 或 - 等符号

- 要素2: 关键字
  - 用于定于变量的类型
- 要素3: 值
  - 用于定义变量的值

![image-20200520195241480](/images/MIPS%E6%8C%87%E4%BB%A4%E9%9B%86%E5%88%9D%E8%AF%86/image-20200520195241480.png)



## 常见的变量类型



| 关键字  | 基本用途                     |
| ------- | ---------------------------- |
| .byte   | 声明8位变量                  |
| .half   | 声明16位变量                 |
| .word   | 声明32位变量                 |
| .ascii  | 声明字符串, 字符串结尾无'\0' |
| .asciiz | 声明字符串, 字符串结尾有'\0' |
| .space  | 为一个变量预留指定的字节数   |



# 指令一览

![image-20200520194647070](/images/MIPS%E6%8C%87%E4%BB%A4%E9%9B%86%E5%88%9D%E8%AF%86/image-20200520194647070.png)

### 加载字: ``lw(load word)``

- 读取地址为base+off的主存单元,然后写入reg.

### 存储字:``sw(sotre word)``

- 读取reg, 然后写入地址为base+off的存储单元



### 读字节: lb(load byte)

`lb rt, offset(base)`

从以编号为base的寄存器为基地址,offset为偏移的地址单元处, 读取一个字节,然后将其写入到编号为rt的寄存器.

#### **注意:**

**所有读/写存储器指令的offset都是以字节为单位的**





#### 用RTL描述lb指令. 

RTL:  Register Transfer Language

![image-20200520195939390](/images/MIPS%E6%8C%87%E4%BB%A4%E9%9B%86%E5%88%9D%E8%AF%86/image-20200520195939390.png)

### 写字节: sb

`sb rt, offset(base)`

用于将寄存器的最低字节写入主存单元

![image-20200520200349699](/images/MIPS%E6%8C%87%E4%BB%A4%E9%9B%86%E5%88%9D%E8%AF%86/image-20200520200349699.png)

![image-20200520200710110](/images/MIPS%E6%8C%87%E4%BB%A4%E9%9B%86%E5%88%9D%E8%AF%86/image-20200520200710110.png)



| 加载与存储指令 | 意思                                  |
| -------------- | ------------------------------------- |
| lb             | load byte                             |
| lbu            | load unsigned byte 没有符号拓展地load |
| sb             | set byte                              |
| lh             | load half  偏移必须是2的倍数          |
| lhu            | load unsigned half 偏移必须是2的倍数  |
| sh             | set half 偏移必须是2的倍数            |
| lw             | 偏移必须是4的倍数                     |
| sw             | 偏移必须是4的倍数                     |





### 加减法

| 指令  | 功能                 | 格式                | 描述                             | 示例                 |
| ----- | -------------------- | ------------------- | -------------------------------- | -------------------- |
| add   | 加法(检测溢出)       | add rd,rs,rt        | R[rd]<-R[rs]+R[rt]               | add \$s1, ​\$s2, ​\$s3 |
| addu  | 加法(不检测溢出)     | add rd,rs,rt        | R[rd]<-R[rs]+R[rt]               | add \$s1, \$s2, \$s3 |
| addi  | 立即数加(检测溢出)   | addi rt,rs imm16    | R[rt]<-R[rs]+sign_ext(imm16)     | addi \$s1, ​\$s2, -3  |
| addiu | 立即数加(不检测溢出) | addiu rt, rs, imm16 | R[rt] <- R[rs] + sign_ext(imm16) | addiu \$s1, ​\$s2, 3  |
| sub   | 减法(检测溢出)       | sub rd, rs, rt      | R[rd] <- R[rs] - R[rt]           | sub \$s1, $s2, \$s3  |
| subu  | 减法(不检测溢出)     | sub rd, rs, rt      | R[rd] <- R[rs] - R[rt]           | subu \$s1, ​\$s2, $s3 |

MIPS会检测溢出（并且当溢出发生时产生错误） 

- 有unsigned关键字的算术类指令忽略溢出

![image-20200520204922404](/images/MIPS%E6%8C%87%E4%BB%A4%E9%9B%86%E5%88%9D%E8%AF%86/image-20200520204922404.png)







### 乘除法指令

乘除法指令计算结果：不是直接写入32个通用寄存器，而是保存在2个特殊寄存器$HI$与$LO$

high, low



用两条专用指令读写HI\LO

`mfhi dst`  move from HI

`mflo dst` move from LO

 



#### 乘法

`mult src1,src2`

src1*src2:  LO保存结果的低32位,HI保存结果的高32位.





#### 除法

`div src1, src2`

src1/src2: LO保存商, HI保存余数



### 逻辑运算

and

andi

or

ori

nor

xor

xori

![image-20200520205541237](/images/MIPS%E6%8C%87%E4%BB%A4%E9%9B%86%E5%88%9D%E8%AF%86/image-20200520205541237.png)

### 分支指令

beq:  branch if equal  等于

bne: branch if not equal  不等于

j:   jump 无条件跳转

![image-20200520210123312](/images/MIPS%E6%8C%87%E4%BB%A4%E9%9B%86%E5%88%9D%E8%AF%86/image-20200520210123312.png)





**bxxz类指令格式均为：`bxxz rs, label `**

blez: branch if less equal than zero 小于等于 0

bgez: branch if greater equal than zero  大于等于0

bltz: branch if less than zero 小于0

bgtz:  branch if greater equal than zero 大于0







### 不等式

不等关系: <, <=, > , >=

在MIPS中用增加一条额外的指令来支持所有的比较

`slt: Set on Less THan`

`slt dst, src1, src2`

如果src1<src2, 则dst写入1, 否则写入0







page 42













# 函数

实现函数的6个步骤

- 1、调用者把参数放置在某个地方以便函数能访问

- 2、调用者转移控制给被调用的函数

- 3、函数获取局部变量对应的空间

- 4、函数执行具体功能

- 5、函数把返回值放置在某个地方，然后恢复使用的资源

- 6、返回控制给调用者





传递参数的寄存器:  `$a0~$a3`

传递返回值的寄存器: `$v0~$v1`

返回地址寄存器, 保存调用者的地址:  `$ra`







## 函数调用指令

jump and link

`jal label`  把jal下一条指令的地址保存在`$ra`, 然后跳转到label



PC, 程序计数器. 对程序员不可见,但是可以被`jal`访问

保存在`$ra`的是`PC+4`(下一条指令的地址), 而不是PC



## 函数返回指令

jump register

`jr src` 无条件跳转到保存在src的地址, 通常就是`$ra`







## 函数模板:

![image-20200521203336552](/images/MIPS%E6%8C%87%E4%BB%A4%E9%9B%86%E5%88%9D%E8%AF%86/image-20200521203336552.png)





# 寄存器的保护分析

![image-20200521203802084](/images/MIPS%E6%8C%87%E4%BB%A4%E9%9B%86%E5%88%9D%E8%AF%86/image-20200521203802084.png)

![image-20200521203809605](/images/MIPS%E6%8C%87%E4%BB%A4%E9%9B%86%E5%88%9D%E8%AF%86/image-20200521203809605.png)

![image-20200521203816859](/images/MIPS%E6%8C%87%E4%BB%A4%E9%9B%86%E5%88%9D%E8%AF%86/image-20200521203816859.png)

![image-20200521203825437](/images/MIPS%E6%8C%87%E4%BB%A4%E9%9B%86%E5%88%9D%E8%AF%86/image-20200521203825437.png)