QPen 类定义了QPainter应当如何画线和形状的轮廓。

一个Pen有style，width，brush，capStyle和joinStyle这几个属性。

画笔（pen）的style定义了线的类型，画刷（brush）被用来填充由画笔生成的线条。使用QBursh类来指定填充类型。顶部（cap）样式决定了QPainter绘制的线条端部的样式，连接（join）样式描述了被绘制的两条线应当如何连接。笔宽可以以整数（width）和浮点（widthF）精度指定。宽度为0的线说明他是一个化妆笔，这意味着笔宽始终是一个像素，不受设置到painter上的变换影响。

这些配置可以使用setStyle，setWidth等相关的函数轻松修改。注意当画笔的属性修改后，painter的画笔必须重新设置。

例如：

```c++
QPainter painter(this);
Qpen pen(Qt::green, 3, Qt::DashDotLine, 
         Qt::RoundCap,Qt::RoundJoin);
painter.setPen(pen);
```

等价于：

```c++
QPainter painter(this);
QPen pen; // 创建一个默认画笔

pen.setStyle(Qt::DashDotLine);
pen.setWidth(3);
pen.setBrush(Qt::green);
pen.setCapStyle(Qt::RoundCap);
pen.setJoinStyle(Qt::RoundJoin);

painter.setPen(pen);
```

默认的画笔为1像素宽，实心黑色画刷，四边形（SquareCap）风格的端部类型，斜切面（BevelJoin）风格的连接类型。

此外QPen提供了color和setColor方便函数，用来导出和设置画笔的画刷的颜色。