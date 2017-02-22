---
title: 选区运算
layout: page
---

## 选区运算

我们在开始介绍过[选区](./conception.html#选区 "选区概念")的概念，并且在[常用工具](./tools.html#选取类 "选取操作")中专门讨论过选取相关的操作，这里我们从运算层面上介绍选区。
**ImagePy 选区操作暂时不支持撤销**

这里演示几个点选区，然后进行膨胀运算，变成了圆形面选区，再做凸包运算，成为一个凸多边形选区。
![](http://home.imagepy.org/manual/roipoint.png "形态学运算")

* ### Selection > All
选取全部
* ### Selection > None
取消选区

这里用自由多段线工具绘制 IPY 字样，然后进行膨胀，成为空心，再用 Shift + 矩形工具，叠加一个下划线。
![](http://home.imagepy.org/manual/roiipy.png "形态学运算")
* ### Selection > Inflate
选区膨胀 （Buffer运算）
* ### Selection > Shrink
选区收缩
* ### Selection > Convex Hull
凸包运算
* ### Selection > Bound Box
最小外接矩形
* ### Selection > Clip
去除图像以外的选区
* ### Selection > Invert
选区取反

将刚才得到的 IPY 添加到选区管理器，然后重新切换到第一幅图，从管理器以Difference方式导入 IPY，并填充。
![](http://home.imagepy.org/manual/roidiff.png "形态学运算")
* ### Selection > Add To Manager
将选区加入到选区管理器
* ### Selection > Load From Manager
从选区管理器加载到当前图像
* ### Selection > Union
从选区管理器加载，并叠加到当前选区
* ### Selection > Differance
从选取管理器加载，并镂空在当前选区