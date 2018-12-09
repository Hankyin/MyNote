# 元对象系统

Qt 元对象系统为对象之间的通信提供了信号与槽机制，还提供了运行时类型信息和动态属性系统。

元对象系统基于下面三点：

1. QObject类为对象利用元对象系统提供了基类。
2. 类声明中的私有段中的Q_OBJECT宏被用来启动原对象特性，比如动态属性，与槽。
3. 元对象编译器（moc）为每个QObject提供了实现元对象特性必要的代码

moc工具读取C++源文件。如果它发现一个或多个类声明中包含了Q_OBJECT宏，它会为这些类中的每一个生成另一个包含元对象代码的C++源文件。这些生成的原文件会被#include到类的源文件中或者编译和链接到这个类的实现中，后一种方式更为常见。

除了为对象之间的通信提供了信号与槽机制（引入这个系统的主要原因），元对象代码还提供了下列额外的特性：

- `QObject::metaObject()` 返回与这个类相关的元对象。
- `QMetaObject::className()` 在运行时返回类名字符串，不需要C++编译器原生的运行时类型检查。
- `QObject::inherits()` 返回一个对象是否是一个继承自特定类的类的实例（它们都需要在QObject继承树下）
- `QObject::tr()`  和 `QObject::trUtf8()` 为国际化翻译字符串。
- `QObject::setProperty()` 和 `QObject::property` 通过name动态设置和获取属性。
- `QMetaObject::newInstance()` 创建这个类的新实例。

对于QObjec类还可以使用qobject_cast()函数进行动态强制类型转换。qobject_cast()与标准C++的dynamic_cast()的行为相似，但前者不需要RTTI的支持，还可以跨动态库工作。它会尝试将它的参数转换为尖括号中指定的指针类型。如果对象是正确的类型（这取决于运行时），他会返回一个非0指针。如果对象的类型不匹配会返回0。

例如，假设 `MyWidget` 继承自 QWidget，并且声明了Q_OBJECT宏：

```c++
QObject *obj = new MyWidget;
```

声明了一个QObject * 类型的变量 obj，指向了一个MyWidget对象，所以我们可以将其强制转换：

```c++
QWidget *widget = qobject_cast<QWidget*>(obj);
```

从QObject到QWidget的转换是成功的，应为这个对象是一个MyWidget，QWidget的子类。应为我们知道obj是一个MyWidget，我们可以把它转换为MyWidget*：

```c++
MyWidget *myWidget = qobject_cast<MyWidget*>(obj);
```

转换到MyWidget是成功的，因为处理内建的Qt类型和自定义类型对于qobject_cast()来说没有区别的。

```c++
 QLabel *label = qobject_cast<QLabel *>(obj);
```

强制转换为QLable会失败，lable会被设为0，这使得在运行时处根据不同的类型进行不同的处理成为可能：

```c++
   if (QLabel *label = qobject_cast<QLabel *>(obj)) {
          label->setText(tr("Ping"));
      } else if (QPushButton *button = qobject_cast<QPushButton *>(obj)) {
          button->setText(tr("Pong!"));
      }
```

虽然可以在没有Q_OBJECT宏且没有元对象代码的情况下将QObject用作基类，但如果未使用Q_OBJECT宏，则此处描述的信号和插槽以及此处描述的其他功能都不可用。从元对象系统的角度来看，没有元代码的QObject子类等同于其最近的具有元对象代码的祖先。这意味着，例如，QMetaObject :: className（）不会返回您的类的实际名称，而是返回此祖先的类名。

因此，我们强烈建议所有的QObject子类都使用Q_OBJECT宏，不管它是否使用信号，槽和属性。