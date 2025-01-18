# Tkinter 教程

## 关于本教程

> [!WARNING]
>
> - 本教程所采用的版本是**Python 3.12**，版本不同可能有个别区别。
> - 本教程 Tkinter 的字样是 Python 所自带的GUI库的统称，而 tkinter 代表旗下的库。两者是从属关系。
> - 本教程将以**Tk/tk**代指 `tkinter`，**Ttk/ttk**代指 `Tkinter.ttk`。
> - 本教程将以实用性为主，不关注底层逻辑与实现，同时受限于作者水平可能会有不严谨的地方。
> - 本教程所有代码运行环境为 Windows10 x64，使用VS Code编写。

参考：

[Tkinter官方文档 | https://docs.python.org/zh-cn/3.13/library/tkinter.html](https://docs.python.org/zh-cn/3.13/library/tkinter.html)

## 0 简介及概览

> [!TIP]
>
> 本章将介绍 GUI库 的功能并介绍Tkinter以及

### 0.1 GUI库的功能

我们平常的代码是基于命令行的，这意味着我们的大部分指令都需要通过命令行输入，这显然与我们现代的程序不符。

早期类似 MS-Dos 的系统是无GUI[^1]的CLI[^2]操作系统，需要操作者了解大量的命令来操作，且受专业训练。而如今的 Windows、MacOS 是有GUI的操作系统，小孩也能熟练上手。可以说 **直观，简便** 是GUI所需要做到的目标，这一部分可以参考 <u>0.3 GUI设计原则</u>。

而GUI库的功能，就是帮助我们快速地构建一个带有GUI的程序。目前先流行的库有 PyQT，wxPython。各个库的语法用法与结构都不同，因此在学习与开发难度上也不尽相同。

[^GUI]: GUI，Graphical User Interface 图形用户界面
[^CLI]: CLI, Command line User Interface 命令行用户接口

### 0.2 Tkinter的功能

Tkinter 是 Python 标准库，这类库非第三方，由 Python 官方发布管理，并随Python的安装一并下载。

Tkinter 作为 Python 原生GUI库，语法简单，兼容性好。此外，Tkinter 结构清晰，故学习成本低，易上手。然而有失有得，用 Python 开发，注定了它的运行效率低；历史悠久，也注定了它的外观平庸（尽管有ttk）。因此涌现了 Tkinter Tools，Customtkinter 等第三方美化库。如果想要更好地开发，可以使用集成开发环境或者 PyMe 等可视化布局工具。值得一提的是，类似Turtle以及Matplotlib针对Tkinter做了专门优化以及适配，因此可用于数据演示等场景。

那么，针对不在意美观，追求小巧的小型程序，Tkinter 是很适合的。

### 0.3 GUI设计原则

怎样的GUI设计才好用？才优秀？每个人都有着不同的见解：对于许多程序员，GUI不重要，由 Tkinter 制作的 Python 的 IDLE 就是一个例子；然而，如果你的程序想要被传播出去，被更多人使用，那么又很重要。

回到开头的问题，怎样的GUI设计才好用？才合理？联系GUI与CLI的概念，不难发现GUI的两个重点：用户、图形。那么不妨回到 GUI 所需要实现的目标：直观，简便。

何为直观？可视的，清晰的，易于分辨识别的。这就要求在开发时精简界面，避免杂乱无章的控件。直接在屏幕上呈现，让人一眼就能看到重点。

何为简便？简易的，便捷又迅速。我常常追求 **高可达性**，此又为何意？一个功能，可以通过多种途径调用，用户可以使用眼睛最快找到的，或者脑中最快想到的方法来激活一个功能。在一个功能的界面又可以通过按钮迅速打开相关联的界面。就像不同的地铁线路互相在枢纽交织，分担客流；而一个目的地可以通过多条线路到达，这样就避免了某一条线路的过度繁忙，同时又节约了乘客的时间。

这般，图形让程序直观，而高通达性又令用户的使用更加简便。

## 1 Tkinter的使用及架构

之后的章节，我们将假设学习者已经正确安装了 Python 并且获得了合适的开发环境。

要想使用Tkinter，首先应该在文件开头引入该库，键入：

```python
import tkinter as tk
```

我们使用`tk`来代表tkinter，这样可以更加方便快捷。

> [!TIP]
>
> 如果你使用了IDE[^3]，那么你将会看到相关的智能代码建议。将鼠标在`tkinter`字样上悬停，即可激活库的介绍。

![tip_example](image-20250118174845008.png)

图1.1 *VS Code所显示的对tkinter的介绍*

<img src="C:\Users\Alpha\Desktop\tkinter教程\image-20250118175511121.png" alt="auto_tip_example"  />

图1.2 *VS Code在导入库时的智能代码提示*

我们接下来通过智能代码提示粗略了解库的构成。在tkinter库中，又有如下子模块[^4]：

| 模块名                 | 功能                                                         |
| ---------------------- | ------------------------------------------------------------ |
| `tkinter.colorchooser` | 提供让用户选择颜色的对话框（类似于绘图软件的颜色选择）。     |
| `tkinter.commandialog` | 本文其他模块定义的对话框的基类。                             |
| `tkinter.constants`    | 当向 Tkinter 调用传入各种形参时可被用来代替字符串的符号常量。 由主 tkinter 模块自动导入。 |
| `tkinter.dnd`          | 针对  tkinter 的（实验性的）拖放支持。 当以 Tk DND 代替时它将会被弃用。 |
| `tkinter.filedialog`   | 允许用户指定文件的通用对话框，用于打开或保存文件。           |
| `tkinter.font`         | 帮助操作字体的工具。                                         |
| `tkinter.messagebox`   | 访问标准的 Tk 对话框。                                       |
| `tkinter.scrolledtext` | 内置纵向滚动条的文本组件。                                   |
| `tkinter.simpledialog` | 基础对话框和一些便捷功能。                                   |
| tkinter.`tix`          | 提供了更丰富的额外可视化部件集.                              |
| `tkinter.ttk`          | 在 Tk 8.5 中引入的带主题的控件集，提供了对应于 tkinter 模块中许多经典控件的现代替代。 |

> [!WARNING]
>
> - `tkinter.tix`已经被弃用，因为其现在已无人维护。请使用`tkinter.ttk`代替。
> - 带“dialog”字样的与对话框有关，提供一些获取诸如文件色彩等系统的集成控件。

它们大多以原版 tkinter 为基础做了集成的模块化，如果想要更加美观丰富的功能，可自己集成设计。

[^IDE]: IDE，集成开发环境。知名的有Pycharm以及安装了扩展的VS Code。
[^模块介绍的引用]: python.org 对tkinter模块的介绍。 https://docs.python.org/zh-cn/3/library/tkinter.html#architecture

## 2 Tkinter基本方法/控件

在 tkinter 中，控件主要分成三类：**标签/文本（Label类）、按钮（Button类）、输入框（Entry与Text类）**。

而带有“var”字样的准确来说不属于控件，这是一类专门存储用户输入的方法，常常与Entry等连用。

此外还有诸如`mainloop`、`Tk`等方法，主要用于GUI程序的初始化。也有一些用于处理数据文件的方法，我们会在下文提及。

接下来，我们将他们分类讲解。我们会先讲解它的基础用法，最后讲解自定义外观等内容。

> [!TIP]
>
> 在定义控件等时，我们会为其命名。除开基本的“驼峰命名法”，我们可以使用各控件首字母做标注，比如我们制作一个获取用户名的程序，核心代码如下：
>
> ```python
> StrVar_getname = tk.StringVar(win, value='')
> E_getname = tk.Entry(win, textvariable=StrVar_getname)
> ```
>
> 由于Entry组件需要配合StringVar使用，两者功能相似，为了在使用时不混淆可读性强，我们添加了标签。读者阅读以下的代码，将会深感其中的好处。

### 2.1 GUI程序初始化

### 2.2 标签/文本

### 2.3 按钮

### 2.4 输入框

一般地，输入框的方法名会带有“entry”字样，而 `tk.Entry`就是其中最基本的单行输入框。

```python
StrVar_password = tk.StringVar(root, value='') # 定义容器
E_password = tk.Entry(root, textvariable=StrVar_password)# 创建控件
print(StrVar_password.get)# 获取内容
```

一般来说，每一个Entry组件都应当配置一个`StringVar`[^1]，因为Entry组件只是向用户提供了一个内容输入的地方，而真正储存内容的是StringVar。就像寄快递，被寄送的东西交给处理的工作人员（就是Entry组件），工作人员获取后将其装入一个容器（比如快递箱子，就是StringVar）来储存它，方便运输等。寄出后收快递的人（程序）打开箱子获取被寄送的东西（在 tkinter 中使用`get`方法将内容获取并储存到一个变量中）。注意，实例中StrVar_password是tkinter定义的成员，而不是一个数据类型。当然实际的应用中，会创建一个按钮来激活获取内容的指令，实例代码中用户还未输入就已经执行过获取内容的操作了，因为`get`不会等待用户完成输入后再执行。

[^配置Var的例外]: 但是诸如RadioButton的勾选按钮，也是需要StringVar的支持的。

### 2.5 数据处理

## 3 Tkinter控件布局

## 4 子模块功能

## 5 基本GUI程序实例

