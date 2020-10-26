# 变量和基本类型

## 基本内置类型

|   类型   |    含义    |   最小尺寸   |
|:---------|:----------|:-------------|
| bool     | 布尔类型   |    未定义    |
| char     | 字符       |    8        | 
| wchar_t  | 宽字符     |   16        |
| char16_t | Unicode字符|   16        |
| char32_t | Unicode字符|   32        |
| short    | 短整型     |   16        |
| int      | 整型       |   16        |
| long     | 长整型     |   32        |
| long long| 长整型     |   64        |
| float    | 单精度浮点数| 6位有效数字  |
| double   | 双精度浮点数| 10位有效数字 |
| long double| 扩展精度浮点数| 10位有效数字 |

**带符号类型和无符号类型**
signed 可表示 *负数、零、正数*

unsigned 可表示 *零、正数*

**字面值常量**
可以将整数字面值写作十进制、八进制、十六进制。以零开头的整数表示八进制、0x开头的整数表示十六进制

**进制转换**
```C++
//C
printf("%05o\n",35);    //按八进制格式输出，保留5位高位补零
printf("%03d\n",35);    //按十进制格式输出，保留3位高位补零
printf("%05x\n",35);    //按十六进制格式输出，保留5位高位补零

//C++
cout << "35的8进制:" << std::oct << 35<< endl;  
cout << "35的10进制" << std::dec << 35 << endl;  
cout << "35的16进制:" << std::hex << 35 << endl;  
cout << "35的2进制: " << bitset<8>(35) << endl;      //<8>：表示保留8位输出
```

## 变量定义
（1）基本形式：

类型说明符，随后紧跟着一个或者多个变量名组成的列表，其中变量名以逗号分隔，最后以分号结束。

（2）初始值

在C++中，初始化和赋值是2个完全不同的操作。初始化的含义是创建变量的时候赋予一个初始值，而赋值的含义是把对象的当前值擦除，用一个新值来替代。两者区别很小。

（3）列表初始化

用花括号来初始化变量的方式，称为列表初始化。

（4）默认初始化

如果定义变量没有指定初始值，则变量被默认初始化。


## 变量声明和定义的关系

变量声明：规定了变量的类型和名字。

变量定义：除声明之外，还需要申请存储空间。

如果想声明一个变量，而非定义它，需要使用extern关键词。

```C++
{
    extern int i;    // 声明i而非定义i
    int j;           // 声明并定义j
}
```
*tip 变量只能被定义一次，但可以被多次声明。*

### C++关键字 不含变量类型和特殊语句
- alignas
- alignof
- asm
- auto
- class
- const              常量，const修饰的变量不可改变值
- constexpr          常量表达式，在编译过程中就得到计算结果的表达式
- const_cast
- decltype           类型指示符：选择并返回操作符的数据类型。只得到类型，不实际计算表达式的值。
- dynamic_cast
- enum
- explicit
- export
- extren
- friend
- goto
- inline
- mutable
- namespace
- noexcept
- nullptr
- operator
- private
- protected
- public
- register
- reinterpret_cast
- sizeof
- static
- static_assert
- static_cast
- struct
- template
- this
- thread_local
- throw
- typedef
- typeid
- typename
- union
- unsigned
- using
- virtual
- void
- volatile

//TODO 补充每个关键字的含义和用法

### 特殊语句关键字
- while
- for
- break
- continue
- return
- switch
- case
- default
- try
- catch
- if
- else
- new
- delete


## 名字的作用域
作用域：C++中大多数作用域都用花括号分隔。

作用域中一旦声明了某个名字，它所嵌套的所有作用域都能访问该名字。同时，允许在内层作用域中重新定义外层作用域中有的名字。

*warning 如果函数有可能用到某全局变量，则不宜再定义一个同名的局部变量。*

## 复合类型
定义: 复合类型是基于其他类型定义的类型。

## 引用
引用：为对象起另外一个名字。

*warning 引用必须被初始化。 引用本身不是对象，所以不能定义引用的引用。 引用要和绑定的对象严格匹配。 引用类型的初始值，必须是一个对象。*

## 指针
指针：本身就是一个对象。允许对指针赋值和拷贝。指针无须在定义的时候赋值。

### 利用指针访问对象

如果指针指向了一个对象，则允许使用解引用符（*）来访问该对象。取址符（&）

```C++
int ival = 42;
int * p  = &ival;
int * p2 = p;
```
空指针 nullptr (C++11)
int *p = nullptr 等价于 int *p = 0;

### void* 指针

## 理解复合类型的声明
### 指向指针的指针

** 表示指向指针的指针

*** 表示指向指针的指针的指针

### 指向指针的引用

不能定义指向引用的指针。但指针是对象，所以存在对指针的引用。

## const 限定符
定义：const 指定一个变量的值为常量，不可被改变。const 变量必须被初始化。

*默认状态下，const对象仅在文件内有效。当多个文件出现了同名的const变量时，等同于在不同文件中分别定义了独立的变量。*

*如果想让const变量在文件间共享，则使用extern修饰。*

### const的引用

允许为一个常量引用绑定非常量的对象、字面值，甚至是个一般表达式。

一般，引用的类型必须与其所引用对象的类型一致，特殊情况是表达式。

### 指针和const
弄清楚类型，可以从右边往左边阅读。

*所谓的指向常量的指针或引用，不过是指针或引用自以为是，仅要求不能通过该指针改变对象的值。而没有规定那个对象的值不能通过其他途径改变*

**const指针**

常量指针（*const）必须初始化，一旦完成初始化，则它的值（存放指针的那个地址）不可改变。

### 顶层const
top-level const 指针本身是一个常量
low-level const 指针所指的对象是一个常量

### constexpr 和常量表达式
常量表达式（const expression)是指值不会改变并且在编译过程就得到计算结果的表达式。
C++新标准规定，允许将变量声明为constexpr类型以便由编译器来验证变量的值是否是一个常量表达式。

## 处理类型

### 类型别名

两种方法定义类型别名

```C++
// 第一种
typedef double wages;   //wages 是double的同义词
typedef wages base, *p; // base是double的同义词，p是 double * 的同义词

//第二种
using SI = Sale_item; //SI 是 Sale_item的同义词
```
### auto 类型说明符

auto类型说明符：让编译器通过初始值来推算变量的类型。

### decltype 类型指示符

decltype类型指示符：选择并返回操作符的数据类型。只得到类型，不实际计算表达式的值。

```C++
const int ci = 0, &cj = ci;
decltype(ci) x = 0; // x的类型是const int
decltype(cj) y = x; // y的类型是const int &, y 绑定到变量x
decltype(cj) z; // 错误 z是const int &, 必须被初始化

// delctype的结果可以是引用类型
int i = 42, *p = &i, &r=i;
delctype(r+0) b; //正确， 加法的结果是int, b是未初始化的int
delctype(*p) c; // 错误， *p的类型是 int &, 必须初始化
```

**切记：delctype((var)) （注意是双层括号）的结果永远是引用，而delctype(var)结果只有当var本身是一个引用时才是引用。**

## 自定义数据结构

### struct

### class

数据结构是把一组相关的数据元素组织起来，然后使用它们的策略和方法。

类一般不定义在函数体内，为了确保各个文件中类的定义一致，类通常被定义在头文件中，而且类所在头文件的名字应该与类的名字一样。

头文件通常包含那些被定义一次的实体。

### 预处理器
头文件保护符

```C++
#ifndef SALES_DATA_H  //当且仅当变量未定义时为真，相反的 #ifdef
#define SALES_DATA_H  // 指定一个名字设定为预处理变量
#include <string>
struct Sales_data{
    std::string bookNo;
    unsigned units_sold = 0;
    double revenue = 0.0;
};
#endif // #ifndef #ifdef 结束符
```
一般把预处理变量的名字全部大写。