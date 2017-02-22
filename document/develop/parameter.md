---
title: 参数对话框
layout: page
---
## ParaDialog
**对于多数做科学计算的程序员来说，界面总是一个不愉快的工作，至少不希望把大部分时间花在界面设计上，而这正式ParaDialog类的设计初衷。ParaDialog采取了数据驱动视图的设计思想，会根据你的数据自动生成交互环境，同时在数据发生变化时，可以进行回调，实时预览。**
![](http://home.imagepy.org/develop/paradialog.png "参数对话框")

## 类结构
```python
class ParaDialog (wx.Dialog):
    def __init__( self, parent, title):
    	...
    def init_view(self, items, para, preview=False, modal = True):
    	...
    def para_check(self, para, key):
    	...
    def para_changed(self, key):
    	...
    def set_handle(self, handle):
    	...
```
* ### init_view:
  根据 items, para 生成界面，preview 是窗口是否需要添加预览复选框， modal 指明窗口是否为模态对话框。
* ### para_check:
  参数改变时调用，key是改变的参数键，检查参数是否合法，如果全部合法返回 True。
* ### para_changed:
  参数改变是调用，并且在预览状态下，会自动调用 handle。
* ### set_handle:
  设定处理函数，将会在参数改变并打开预览情况下调用。

## 参数配置方法
#### 这里只是介绍类的构成，事实上，你很少需要直接与它打交道。然而下面介绍的内容，是非常重要的。
* ### 第一个例子：
```python
para = {'m':1}
view = [(float, (0,150), 1, 'weight', 'm', 'kg')]
IPy.get_para('Test', view, para)
```
  解释一下：有一个参数 m, 默认值为1，(int, (0,150), 1, 'weight', 'm', 'kg')的意思是说，该参数之一个整数，取值范围在0-150之间，有一位小数精度，交互提示为 weight，对应与参数 m，单位是 kg。通过下图，我们清楚地看到了，当输入操作超出给定的范围或精度时，背景变成了黄色。
![](http://home.imagepy.org/develop/paratest.png "参数测试")
  我们在并没有写关于界面的代码，但却实现了一个实时验证的交互对话框，是不是很神奇，接下来我们看看 ParaDialog 还支持哪些数据类型。
* ### int
  **(int, (0,10), 0, 'title', 'key', 'unit')**
  (整数，0-10，无小数，标题，键， 单位)
* ### float
  **(float, (0,1), 2, 'title', 'key', 'unit')**
  (浮点，0-1，两位小数，标题，键， 单位)
* ### 'slide'
  **('slide', (0,10), 'title', 'key', 'unit')**
  与 int 类似，只是用滑块进行交互。
* ### bool
  **(bool, title, key)**
  获取bool，标题，键
* ### str
  **(str, title, key, unit)**
  获取字符串 标题，键，单位
* ### list
  **(list, ty, title, key, unit)
  (列表，类型，标题，键，单位)
* ### 'color'
  **('color', title, key, unit)**
  获取颜色，标题，键，单位
* ### 'lab'
  **('lab', cont)**
  展示一段提示语
* ### 'img'
  **('img', title, key, unit)**
  从框架的Manager中获取一幅图像
* ### 'tab'
  **('tab', title, key, unit)**
  从框架的Manager中获取一张表
* ### 'ctrl'
  **('ctrl', key, ctrl)**
  添加任意的控件

最后附上一个比较完整的例子：
```python
para = {'i':10, 'f':1.0, 's':50, 'b':True, 'str':'abc', 'l':'2','c':(255,0,0)}
view = [('lab', 'This is a parameter test'),
        (int, (0,150), 1, 'int', 'i', 'u'),
        (float, (0,1), 1, 'float', 'f', 'u'),
        ('slide', (0,150), 'slide', 's', 'u'),
        (bool, 'this is a bool test', 'b'),
        (str, 'str', 'str', 'u'),
        (list, ['1','2','3'], int, 'list', 'l', 'u'),
        ('color', 'color','c','u')]
IPy.get_para('Test', view, para)
```
效果如下：
![](http://home.imagepy.org/develop/multipara.png "参数测试")