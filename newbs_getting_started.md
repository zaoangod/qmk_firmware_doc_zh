# 引言

你的计算机键盘内部有处理器，与计算机内部的处理器不同。该处理器运行的软件负责检测按钮按下或者松开，并且发送按键的状态。QMK 充当该软件的角色，检测按钮按下并将该信息传递到计算机。当你构建自定义按键映射时，你将为键盘创建一个等效的.exe。

QMK 试图通过让简单的事情变得简单，让困难的事情成为可能，来为你提供大量的能力。不需要知道如何编程，你只需要遵循一些简单的语法规则，就能够创建出强大的按键映射。

# 入门

在构建键盘按键映射之前，你需要设置构建环境并且安装一些软件。无论你想为多少个键盘编译固件，这个过程都只需要执行一次。

## 下载软件

### Text Editor

你需要一个可以编辑和保存纯文本文件的程序。如果你使用的是 Windows，则可以使用记事本进行操作，而在 Linux 上则可以使用 Gedit，这两者都是使用简单但功能强大的文本编辑器。在 macOS 上要小心 TextEdit.app，它不会保存纯文本文件，除非你确保从`格式`菜单中选择`制作纯文本`，或者你可以使用其他程序，如 `Sublime Text`。

?> 不确定要使用哪个文本编辑器？Laurence Bradford 写了一篇关于这个主题的[精彩介绍](https://learntocodewith.me/programming/basics/text-editors/)。

### QMK Toolbox

QMK Toolbox 是一个可选的图形化 Windows 和 macOS 程序，允许您编程和调试自定义键盘。你可能更喜欢它轻松刷写键盘并接收键盘打印的调试消息。

从以下链接下载文件：

Windows: "qmk_toolbox.exe" or "qmk_toolbox_install.exe"(需要安装)

Mac: "QMK.Toolbox.app.zip" or "QMK.Toolbox.pkg"(需要安装)

* [最新发布](https://github.com/qmk/qmk_toolbox/releases/latest)
* [源码](https://github.com/qmk/qmk_toolbox/)

## 环境设置

我们试图让 `QMK` 尽可能易于设置。你只需准备 `Linux` 或 `Unix` 环境，然后安装 `QMK` 其余部分。

?> 如果你没有使用过 `Linux/Unix` 命令行，那么应该在开始之前学习一些基础知识和命令。这些资源将可以满足你在 `Linux` 上使用 `QMK`：

[必须掌握的 Linux 命令](https://www.guru99.com/must-know-linux-commands.html)
[一些基本的 Unix 命令](https://www.tjhsst.edu/~dhyatt/superap/unixcmd.html)

### Windows

你需要安装 MSYS2 和 Git。

* 按照 MSYS2 主页上的安装说明进行操作：http://www.msys2.org
* 关闭所有打开的 MSYS2 终端，然后打开一个新终端
* 运行命令安装 Git：`pacman -S git`

### macOS

你需要安装 `homebrew`。按照 `homebrew` 主页上的说明操作：https://brew.sh

安装 `homebrew` 后继续 “下载QMK”，下载完成，执行 “安装QMK” 步骤，运行将安装其他软件包的脚本。

### Linux

你需要安装 `Git`。你可能已经安装了 `Git`，如果没有，运行下面的命令进行安装：

* Debian/Ubuntu/Devuan: `apt-get install git`
* Fedora/Redhat/Centos: `yum install git`
* Arch: `pacman -S git`

## 下载 QMK

一旦设置了 `Linux/Unix` 环境，就可以下载 `QMK` 了。我们使用 `Git` 来克隆 `QMK` 仓库。打开终端或 `MSYS2` 控制台窗口，并保持全程打开状态。

```
git clone https://github.com/qmk/qmk_firmware.git
cd qmk_firmware
```

?> 如果你已经知道如何使用 [GitHub](getting_started_github.md)，我们建议你创建并克隆自己的 fork。如果你不知道这意味着什么，那么你可以忽略这条建议。

## 设置 QMK

QMK 附带一个脚本，可帮助你设置剩下的步骤。现在通过命令行输入以下命令来运行它：

```
./util/qmk_install.sh
```

## 测试你的构建环境

现在你已经设置了 `QMK` 构建环境，可以为键盘构建固件了。首先尝试为键盘构建默认布局。你可以使用以下格式的命令执行此操作：

```
make <keyboard>:default
```

例如，要为 `Clueboard 66％` 构建固件，请使用：

```
make clueboard/66/rev3:default
```

当它完成时，你将看到类似下面的输出内容：

```
Linking: .build/clueboard_66_rev2_default.elf                                                       [OK]
Creating load file for flashing: .build/clueboard_66_rev2_default.hex                               [OK]
Copying clueboard_66_rev2_default.hex to qmk_firmware folder                                        [OK]
Checking file size of clueboard_66_rev2_default.hex                                                 [OK]
 * File size is fine - 25174/28672
```

## 创建你的布局

现在你已准备好创建自己的键盘按键映射了。继续[构建](newbs_building_firmware.md)你的第一个固件。