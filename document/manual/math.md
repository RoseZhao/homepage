---
title: 数学运算
layout: page
---

## 数学运算
直方图运算的实质是对像素值做一个线性运算，而数学运算则更广义的针对每个值做一个预定义的数学运算。
**ImagePy 中所有的数学运算都支持图像预览和撤销操作，如果滤波器有参数输入会提供一个友好的交互对话框。如果有选区在图像上，则自动只处理选取内的像素，在处理图像栈的时候，会询问是否进行批量处理。**

![](http://home.imagepy.org/manual/math.png "数学运算")

* ### Process > Math > Add
加法运算（等价于亮度调整，因为加法是线性运算）
* ### Process > Math > Multiply
乘法运算（等价于对比度调整，因为加法是线性运算）
* ### Process > Math > Max
最大值运算，图像上各个像素与一个定值求较大值
* ### Process > Math > Min
最小值运算，图像上各个像素与一个定值求较小值
* ### Process > Math > Squre Root
平方根运算，对图像上各个像素求平方根
* ### Process > Math > Garmma
Garmma曲线矫正，对图像进行Garmma修正，这在一些硬件设备的增益矫正中非常常见。

## 多图运算
* ### Process > Image Calculator
进行多图之间的运算，支持两附图之间对应像素进行加法，减法，最大，最小，差异运算。

![](http://home.imagepy.org/manual/multimath.png "多图之间运算")