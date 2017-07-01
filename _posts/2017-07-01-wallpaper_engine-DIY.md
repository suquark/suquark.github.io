---
layout: post
title: Wallpaper Engine DIY
comments: true
mathjax: true
excerpt: "windows"
date:   2017-07-01 +1627
categories: lecture
---

Steam 上面可以自定义桌面背景的 Wallpaper Engine 可以说在前一段时间非常火。这里我给出一种实现 Wallpaper Engine 的方式，并给出探究的具体过程。你可能只对最后的结果和方法感兴趣，但是我仍然希望你能够了解其中的原理。方法是只对一定时期的windows有效的，但是原理却是通用的。

这篇文章用来揭示windows（特别是windows10的）窗口机制，并介绍如何创建自己的 Wallpaper Engine。主要使用的工具是Spy++（装 Visual Studio 的时候附属的工具）；使用的语言是 C#，因为它既是方便高效的语言，也很容易对接 windows 底层 API。

(注：API 指Application Platform Interface，应用平台接口。是平台向依赖平台的程序提供的一组必要的服务接口。这应当是个常识。

## 什么是窗口 (window)

说到窗口，你的印象可能是一个方框，右上角有着关闭，最小化这些按钮（macosx等在左上角）。微软 windows 系统的命名很显然受到 window 的影响，window 代表了当时图形界面的最先进组织方式，直到现在都是桌面端的最主要交互形式。

但是，为了精确表述概念，我们需要将窗口表述为一个数学上的抽象的对象。实质上，你在windows上看到的大多数东西，包括开始菜单、任务栏、任务栏缩略图、桌面背景(vista之后)等都是某种形式的窗口。并且还有大量的窗口甚至根本不提供任何可以看到的东西。

### 窗口与抽象文件

#### 窗口的生命周期和操作方式类似文件

生命周期 (lifecycle) 涉及了一个对象的创建、操作和回收。

窗口的生命周期和一个抽象文件是类似的，都拥有对应的系统级API。

窗口创建后，会返回一个称为“句柄(handle)”的整数（linux/*nix下面一般称为文件描述符(FD)）。句柄代表了对内核中的窗口对象的引用。

下面的所有操作都用句柄代替窗口对象本身，这样应用程序就无需涉及到窗口对象操作的细节和实质，起到了隔离的作用。

#### 窗口的名称、类和属性

窗口像文件一样，有名称和属性。属性决定窗口是否可见、窗口是否有边框等等。

除此之外，窗口还有特殊的称为类名称(ClassName)的东西，它一般用来表示类型或者用途。

比如类名是 TaskListThumbnailWnd 显示鼠标移动到任务栏上面的时候对应任务的缩略图。

Shell_TrayWnd  则是windows任务栏。

### 窗口与消息队列

一个消息队列处理系统执行下面的功能：

1. 拥有 SendMessage 函数，可以向指定的目标发送自定义的消息。
2. 系统本身实现了处理接受到的消息的功能。

窗口是一个消息队列处理系统的接受部分 -- 它会接受各种消息并处理它们。敲击键盘，移动鼠标，甚至关闭窗口等都会以消息的形式发送给窗口。如果你试图忽略关闭窗口的消息，就会发现怎么点窗口右上方的关闭按钮，窗口都不会有反应，也就是窗口关闭是程序自己处理的过程，而不是“用户实现”的，关闭按钮仅仅给你一种主动关闭的感受，而实质上这是个程序自己意愿完成的被动任务。

如果窗口超过一段时间无法处理消息，比如程序出现卡死的情况，windows会给窗口加上“无响应”的标题。这个时候你试图关闭窗口往往不能一下子成功，因为窗口无法处理你发送给它的关闭消息。有时候在无响应时你一直点关闭，过一会儿窗口就关闭了，那是因为窗口已经开始处理消息，并收到了先前要求关闭的内容。（当然，你可以通过任务管理器等强行关闭程序，不过那是强行结束进程，回收进程所有的内核对象（窗口当然也不例外），而不是仅仅关闭窗口。

一个windows窗口可以不显示任何界面，仅仅接受消息。它仍然是一个窗口，只是不可见而已。比如说触控板和数位板等会建立一个用于采集用户输入的窗口，以确定位置和用户手势。

PS：为什么正常关闭窗口这个行为要求程序自己实现？这是因为关闭前程序有必要进行一些必要的操作，比如提醒用户是否放弃编辑等等。如果用户可以直接关闭窗口本身，那么程序将无法保证一致性。

### 窗口坐标和层次

Windows 的窗口拥有坐标的概念，一是窗口的坐标（左上角的位置），二是所谓的 z-index，代表了z轴（垂直于屏幕方向的）的坐标。

z-index是相对于同一个窗口的子窗口而言的。一个窗口可以拥有多个子窗口，一个子窗口仅对应唯一的父窗口。

影响窗口坐标的还有TOPMOST属性。

窗口的显示层次可以用以下的一阶逻辑形式化语言表述：

* 约定自由变量和约束变量均为窗口实例
* 谓词 $parent(x,y)$ 语义为 “y是x的子窗口”
* 谓词 $ancestor(x,y)$ 语义为“x是y的祖先（自反的）”
* 谓词 brothers(x,y)$ 语义为“x和y是兄弟”
* 谓词 $topmost(x)$ 语义为“x具有topmost属性”
* 等词 $x>y$ 语义是“x显示在y之上”，且是一个偏序关系
* 等词 $x=y$ 语义是“x和y是同一窗口实例”
* 函数 $zorder(x)$ 得出窗口x的z-order值

则存在下面的完备的可以推断任意两个窗口显示层次先后的公理集：

$$
\begin{equation}
  \begin{array}{lr}
    ancestor(x,x) &(0)\\
    ancestor(x,y)\land ancestor(y,z)\rightarrow ancestor(x,z) &(1)\\
    parent(x,y)\rightarrow ancestor(x,y) &(2)\\
    brothers(x,y)\leftrightarrow x\neq y\land(\exists p,parent(p,x)\land parent(p,y)) &(3)\\
    ancestor(x,y)\rightarrow y>x &(4)\\
    brothers(x,y)\land(zorder(x)>zorder(y)\lor(topmost(x)\land\lnot topmost(y))) \rightarrow x>y &(5)\\
    (\exists p\exists q,brothers(p,q)\land p > q\land ancestor(p,x)\land ancestor(q,x))\rightarrow x>y &(6)\\
  \end{array}
\end{equation}
$$


windows 窗口可以根据父节点和子节点的关系画成一棵树。一棵树的根节点是“桌面”对象。曾经的windows第三方多桌面实现都是通过创建多个桌面对象决定的。Win10之后，我们可以看到多桌面实质上是通过一个桌面包装而成，也就是所有的窗口都在同一个桌面下，即使看上去它们处于不同的桌面。**根节点的（直接）子节点被称为“顶级窗口”**。

(注：锁屏、UAC等任务仍然可能使用了其他的桌面)

一个例子如下：

![1-2.PNG](/static/wallpaper_engine-DIY/EB80F41CE2A86998C56D2B3256336FDB.png)

任务栏是带有TOPMOST但z-index最小的顶级窗口，因此任何不具有TOPMOST属性的窗口都会盖在任务栏之下。任务管理器选择了“始终显示在最前面”之后也具有了TOPMOST属性，且z-index高于任务栏，因此会始终盖在任务栏和其他窗口上面。

## windows 桌面图标和背景机制

按照我们的尝试，桌面背景和图标都会在一般窗口的下面，同时图标会显示在桌面背景前面。

以win10为例，使用spy++查看就可以知道原因：

显示桌面背景的窗口类名称是 Program，它是z-index最低的顶级窗口，所以始终在所有窗口下面。而显示桌面图标的窗口类名称是 SHELLDLL_DefView，是它的子窗口，因此覆盖在桌面背景上面，但是不会盖在任何其他窗口上面。

![0.png](/static/wallpaper_engine-DIY/45065DA0DA1C168044532E2DD39B5F7B.png)

这时候我们强行将名称为Test Window的窗口作为Program的子窗口：

![1-1.PNG](/static/wallpaper_engine-DIY/651B173FA794EC374F29D233F8CD4120.png)

由于其z-index最高，所以显示在最上面

![1.png](/static/wallpaper_engine-DIY/D18914829B0F1E0185AF31F3E0C02BA3.png)

但是使用windows的任务导航（这个按钮

![IMAGE](/static/wallpaper_engine-DIY/29B7FBBAE11D9BCC4EFEA7ED9F7D8C31.jpg)

之后，事情变得有趣了：

![2.PNG](/static/wallpaper_engine-DIY/AA02CF1E6B4A1A57005380EF0C89CF91.png)

之前我们创建的Test Window似乎变得透明，而且还洞穿了桌面上面的图标，直接把桌面背景透了上来。

到底发生了什么？我们看现在的窗口树：

![2-1.PNG](/static/wallpaper_engine-DIY/E07E2BD3B52314F2A919214EEE5EA602.png)

Program 窗口新建了两个WorkerW窗口，置于自己的上方。并且将自己的所有子窗口甩给了第一个WorkerW。

窗口变透明是什么回事？几乎唯一的可能是为了让第二个WorkerW的东西能够透上来，windows设置了透明色，如果是黑色那么就直接透过不会遮挡后面的内容。第一个WorkerW就是一个黑色的窗口，现在Test Window内容也是黑的，所以被一起镂空了，直接透露了下面的桌面背景。

那么现在显示桌面背景的很可能就是下面的WorkerW。我们转而在下面的WorkerW上建了子窗口，发现确实如我们所料。

但是为什么要单独让一个WorkerW显示桌面背景呢？在预览各个桌面时发现了这个现象：

![3-1.png](/static/wallpaper_engine-DIY/7B5352DA29912CCECD9870F6BA296BA7.png)

对比一下正常的：

![3-0.png](/static/wallpaper_engine-DIY/F8DD92143B4FBC7AE30F3389DBC7B34D.png)

看来目的是让这个WorkerW当做预览后面的背景用的。现在我们的窗口也变成预览背景的一部分了，看上去很滑稽。

如果隐藏这个WorkerW，会变成这个样子：

![3.png](/static/wallpaper_engine-DIY/D1DC8C8FD503B14C3A53316ACDEBDD9C.png)

桌面直接没了，预览的时候也变透明了。。。

## 如何诱导出WorkerW

前面看到，如果存在WorkerW的时候，我们直接建个窗口当做它的子窗口就大功告成了，这个时候我们可以在这个子窗口里面干任何我们想要做的事情，比如看视频什么什么，已经接近一个Wallpaper Engine了。

显然每次调出任务视图太麻烦。有没有自动的方法呢？当然是有的，实际上win7的时候微软就早有准备做好了。方法是通过 SendMessage 向 Program 窗口发送内容为 0x052C 的消息（还记得窗口是消息系统吗）。这时候 Program 窗口就会像之前那样甩出两个WorkerW窗口。

那么如何真正做到功能类似 Wallpaper Engine 这样的支持视频甚至脚本的程序呢？很简单，为你的程序套上一个浏览器（想象一下如果你把Chrome变成桌面背景，那么你就可以在创意工坊里面发 Chrome 插件来实现各种功能。Steam的Wallpaper Engine就是某种浏览器。

## Show me the code

使用C#编写。我不准备在这里叙述C#语法。其中用到的win32 api的意义正如其名称所示。具体信息可以查询MSDN。

{% highlight csharp %}
using System;
using System.Collections.Generic;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading;
using System.Threading.Tasks;
using System.Windows.Forms;
using System.Runtime.InteropServices;

namespace DrawBehindDesktopIcons
{
    class Program
    {
        [STAThread]
        static void Main(string[] args)
        {
            // Fetch the Progman window
            var progman = FindWindow("Progman", null);
            var result = IntPtr.Zero;

            // Send 0x052C to Progman. This message directs Progman to spawn a 
            // WorkerW behind the desktop icons. If it is already there, nothing 
            // happens.

            SendMessageTimeout(progman, 0x052C, new IntPtr(0), IntPtr.Zero,
                               SendMessageTimeoutFlags.SMTO_NORMAL,
                               1000,
                               out result);

            var workerw = IntPtr.Zero;

            // We enumerate all Windows, until we find one, that has the SHELLDLL_DefView 
            // as a child. 
            // If we found that window, we take its next sibling and assign it to workerw.
            EnumWindows(new EnumWindowsProc((tophandle, topparamhandle) =>
            {
                var p = FindWindowEx(tophandle,
                                        IntPtr.Zero,
                                        "SHELLDLL_DefView",
                                        IntPtr.Zero);

                if (p != IntPtr.Zero)
                {
                    // Gets the WorkerW Window after the current one.
                    workerw = FindWindowEx(IntPtr.Zero,
                                           tophandle,
                                           "WorkerW",
                                           IntPtr.Zero);
                }

                return true;
            }), IntPtr.Zero);

            var form = new Form() { Text = "Test Window" };

            form.Load += new EventHandler((s, e) =>
            {
                // hide the border of the form
                form.FormBorderStyle = FormBorderStyle.None;
                form.Controls.Add(new WebBrowser() { 
                    Url = new Uri("http://ustc.edu") 
                });
                SetParent(form.Handle, workerw);
                form.WindowState = FormWindowState.Maximized;
                webview.Dock = DockStyle.Fill;
            });
            form.Show();
            // Start the Application Loop for the Form.
            Application.Run(form);
        }
    }
}
{% endhighlight %}

有一些Win32 API的声明。你应当将它们加入到代码中：

{% highlight csharp %}
[DllImport("user32.dll", SetLastError = true)]
public static extern IntPtr SetParent(IntPtr hWndChild, IntPtr hWndNewParent);

public delegate bool EnumWindowsProc(IntPtr hwnd, IntPtr lParam);

[DllImport("user32.dll")]
[return: MarshalAs(UnmanagedType.Bool)]
public static extern bool EnumWindows(EnumWindowsProc lpEnumFunc, IntPtr lParam);

[DllImport("user32.dll", SetLastError = true)]
public static extern IntPtr FindWindow(string lpClassName, string lpWindowName);

[DllImport("user32.dll", SetLastError = true)]
public static extern IntPtr FindWindowEx(IntPtr parentHandle, IntPtr childAfter, string className, IntPtr windowTitle);

[Flags]
public enum SendMessageTimeoutFlags : uint
{
    SMTO_NORMAL = 0x0,
    SMTO_BLOCK = 0x1,
    SMTO_ABORTIFHUNG = 0x2,
    SMTO_NOTIMEOUTIFNOTHUNG = 0x8,
    SMTO_ERRORONEXIT = 0x20
}

[DllImport("user32.dll", SetLastError = true, CharSet = CharSet.Auto)]
public static extern IntPtr SendMessageTimeout(IntPtr windowHandle, uint Msg, IntPtr wParam, IntPtr lParam, SendMessageTimeoutFlags flags, uint timeout, out IntPtr result);
{% endhighlight %}