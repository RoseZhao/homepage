---
title: 直方图调整
layout: page
---

## 直方图
直方图是对图像内的像素进行频率统计而绘制出来的，他体现了图像的像素值的统计分布，属于全局特征，也称之为色阶。

** ImagePy 中所有的直方图运算都支持图像预览和撤销操作，如果有选区在图像上，则自动只处理选取内的像素，在处理图像栈的时候，会询问是否进行批量处理。**

* ### Image > Grey Stairs
色阶调整

![](http://home.imagepy.org/manual/stairs.png "色阶调整")
* ### Image > Bright & Constract
亮度对比度

![](http://home.imagepy.org/manual/bandc.png "亮度对比度")
* ### Image > Threshold
阈值调整，一种非此即彼的映射，等价于对比度的极限调整。
* ### Image > Color Balance
色彩平衡（只对彩色图像有效，可以理解成依次调整各通道的亮度，对比度）
* ### Image > Color Stairs
彩色色阶（只对彩色图像有效，可以理解成依次调整各通道的色阶）

![](http://home.imagepy.org/manual/colorbalance.png "选区演示")

#### 注：所有的直方图调整，实质相当与对原图的像素值做一个 y = kx + b 的运算，通过一个线性变换，映射到一个新值的过程。