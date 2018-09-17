# Quantum Mechanical Keyboard Firmware

[![Current Version](https://img.shields.io/github/tag/qmk/qmk_firmware.svg)](https://github.com/qmk/qmk_firmware/tags)
[![Build Status](https://travis-ci.org/qmk/qmk_firmware.svg?branch=master)](https://travis-ci.org/qmk/qmk_firmware)
[![Discord](https://img.shields.io/discord/440868230475677696.svg)](https://discord.gg/Uq7gcHh)
[![Docs Status](https://img.shields.io/badge/docs-ready-orange.svg)](https://docs.qmk.fm)
[![GitHub contributors](https://img.shields.io/github/contributors/qmk/qmk_firmware.svg)](https://github.com/qmk/qmk_firmware/pulse/monthly)
[![GitHub forks](https://img.shields.io/github/forks/qmk/qmk_firmware.svg?style=social&label=Fork)](https://github.com/qmk/qmk_firmware/)

## QMK 固件是什么?

QMK (*Quantum Mechanical Keyboard*) 是一个维护QMK固件的开源社区，QMK 工具箱，qmk.fm，这些文档。QMK 固件是基于 [tmk_keyboard](http://github.com/tmk/tmk_keyboard) 的键盘固件，具有 Atmel AVR 控制器的一些有用功能，更具体地说，[OLKB](http://olkb.com) 产品线，ErgoDox EZ键盘，[ErgoDox EZ](http://www.ergodox-ez.com) 键盘，[Clueboard](http://clueboard.co/) 产品线，它也被使用 ChibiOS 移植到 ARM 芯片上，你可以使用在自己的手工布线或自定义 PCB 的键盘上。

## 如何获得它

如果您打算向 QMK 贡献一个按键映射，键盘或特性，最简单的方法是通过 Github fork 这个[仓库](https://github.com/qmk/qmk_firmware#fork-destination-box)，并且克隆仓库到本地进行更改，推送它们，然后从你 fork 的仓库 [Pull Request](https://github.com/qmk/qmk_firmware/pulls) 。

否则，您可以直接下载 ([zip](https://github.com/qmk/qmk_firmware/zipball/master), [tar](https://github.com/qmk/qmk_firmware/tarball/master))，或通过 git(git@github.com:qmk/qmk_firmware.git) 或者 https (https://github.com/qmk/qmk_firmware.git) 克隆它 。

## 如何编译

在你能够编译之前，怒需要为 AVR 或 ARM 开发[安装](getting_started_build_tools.md)一个环境。一旦完成，你就可以使用 `make` 命令用以下表示法构建键盘和按键映射：
```
    make planck/rev4:default
```
这将使用默认的按键映射构建 `planck` 的 `rev4` 修订版。并非所有键盘都有修订版（也称为子项目或文件夹），在这种情况下，它可以省略：
```
    make preonic:default
```
## 如何定制

QMK 有许多值得探索的[特点](features.md)，以及大量的[参考文档](http://docs.qmk.fm)。通过修改[按键映射](keymap.md)和更改[键码](keycodes.md)可以充分利用大多数功能。