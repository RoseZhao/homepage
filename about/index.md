---
title: About
date: 2017-02-05 02:25:51
layout: page
---
## 关于 ImagePy
**ImagePy 是一款基于 Python 的可扩展图像处理框架。**

## 设计初衷
* ### ImageJ 的使用经历
  ** ImageJ 是一款基于 Java 平台的开源图像处理软件，它由国际健康学会主持研发。个人认为它的成功很大程度上是如下原因：**
  > **1. 提供了友好的可视化界面以及交互环境**
    **2. 基于插件式设计思想，以及社区的建立，逐渐吸纳了很多优秀的插件贡献（也包括了我的贡献）**
    **3. 借助国际健康学会的影响力**

  **我也长期使用 ImageJ 处理图像，并编写了一些高质量的插件，个人认为 ImageJ 也有他的不足：**
  > **1. Java 语言对于非计算机行业人士过于专业，学习门槛高，开发环境搭建复杂**
    **2. Java 下科学计算方面的开源库不多，因而开发难度较大，时常不得不编写算法，反复测试**

* ### 神奇的 Python
  **接触 Python 也有几年了，本人从事数据分析行业，时常用 Python 做科学计算，并且越发喜爱这门脚本语言，它有如下优势：**
  > **1. 语法简明，灵活，易学。对于非计算机专业的科学研究人员尤为适合。**
    **2. 类库丰富，拿图像处理来说有：Scipy，scikit-image, Opencv-python, itk 等诸多大名鼎鼎的开源库，同时有 matplotlib, mayavi 等功能强大的可视化库**
    **3. 最难得的是，几乎所有科学计算方面的库，都是基于 Numpy 作为基础数据结构**
    #### **但是很遗憾，这些库基本没有做任何的交互，需要借助 matplotlib 来完成展示，换句话说，这些库只是给程序员用的，很难让医生，生物学家等业内专业人士使用。**

* ### ImagePy
  在这样的情况下，我决定开发 ImagePy！并要具备如下特性：
  > **1. 采用 Python 语言开发，插件式设计思想。**
    **2. 提供友好的可视化界面以及交互环境，让非计算机人士得以使用。**
    **3. 以 Numpy 为基础数据类型，并能够快速接入任何基于 Numpy 的第三方库。**
    #### **这可以说是融合 ImageJ 与 Python 的优势，设计一个轻量级，可扩展的图像处理框架！**

## 编写历程
* ### 框架设计阶段
  **项目始于2017年11月，万事开头难，而对于框架设计来说起初更是一个反复斟酌的过程，（我不想过多参考ImageJ，毕竟 Python 有自己的语言优势，可以作出更灵活的设计），选定了 wxpython 作为 ui 框架，对于科学计算出身的我，ui 永远是一个令人头痛的问题，虽说框架可以尽可能与 ui 分离，但我很需要一个看得到的东西来鼓舞士气，让自己不会半途而废。接下来图像的刷新，展示，事件处理，大概一周时间花在了图像展示窗口上。接下来是插件的设计，插件加载方式，解析目录，映射成菜单，工具栏，这其中也踩了不少的坑，不管怎么说，大概半个月的时间，我的框架有了雏形。真是废寝忘食的半个月，那段时间的代码前面的自动生成的注释，时常是两三点钟。**
* ### 自我磨合阶段
  **有了插件系统，剩下的就是不断的用插件去完善其功能，然而毕竟框架没有经过实战检验，初期插件的接入各种水土不服，有时做着做着，发现某个功能实现不了，还有一些功能实现很麻烦，当然，又要回去修改框架，这段时间也是最折腾的一段时间，记得编写了一个高斯模糊，一个打开图像，一个引入序列，一个画笔工具，就在反复掂兑，规范插件的启动流程，还有就是对于不同的图像类型，8位，16位，rgb的，如何能够进来不让插件来做处理，都由系统自动处理。大概花了十天左右，ok，基本吃得消了！**
* ### 啃下几个复杂交互
  **框架磨合得差不多了，但这是我没有大规模的扩展插件，因为在我心里还有个障碍，Roi交互，在界面上绘制各种矩形，椭圆，多边形，还要支持叠加，支持镂空，支持节点编辑，这些想想都头痛。。。时间进入了十二月中旬中旬，成都的冬天没有暖气，手指冻得僵硬，而交互测试不得不在键盘与鼠标之间来回切换。不知为什么心血来潮，好不容易做好了选区，竟然想来个更刺激的，交互旋转，变换工具。。。这个功能只有在 Photoshop 类的软件上才有实现，不过意想不到的是，实现得竟然比较简洁，这也侧面论证了框架的正确性。**
* ### 大量扩展功能
  **这段时间，我开始大量吸纳 Scipy 的 ndimage 库，都还比较顺利，这肯定了基础设计，这段时间的效率是很高的，几乎是一天一个大的菜单项，各种流氓的接入和吸收，似乎真的有练成吸星大法的成就感。并且赶在元旦之前，成功的昨完了每个菜单，这时其实已经实现了 ImageJ 80%的功能了。不过还不具备宏录制，一直觉得这个是 ImageJ 最绚的功能，一直在回避这个问题，但现在必须面对了，但结果，用了十分钟时间，加了十几行代码就ok了，真是出乎意料。**
* ### 完善工作
  **自己的项目，永远会有些洁癖，于是做了一次小的重构，调整了一下文件的组织结构，另外由于前期赶进度，命名很多不规范的地方，全部都 review 了一边，每个功能又都测试了一边。至此基本完成，作为一个可扩展的框架，我的主要功能依赖了 Numpy, Scipy 实现，并且这两者也已经足够强大，为了保证框架的最小依赖于纯净，我们有融入其他库，只是象征性的写了一个接入 opencv-surf 的例子，以及一个接入 scikit-image canny 的例子，还有一个 mayavi 三维重建的例子，一切 ok！**
  #### 有我吸星大法，加上 scikit-image，opencv 做后盾，我似乎觉得可以瞬间秒杀ImageJ（元旦加了三天班。。。但内心被快乐和满足充斥）

## 接下来的事
* **项目发了 github，接下来，年末了，虽说是自由职业，但一连两个月没有收入了，难免心慌，做了两个数据处理的外包，赚了个回家路费，本想回大连后花时间把文档好好写写，但回家看到爸妈，总觉得一年到头，就这些时间陪他们，所以真心不应该这个时候刻苦，时常看一下 github 帐号，项目无人问津，看来是有必要做一些推广了。春节结束，回成都，又开始废寝忘食的花了几天时间写文档，一方面是写各人主页，另外是写软件操作手册，还有就是开发文档，截止现在总算都有了眉目，接下来，有没有人看，有没有人用，听天由命吧，哈哈 ！岂能尽如人意，但求无愧于心。如果你看到这篇博文，并且喜欢我的作品，请你转载或转告你的朋友，另外，如果在使用过程中，发现什么问题，或者是要实现什么新的功能，千万要告诉我。**

## 作者信息
* ### 大家好：
  **我是 ImagePy 的作者。在四川师范大学读书，专业是地理，毕业后在成都工作。从事计算机，测绘，数据处理相关的工作，闲暇时间喜欢运动，户外，旅行。喜欢数理，文学，艺术，哲学类的书。关于 ImagePy 或者任何图像处理方面的问题，甚至数学，理论，哲学方面的问题，随时欢迎大家与我讨论，我很乐意与大家分享。另外，如果你觉得 ImagePy 是个不错的项目，请给我 [github](https://github.com/yxdragon/imagepy.git) star一下，也请帮我推荐给你的朋友使用！**

![](http://home.imagepy.org/about/me.png "我")

### E-mail:imagepy@sina.com
### QQ:498264240