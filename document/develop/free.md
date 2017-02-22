---
title: 自由引擎
layout: page
---

## Free
Free 是与系统相关性最若的一种引擎，它仅仅是完成一个任务，之所以称之为自由，是因为 Filter，Simple 处理的对象都是 ImagePlus，（如果没有图像，那么他们的 check 函数会提示并终止运行），而 Free 可以不依赖图像运行。
#### 的确图像是我们的核心，但总有一些工作是与处理无关的，比如打开，新建图像，打开主题帮助，查看版本信息等操作。虽然这些看起来可以集成到系统功能中，但 ImagePy 奉行的是一切功能皆插件。

## 类结构
```python
class Free:
    title = 'Free'

    para, view = None, None
    
    def __init__(self):
        #...
    def show(self):
        #...
    def run(self, para = None):
        #...
    def start(self, para=None):
        #...
```

* ### title:
  插件的标题，将作为菜单栏的显示，交互对话框的标题，以及插件管理器中的主键。
* ### para， view:
  核心函数需要用到的参数，以及他们的交互方式，默认为 None，代表不需要交互。参阅[参数对话框](./parameter.html)。
* ### show:
  弹出交互对话框，一般时候我们只需要设定 para， view，Filter 会自动调用 ParaDialog 生成交互对话框，但必要时，可以覆盖 show 方法。
* ### run:
  核心函数，para 将作为参数传入，在这里做你想要做的。
* ### start:
  启动函数，当 Free 被执行时调用，参数 para 如果为 None，则进入交互模式，如果有值，则直接执行 run。（菜单点击的方式下都是传入的 None，而运行宏的时候，可以传入 para 参数）

## 一个打开图像的例子
最后我们用一个打开图像的例子来结束本章：
```python
from core.engines import Free

class OpenFile(Free):
    title = 'Open'
    para = {'path':''}
    
    def show(self):
        filt = 'BMP files (*.bmp)|*.bmp|PNG files (*.png)|*.png|JPG files (*.jpg)|*.jpg|GIF files (*.gif)|*.gif'
        return IPy.getpath('Open..', filt, self.para)

    def run(self, para = None):
        path = para['path']
        fp, fn = os.path.split(path)
        fn, fe = os.path.splitext(fn) 
        img = imread(path)
        IPy.show_img([img], fn)
```
注意：一些与图像处理不相关的工作都是继承于 Free 的，可以是打开图像，查看版本号，自动更新，甚至是退出程序。
