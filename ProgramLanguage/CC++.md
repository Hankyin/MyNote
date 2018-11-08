# C语言预处理

C/C++ 程序中的源代码中包含以 # 开头的各种编译指令，这些指令称为预处理指令。预处理指令不属于 C/C++ 语言的语法，但在一定意义上可以说预处理扩展了 C/C++。

 ANSI C 定义的预处理指令主要包括：

1. 文件包含
2. 宏定义
3. 条件编译
4. 其他的控制指令

## 文件包含 

`#include`

该指令是 C 程序设计中最常用的预处理指令。表示将

 包含文件的格式有 #include 后面跟尖括号 <> 和双引号 "" 之分。两者的主要差别是搜索路径的不同。

-  尖括号形式：如 #include<math.h>，预处理器直接到系统目录对应文件中搜索 math.h 文件，搜索不到则报错。系统提供的头文件一般采用该包含方式，而自定义的头文件不能采用该方式。
-  双引号形式：如 #include"cal.h"，首先到当前工作目录下查找该文件，如果没有找到，再到系统目录下查找。包含自定义的头文件，一般采用该方式。虽然系统头文件采用此方式也正确，但浪费了不必要的搜索时间，故系统头文件不建议采用该包含方式。

## 宏定义：

包括定义宏 #define 和宏删除 #undef。

 以 #define 开头，可以定义无参数宏和带参的宏定义。程序中经常使用无参宏定义来定义符号常量。例如：

```
#define PI 3.1416 //定义无符号宏，或定义符号常量 PI
```

 \#undef 表示删除已定义的宏，例如：

```
#undef PI //删除前面该宏的定义
```

 ## 条件编译：

条件编译（conditional compiling）命令指定预处理器依据特定的条件来判断保留或删除某段源代码。

主要是为了有选择性地执行相应操作，可以用作如下功能：

- 防止头文件多次包含。
- 让源码适应于不同的目标系统与构建工具链。

大多数编译器会提供预定义宏，在 Unix 系统中，通常预先定义好了宏 __unix__，而GCC则会预先定义好了宏 __GNUC__。类似地，微软 Windows 平台上的 Visual C 编译器会自动定义好宏 _WIN32 和宏 _MSC_VER。这样源代码就可以根据不同的宏来判断当前的编译器和操作系统，从而可以有针对性的进行一些特殊处理。

条件编译指令有 #if、#elif、#else、#endif、#ifdef、#ifndef。

if或elif后面跟整数常量预处理器表达式，非0为真，0为假。

整数常量预处理器表达式语法：

- 语法类似于C语言表达式，但有所不同
- 支持算术运算+-/<<>>，比较运算，逻辑运算
- 表达式中没有变量，取而代之的是宏。
- 一个宏没有被定义，它的值是0
- 一个宏定义了但没有复制，它的值是0.
- 支持defined运算符。

defined运算符：
使用格式：`defined (identifier)` 
如果指定的  identifier 是一个宏名称（也就是说，它已被 #define 命令定义，并且未被 #undef 命令取消定义），则 defined 表达式会生成值 1。否则，defined 表达式会生成值 0。

defined 运算符相对于 #ifdef 和 #ifndef 命令的优点是可以进行表达式求值。如下：

```c
#if defined(__unix__) && defined(__GNUC__)
/* ... */
#endif
```

## 特殊控制
ANSI C 还定义了特殊作用的预处理指令，如 #error、#pragma。

### \#pragma



 \#error：使预处理器输出指定的错误信息，通常用于调试程序。

 \#pragma：是功能比较丰富且灵活的指令，可以有不同的参数选择，从而完成相应的特 定功能操作。调用格式为：#pragma 参数。

 其中，参数可以有 message 类型、code_seg、once、warning、pack 等。通常使用如下的预处理指令来设定内存以 n 字节对齐方式。

 \#pragma pack (n) //其中 n 称为对齐系数，取 1、2、4、8...

# 内存对齐



# C++构造函数

C++11之前，对象的拷贝控制由三个函数决定：**拷贝构造函数**（Copy Constructor）、**拷贝赋值运算符**（Copy
 Assignment operator）和**析构函数**（Destructor）。

C++11之后，新增加了两个函数：**移动构造函数**（Move Constructor）和**移动赋值运算符**（Move Assignment opera）。

**口诀**：构造函数与赋值运算符的区别是，构造函数在创建或初始化对象的时候调用，而赋值运算符在更新一个对象的值时调用。



```c++
//构造函数测试类
class A
{
public:
	int x;
	A(int x) : x(x) 
    { 
        cout << "Constructor" << endl; 
    }
    ~A()
    { 
        cout << "destructor" << endl; 
    }
	A(const A& a) : x(a.x) 
    { 
        cout << "Copy Constructor" << endl; 
    }
	A& operator=(A& a) 
    { 
        x = a.x; 
        cout << "Copy Assignment operator" << endl; 
        return *this; 
    }
	A(A&& a) : x(a.x) 
    { 
        cout << "Move Constructor" << endl; 
    }
	A& operator=(A&& a) 
    { 
        x = a.x;
        cout << "Move Assignment operator" << endl; 
        return *this; 
    }
};
```



## 移动构造函数

