---
title: race debug
date: 2023-01-05 23:14:35
categories:
      - gwx
      - c++
tags:
      - c++ debug
      - 竞赛
---





佬的笔记😍😍😍

<!-- more -->

# C++比赛中调试的方法

## 1.输入输出重定向

比赛中数据的手动输入总是花费很长的时间，所以要对数据的输入进行从定向。将数据写入文件中，然后当作标准输入提供给程序就行。
重定向输入有两种方法 这里假定将输入放进input.txt,输入放在out.txt中。程序为a.exe  （linux为 a.o)

### 1 临时重定向

在命令行中输入   
```a.exe < input.txt```
这是输入的重定向   
```a.exe > out.txt```
这是输出的重定向   
同时   
```a.exe < input.txt > out.txt```   
可以同时完成输入输出的重定向。   
临时的重定向虽好，但是每次都要手动输入，而且有时候利用IDE调试的时候也不方便，这时候就有

### 2 重定向函数

在main()的入口加一段

```
freopen("input.txt","r",stdin);
freopen("out.txt","w",stdout);
```

第一行表示将input.txt作为标准输入，stdin表示标准输入。   
第二行表示将out.txt作为标准输出，stdout表示标准输出。   
当要提交的时候将这两行注释掉即可。   
但是这样也比较麻烦，我们下面要介绍一个方法，在本机上会执行对应的代码，但测试平台上则不执行

## 2 宏定义

在代码入下

```
 #define LOCAL
 #include <iostream>
 using namespace std;
char a[100];
int main()
{
#ifdef LOCAL
    freopen("input.txt", "r", stdin);
#endif
    cin >> a;
    cout << a;
    return 0;
}
```

第一行先定义 LOCAL符号
在 #ifdef 和 #endif 之间存放在本机才执行的代码。比如刚才的重定向输入。
当提交的时候要把#define LOCAL 注释掉。    
其实也可以在编译的时候定义LOCAL符号，即
     

    g++ -DLOCAL ./test.cpp -o ./test.exe

在编译时加入-D变量名  选项即可在编译时定义变量。如果你用的是vscode就可以在task.json中添加这个选项。

## 3 对比输出

当输出很多的时候很难去一个个的和标准答案比较，这时候就要用系统自带的工具了       
window系统在命令行中输入
    

    fc out.txt 答案.txt

用于对比输出和答案之间的差异（如果用的是linux这个指令为diff）

## 4 调整栈的大小

虽然比赛中是无法调整平台栈的大小的，但一般评测平台为linux系统，默认调用栈为10mb，但是vc++ 的默认大小却只有1mb。有时会出现在本机上调试不过的现象，这时候就要将栈的大小调整一下了。    
对于vs可以之间在项目-属性中调整    
而对于g++则可以通过加-Wl,--stack=16777216   (16MB) 编译选项，来调整调用栈的大小。

