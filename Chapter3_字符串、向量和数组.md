# 字符串、向量和数组

## 命名空间的 using 声明
```C++
using namespace:name;
```
**头文件不应包含using声明。**

## 标准库类型 string

标准库类型 string 表示可变长的字符类型

```C++
#include <string>
using std::string;
```

### 定义和初始化

```C++
string s1;
string s2(s1);
string s3("value");
string s3 = "value";
string s4(n, 'c'); //把 s4 初始化为连续 n 个字符 c 组成的串
```

*允许把字面值和字符串字面值转换成string对象。字面值和string是不同的类型。*

### string 对象上的操作

```C++
string s;
os << s       // 将s写到输出流os当中，返回os
is >> s       // 从is中读取字符串赋给s，字符串以空白分割，返回is
getline(is, s) // 从is中读取一行赋值给s,返回is
s.empty()     // 判空
s.size()      // 字符个数，返回值类型 string::size_type 无符号整型值
s[n]          // 第 n 个字符的引用，从0开始
s1+s2         // 字符拼接
s1=s2         // 用s2的副本代替s1中原来的字符
s1==s2        // 比较是否相同，大小写敏感
s1!=s2        // 比较是否不同，大小写敏感
<, <=, >, >=  // 利用字符在字典中的顺序比较，大小写敏感
```

### 处理 string 对象中的字符

*tip C++程序的头文件应该使用cname，cctype，而不应该使用name.h，ctype.h的形式*

遍历给定序列中的每个值执行某种操作

```C++
for (declaration : expression)
    statement

for (auto s:str)
    cout << s <<endl;

for (auto &s:str)
    s = toupper(s);  //调整成大写
```

也可以使用下标索引、遍历，但要注意防止越界错误

## 标准库类型 vecotr

标准库vector表示对象的集合，其中所有对象的类型都相同。

vector是一个类模板，而不是类型。

### 定义和初始化vector对象

```c++
vector<T> v1;
vector<T> v2(v1);
vector<T> v2 = v1;
vector<T> v3(n, val); // V3为n个val组成的动态数组
vector<T> v4(n);      // 创建长度为n的动态数组，重复执行值初始化
vector<T> v5{a,b,c...};
vecrot<T> v5={a,b,c...};
```
*Tips: Vector 能实现高效的增长，初始化时指定其大小没有必要，事实上性能反而会变差*

### vector的其他操作

```C++
v.empty()
v.size()         // return vector<T>::size_type
v.push_back()    //先定义一个空的vector对象，在运行的时候使用push_back在对象的尾部向其中添加具体值。
v.pop_back()     // 从头部取出第一个元素
v[n]             //使用下标索引时切忌越界访问
v1 = v2
v1 = (a,b,c...)  //用列表中元素的copy替换v1中的元素
v1 == v2
v1 != v2
<, <=, >, >=

/*
...
*/

```

**不能使用下标形式添加元素**

### 迭代器介绍

```C++
*iter            // 解引用，返回引用
iter->mem        // 等价于  (*iter).mem
++iter
--iter
iter1 == iter2
iter1 != iter2
iter + n
iter - n
iter += n
iter -= n
iter1 - iter2     // 两个迭代器相减的结果是它们之间的距离
>, >=, <, <=      // 位置比较
```

迭代器类型

```C++
vector<T> v;
const vector<T> v1;
auto t1 = v.begin()   // return vector<T>::iterator, 可读写
auto t2 = v2.begin()   // return vector<T>::const_iterator, 只能读，不可写
```

## 数组

使用数组下标的时候，通常将其定义为size_t类型。数组变量对应数组的第一个元素的指针，例如 `int a[] = {1,1,1}`, 可通过 `++a `进行遍历

定义数组必须指定数组的类型，不允许用auto推断。

不存在引用的数组。

如果两个指针分别指向不相关的对象，则不能进行对这2个指针进行比较。

C++11引入新的标准库函数 `begin()` `end()`, 可通过以下方法实现遍历

```C++
int *pbeg = begin(arr), *pend = end(arr)
while(pbeg !=pend){
    cout << *pbeg << endl;
    ++pbeg;
}
```

两个数组指针相减的结果为 `auto n = end(arr) - begin(arr)` ，返回类型为`ptrdiff_t`的标准库类型。

**C风格字符串**

*C++代码程序尽量不使用*

以空字符 `\0` 结束

头文件`cstring`，对应C语言头文件 `string.h` 的C++版本

```C++
// C 风格字符串的函数
strlen(p)          // 返回长度，空字符不计算在内
strcmp(p1, p2)     // 比较相等性
strcat(p1, p2)     //字符串拼接，p1->p2, 返回p1
strcpy(p1, p2)     // 将p2拷贝给p1, 返回p1
```

混用string对象和C风格字符串
```
string a;
const char* b = a.c_str()
```
*如果执行完c_str()函数后程序想一直能使用其返回的数组，最好将该数组重新strcpy()一份*

**多维数组**

多维数组实际上是数组的数组。

```C++
size_t cnt = 0;
for(auto &row : a)
    for (auto &col : row){
        col = cnt;
        ++cnt;
    }
int *ip[4];    // 整型指针的数组
int (*ip)[4];  // 指向含有4个整数的数组
```