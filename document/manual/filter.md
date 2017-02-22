---
title: 滤波器
layout: page
---
## 滤波器
前面两节的直方图调整和数学运算有个共同点，就是新图像的像素由原图相同位置的像素经过一个数学运算得到，某种意义上，直方图调整可以看作是数学运算的一个子集，而这里我们讨论的滤波器运算，新图像的像素不仅由原图相同位置的像素决定，而且和与之邻近的一些像素有关。

**ImagePy 中绝大多数的滤波器（除了一些三维的）都支持图像预览和撤销操作，如果滤波器有参数输入会提供一个友好的交互对话框。如果有选区在图像上，则自动只处理选取内的像素，在处理图像栈的时候，会询问是否进行批量处理。**

## 经典高通-低通滤波器
![](http://home.imagepy.org/manual/gaussfilter.png "经典滤波器")
* ### Process > Filter > Gaussian
高斯模糊，由一个二维正太分布做滤波核。
* ### Process > Filter > Gaussian Laplace
高斯-拉普拉斯，由一个墨西哥帽子形的函数做滤波核


## 排序滤波器
![](http://home.imagepy.org/manual/sortfilter.png "排序滤波器")
* ### Process > Filter > Maximum
窗口内最大值
* ### Process > Filter > Minimum
窗口内最小值
* ### Process > Filter > Midian
中值滤波器

## 基础梯度算子
* ### Process > Filter > Prewitt
正交边缘算子
* ### Process > Filter > Sobel
对角边缘算子

## USM 
* ### Process > Filter > Unsharp Mask
非锐化掩膜（原图 + k * （原图-原图的高斯模糊）），它增强了图像的细节，但同时也对噪声敏感，为了降低噪声的影响，可以在之前使用高斯滤波器。

![](http://home.imagepy.org/manual/usmfilter.png "USM滤波器")

## 三维滤波器
* ### Process > Filter > Gaussian3D
需要图像栈，在三维空间进行高斯模糊