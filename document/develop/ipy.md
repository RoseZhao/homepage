---
title: 常用函数
layout: page
---
## IPy
### imagepy > IPy
IPy 是一些常用功能的汇总，比如展示一幅图像，获取当前图像窗口等功能，其实这些功能是分布在各个功能组建中的，IPy只是重新引用和整理，并且IPy处于最顶层目录，随处都可以方便的引用这样以来，提高了开发效率。


* ### curapp = None
  当前程序主窗口对象

* ### get_window()
  获取当前窗口
    
* ### get_ips():
  获取当前的 ImagePlus
    
* ### show_img(imgs, title):
  展示图像，标题为 title
    
* ### alert(info, title='image-py'):
  弹出警告框，标题可设定，默认为 'image-py'
    
* ### yes_no(info, title='image-py'):
  弹出是非对话框，标题可设定，默认为 'image-py'
    
* ### get_path(title, filt, para=None):
  弹出对话框，获取文件，结果填写在 para
    
* ### get_dir(title, filt, para=None):
  弹出对话框，获取目录，结果填写在 para
    
* ### get_para(title, view, para):
  调用 ParaDialog 解析 view，para
    
* ### table(title, data, cols=None, rows=None):
  写表格，标题行，数据块，列标，行标
    
* ### write(cont, title='ImagePy'):
  写日志，窗口标题可设定，默认为'ImagePy'
    
* ### set_progress(i):
  设置住节目进度条
    
* ### set_info(i):
  设置住界面状态栏的信息
    
* ### run_macros(cmds):
  执行宏