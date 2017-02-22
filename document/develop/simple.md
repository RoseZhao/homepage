---
title: 基础引擎
layout: page
---

## Simple
Simple 是另一个重要的图像处理引擎，它的结构和 Filter 很像，却又有所区别，我们可以类比来学习。
#### Simple 不是针对单张图像，而是整个图像序列，或者 ImagePlus 本身进行操作。如撤销操作，选区扩张操作，或者 3D 滤波器等。

## 类结构
```python
class Simple:
    title = 'Simple'

    note = []

    para, view = None, None
    
    def __init__(self, ips=None):
        #...
    def show(self):
        #...
    def run(self, ips, imgs, para = None):
        #...
    def check(self, ips):
        #...
    def load(self, ips):
    	#...
    def start(self, para=None):
        #...
```

* ### title:
  插件的标题，将作为菜单栏的显示，交互对话框的标题，以及插件管理器中的主键。
* ### para， view:
  核心函数需要用到的参数，以及他们的交互方式，默认为 None，代表不需要交互。参阅[参数对话框](./parameter.html)。
* ### note:
  插件标签，他们指明 Simple 能处理哪些类型：
  **all:**滤镜能处理所有类型
  **8_bit:**滤镜能处理8位灰度图像
  **16_bit:**滤镜能处理16位灰度图像
  **rgb:**滤镜能处理rgb彩色图像
  **float:**滤镜能处理浮点图像
  **req_roi:**滤镜需要选区
  **req_stack:**滤镜需要图像栈
  **req_stack2d:**滤镜需要图像列表
  **req_stack3d:**滤镜需要连续图像栈
  #### 由于 Simple 是针对整体进行处理，因而相比 Filter 不需要自动便利通道和图像栈，因而也没有行为参数。

* ### check:
  根据 note 标识，对当前图像进行检查，如果不符合要求则弹出提示，退出。
* ### load:
  插件的加载，可以做一些准备工作，比如获取当前图像的像素直方图等，也可以用作进一步的检查，比如检查图像是否为二值图像。返回 True，则继续执行后续流程，返回 False，则终止。

* ### show:
  弹出交互对话框，一般时候我们只需要设定 para， view，Filter 会自动调用 ParaDialog 生成交互对话框，但必要时，可以覆盖 show 方法。
* ### run:
  核心函数，我们将得到如下参数：ips, imgs, para = None，解释如下：
  **ips:**当前处理的 ImagePlus
  **imgs:**当前处理的 ImagePlus 的图像序列
  **para:**当前的处理函数参数
  #### 相比 Filter 缺少了 snap，且 img 换成了 imgs，可见两者侧重点的不同。

* ### start:
  启动函数，当 Simple 被执行时调用，参数 para 如果为 None，则进入交互模式，如果有值，则直接执行 run。（菜单点击的方式下都是传入的 None，而运行宏的时候，可以传入 para 参数）

## 一个扩张的例子
最后我们用一个选区扩张的例子来结束本章：
```python
from core.engines import Simple

class Inflate(Simple):
    title = 'Inflate'
    note = ['all', 'req_roi']
    para = {'r':5}
    view = [(int, (1,100),0, 'radius', 'r','pix')]

    def run(self, ips, imgs, para = None):
        ips.roi = ips.roi.buffer(para['r'])
```
注意：Inflate 既然是要扩张选区，那么自然要求图像必须有选区，我们在 note 里加上 'req_roi'，这样我们可以免于在执行之前判断是否存在选区，以及如果不存在如何提示用户，只需专心做核心工作。
![](http://home.imagepy.org/develop/simple.png "缓冲区的例子")
