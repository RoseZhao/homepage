---
title: 插件加载
layout: page
---
## 插件加载 PluginsLoader
**ImagePy 运行时，PluginsLoader负责加载插件，插件会被 PluginManager 管理起来，并且映射成菜单，在用户点击的时候执行**

* ### 插件目录
  **imagepy > menus**

* ### 加载规则
  1.位于 menus 目录及其子目录下
  2.若文件以 _plg.py 结尾，则文件内的 Plugin 类会被加载。
  3.若文件以 _plgs.py 结尾，则文件内的 plgs 列表将依次被加载。
  4.若文件以 .mc结尾，则会被解析成宏命令进行加载。

* ### 插件和菜单
  插件将会被解析成主程序的菜单，事实上 ImagePy 的菜单也全部是插件。他们会这样映射：
  1.对应的文件夹结构会被映射成相应的菜单结构
  2.菜单的标题由插件类的 Title 属性决定
  3.对于宏映射成的菜单，标题就是文件名（不包括扩展名）

* ### 顺序调控
  由于菜单是由文件目录映射而成的，因此顺序是按照字母排序形成的，好在我们可以指定其顺序。
  1.plgs 的内部顺序，由序列决定，我们可以在其中加入'-'，这将会被映射成菜单分割线。
  例如 menus > Process > Filter > binary_plgs.py：
  ```python
  # ......
  plgs = [Dilation, Erosion, '-', Closing, Opening, '-', Outline, FillHoles, EDT]
  ```
  2.目录中的插件可以在包的 __init__.py 文件中加入 catlog = [...] 来指定，里面填写文件夹名称或文件名（不包括扩展名）
  比如 menus > __init__.py
  ```python
  catlog = ['File','Edite','Image','Process','Selection','Analysis','Plugins','Window','Help']
  ```
![](http://home.imagepy.org/develop/menu.png "菜单展示")


## 工具加载 ToolsLoader

* ### 工具目录
  **imagepy > tools**

* ### 加载规则
  1.位于tools下的以及子目录
  2.若文件以 _tol.py 结尾，则文件内的 Plugin 类会被加载。
  3.若文件以 _tols.py 结尾，则文件内的 plgs 列表将依次被加载。
  4.若文件以 .mc结尾，则会被解析成宏命令进行加载。
  （加载规则基本与插件加载规则相同，但是需要注意工具的 plgs 列表是一个二元组（Plugin， '*.gif'），后者将会被当作图标加载到工具栏上）

* ### 工具与工具栏
  1.位于 tools > standud 目录下的工具称之为标准工具，它们始终出现在工具栏左侧。
  2.其他目录下的工具称之为专业工具，他们共用右侧的空间，可以点击最左侧的下拉按钮进行切换。

* ### 顺序调控
  与插件的调控方式相同

* ### 工具栏图标
  准备一个与工具文件名相同（不包括扩 _tol.py）的 16×16 的 gif 小图标，放在形同目录下，当程序加载时，将作为该工具的图标。
  下面展示一个 Measure 工具集的例子
  以下为 __init__.py 中的内容
  ```python
  catlog = ['coordinate_tol', 'distance_tol', 'angle_tol'， 'area_tol']
  ```
  ![](http://home.imagepy.org/develop/meatools.png "测量目录")
  ![](http://home.imagepy.org/develop/tools.png "工具")

