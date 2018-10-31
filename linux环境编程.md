# Linux 基础

## shell

shell 与linux内核交互的软件。可以在其中输入命令

shell命令分为内部和外部命令，内部命令是由shell实现的，外部命令是一个可执行程序，shell 会使用exec函数来启动这个可执行程序。

type命令：可以通过type命令来判断一个命令是内部还是外部命令。

history命令：可以查看用户输入命令的历史记录。

PATH变量：shell执行外部命令时他是从哪里查找这个可执行程序的呢？shell会根据它的PATH变量中存储的地址来查找用户输入的命令。如果在这些目录下没有找到用户输入的命令，就会报错：×××不是内部或外部命令。

##shell快捷键

ctrl + p 显示上一条命令（previous）

ctrl + n 显示下一条命令（next）

ctrl + b 光标往回移动（back）

ctrl + f 光标向右移动（forword）

ctrl + a 光标移动到开头 （ahead）

ctrl + e 光标移动到结尾 （end）

## linux系统目录结构

/ 
 |-bin/ ：ls，cat 等常用命令的位置。
 |-boot/ ：启动Linux用的一些文件
 |-dev/ ：Linux设备文件
 |-etc/ ：各种配置文件
 |-home/ ： 用户家目录
 |-lib/ ：存放共享库的目录。
 |-media/ ： 挂载外设
 |-mnt/ ：挂载外设
 |-opt/ ：第三方软件安装目录。
 |-proc/：虚拟目录，可以查看或设置系统状态。
 |-root/： root用户家目录
 |-sbin/：root用户专用软件。
 |-usr/ ：unix system resource，保存用户数据。
 	 |-bin/: 
 	 |-sbin/:
 	 |local/:
 	 |include/：头文件
 	 |lib/：共享库或静态库
 	 |src/: 内核源码
 |-var/:

## linux 文件类型

- 普通文件 -
- 目录 d
- 链接 l
- 块设备 b
- 字符设备 c
- socket文件 s
- 管道 p



## gcc用法

## 工作流程

1. 预处理，-E  .c-> .i
2. 编译 -S .i ->.s
3. 汇编 -c .s -> .o
4. 链接

直接输入 gcc test.c,没有加任何参数，进行链接操作，但是没有对象文件，gcc便会自动调用汇编器，但是没有编译后的汇编源码，gcc便会自动进行编译操作，但是没有预处理后的文件，便会自动调用预处理器进行预处理，此时发现了c源码文件，于是进行预处理，接下来进行编译，汇编和链接操作。

## 常用参数

-E ：只预处理

-S：只编译

-c ：只汇编。

这三部简称esc

-v/--version：查看gcc状态版本相关信息。

-o ：指定生成文件的名称

-I ：指定头文件的路径。 

-l：指定使用的静态动态库

-L ： 指定库的搜索路径。

 -g ：即debug模式，生成的elf文件中会包含调试信息，可以使用gdb对该文件进行调试。

-D：编译时指定一个宏，-D ABC 等同于 在程序中添加`#define ABC`

-Wall：显示所有警告。

-On：优化代码，n代表优化级别，可以是：1，2，3

## 库的制作与使用

### 库的命名：

libxxx.a.1.2.3

libxxx.so.1.2.3

### 生成静态库

源文件生成目标文件，然后使用将目标文件打包。

```bash
gcc test.c -c
ar rcs libtest.a testA.o
```

格式：ar rcs  libxxx.a xx1.o xx2.o

参数r：在库中插入模块(替换)。当插入的模块名已经在库中存在，则替换同名的模块。如果若干模块中有一个模块在库中不存在，ar显示一个错误消息，并不替换其他同名模块。默认的情况下，新的成员增加在库的结尾处，可以使用其他任选项来改变增加的位置。【1】

参数c：创建一个库。不管库是否存在，都将创建。

参数s：创建目标文件索引，这在创建较大的库时能加快时间。（补充：如果不需要创建索引，可改成大写S参数；如果.a文件缺少索引，可以使用ranlib命令添加）

 

格式：ar t libxxx.a

显示库文件中有哪些目标文件，只显示名称。

 

格式：ar tv libxxx.a

显示库文件中有哪些目标文件，显示文件名、时间、大小等详细信息。

 

格式：nm -s libxxx.a

显示库文件中的索引表。

 

格式：ranlib libxxx.a

为库文件创建索引表。

### 生成动态库

```bash
 gcc -fPIC -shared test.c -o lib.so
```

​    或者是：

```
    gcc -fPIC test.c -c -o test.o
    ld -shared test.o -o lib.so
```

​    上面的命令行中-shared表明产生共享库，而-fPIC则表明使用地址无关代码。PIC：Position Independent Code.    

​    Linux下编译共享库时，必须加上-fPIC参数，否则在链接时会有错误提示



### 库的使用

在编译的时候指定需要的库的名字和路径就好了。

```bash
gcc test.c -L ./ -lmylib 
```



# makefile



# 文件io函数



文件操作函数



目录操作函数

