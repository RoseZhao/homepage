---
title: 常用工具
layout: page
---

## 选取类
这些工具能够通过鼠标操作，在画布上绘制一个选取，ImagePy 支持点，线，面，复杂多边形。
![](http://home.imagepy.org/manual/roitools.png "选区工具")
![](http://home.imagepy.org/manual/roisim.png "选区演示")
* ### Rectangle
指定矩形选区，鼠标位于矩形内部，可以拖拽移动选区，鼠标位于四角或边缘时，可以调整选取的大小。
* ### Ellipse
指定椭圆选区，鼠标位于椭圆内部，可以拖拽移动选区，鼠标位于四角或边缘时，可以拖拽调整选取的大小。
* ### Polygon
多边形选区，鼠标依次点击，最后一个点右键闭合。当鼠标位于多边形内部，可以拖拽移动选区，鼠标位于节点时，可以拖拽调整节点位置。
* ### FreeArea
自由区域选区，按下鼠标，绘制区域，抬起时自动闭合。当鼠标位于多边形内部，可以拖拽移动选区，鼠标位于节点时，可以拖拽调整节点位置。
* ### Line
多段线选区，鼠标依次点击，点右键结束。当鼠标位于节点时，可以拖拽调整节点位置。
* ### FreeLine
自由轨迹选区，按下鼠标，绘制区域，抬起时自动闭合。当鼠标位于节点时，可以拖拽调整节点位置。
* ### Point
鼠标点击添加一个点选区，当鼠标位于某个点附近，可以拖拽移动点的位置。
* **关于叠加：**所有的选区都可以按住 Shift 键进行叠加操作，另外面类型选区，还支持按住 Ctrl 键进行裁剪和镂空操作。
![](http://home.imagepy.org/manual/roicomp.png "选区演示")

## 查看类
用于浏览图像，进行放大，缩小，平移等操作。
![](http://home.imagepy.org/manual/viewtools.png "查看工具")
![](http://home.imagepy.org/manual/view.png "查看工具")
* ### Scale
单击左键放大，右键缩小，按住滚轮拖拽可进行移动。
* ### Move
拖拽进行移动，滚轮上下翻滚，可改变比例。

## 绘图类
简单的绘图工具，可以在画布上选取颜色，通过调色板设定颜色，在图像上绘制笔记。
![](http://home.imagepy.org/manual/drawtools.png "绘图工具")
![](http://home.imagepy.org/manual/painter.png "绘图")
* ### Painter
画笔，在画布上绘制，双击图标可以弹出对话框设置笔尖半径。
* ### ColorPicker
点击画布上的某一点摄取颜色，左键设为前景色，右键则是设置背景色。双击图标可以弹出颜色对话框。

#### 以上为常规工具，完成一些通用工作，此外 ImagePy 有一系列专用工具，这些工具用于完成一些一些专业的特定工作，专业工具在最右边的下拉按钮中，可以相互切换。
## 变换类
几何变换工具，支持旋转，缩放，当有选区时只作用在选区内。
![](http://home.imagepy.org/manual/transtools.png "变换工具")
![](http://home.imagepy.org/manual/trans.png "变换")
* ### Rotate
交互式进行图像旋转变换，可以用鼠标拖拽圆心到指定位置，图像将围绕该点旋转，同时可以在对话框输入各参数。
* ### Scale
交互式进行图像缩放变换，可以用鼠标拖拽选区四角和四边进行缩放，也可以在选区内拖拽，进行图像平疑，同时可以在对话框输入各参数。

## 测量类
![](http://home.imagepy.org/manual/measuretools.png "测量工具")
![](http://home.imagepy.org/manual/measure.png "测量")
* ### Coordinate
鼠标点击添加一个点测点，测点旁边会显示其坐标。
* ### Distance
鼠标依次点击，点右键结束，形成的各点之间会用线段相连，在线段中间部位，显示线段长度。
* ### Angle
鼠标依次点击，点右键结束，形成的各点之间会用线段相连，在角点处会显示该点所链接两线段的夹角。
* ### Area
鼠标依次点击，最后一个点右键闭合。多边形中间显示面积。当鼠标位于多边形内部，可以拖拽移动选区，鼠标位于节点时，可以拖拽调整节点位置。

## 图像栈操作
![](http://home.imagepy.org/manual/stacktools.png "图像栈工具")
* ### Add Slice
在当前位置添加一张图像
* ### Delete Slice
删除当前图像
* ### Previous Slice
跳转到前一张
* ### Next Slice
跳转到后一张
* ### Set Slice
跳转到特定的位置
* ### Orthogonal
三视图观察