---
title: 系统架构
layout: page
---
## ImagePy 系统架构

* ### 软件架构
**Python:**基础开发语言
**Numpy:**Python对科学计算的支持，提供基础的数组存储和操作，ImagePy的图像数据基础。
**Scipy:**基于Numpy数组，提供更高级的一系列数学函数。
**Wxpython:**ImagePy的界面框架啊。

## ImagePy 设计架构

![](http://home.imagepy.org/develop/view.png "设计架构")
* ### 展示层
ImagePy 由主界面，菜单栏，工具条，以及图像窗口构成。
* ### 逻辑层
当用户执行操作的时候，软件会将对应的功能作用与当前图像
* ### 管理层
系统底层有若干管理器，组织所有的插件和工具，以及打开的图像。

**项目启动时，加载器会扫描项目的文件夹，并按照其组织结构，映射成对应的菜单项和工具栏。**

## ImagePy 项目结构
### ImagePy
> **ImagePlus:**图像封装类，里面包含图像数据 Image，图像的 Snap 镜像，ROI，色彩索引表，Mark表层标记等。
  **IPy:**对一些常用功能的引用类，你可以通过 IPy 访问 ImagePy的许多常用功能，比如打开图像，输出日志等。
> ### ui
>> **Canvas:**负责绘制 ImagePlus,这其中包括绘制图像数据，绘制选区，以及 Mark 标记。
   **CanvasFrame:**Canvas的包裹类，使之能以一个窗口的形式展示。
   **ParaDialog:**参数交互类，图像处理的诸多汗说有各种的参数，ParaDialog采用数据驱动视图的方式，可以为你自动生成各类交互对话框。
   **...**

> ### core
>> #### loader
>>> **PluginLoader:**插件加载类，负责解析 Menus 目录，并加载其中的插件。
    **ToolsLoader:**工具加载类，负责解析 Tools 目录，并加载其中的工具。

>> #### engines
>>> **Filter:**滤波器基类，用于图像处理类的插件，他将帮助你做一系列的工作，比如处理多通道和图像站，支持选区等。
    **Simple:**简单插件基类，不同与Filter，它处理的对象不是图像，而是 ImagePlus 整体（比如处理图像栈，或 ROI）
    **Free:**自由插件基类，他的运行不需要依赖图像，可以在任何情况下执行（比如图像的打开功能）
    **Macros:**宏插件，他可以由一组命令字符串构成，并依次执行。
    **Tool:**工具基类，他定义一组鼠标事件的处理函数，可以在 Canvas 的鼠标事件中被回调。

>> #### roi
>>> **Point:**点选区
    **Line:**线选区
    **Polygon:**多边形选区
    **...**

>> #### managers
>>> **PluginsManager:**用于管理所有的插件
    **ToolsManager:**管理所有的工具
    **WindowsManager:**管理全部打开的图像窗口
    **ClipboardManager:**管理剪贴板
    **ColorManager:**颜色管理期器
    **...**

> ### menus
>> #### File
>>> **...**

>> #### Edite
>>> **...**

>> **这里用于存放全部的插件，可以按照任意目录解析...**

> ### tools
>> #### Standud
>>> **...**

>> #### Transform
>>> **...**

>> **这里用于存放所有的工具，注意工具只能存放在 tools 的一级子目录下**

## 设计思想
**ImagePy 采用插件式设计思想，根据功能的形式，制定了五种引擎模板。具体功能都是他们的子类，按照一定方式组织起来，然后由相应的加载器和管理器维护。某种意义上说，功能即文件，菜单即目录。这一点，我们将在下一章介绍PluginLoader时详细讲解。**