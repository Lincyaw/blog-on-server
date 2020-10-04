---
title: C++笔记之STL
date: 2019-08-13 13:22:53
tags: C++笔记
---
关于STL简介

C++标准模板库的核心包括:	容器Containers\算法Algorithms\迭代器iterator  
<!--more-->
目前，STL 中已经提供的容器主要如下：  

```
ector <T>：一种向量。  
list <T>：一个双向链表容器，完成了标准 C++ 数据结构中链表的所有功能。  
queue <T>：一种队列容器，完成了标准 C++ 数据结构中队列的所有功能。  
stack <T>：一种栈容器，完成了标准 C++ 数据结构中栈的所有功能。  
deque <T>：双端队列容器，完成了标准 C++ 数据结构中栈的所有功能。  
priority_queue <T>：一种按值排序的队列容器。  
set <T>：一种集合容器。  
multiset <T>：一种允许出现重复元素的集合容器。  
map <key, val>：一种关联数组容器。  
multimap <key, val>：一种允许出现重复 key 值的关联数组容器。  
```

# STL详情
## string类简介
STL 中只有一个字符串类，即 basic_string。类 basic_string 实现管理以 \0 结尾的字符数组，字符类型由模板参数决定。  
STL 的 C++ 标准程序库中的 string 类，使用时不必担心内存是否充足、字符串长度等问题。  
string 作为类出现，其集成的操作函数足以完成多数情况下的需要。可以使用 "=" 进行赋值，使用 "==" 进行等值比较，使用 "+" 做串联。
要使用 string 类，必须包含头文件 <string>。在 STL 库中，basic_string 有两个预定义类型：包含 char 的 string 类型和包含 wchar 的 wstring 类型。  
string 类的 string::npos 可同时定义字符串的最大长度，通常设置为无符号 int 的最大值。string 类包含了 6 个构造函数。string 类支持 cin 方式和 getline() 方式两种输入方式。简单示例如下：
``` bash
string stuff;
cin >> stuff;
getline(cin, stuff);
```
上述三行代码，第一行是声明 string 类的对象 stuff，第二行是从屏幕读入输入的字符串，第三行同样实现第二行代码的功能。

string 库提供了许多其他功能，如删除字符串的部分或全部，用一个字符的部分或全部替换另一个字符串的部分或全部，插入、删除字符串中数据，比较、提取、复制、交换等。

### string类成员函数汇总
|函数名称	|功能
|-----------|:-----------------:|
|构造函数	|产生或复制字符串|
|析构函数	|销毁字符串|
|=，assign	|赋以新值|
|Swap	|交换两个字符串的内容|
|+ =，append( )，push_back()	|添加字符|
|insert ()	|插入字符|
|erase()	|删除字符|
|clear ()	|移除全部字符|
|resize ()	|改变字符数量|
|replace()	|替换字符|
|+	|串联字符串|
|==，！ =，<，<=，>，>=，compare()	|比较字符串内容|
|size()，length()	|返回字符数量|
|max_size ()	|返回字符的最大可能个数|
|empty ()	|判断字符串是否为空|
|capacity ()	|返回重新分配之前的字符容量|
|reserve()	|保留内存以存储一定数量的字符|
|[ ],at()	|存取单一字符|
|>>，getline()	|从 stream 中读取某值|
|<<	将值写入 |stream|
|copy()	|将内容复制为一个 C - string|
|c_str()	|将内容以 C - string 形式返回|
|data()	|将内容以字符数组形式返回|
|substr()	|返回子字符串|
|find()	|搜寻某子字符串或字符|
|begin( )，end()	|提供正向迭代器支持|
|rbegin()，rend()	|提供逆向迭代器支持|
|get_allocator()	|返回配置器|

### string构造函数和析构函数详解

构造函数有四个参数，其中三个具有默认值。要初始化一个 string 类，可以使用 C 风格字符串或 string 类型对象，也可以使用 C 风格字符串的部分或 string 类型对象的部分或序列。

```
注意，不能使用字符或者整数去初始化字符串。
```
常见的 string 类构造函数有以下几种形式：   

```
string strs //生成空字符串
string s(str) //生成字符串str的复制品
string s(str, stridx) //将字符串str中始于stridx的部分作为构造函数的初值
string s(str, strbegin, strlen) //将字符串str中始于strbegin、长度为strlen的部分作为字符串初值
string s(cstr) //以C_string类型cstr作为字符串s的初值
string s(cstr,char_len)    //以C_string类型cstr的前char_len个字符串作为字符串s的初值
strings(num, c) //生成一个字符串，包含num个c字符
strings(strs, beg, end)    //以区间[beg, end]内的字符作为字符串s的初值
```

析构函数的形式如下：

```
~string() //销毁所有内存，释放内存
```
如果字符串只包含一个字符，使用构造函数对其初始化时，使用以下两种形式比较合理：
```
std::string s('x');    //错误
std::string s(1, 'x');    //正确
```
或
```
std::string s("x");    //正确
```
C_string 一般被认为是常规的 C++ 字符串。目前，在 C++ 中确实存在一个从 const char * 到 string 的隐式型别转换，却不存在从 string 对象到 C_string 的自动型别转换。对于 string 类型的字符串，可以通过 c_str() 函数返回该 string 类对象对应的 C_string 

通常，程序员在整个程序中应坚持使用 string 类对象，直到必须将内容转化为 char* 时才将其转换为 C_string。

```
#include <iostream>
#include <string>
using namespace std;

int main ()
{
    string str ("12345678");
    char ch[ ] = "abcdefgh";
    string a; //定义一个空字符串
    string str_1 (str); //构造函数，全部复制
    string str_2 (str, 2, 5); //构造函数，从字符串str的第2个元素开始，复制5个元素，赋值给str_2
    string str_3 (ch, 5); //将字符串ch的前5个元素赋值给str_3
    string str_4 (5,'X'); //将 5 个 'X' 组成的字符串 "XXXXX" 赋值给 str_4
    string str_5 (str.begin(), str.end()); //复制字符串 str 的所有元素，并赋值给 str_5
    cout << str << endl;
    cout << a << endl ;
    cout << str_1 << endl;
    cout << str_2 << endl;
    cout << str_3 << endl;
    cout << str_4 << endl;
    cout << str_5 << endl;
    return 0;
}
```
运行结果为

```
12345678

12345678
34567
abcde
XXXXX
12345678
```
使用 cout 输出 string 类型对象 a 时，输出为空。这是因为没有给 string 类型对象 a 赋值。

### 获取字符串长度详解
String 类型对象包括三种求解字符串长度的函数：size() 和 length()、 maxsize() 和 capacity()：
- size() 和 length()：  这两个函数会返回 string 类型对象中的字符个数，且它们的执行效果相同。
- max_size()：           max_size() 函数返回 string 类型对象最多包含的字符数。一旦程序使用长度超过 max_size() 的 string 操作，编译器会拋出 length_error 异常。
- capacity()：           该函数返回在重新分配内存之前，string 类型对象所能包含的最大字符数。

string 类型对象还包括一个 reserve() 函数。调用该函数可以为 string 类型对象重新分配内存。重新分配的大小由其参数决定。reserve() 的默认参数为 0。

上述几个函数的使用方法如下程序所示：

```
#include <iostream>
#include <string>
using namespace std;
int main ()
{
    int size = 0;
    int length = 0;
    unsigned long maxsize = 0;
    int capacity=0;
    string str ("12345678");
    string str_custom;
    str_custom = str;
    str_custom.resize (5);
    size = str_custom.size();
    length = str_custom.length();
    maxsize = str_custom.max_size();
    capacity = str_custom.capacity();
    cout << "size = " << size << endl;
    cout << "length = " << length << endl;
    cout << "maxsize = " << maxsize << endl;
    cout << "capacity = " << capacity << endl;
    return 0;
}
```

程序执行结果为：

```
size = 8
length = 8
maxsize = 2147483647
capacity = 15
```

### string获取字符串元素：[]和at()

在通常情况下，string 是 C++ 中的字符串。字符串是一种特殊类型的容器，专门用来操作字符序列。

字符串中元素的访问是允许的，一般可使用两种方法访问字符串中的单一字符：下标操作符[] 和 成员函数at()。两者均返回指定的下标位置的字符。第 1 个字符索引（下标）为 0，最后的字符索引为 length()-1。

需要注意的是，这两种访问方法是有区别的：
- 下标操作符 [] 在使用时不检查索引的有效性，如果下标超出字符的长度范围，会示导致未定义行为。对于常量字符串，使用下标操作符时，字符串的最后字符（即 '\0'）是有效的。对应 string 类型对象（常量型）最后一个字符的下标是有效的，调用返回字符 '\0'。
- 函数 at() 在使用时会检查下标是否有效。如果给定的下标超出字符的长度范围，系统会抛出 out_of_range 异常。

[例一]

```
#include <iostream>
#include <string>
int main()
{
    const std::string cS ("c.biancheng.net");
    std::string s ("abode");
    char temp =0;
    char temp_1 = 0;
    char temp_2 = 0;
    char temp_3 = 0;
    char temp_4 = 0;
    char temp_5 = 0;
    temp = s [2]; //"获取字符 'c'
    temp_1 = s.at(2); //获取字符 'c'
    temp_2 = s [s.length()]; //未定义行为，返回字符'\0'，但Visual C++ 2012执行时未报错
    temp_3 = cS[cS.length()]; //指向字符 '\0'
    temp_4 = s.at (s.length ()); //程序异常
    temp_5 = cS.at(cS.length ()); //程序异常
    std::cout << temp <<temp_1 << temp_2 << temp_3 << temp_4 << temp_5 << std::endl;
    return 0;
}
```
通过对上述代码的分析可知，要理解字符串的存取需要多实践、多尝试，并且要牢记基础知识和基本规则。

为修改 string 字符串的内容，下标操作符 [] 和函数 at() 均返回字符的“引用”。但当字符串的内存被重新分配以后，可能会发生执行错误。

[例二]

```
#include <iostream>
#include <string>
int main()
{
    std::string s ("abode");
    std::cout << s << std::endl ;
    char& r = s[2] ; //建立引用关系
    char*p=&s[3]; //建立引用关系
    r='X' ;//修改内容
    *p='Y' ;//修改内容
    std::cout << s << std::endl; //输出
    s = "12345678"; //重新赋值
    r ='X'; //修改内容
    *p='Y'; //修改内容
    std::cout << s << std::endl; //输出
    return 0;
}
```

结果为:

```
abode
abXYe
12XY5678
```

### string字符串比较方法详解

字符串可以和类型相同的字符串相比较，也可以和具有同样字符类型的数组比较。

Basic_string 类模板既提供了  >、<、==、>=、<=、!= 等比较运算符，还提供了 compare() 函数，其中 compare() 函数支持多参数处理，支持用索引值和长度定位子串进行比较。该函数返回一个整数来表示比较结果。如果相比较的两个子串相同，compare() 函数返回 0，否则返回非零值。

#### compare()函数

类 basic_string 的成员函数 compare() 的原型如下：

```
int compare (const basic_string& s) const;
int compare (const Ch* p) const;
int compare (size_type pos, size_type n, const basic_string& s) const;
int compare (size_type pos, size_type n, const basic_string& s,size_type pos2, size_type n2) const;
int compare (size_type pos, size_type n, const Ch* p, size_type = npos) const;
```

如果在使用 compare() 函数时，参数中出现了位置和大小，比较时只能用指定的子串。例如：

```
s.compare {pos,n, s2);
```

若参与比较的两个串值相同，则函数返回 0；若字符串 S 按字典顺序要先于 S2，则返回负值；反之，则返回正值。下面举例说明如何使用 string 类的 compare() 函数。

_例一_
```
#include <iostream>
#include <string>
using namespace std;
int main ()
{
    string A ("aBcdef");
    string B ("AbcdEf");
    string C ("123456");
    string D ("123dfg");
    //下面是各种比较方法
    int m=A.compare (B); //完整的A和B的比较
    int n=A.compare(1,5,B,4,2); //"Bcdef"和"AbcdEf"比较
    int p=A.compare(1,5,B,4,2); //"Bcdef"和"Ef"比较
    int q=C.compare(0,3,D,0,3); //"123"和"123"比较
    cout << "m = " << m << ", n = " << n <<", p = " << p << ", q = " << q << endl;
    cin.get();
    return 0;
}
```
程序的执行结果为：
```
m = 1, n = -1, p = -1, q = 0
```
由此可知，string 类的比较 compare() 函数使用非常方便，而且能区分字母的大小写。

#### 比较运算符

String 类的常见运算符包括 >、<、==、>=、<=、!=。其意义分别为"大于"、"小于"、"等于"、"大于等于"、"小于等于"、"不等于"。

比较运算符使用起来非常方便，此处不再介绍其函数原型，读者直接使用即可。下面以例 2 进行说明。

```
#include <iostream>
#include <string>
using namespace std;
void TrueOrFalse (int x)
{
    cout << (x?"True":"False")<<endl;
}
int main ()
{
    string S1 = "DEF";
    string CP1 = "ABC";
    string CP2 = "DEF";
    string CP3 = "DEFG";
    string CP4 ="def";
    cout << "S1= " << S1 << endl;
    cout << "CP1 = " << CP1 <<endl;
    cout << "CP2 = " << CP2 <<endl;
    cout << "CP3 = " << CP3 <<endl;
    cout << "CP4 = " << CP4 <<endl;
    cout << "S1 <= CP1 returned ";
    TrueOrFalse (S1 <=CP1);
    cout << "S1 <= CP2 returned ";
    TrueOrFalse (S1 <= CP2);
    cout << "S1 <= CP3 returned ";
    TrueOrFalse (S1 <= CP3);
    cout << "CP1 <= S1 returned ";
    TrueOrFalse (CP1 <= S1);
    cout << "CP2 <= S1 returned ";
    TrueOrFalse (CP2 <= S1);
    cout << "CP4 <= S1 returned ";
    TrueOrFalse (CP4 <= S1);
    cin.get();
    return 0;
}
```

结果为	

```
S1= DEF
CP1 = ABC
CP2 = DEF
CP3 = DEFG
CP4 = def
S1 <= CP1 returned False
S1 <= CP2 returned True
S1 <= CP3 returned True
CP1 <= S1 returned True
CP2 <= S1 returned True
CP4 <= S1 returned False
```

由上述内容可知，使用比较运算符可以非常容易地实现字符串的大小比较。在使用时比较运算符时，读者应注意，对于参加比较的两个字符串，任一个字符串均不能为 NULL，否则程序会异常退出。

### 字符串内容的修改和替换方法

#### 字符串内容的修改  

可以通过使用多个函数修改字符串的值。例如 assign()，operator=，erase()，交换（swap），插入（insert）等。另外，还可通过 append() 函数添加字符。

下面逐一介绍各成员函数的使用方法。

##### assign()函数

使用 assign() 函数可以直接给字符串赋值。该函数既可以将整个字符串赋值给新串，也可以将字符串的子串赋值给新串。其在 basic_string 中的原型为：

```
basic_string& assign (const E*s); //直接使用字符串赋值
basic_string& assign (const E*s, size_type n);
basic_string& assign (const basic_string & str, size_type pos, size_type n);
//将str的子串赋值给调用串
basic_string& assign (const basic_string& str);    //使用字符串的“引用”賦值
basic_string& assign (size_type n, E c) ; //使用 n个重复字符賦值
basic_string& assign (const_iterator first, const_iterator last);    //使用迭代器赋值
```

以上几种方法在例 1 中均有所体现。请读者参考下述代码。

【例 1】

```
#include <iostream>
#include <string>
using namespace std;
int main()
{
    string str1 ("123456");
    string str;
    str.assign (str1); //直接赋值
    cout << str << endl;
    str.assign (str1, 3, 3); //赋值给子串
    cout << str << endl;
    str.assign (str1,2,str1.npos);//赋值给从位置 2 至末尾的子串
    cout << str << endl;
    str.assign (5,'X'); //重复 5 个'X'字符
    cout << str << endl;
    string::iterator itB;
    string::iterator itE;
    itB = str1.begin ();
    itE = str1.end();
    str.assign (itB, (--itE)); //从第 1 个至倒数第 2 个元素，赋值给字符串 str
    cout << str << endl;
    return 0;
}
```

结果为
```
123456
456
3456
XXXXX
12345
```
##### operator= 函数

operator= 的功能就是赋值。

##### erase()函数

erase() 函数的原型为：

```
iterator erase (iterator first, iterator last);
iterator erase (iterator it);
basic_string& erase (size_type p0 = 0, size_type n = npos);
```

erase() 函数的使用方法为：

```
str.erase (str* begin(), str.end());
或 str.erase (3);
```

##### swap()函数

swap()函数的原型为：

```
void swap (basic_string& str);
```

swap()函数的使用方法为：

```
string str2 ("abcdefghijklmn");
str.swap (str2);
```

##### insert()函数
insert () 函数的原型为：
```
basic_string& insert (size_type p0 , const E * s); //插人 1 个字符至字符串 s 前面
basic_string& insert (size_type p0 , const E * s, size_type n); // 将 s 的前 3 个字符插入p0 位置
basic_string& insert (size_type p0, const basic_string& str);
basic_string& insert (size_type p0, const basic_string& str,size_type pos, size_type n); //选取 str 的子串
basic_string& insert (size_type p0, size_type n, E c); //在下标 p0 位置插入  n 个字符 c
iterator insert (iterator it, E c); //在 it 位置插入字符 c
void insert (iterator it, const_iterator first, const_iterator last); //在字符串前插入字符
void insert (iterator it, size_type n, E c) ; //在 it 位置重复插入 n 个字符 c
```
insert() 函数的使用方法为：
```
string A("ello");
string B ;
B.insert(1,A);
cout << B << endl;
A = "ello";
B = "H";
B.insert (1,"yanchy ",3);
cout<< B <<endl;
A = "ello";
B = "H";
B.insert (1,A,2,2);
cout << B << endl;
A="ello";
B.insert (1 , 5 , 'C');
cout << B << endl;
A = "ello";
string::iterator it = B.begin () +1;
const string:: iterator itF = A.begin();
const string:: iterator itG = A.end();
B.insert(it,itF,itG);
cout << B << endl;
```

##### append 函数
append() 函数的原型为：
```
basic_string& append (const E * s); //在原始字符串后面追加字符串s
basic_string& append (const E * s, size_type n);//在原始字符串后面追加字符串 s 的前 n 个字符
basic_string& append (const basic_string& str, size_type pos,size_type n);//在原始字符串后面追加字符串 s 的子串 s [ pos,…,pos +n -1]
basic_string& append (const basic_string& str);
basic_string& append (size_type n, E c); //追加 n 个重复字符
basic_string& append (const_iterator first, const_iterator last); //使用迭代器追加
```
append() 函数的使用方法为：
```
A = "ello";
cout << A << endl;
cout << B << endl;
B.append(A);
cout << B << endl;
A = "ello";
cout << A << endl;
cout << B << endl;
B.append("12345",2);
cout << B << endl;
A = "ello";
cout << A << endl;
cout << B << endl;
B.append("12345",2,3);
cout << B << endl;
A = "ello";
B = "H";
cout << A << endl;
cout << B << endl;
B.append (10, 'a');
cout << B << endl;
A = "ello";
B = 'H';
cout << A << endl ;
cout << B << endl;
B.append(A.begin(), A, end());
cout << B << endl;
```
下面通过一个完整的例子介绍这些函数的使用：
```
#include <iostream>
#include <string>
using namespace std;
int main ()
{
    string str1 ("123456");
    string str2 ("abcdefghijklmn");
    string str;
    str.assign(str1);
    cout << str << endl;
    str.assign (str1 , 3, 3);
    cout << str << endl;
    str.assign (str1, 2, str1.npos);
    cout << str << endl;
    str.assign (5, 'X');
    cout << str << endl;
    string::iterator itB;
    string::iterator itE;
    itB = str1.begin ();
    itE = str1.end();
    str.assign (itB, (--itE));
    cout << str << endl;
    str = str1;
    cout << str << endl;
    str.erase(3);
    cout << str << endl;
    str.erase (str.begin (), str.end());
    cout << ":" << str << ":" << endl;
    str.swap(str2);
    cout << str << endl;
    string A ("ello");
    string B ("H");
    B.insert (1, A);
    cout << B << endl;
    A = "ello";
    B ='H';
    B.insert (1, "yanchy ", 3);
    cout << "插入: " << B << endl;
    A = "ello";
    B = "H";
    B.insert(1,A,2,2);
    cout << "插入:" << B << endl;
    A = "ello";
    B = "H";
    B.insert (1,5,'C');
    cout << "插入:" << B << endl;
    A = "ello";
    B = "H";
    string::iterator it = B.begin () +1;
    const string::iterator itF = A.begin ();
    const string::iterator itG = A.end ();
    B.insert(it,itF,itG);
    cout<<"插入："<< B << endl;
    A = "ello";
    B = "H";
    cout << "A = " << A <<", B = " << B << endl ;
    B.append (A);
    cout << "追加：" << B << endl;
    B = "H";
    cout << "A = "<< A << ", B= " << B << endl;
    B.append("12345", 2);
    cout << "追加：" << B << endl;
    A = "ello";
    B = "H";
    cout << "A = " << A << ", B= " << B << endl;
    B.append ("12345", 2, 3);
    cout << "追加：" << B << endl;
    A = "ello";
    B = "H";
    cout << "A = " << A <<", B = " << B << endl;
    B.append (10 , 'a');
    cout << "追加:"<< B << endl;
    A = "ello";
    B = "H";
    cout << "A = " << A << ", B = " << B << endl;
    B.append(A.begin() , A.end());
    cout << "追加:" << B << endl;
    cin.get();
    return 0;
}
```
程序运行结果：
```
123456
456
3456
XXXXX
12345
123456
123
::
abcdefghijklmn
Hello
插入: Hyan
插入:Hlo
插入:HCCCCC
插入：Hello
A = ello, B = H
追加：Hello
A = ello, B= H
追加：H12
A = ello, B= H
追加：H345
A = ello, B = H
追加:Haaaaaaaaaa
A = ello, B = H
追加:Hello
```
##### 字符串内容的替换
如果在一个字符串中标识出具体位置，便可以通过下标操作修改指定位置字符的值，或者替换某个子串。完成此项操作需要使用 string 类的成员函数 replace()。

replace() 函数的原型如下：
```
basic_string& replace (size_type p0, size_type n0, const E * s); //使用字符串 s 中的 n 个字符，从源串的位置 P0 处开始替换
basic_string& replace (size_type p0, size_type n0, const E *s, size_type n); //使用字符串 s 中的 n 个字符，从源串的位置 P0 处开始替换 1 个字符
basic_string& replace (size_type p0, size_type n0, const basic_string& str); //使用字符串 s 中的 n 个字符，从源串的位置 P0 处开始替换
basic_string& replace (size_type p0, size_type n0, const basic_string& str, size_type pos, size_type n); //使用串 str 的子串 str [pos, pos + n-1] 替换源串中的内容，从位置 p0 处开始替换，替换字符 n0 个
basic_string& replace (size_type p0, size_type n0, size_type n, E c); //使用 n 个字符 'c' 替换源串中位置 p0 处开始的 n0 个字符
basic_string& replace (iterator first0, iterator last0, const E * s);//使用迭代器替换，和 1) 用法类似
basic_string& replace (iterator first0, iterator last0, const E * s, size_type n);//和 2) 类似
basic_string& replace (iterator first0, iterator last0, const basic_string& str); //和 3) 类似
basic_string& replace (iterator first0, iterator last0, size_type n, E c); //和 5) 类似
basic_string& replace (iterator first0, iterator last0, const_iterator first, const_iterator last); //使用迭代器替换
```
该函数的使用方法参照下面的程序：
```
#include <iostream>
#include <string>
using namespace std;
int main ()
{
    string var ("abcdefghijklmn");
    const string dest ("1234");
    string dest2 ("567891234");
    var.replace (3,3, dest);
    cout << "1: " << var << endl;
    var = "abcdefghijklmn";
    var.replace (3,1, dest.c_str(), 1, 3);
    cout << "2: " << var << endl;
    var ="abcdefghijklmn";
    var.replace (3, 1, 5, 'x');
    cout << "3: " << var << endl;
    string::iterator itA, itB;
    string::iterator itC, itD;
    itA = var.begin();
    itB = var.end();
    var = "abcdefghijklmn";
    var.replace (itA, itB, dest);
    cout << "4: " << var << endl;
    itA = var.begin ();
    itB = var.end();
    itC = dest2.begin () +1;
    itD = dest2.end ();
    var = "abodefghijklmn";
    var.replace (itA, itB, itC, itD);
    cout << "5: " << var << endl;
    var = "abcdefghijklmn";
    var.replace (3, 1, dest.c_str(), 4); //这种方式会限定字符串替换的最大长度
    cout <<"6: " << var << endl;
    return 0;
}
```
程序执行结果为：
```
1: abc1234ghijklmn
2: abc234efghijklmn
3: abcxxxxxefghijklmn
4: 1234
5: 67891234efghijklmn
6: abc1234efghijklmn
```
本节讲述了诸多可进行字符串内容的修改和替换的函数及其使用方法，并给出了例题。由于每个函数可能有多个原型，希望读者根据自己的情况，掌握其中的一种或两种，以满足自己使用的需要。同时，希望读者能够对照例题的执行效果，认真阅读本章节中的源代码，彻底掌握本节内容。

### 字符串输入输出操作详解

"<<" 和 ">>" 提供了 C++ 语言的字符串输入和字符串输出功能。"<<" 可以将字符读入一个流中（例如 ostream）；">>" 可以实现将以空格或回车为 "结束符" 的字符序列读入到对应的字符串中，并且开头和结尾的空白字符不包括进字符串中。

还有一个常用的 getline() 函数，该函数的原型包括两种形式：
```
template <class CharType, class Traits, class Allocator > basic_istream<CharType, Traits>& getline (basic_istream<CharType, Traits>& _Istr,basic_string <CharType，Traits, Allocator> &_Str);
//上述原型包含 2 个参数：第 1 个参数是输入流；第 2 个参数是保存输入内容的字符串
template <class CharType, class Traits, class Allocator> basic_istream<CharType, Traits>& getline (basic_istream <CharType, Traits>&_ Istr, basic_string <CharType, Traits, Allocator>& _Str,CharType_Delim);
//上述原型包含 3 个参数：第 1 个参数是输入流，第 2 个参数保存输入的字符串，第 3 个参数指定分界符。
```
该函数可将整行的所有字符读到字符串中。在读取字符时，遇到文件结束符、分界符、回车符时，将终止读入操作，且文件结束符、分界符、回车符在字符串中不会保存；当已读入的字符数目超过字符串所能容纳的最大字符数时，将会终止读入操作。

下面分别按上述两种函数原型举例说明，参见下述程序：
```
#include <iostream>
#include <string>
using namespace std;
void main ()
{
string s1, s2;
getline(cin, s1);
getline(cin, s2, ' ');
cout << "You inputed chars are: " << s1 << endl;
cout << "You inputed chars are: " << s2 << endl;
}
```
程序的执行结果为：
```
123456
asdfgh klj
You inputed chars are: 123456
You inputed chars are: asdfgh
```
注意，程序中输入的第二行字符中间包含空格字符，而空格之后的字符没有被存储到字符串 s2 中。

### 字符串查找函数详解

在 C 语言和 C++ 语言中，可用于实现字符串查找功能的函数非常多。在 STL 中，字符串的查找功能可以实现多种功能，比如说：
- 搜索单个字符、搜索子串；
- 实现前向搜索、后向搜索；
- 分别实现搜索第一个和最后一个满足条件的字符（或子串）；

若查找 find() 函数和其他函数没有搜索到期望的字符（或子串），则返回 npos；若搜索成功，则返回搜索到的第 1 个字符或子串的位置。其中，npos 是一个无符号整数值，初始值为 -1。当搜索失败时， npos 表示“没有找到（not found）”或“所有剩佘字符”。

值得注意的是，所有查找 find() 函数的返回值均是 size_type 类型，即无符号整数类型。该返回值用于表明字符串中元素的个数或者字符在字符串中的位置。

下面分别介绍和字符查找相关的函数。

#### find()函数和 rfind()

find() 函数的原型主要有以下 4 种：
```
size_type find (value_type _Chr, size_type _Off = 0) const;
//find()函数的第1个参数是被搜索的字符、第2个参数是在源串中开始搜索的下标位置
size_type find (const value_type* _Ptr , size_type _Off = 0) const;
//find()函数的第1个参数是被搜索的字符串，第2个参数是在源串中开始搜索的下标位置
size_type find (const value_type* _Ptr, size_type _Off = 0, size_type _Count) const;
//第1个参数是被搜索的字符串，第2个参数是源串中开始搜索的下标，第3个参数是关于第1个参数的字符个数，可能是 _Ptr 的所有字符数，也可能是 _Ptr 的子串宇符个数
size_type find (const basic_string& _Str, size_type _Off = 0) const;
//第1个参数是被搜索的字符串，第2参数是在源串中开始搜索的下标位置
```
rfind() 函数的原型和find()函数的原型类似，参数情况也类似。只不过 rfind() 函数适用于实现逆向查找。

find() 函数和 rfind() 函数的使用方法参见如下程序：
```
#include <iostream>
#include <string>
using namespace std;
int main ()
{
    string str_ch (" for");
    string str (" Hi, Peter, I'm sick. Please bought some drugs for me.");
    string::size_type m= str.find ('P', 5);
    string::size_type rm= str.rfind('P', 5);
    cout << "Example - find() : The position (forward) of 'P' is: " << (int) m << endl;
    cout << "Example - rfind(): The position (reverse) of 'P' is: " << (int) rm << endl;
    string::size_type n = str.find (" some", 0);
    string::size_type rn = str.rfind (" some", 0);
    cout << "Example - find () : The position (forward) of 'some' is: " << (int) n << endl;
    cout << "Example - rfind () : The position (reverse) of 'some' is: " << (int) rn << endl;
    string::size_type mo = str.find (" drugs", 0, 5);
    string::size_type rmo = str.rfind (" drugs", 0, 5);
    cout << "Example - find(): The position (forward) of 'drugs' is: " << (int) mo << endl;
    cout << "Example - rfind(): The position (reverse) of 'drugs' is: " << (int) rmo << endl;
    string::size_type no = str.find (str_ch, 0);
    string::size_type rno = str.rfind(str_ch, 0);
    cout << "Example - find (): The position of 'for' is: " << (int) no << endl;
    cout << "Example - rfind(): The position of 'for' is: " << (int) rno << endl;
    cin.get ();
}
```
程序的运行结果为：
```	
Example - find() : The position (forward) of 'P' is: 5
Example - rfind(): The position (reverse) of 'P' is: 5
Example - find () : The position (forward) of 'some' is: 35
Example - rfind () : The position (reverse) of 'some' is: -1
Example - find(): The position (forward) of 'drugs' is: 40
Example - rfind(): The position (reverse) of 'drugs' is: -1
Example - find (): The position of 'for' is: 46
Example - rfind(): The position of 'for' is: -1
```
#### find_first_of()函数和 find_last_of()函数
find_first_of() 函数可实现在源串中搜索某字符串的功能，该函数的返回值是被搜索字符串的第 1 个字符第 1 次出现的下标（位置）。若查找失败，则返回 npos。

find_last_of() 函数同样可实现在源串中搜索某字符串的功能。与 find_first_of() 函数所不同的是，该函数的返回值是被搜索字符串的最后 1 个字符的下标（位置）。若查找失败，则返回 npos。

上述两个函数的原型分别为：
```
size_type find_first_not_of (value_type_Ch, size_type_Off = 0) const; size_type find_first_of (const value_type* _Ptr, size_type _Off = 0) const;
size_type find_first_of (const value_type* _Ptr, size_type_Off, size_type_Count) const;
size_type find_first_of (const basic_string & _Str, size_type_Off = 0) const;
size_type find_last_of (value_type _Ch, size_type_Off = npos) const;
size_type find_last_of (const value_type* _Ptr, size_type_Off = npos) const;
size_type find_last_of (const value_type* _Ptr, size_type _Off, size_type _Count) const;
size_type find_last_of (const basic_string& _Str, size_type_Off = npos) const;
```
下面的程序示例详细阐述了 find_first_of() 函数和 find_last_of() 函数的使用方法。这两个函数和 find() 函数及 rfind() 函数的使用方法相同，具体参数的意义亦相同。
```
#include <iostream>
#include <string>
using namespace std;
int main ()
{
    string str_ch ("for");
    string str("Hi, Peter, I'm sick. Please bought some drugs for me. ");
    int length = str.length();
    string::size_type m = str.find_first_of ('P', 0);
    string::size_type rm = str.find_last_of ('P', (length - 1));
    cout << "Example - find_first_of (): The position (forward) of 'P' is: " << (int) m << endl;
    cout << "Example - find_last_of (): The position (reverse) of 'P' is： " << (int) rm << endl;
    string:: size_type n = str.find_first_of ("some", 0);
    string:: size_type rn = str.find_last_of ("some", (length -1));
    cout << "Example - find_first_of(): The position (forward) of 'some' is: " << (int) n << endl;
    cout << "Example - find_last_of(): The position (reverse) of 'some' is: " << (int) rn << endl;
    string:: size_type mo = str.find_first_of ("drugs", 0, 5);
    string:: size_type rmo = str.find_last_of ("drugs", (length-1), 5);
    cout << "Example - find_first_of () : The position (forward) of 'drugs' is: " << (int) mo << endl;
    cout << "Example - find_last_of () : The position (reverse) of 'drugs' is: " << (int) rmo << endl;
    string::size_type no = str.find_first_of (str_ch, 0);
    string::size_type rno = str.find_last_of (str_ch, (length -1));
    cout << "Example - find_first_of() : The position of 'for' is: " << (int) no << endl;
    cout << "Example - find_last_of () : The position of 'for' is: " << (int) rno << endl;
    cin.get();
    return 0;
}
```
程序执行结果：
```
Example - find_first_of (): The position (forward) of 'P' is: 4
Example - find_last_of (): The position (reverse) of 'P' is： 21
Example - find_first_of(): The position (forward) of 'some' is: 5
Example - find_last_of(): The position (reverse) of 'some' is: 51
Example - find_first_of () : The position (forward) of 'drugs' is: 8
Example - find_last_of () : The position (reverse) of 'drugs' is: 48
Example - find_first_of() : The position of 'for' is: 8
Example - find_last_of () : The position of 'for' is: 48
```
#### find_first_not_of()函数和 find_last_not_of()函数
find_first_not_of() 函数的函数原型为：
```
size_type find_first_not_of (value_type _Ch, size_type_Off = 0) const;
size_type find_first_not_of (const value_type * _Ptr, size_type_Off = 0) const;
size_type find_first_not_of (const value_type* _Ptr, size_type_Off, size_type_Count) const;
size_type find_first_not_of (const basic_string & _Str, size_type_Off = 0) const;
```
find_first_not_of() 函数可实现在源字符串中搜索与指定字符（串）不相等的第 1 个字符；find_last_not_of() 函数可实现在源字符串中搜索与指定字符（串）不相等的最后 1 个字符。这两个函数的参数意义和前面几个函数相同，它们的使用方法和前面几个函数也基本相同。详见下面的程序：
```
#include < iostream >
#include <string>
using namespace std;
int main ()
{
    string str_ch (" for");
    string str ("Hi, Peter, I'm sick. Please bought some drugs for me.");
    int length = str.length ();
    string::size_type m= str.find_first_not_of ('P',0);
    string::size_type rm= str.find_last_not_of ('P', (length -1);
    cout << "Example - find_first_of (): The position (forward) of 'P' is: " << (int) m << endl;
    cout << "Example - find_last_of (): The position (reverse) of 'P' is: " << (int) rm << endl;
    string:: size_type n = str.find_first_not_of ("some", 0);
    string:: size_type rn = str.find_last_not_of ("some", (length -1));
    cout << "Example - find_first_of (): The position (forward) of 'some' is: " << (int) n << endl;
    cout << "Example - find_last_of (): The position (reverse) of 'some' is: " << (int) rn << endl;
    string:: size_type mo = str.find_first_not_of ("drugs", 0, 5);
    string:: size_type rmo = str.find_last_not_of ("drugs", (length-1), 5);
    cout << "Example - find_first_of (): The position (forward) of 'drugs' is: " << (int) mo << endl;
    cout << "Example - find_last_of (): The position (reverse) of 'drugs' is: " << (int) rno << endl;
    string::size_type no = str.find_first_not_of (str_ch, 0);
    string::size_type rno = str.find_last_not_of (str_ch, (length-1));
    cout << "Example - find_first_of (): The position of 'for' is: " << (int) no << endl;
    cout << "Example - find_last_of () : The position of 'for' is: " << (int) rno << endl;
    cin.get ();
    return 0;
}
```
程序运行结果为：
```
Example - find_first_of (): The position (forward) of 'P' is: 0
Example - find_last_of (): The position (reverse) of 'P' is: 52
Example - find_first_of (): The position (forward) of 'some' is: 0
Example - find_last_of (): The position (reverse) of 'some' is: 52
Example - find_first_of (): The position (forward) of 'drugs' is: 0
Example - find_last_of (): The position (reverse) of 'drugs' is: 52
Example - find_first_of (): The position of 'for' is: 0
Example - find_last_of () : The position of 'for' is: 52
```
本小节主要讲述 C++ STL 中的字符串查找函数。对于所述的 6 个查找函数，它们的使用形式大致相同，对于每个函数均配备了实例作为参考。请读者能认真对照例题，深刻理解这 6 个函数的使用方法，仔细体会函数每个参数的意义。



