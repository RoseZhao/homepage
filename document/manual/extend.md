---
title: 扩展开发
layout: page
---

## 扩展开发
* ### ImagePy 是什么
ImagePy 不只是一款图像处理软件，更是一个超轻量级，高扩展性的插件式图像处理框架。框架基于 Python 实现，图像数据基于 Numpy，任何基于 Numpy 的算法库，都可以轻松接入，同时 ImagePy 为其提供有好交互环境，包括对话框，图像预览，撤销支持，选区支持，多通道支持和图像栈支持等...

* ### 为什么选择 Python
Python语言近年来持续升温，在这里，它有如下优势
1. 语法简洁，易学，开发环境搭建简单。
2. 语言灵活性高，编程更方便
3. 有大量的第三方类库支持，图像方面有 scipy, scikit-image, opencv等。
4. 大多数科学计算库都是基于 Numpy 的，这让设计统一框架变得容易。


**拿来主义可以说是 ImagePy 的设计精髓，scikit-image， opencv 等鼎鼎大名的开源图像处理库，尽为我所用，并且是轻松无缝结合。同样你也可以轻松的扩展一个工具，由于更深入的内容与操作手册的主旨无关，关于扩展开发，我将在[开发文档](../#开发文档)中展开介绍，这里仅仅是一个初步认识，下面就以scikit-image的一个Canny算子为例，施展吸星大法。同时也结束操作手册的文档编写。**

## 接入Canny算子的例子
```python
# -*- coding: utf-8 -*
from skimage import feature
from core.engines import Filter

class Plugin(Filter):
    title = 'Canny'
    note = ['all', 'auto_msk', 'auto_snap', 'preview']
    
    para = {'sigma':1.0, 'low_threshold':10, 'high_threshold':20}
    
    #parameter
    view = [(float, (0,10), 1,  'sigma', 'sigma', 'pix'),
            ('slide',(0,30), 'low_threshold', 'low_threshold',''),
            ('slide',(0,30), 'high_threshold', 'high_threshold','')]

    #process
    def run(self, ips, snap, img, para = None):
        return feature.canny(snap, sigma=para['sigma'], low_threshold=para[
            'low_threshold'], high_threshold=para['high_threshold'], mask=ips.get_msk())*255
```

* ### 1. 引入核心类库，引入 Filter
Filter是滤波器积累，核心类库是准备接入的核心函数。
* ### 2. 继承 Filter
所有滤波器的基类，集成之后自动获得了很多交互功能。
* ### 3. 设定 Title
这将是菜单栏上展示的内容
* ### 4. 设定 Note
这告诉ImagePy需要帮你做哪些前期和后期工作，比如对选区的支持，对图像栈的支持等。
* ### 5. 设定 Para
核心函数需要用到的参数
* ### 6. 设定 view
插件执行时的交互方式（与参数对应，只需要指明参数类型，取值范围等信息即可）
* ### 7. 核心函数，run
这一步仅仅是调用核心函数，snap是缓存图像，img是前景图，para是通过对话框交互得到的参数。你要做的仅仅是把snap的值经过作用，赋予img。
#### OK，一个插件就写好了，我们试一下效果：

![](http://home.imagepy.org/manual/canny.png "边缘算子")

可以看到，短短12行代码，就接入了一个非常酷的边缘提取功能，是不是很令人兴奋！
