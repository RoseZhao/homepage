---
title: 形态学
layout: page
---

## 形态学滤波器
前几节介绍的都是线性滤波器，这里我们介绍形态学运算，形态学多应用在二值图像中。
**ImagePy 中所有的形态学滤波器都支持图像预览和撤销操作，如果滤波器有参数输入会提供一个友好的交互对话框。如果有选区在图像上，则自动只处理选取内的像素，在处理图像栈的时候，会询问是否进行批量处理。**
## 基础运算
形象的理解，形态学基础运算好比是一个筛子，能够透过特定的集合图形，而新图像上的点，由能否透过决定。
![](http://home.imagepy.org/manual/erode.png "形态学运算")

* ### Process > Binary > Dilation
膨胀运算，前景区域按照滤波核扩张
* ### Process > Binary > Erosion
腐蚀运算，前景区域按照滤波核收缩
* ### Process > Binary > Closing
闭运算（腐蚀 + 膨胀），这种运算能够去除前景中细微的连接
* ### Process > Binary > Opening
开运算（膨胀 + 腐蚀），这种运算能够使得前景中狭小的缝隙联通

## 高级运算
基于二值图像的其他一些运算
![](http://home.imagepy.org/manual/edt.png "形态学运算")
* ### Process > Binary > Outline
轮廓计算，本质是进行扩张之后与原图相减
* ### Process > Binary > Fill Holes
填充镂空，前景区域上封闭的空洞
* ### Process > Binary > Distance Transform
距离变换，计算每一个背景像素到与之最近的前景像素的距离