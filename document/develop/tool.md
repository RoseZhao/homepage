---
title: 工具
layout: page
---

## Tool
Filter， Simple 都可以处理图像，但有时候我们需要用鼠标交互对图像进行一些操作。比如我们的选区操作，绘图操作等。ImagePlus 被绘制在一个 Canvas 上，Canvas 是 wxpython 的 Panel 子类，当然我们可以对其添加鼠标事件，但我们并不推荐这样做，原因之一是这样做比较繁琐，其次，多工具同时注册事件，会引起管理混乱和事件冲突。

## 结构图
![](http://home.imagepy.org/develop/tool.png "工具结构图")
* ### 事件的调用遵循如下规则：
  1.事件最初由 Canvas 类触发。
  2.如果 Canvas 持有的 ImagePlus 有一个 CustomTool，则交给它来处理。
  3.如果没有，则交割 ToolsManager 的当前工具来处理。
  #### 一般来说，比如选区，画笔等工具，是全局有效的，但有时我们需要于单一图像做特定交互，比如当某个图像栈进入了三视图观察状态时，这是 CustomTool 就变得很有用。

## 类结构
```python
class Tool:
    title = 'Tool'
    view, para = None, None 
           
    def show(self):
        #...
    
    def config(self):pass
    def load(self):pass
    def switch(self):pass

    def mouse_down(self, ips, x, y, btn, **key): pass
    def mouse_up(self, ips, x, y, btn, **key): pass
    def mouse_move(self, ips, x, y, btn, **key): pass
    def mouse_wheel(self, ips, x, y, d, **key): pass

    def start(self):ToolsManager.set(self)
```

* ### title:
  工具标题，当鼠标进入工具时 ImagePy 主界面的状态栏上显示的内容。也是工具管理器中的主键。
* ### para， view:
  核心函数需要用到的参数，以及他们的交互方式，默认为 None，代表不需要交互，这里的 para 代表工具自身特性，比如画笔的宽度书属性等。参阅上一节[参数对话框](./parameter.html)。
* ### show:
  双击工具按钮时，弹出交互对话框，一般时候我们只需要设定 para， view，Tool 会自动调用 ParaDialog 生成交互对话框，但必要时，可以覆盖 show 方法。
* ### config:
  当交互对话框确认时将会被调用，用于生效我们的设置。一些时候参数值的改变本身就会生效，例如调整画笔宽度，但有些时候，需要对外部进行一些通讯，比如设置全局颜色，就需要和 ColorManager 通讯。
* ### load:
  工具被选中时调用
* ### swith:
  由当前工具切换到另一个工具时调用（可以处理绘制了一半还没有闭合的多边形选区等）
* ### mouse_down
  鼠标按下时调用，其参数意义如下：
  **ips:**与事件相关的 ImagePlus
  **x:**数据坐标系下的 x
  **y:**数据坐标系下的 y
  **btn:**按下的按钮（1：左键，2：中键，3：右键）
  ****key** 其他参数
  > 'shift':shift 是否被按下
    'ctrl':ctrl 是否被按下
    'alt':alt 是否被按下
    'canvas:'获取与事件关联的 canvas
* ### mouse_up
  参数和意义与 mouse_down 完全相同
* ### mouse_move
  参数和意义与 mouse_down 完全相同，另外附加如果没有按键按下，btn=0
* ### mouse_wheel
  参数和意义与 mouse_down 基本相同，除了btn参数变成了d，代表滚动量

## 一个画笔的例子
```python
from core.draw import paint
from core.engines import Tool
import wx

class Plugin(Tool):
    title = 'Pencil'
    view = [(int, (0,30), 0,  u'width', 'width', 'pix')]
    para = {'width':1}
    
    def __init__(self):
        self.sta = 0
        self.paint = paint.Paint()
        self.cursor = wx.CURSOR_CROSS
        
    def mouse_down(self, ips, x, y, btn, **key):
        self.sta = 1
        self.paint.set_curpt(x,y)
        ips.snapshot()
    
    def mouse_up(self, ips, x, y, btn, **key):
        self.sta = 0
    
    def mouse_move(self, ips, x, y, btn, **key):
        if self.sta==0:return
        self.paint.lineto(ips.get_img(),x,y, self.para['width'])
        ips.update = True
        
    def mouse_wheel(self, ips, x, y, d, **key):pass
```
### 效果如下：

![](http://home.imagepy.org/develop/painter.png "画笔工具")