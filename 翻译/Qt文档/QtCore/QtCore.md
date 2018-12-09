# Qt Core

## 开始

其他的所有Qt模块都依赖这个模块。想要引用这个模块的中类，使用下面的指令

`#include<QtCore>`

如果你使用qmake构建你的项目，Qt Core会被默认包含。

## Core模块的设计目的

Qt为C++添加了下列特性：

- 信号与槽，一种用于对象之间无缝交流的强大机制。
- 可查询和可设计的对象属性。
- 层次化和可查询的对象树
- 使用受保护的指针以一种自然的方式实现的对象所有权
- 在整个库中都工作的动态类型转换。

下面的文章提供了更多有关Qt 的核心特性

- 元对象系统
- 属性系统
- 对象模型
- 对象树与所有权
- 信号与槽



## 线程和并发编程

Qt提供了对线程的支持，提供了与平台无关的线程类，一个线程安全的传递事件的方法，和跨线程的信号与槽连接。对于处理耗时操作但不想冻结用户界面的应用来说，多线程编程依然是一个很有用的编程范式。

Thread Support in Qt 页面在应用中实现线程的相关信息。此外Qt Concurrent模块提供了并发编程的相关类。

## 输入输出，资源和容器

Qt 提供了一个资源系统来管理应用的文件和资源，还提供了容器集合和一些接收输入和打印输出的类。

- Container Classes
- Serializing Qt Data Types
- implicit Sharing

此外，Qt Core 提供了一个平台无关的机制来在可执行文件中存储二进制文件。

- Qt Resource System



## 额外的框架

Qt Core 还提供了一些Qt 的关键性框架

- The Animation Framework
- JSON Support in Qt 
- The State Machine Framework
- How to Create Qt Plugins
- The Event System



