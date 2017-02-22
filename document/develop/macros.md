---
title: 宏引擎
layout: page
---

## Macros
Macros 是一个宏执行器引擎，它负责将一串 ImagePy 命令依次执行。
#### 事实上我们几乎不会去继承 Macros，它仅仅是 ImagePy 为了实现宏功能，并统一为一种引擎接口而设计的辅助类。

## 类结构
```python
class Macros:
    title = 'Macros'
    cmds = [....]
        
    def run(self):
        # run every line in cmds
        
    def start(self, para=None):
        # just run
```

* ### title:
  插件的标题，将作为菜单栏的显示，交互对话框的标题，以及插件管理器中的主键。
* ### run:
  依次执行每一行命令
* ### start:
  run

## 实现机制
**宏录制功能应该是 ImagePy 里面非常绚的一个功能了，但事实上它的代码实现不超过20行，这主要是得益于整体的高弹性式设计。我们还是以最简单的高斯模糊为例，来看看它的实现机制。**

* ### 录制演示
  **Plugins > Macros > Recoder**
![](http://home.imagepy.org/develop/macros.png 宏录制)

* ### 录制机制
  无论是 Filter，Simple，Free 他们都是引擎类，都有共同的接口 start(self, para)，当某个插件被执行后，title > para 将被录制器记录。Gaussian>{'sigma':8.0}

* ### 执行机制
  所有的插件都被 PluginsManager 所管理，PluginsManager 内部实际上是维护了一个以插件的 title 为主键的键值对。所以我们这样做：
  1.解析宏命令，用 '>' 进行字符串分割
  2.用分割的 title 作为主键去 PluginsManager 中查找，得到滤波器的实例。
  3.调用 eval 函数，把 para 重新解析成 python 对象（这里充分发挥了脚本语言的优势）
  4.执行获取的滤波器的 start 方法，把 para 当作参数输入。
  （还记得引起的 start 方法特性，当 para 为 None 时进行交互，否则直接执行 run）