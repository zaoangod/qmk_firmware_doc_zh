# 刷写你的键盘

既然您已经构建了一个自定义固件文件，那么您需要刷写键盘。

## 使用 QMK 工具箱刷写键盘

刷写键盘的最简单方法是使用 [QMK Toolbox](https://github.com/qmk/qmk_toolbox/releases)。

然而，QMK 工具箱目前仅适用于 Windows 和 macOS。如果你正在使用 Linux（或者只是希望从命令行刷写固件），则必须使用下面的[方法](newbs_flashing.md#从命令行刷写键盘)

### 进入 QMK Toolbox 加载文件

首先打开 QMK Toolbox 应用程序，在 Finder 或 Explorer 中找到固件文件。你的键盘固件可能有以下两种格式之一：`.hex` 或 `.bin`。QMK 将会把其中合适之一复制到你的键盘的根 `qmk_firmware` 目录中。

?> 如果你用的是 Windows 或 macOS 系统，你可以使用命令来当前打开 Explorer 或 Finder 中的固件文件夹。

?> Windows:
```
start .
```
?> macOS:
```
open .
```

固件文件始终遵循以下命名格式：
```
<keyboard_name>_<keymap_name>.{bin,hex}
```
例如，`plank/rev5` 的 `default` 按键映射将具有以下文件名：
```
planck_rev5_default.hex
```

找到固件文件后，将其拖到 QMK Toolbox 的 "Local file" 框中，或单击 "Open" 并找到到存储固件文件的位置。

### 将键盘进入DFU（Bootloader）模式

要想刷入自定义固件，必须将键盘设置为特殊的刷写模式。在此模式下，你将无法输入或以其他方式使用键盘。切记，在写入固件时，不要拔掉键盘或中断刷写过程。

不同的键盘有不同的方式进入这种特殊模式。如果您的 PCB 当前运行 QMK 或 TMK 并且未给出具体说明，请按顺序尝试以下操作：

* 按住两个 `shift` 键并按 `Pause`
* 按住两个 `shift` 键并按 `B`
* 拔下键盘，同时按住空格键和 `B`，然后插上键盘并等待一秒钟然后松开按键
* 按下 PCB 底部的 `RESET` 按钮
* 找到标有 `BOOT0` 或 `RESET` 的 PCB 上的插头引脚，在插入 PCB 时将它们短接在一起

成功后，您将在 QMK Toolbox 中看到类似的消息：

```
*** Clueboard - Clueboard 66% HotSwap disconnected -- 0xC1ED:0x2390
*** DFU device connected
```

### 刷写你的键盘

点击 QMK Toolbox 中的 `Flash` 按钮。您将看到类似于以下的内容输出：

```
*** Clueboard - Clueboard 66% HotSwap disconnected -- 0xC1ED:0x2390
*** DFU device connected
*** Attempting to flash, please don't remove device
>>> dfu-programmer atmega32u4 erase --force
    Erasing flash...  Success
    Checking memory from 0x0 to 0x6FFF...  Empty.
>>> dfu-programmer atmega32u4 flash /Users/skully/qmk_firmware/clueboard_66_hotswap_gen1_skully.hex
    Checking memory from 0x0 to 0x55FF...  Empty.
    0%                            100%  Programming 0x5600 bytes...
    [>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>]  Success
    0%                            100%  Reading 0x7000 bytes...
    [>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>]  Success
    Validating...  Success
    0x5600 bytes written into 0x7000 bytes memory (76.79%).
>>> dfu-programmer atmega32u4 reset
    
*** DFU device disconnected
*** Clueboard - Clueboard 66% HotSwap connected -- 0xC1ED:0x2390
```

## 从命令行刷写键盘

首先你需要知道键盘使用哪个引导程序（bootloader）。通常有四种主要的引导程序（bootloader）。Pro-Micro 和它的克隆使用 CATERINA，Teensy's 使用 Halfkay，OLKB 主板使用 QMK-DFU，其他 atmega32u4 芯片使用 DFU。

你可以在[刷写操作指南和引导程序（bootloader）信息页](flashing.md)中找到关于引导程序（bootloader）的更多信息。

如果你知道你的键盘正在使用的引导程序（bootloader），那么在编译固件时，你可以在 `make` 命令中添加一些额外的文本来自动执行刷写过程。

### DFU

对于 DFU 引导程序，当你准备好编译和刷写固件时，可以打开终端窗口并运行构建命令：
```
make <my_keyboard>:<my_keymap>:dfu
```

例如，如果你的键盘映射名为 “xyverz” 并且您正在为 `rev5 planck` 构建键盘按键映射，那么你将使用以下命令：
```
make planck/rev5:xyverz:dfu
```
完成编译后，应输出看起来像以下的内容：

```
Linking: .build/planck_rev5_xyverz.elf                                                              [OK]
Creating load file for flashing: .build/planck_rev5_xyverz.hex                                      [OK]
Copying planck_rev5_xyverz.hex to qmk_firmware folder                                               [OK]
Checking file size of planck_rev5_xyverz.hex                                                        
* File size is fine - 18574/28672
```

到这一步时，构建脚本将每5秒钟查找一次 DFU 引导程序。它将重复以上操作，直到找到设备或你取消它。
```
dfu-programmer: no device present.
Error: Bootloader not found. Trying again in 5s.
```
完成后，你将需要重置控制器。然后它应该显示与此类似的输出：

```
*** Attempting to flash, please don't remove device
>>> dfu-programmer atmega32u4 erase --force
    Erasing flash...  Success
    Checking memory from 0x0 to 0x6FFF...  Empty.
>>> dfu-programmer atmega32u4 flash /Users/skully/qmk_firmware/clueboard_66_hotswap_gen1_skully.hex
    Checking memory from 0x0 to 0x55FF...  Empty.
    0%                            100%  Programming 0x5600 bytes...
    [>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>]  Success
    0%                            100%  Reading 0x7000 bytes...
    [>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>]  Success
    Validating...  Success
    0x5600 bytes written into 0x7000 bytes memory (76.79%).
>>> dfu-programmer atmega32u4 reset
```

如果有什么问题的话，你可以这样做：
```
sudo make <my_keyboard>:<my_keymap>:dfu
```

### Caterina 

对于 Arduino 主板板及其衍生产品（例如 SparkFunPro），当你准备好编译和刷写固件时，打开终端窗口并运行构建命令：
```
make <my_keyboard>:<my_keymap>:avrdude
```
例如，如果你的键盘按键映射名为 “xyverz” 并且你正在为 `rev2 Lets Split` 构建键盘按键映射，则你将使用以下命令：
```
make lets_split/rev2:xyverz:avrdude
```
完成编译后，输出看起来像是以下的内容：

```
Linking: .build/lets_split_rev2_xyverz.elf                                                            [OK]
Creating load file for flashing: .build/lets_split_rev2_xyverz.hex                                    [OK]
Checking file size of lets_split_rev2_xyverz.hex                                                      [OK]
 * File size is fine - 27938/28672
Detecting USB port, reset your controller now..............
```
此时，重置主板，然后脚本将检测引导程序，然后刷写主板。输出类似于下面的内容：

```
Detected controller on USB port at /dev/ttyS15

Connecting to programmer: .
Found programmer: Id = "CATERIN"; type = S
    Software Version = 1.0; No Hardware Version given.
Programmer supports auto addr increment.
Programmer supports buffered memory access with buffersize=128 bytes.

Programmer supports the following devices:
    Device code: 0x44

avrdude.exe: AVR device initialized and ready to accept instructions

Reading | ################################################## | 100% 0.00s

avrdude.exe: Device signature = 0x1e9587 (probably m32u4)
avrdude.exe: NOTE: "flash" memory has been specified, an erase cycle will be performed
             To disable this feature, specify the -D option.
avrdude.exe: erasing chip
avrdude.exe: reading input file "./.build/lets_split_rev2_xyverz.hex"
avrdude.exe: input file ./.build/lets_split_rev2_xyverz.hex auto detected as Intel Hex
avrdude.exe: writing flash (27938 bytes):

Writing | ################################################## | 100% 2.40s

avrdude.exe: 27938 bytes of flash written
avrdude.exe: verifying flash memory against ./.build/lets_split_rev2_xyverz.hex:
avrdude.exe: load data flash data from input file ./.build/lets_split_rev2_xyverz.hex:
avrdude.exe: input file ./.build/lets_split_rev2_xyverz.hex auto detected as Intel Hex
avrdude.exe: input file ./.build/lets_split_rev2_xyverz.hex contains 27938 bytes
avrdude.exe: reading on-chip flash data:

Reading | ################################################## | 100% 0.43s

avrdude.exe: verifying ...
avrdude.exe: 27938 bytes of flash verified

avrdude.exe: safemode: Fuses OK (E:CB, H:D8, L:FF)

avrdude.exe done.  Thank you.
```
如果有什么问题的话，你可以这样做：
```
sudo make <my_keyboard>:<my_keymap>:avrdude
```

## HalfKay

对于 PJRC 设备（Teensy's），当你准备好编译和刷写固件时，打开终端窗口并运行构建命令：
```
make <my_keyboard>:<my_keymap>:teensy
```
例如，如果你的键盘按键映射名为 “xyverz” 并且你正在为 Ergodox 或 Ergodox EZ 构建键盘按键映射，则你将使用以下命令：
```
make erdogox_ez:xyverz:teensy
```
完成编译后，输出看起来像是以下的内容：
```
Linking: .build/ergodox_ez_xyverz.elf                                                               [OK]
Creating load file for flashing: .build/ergodox_ez_xyverz.hex                                       [OK]
Checking file size of ergodox_ez_xyverz.hex                                                         [OK]
 * File size is fine - 25584/32256
 Teensy Loader, Command Line, Version 2.1
Read "./.build/ergodox_ez_xyverz.hex": 25584 bytes, 79.3% usage
Waiting for Teensy device...
 (hint: press the reset button)
```
此时，重置你的主板。完成后，你将看到像一下的输出内容：

```
Found HalfKay Bootloader
Read "./.build/ergodox_ez_drashna.hex": 28532 bytes, 88.5% usage
Programming......................................................................
...................................................
Booting
```

## 测试一下
恭喜！你的自定义固件已刷写到键盘里了！
尝试一下，确保一切按照你希望的方式运行。我们已经编写了[测试和调试](newbs_testing_debugging.md)来完善这个新手指南，所以请到那里了解如何测试和调试你的自定义功能。
