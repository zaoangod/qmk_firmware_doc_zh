# 构建你的第一个固件

现在你已经设置好了构建环境，准备开始构建自定义固件。对于本指南的这一部分，我们将在3个应用之间进行跳转：文件管理器、文本编辑器和终端窗口。保持所有3个应用打开，直到你完成满意的键盘固件为止。

如果你已按照指南的第一部分重新打开终端窗口，不要忘记`cd qmk_firmware`，以便在终端中打开正确的目录。

## 导航到您的 Keymaps 文件夹

首先导航到键盘的 `keymaps` 文件夹。

?> 如果你使用的是 macOS 或 Windows，则可以使用命令轻松打开 keymaps 文件夹。
?> macOS:

    open keyboards/<keyboard_folder>/keymaps

?> Windows:

    start keyboards/<keyboard_folder>/keymaps

## 创建 `default` Keymap 的副本

打开 `keymaps` 文件夹后，您将需要创建 `default` 文件夹的副本。我们强烈建议你将文件夹命名为与 GitHub 用户名相同，但只要它包含小写字母，数字和下划线字符，你就可以使用任何您想要的名称。

要自动执行该过程，您还可以选择运行 `new_keymap.sh` 脚本。

导航到 `qmk_firmware/util` 目录并且输入下面内容：

```
./new_keymap.sh <keyboard path> <username>
```

例如，对于名为 John 的用户，尝试为 1up60hse 创建新的按键映射，他会输入：

```
./new_keymap.sh 1upkeyboards/1up60hse john
```

## 在您喜欢的文本编辑器中打开 `keymap.c`

打开 `keymap.c`，在该文件中，您可以找到控制键盘行为的规则。在 `keymap.c` 的顶部，可能有一些定义和枚举使按键映射更容易阅读。再向下，你会找到如下所示的一行内容：

```
const uint16_t PROGMEM keymaps[][MATRIX_ROWS][MATRIX_COLS] = {
```

该行指示层列表的开始。在下面你会找到包含 `LAYOUT` 或 `KEYMAP` 的行，这些行表示按键层的开始。在该行下是包含该特定层的按键的列表。

?> 编辑按键映射文件时，请注意不要添加或删除任何逗号。如果删除了，编译固件的时候将会异常，可能不容易找出缺少或多出的逗号。

## 根据你的喜好自定义布局

如何完成这一步完全取决于你。如果有异常一直困扰着你，你可以重新开始。如果你不需要所有的按键层，你可以删除它们，或者添加最多32个按键层。请查看以下文档解您可以在此处定义的内容：

* [键码](keycodes.md)
* [特色](features.md)
* [常见问题解答](faq.md)

?> 当你对 keymaps 的工作方式有所了解之前，保持每一次修改都不要太多。更大的变化使得出现问题时调试变得更困难。

## 构建你的固件

完成对按键映射的更改后，你需要构建固件。请返回终端窗口并运行 build 命令：
```
make <my_keyboard>:<my_keymap>
```
例如，如果你的键盘映射名为“xyverz”并且您正在为 rev5 planck 构建键盘映射，那么将使用以下命令：
```
make planck/rev5:xyverz
```
在编译时，将有大量输出日志在屏幕上，告诉你正在编译什么文件。它的输出应该与以下内容相似：

```
Linking: .build/planck_rev5_xyverz.elf                                                              [OK]
Creating load file for flashing: .build/planck_rev5_xyverz.hex                                      [OK]
Copying planck_rev5_xyverz.hex to qmk_firmware folder                                               [OK]
Checking file size of planck_rev5_xyverz.hex                                                        [OK]
 * File size is fine - 18392/28672
```

## 刷写你的固件
转到[刷写固件](newbs_flashing.md)，了解如何将新固件写入键盘。
