# 开始
## 1.1 编写一个简单的C++程序

```C++
int main()
{
    return 0;
}
```

## 1.1.1 编译、运行程序

1. Integrated Developed Environment, IDE

2. 程序源文件命名约定
   
Source file .cc .cxx .cpp .cp .C

3. 从命令行中运行编译器
GNU g++/Visual Studio
$ g++ -o progl progl.cc

## 1.2 输入输出

库 isotream istream ostream

1. 标准输入输出对象
   
   cin(see-in) cout(see-out) ceer(see-error) clog(see-log)
2. 简单输入输出样例
   
```c++
#include <iostream>
using namespace std;
int main()
{
    cout << "Enter two number: ";
    int a, b;
    cin >> a >> b;
    cout <<"the add result: " <<a+b << endl;
    return 0;
}
```
## 1.3 注释

> 行注释 //

> 注释界 /* 注释内容 */

## 1.4 控制流
while for if
