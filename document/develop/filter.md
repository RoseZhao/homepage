---
title: 滤波器引擎
layout: page
---

## Filter
Filter 是图像处理插件的基类，可以说是最终要的一种插件引擎，它的使用场景是处理一副图像，继承它并加以简单配置，Filter 将会为你做很多的预处理和后处理。
* ### 帮我们做了什么
  1.做必要的类型检查
  2.帮我们生成参数交互节目，并支持实时预览
  3.提供快照，撤销支持
  4.提供选区支持
  5.提供多通道支持
  6.提供图像栈支持

![](http://home.imagepy.org/develop/filter.png "滤波器")

## 类结构
```python
class Filter:
    title = 'Filter'

    modal = True

    note = []

    para, view = None, None
    
    def __init__(self, ips=None):
        #...
    def show(self):
        #...
    def run(self, ips, snap, img, para = None):
        #...
    def check(self, ips):
        #...
    def preview(self, para):
        #...
    def load(self, ips):
    	#...
    def start(self, para=None):
        #...
```

* ### title:
  插件的标题，将作为菜单栏的显示，交互对话框的标题，以及插件管理器中的主键。
* ### modal:
  当 modal 为 True 时，参数对话框将以模态展示，这也是默认情况，这满足大多数的使用场景。
* ### para， view:
  核心函数需要用到的参数，以及他们的交互方式，默认为 None，代表不需要交互。参阅上一节[参数对话框](./parameter.html)。
* ### note:
  **插件标签，这决定了 Filter 的运行特性，下面依次解释：**
  > #### 检查类(作用于check)
  >> **all:**滤镜能处理所有类型
     **8_bit:**滤镜能处理8位灰度图像
     **16_bit:**滤镜能处理16位灰度图像
     **rgb:**滤镜能处理rgb彩色图像
     **float:**滤镜能处理浮点图像
     **req_roi:**滤镜需要选区

  > #### 行为类(作用于run)
  >> **preview:**是否需要提供预览功能
     **auto_snap:**是否需要执行前自动快照
     **auto_msk:**是否要支持选区
     **not_channel:**是否在处理彩色图像时自动处理每个通道（如不填写为是）
     **not_slice:**是否在处理图像栈的时候询问，从而处理每个层（如不填写为是）
     **2int:**如果精度低于16位整数，是否在处理之前把图像转为16位整数（一些运算会产生负数或溢出）
     **2float:**如果精度低于32位浮点，是否在处理之前把图像转为32位浮点（一些运算需要在浮点上做才能保证质量）

* ### check:
  根据 note 标识，对当前图像进行检查，如果不符合要求则弹出提示，退出。
* ### load:
  插件的加载，可以做一些准备工作，比如获取当前图像的像素直方图等，也可以用作进一步的检查，比如检查图像是否为二值图像。返回 True，则继续执行后续流程，返回 False，则终止。

* ### show:
  弹出交互对话框，一般时候我们只需要设定 para， view，Filter 会自动调用 ParaDialog 生成交互对话框，但必要时，可以覆盖 show 方法。
* ### run:
  #### 核心函数，我们将得到如下参数：ips, snap, img, para = None，解释如下：
  **ips:**当前处理的 ImagePlus
  **snap:**当前 ImagePlus 的快照（只有在 note 设定了 auto_snap 标签后才会自动生成）
  **img:**当前处理的 ImagePlus 的当前图像
  **para:**当前的处理函数参数
  #### 关于返回值，我们最终目的是把处理后的结果填入 img，理想情况下，我们用 snap 进行处理，吧结果输出到 img，这样，我们不必返回结果。而另一些时候，我们没有条件这样做，那么返回你的处理结果，Filter 会帮你把结果填入 img。

* ### start:
  启动函数，当 Filter 被执行时调用，参数 para 如果为 None，则进入交互模式，如果有值，则直接执行 run。（菜单点击的方式下都是传入的 None，而运行宏的时候，可以传入 para 参数）

## 一个高斯模糊的例子
最后我们用一个高斯模糊的例子来结束本章：
```python
import scipy.ndimage as nimg
from core.engines import Filter

class Gaussian(Filter):
    title = 'Gaussian'
    note = ['all', 'auto_msk', 'auto_snap','preview']

    #parameter
    para = {'sigma':2}
    view = [(float, (0,30), 1,  'sigma', 'sigma', 'pix')]

    #process
    def run(self, ips, snap, img, para = None):
        nimg.gaussian_filter(snap, para['sigma'], output=img)
```
效果如下：我们并没有做任何关于彩色图像的处理，以及如何处理选区，仅仅9行代码，我们就得到了一个界面友好的交互式滤镜，并且它支持任意图像类型，支持选区，能够撤销！
![](http://home.imagepy.org/develop/filterdemo.png "高斯模糊的例子")
