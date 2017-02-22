---
title: ImagePy Home
top: true
---

**一个细胞计数的例子：**
![](http://home.imagepy.org/cell.png "cell count")

**简介：**
* 支持bmp, rgb, png等常用图像格式
* 可以处理灰度图像和多通道（彩色）图像，支持图像栈（序列）操作
* 可以进行常用的各种数学运算，常用的滤波器操作
* 支持各种选区操作（点，线，面，多线，多面，镂空多边形）
* 可以进行像图像测量，以及像素统计
* 能够进行dem地表重建，图像序列的三维重建
* 支持宏录制，可接入scikit-image, opencv, itk等基于numpy的第三方库



**获取：** GitHub: [https://github.com/yxdragon/imagepy.git](https://github.com/yxdragon/imagepy.git)
> ``` bash
$ git clone https://github.com/yxdragon/imagepy.git
```

**安装：**
> 安装 Python，Linux已经预装，Windows 到[官网](http://www.python.org)下载
> 安装依赖包 Numpy, Scipy, wxpython [opencv, scikit-image, mayavi]
> Ubuntu:
``` bash
$ apt-get install python-numpy
$ apt-get install python-scipy
$ apt-get install python-wxpython
```
> Windows:
你可以从[这里](http://www.lfd.uci.edu/%7Egohlke/pythonlibs/)获取 Numpy, Scipy, wxpython 等二进制文件(whl)
然后依次用pip进行安装
``` bash
$ python -m pip install your_filen_ame.whl
```

**运行：** 进入克隆下来的项目主目录，运行main.py脚本文件, 你将会看到如下的主界面。
![](http://home.imagepy.org/main.png "main")

**文档：**
> [ImagePy 操作手册](document#操作手册)
> [ImagePy 开发文档](document#开发文档)