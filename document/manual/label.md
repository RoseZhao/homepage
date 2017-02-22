---
title: 标记与像素统计
layout: page
---
**本节的操作多数与统计相关，结果往往是一张表格，ImagePy 中的表格以独立窗口形式体现，可以另存为Excel。**

## 区域标记
针对二值图像，像素形成联通的区域，所谓区域标记，就是给每个区域标记成一个唯一的颜色。
* ### Analysis > Label Image

![](http://home.imagepy.org/manual/label.png "图像标记")

## 像素统计
对图像中的点进行频率统计并制成表格展示，对于一张经过区域标记的图像来说，其统计结果也意味着每个区域的面积。
* ### Analysis > Histogram

![](http://home.imagepy.org/manual/histsta.png "像素统计")

## 碎片分析
* ### Analysis > Segment > Statistic
统计每个碎片内部的像素最大值，最小值，方差等信息

* ### Analysis > Segment > Position
统计每个碎片的质心，外接矩形等位置信息

* ### Analysis > Segment > Mark Point
计算并绘制每个碎片的质心

![](http://home.imagepy.org/manual/segment.png "碎片分析")

* ### Analysis > Tables > Save As CSV
将表格另存为Excel兼容的CSV文本格式

* ### Analysis > Tables > Save As Tab
将表格另存为Excel兼容的Tab制表符格式