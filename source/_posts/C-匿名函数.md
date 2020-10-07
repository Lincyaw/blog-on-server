---
title: C++匿名函数
date: 2020-10-07 16:53:12
tags: 
	- 算法
	- C++
categories: 
	- 学习
---

在做[354. 俄罗斯套娃信封问题](https://leetcode-cn.com/problems/russian-doll-envelopes/)时在思考如何给`sort()`加个判断的函数。自己不是很想新写一个函数来用于判断，想着要是有个匿名函数就好了，结果发现是自己孤陋寡闻了QAQ 然后才反应过来在qt中自己就已经用过匿名函数了, 不过时间有点久了忘了...    经典的中括号小括号大括号

<!--more-->

# sort

先了解一下`sort`函数

`sort(begin, end, cmp)`，其中`begin`为指向待`sort()`的数组的第一个元素的指针，`end`为指向待`sort()`的数组的**`最后一个元素的下一个位置`**的指针，`cmp`参数为排序准则，如果没有的话，默认以非降序排序。

## 自定义cmp参数

```cpp
#include <iostream>
#include <algorithm>
using namespace std;
bool cmp(int x, int y) {
    return x > y;
}
int main() {
    int a[5] = {1, 3, 4, 2, 5};
    sort(a, a + 5, cmp);
    for (int i = 0; i < 5; i++) cout << a[i] << ' ';
    return 0;
}
```

输出结果为：`5 4 3 2 1`





# 匿名函数

匿名函数的基本语法为：

```c++
//[捕获列表](参数列表)->返回类型{函数体}
int main()
{
	auto Add = [](int a, int b)->int {
		return a + b;
	};
	std::cout << Add(1, 2) << std::endl;
	return 0;
}
```

这个返回类型和rust的有点像, 但是也可以不填返回类型, 编译器一般来说能能够自动推断出来

```c++
//[捕获列表](参数列表)->返回类型{函数体}
int main()
{
	auto Add = [](int a, int b) {
		return a + b;
	};
	std::cout << Add(1, 2) << std::endl;
	return 0;
}
```

## 捕获列表

试图在Lambda内使用外部变量是错误的，例如：

```c++
#include <iostream>

int main()
{
	int c = 12;
	auto Add = [](int a, int b)->int {
		return c;
	};
	std::cout << Add(1, 2) << std::endl;
	return 0;
}
```

但是有些时候我们需要使用外部变量，所以需要使用捕获列表，上述代码改写成一下形式便可以通过编译。

```c++
#include <iostream>

int main()
{
	int c = 12;
	auto Add = [c](int a, int b)->int {
		return c;
	};
	std::cout << Add(1, 2) << std::endl;
	return 0;
}
```

但是如果你更改一下lambda表达式中代码块的内容，比如在上述代码中添加一句

```c++
c = a;
```

这样又会无法编译通过了，因为你的c是按值传递的，所以要将捕获列表改成

```c++
[&c](int a, int b)->int{……}；
```

这样c的值便是按引用传递了，便可以进行修改。

补充知识：

1. 如果捕获列表为[&]，则表示所有的外部变量都按引用传递给lambda使用
2. 如果捕获列表为[=]，则表示所有的外部变量都按值传递给lambda使用
3. 匿名函数构建的时候对于按值传递的捕获列表，会立即将当前可以取到的值拷贝一份作为常数，然后将该常数作为参数传递，即：

```c++
int main()
{
	int c = 12;
    //Add构建的时候实际是：[12](int a,int b)->int{}
	auto Add = [c](int a, int b)->int {
		return c;
	};
	std::cout << Add(1, 2) << std::endl;
	return 0;
}
```





|                     | 捕获列表参数一览                                             |
| :-----------------: | :----------------------------------------------------------- |
|       [names]       | names是一个逗号分隔的名字列表，这些名字都是Lambda所在函数的局部变量。默认情况下，这些变量会被拷贝，然后按值传递，名字前面如果使用了&，则按引用传递 |
|         [&]         | 隐式捕获列表，Lambda体内使用的局部变量都按引用方式传递       |
|         [=]         | 隐式捕获列表，Lanbda体内使用的局部变量都按值传递             |
| [&,identifier_list] | identifier_list是一个逗号分隔的列表，包含0个或多个来自所在函数的变量，这些变量采用值捕获的方式，其他变量则被隐式捕获，采用引用方式传递，identifier_list中的名字前面不能使用&。 |
| [=,identifier_list] | identifier_list中的变量采用引用方式捕获，而被隐式捕获的变量都采用按值传递的方式捕获。identifier_list中的名字不能包含this，且这些名字面前必须使用&。 |
|         []          | 空捕获列表，Lambda不能使用所在函数中的变量。                 |