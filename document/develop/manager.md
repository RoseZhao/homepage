---
title: 管理器
layout: page
---
## Manager
### imagepy > core > managers
**管理器是 ImagePy 里很重要的一个概念，作为插件系统，各个部件都是松散耦合。而管理器的作用就是全局协调。目前 ImagePy中有如下一些管理器，我们将一一介绍。**

## WindowsManager
最重要的管理器，他负责管理和调度窗口
* ### add(cls, win):
  将窗口添加到管理器中（窗口打开时自动添加）
* ### remove(cls, win):
  将窗口从管理器中移除（窗口关闭时自动移除）
* ###  get(cls, title=None):
  获取指定的窗口，如果没有指定，则返回最前端的一个
* ### get_titles(cls):
  获取当前所有窗口的标题序列
* ### name(cls, name):
  获得命名，如果没有重复则返回本身，有重复则添加数字后缀
* ### close(cls, name):
  关闭窗口

## TextLogManager
  **日志窗口管理器，方法与 WindowsManager 完全相同**
## TableLogManager
  **表格窗口管理器，方法与 WindowsManager 完全相同**

## PluginsManager
**在插件被 PluginsLoader 解析之后，会以键值对形式保存在这里。**
* ### add(cls, plg)
  将插件添加到管理器
* ### get(cls, name)
  根据名称获取插件实例

## ToolsManager
**在工具被 ToolsLoader 解析之后，会以键值对形式保存在这里。**
* ### add(cls, tool)
  将工具添加到管理器
* ### get(cls, name)
  根据名称获取工具实例
* ### set(cls, tool)
  设定当前工具，一般由工具栏的点击事件触发

## RoiManager
**用于存储选取，以便在需要的时候加载**
* ### add(cls, name, roi)
  将选区添加到管理器
* ### get(cls, name)
  根据名称获取选区实例

## ColorManager
* ### get_color(cls):
  弹出颜色对话框，交互式获取颜色
* ### set_front(cls, color):
  设定前景色
* ### set_back(cls, color):
  设定背景色
* ### get_front(cls, one=False):
  获取前景色
* ### get_back(cls, one):
  获取背景色
* ### get_lut(cls, name='grays'):
  获取索引表，默认是灰度色阶

## ClipBoardManager:
* ### roi
  剪切的选区
* ### img
  剪切的图像