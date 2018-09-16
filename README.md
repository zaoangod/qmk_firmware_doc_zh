# Quantum Mechanical Keyboard Firmware

[![Current Version](https://img.shields.io/github/tag/qmk/qmk_firmware.svg)](https://github.com/qmk/qmk_firmware/tags)
[![Build Status](https://travis-ci.org/qmk/qmk_firmware.svg?branch=master)](https://travis-ci.org/qmk/qmk_firmware)
[![Discord](https://img.shields.io/discord/440868230475677696.svg)](https://discord.gg/Uq7gcHh)
[![Docs Status](https://img.shields.io/badge/docs-ready-orange.svg)](https://docs.qmk.fm)
[![GitHub contributors](https://img.shields.io/github/contributors/qmk/qmk_firmware.svg)](https://github.com/qmk/qmk_firmware/pulse/monthly)
[![GitHub forks](https://img.shields.io/github/forks/qmk/qmk_firmware.svg?style=social&label=Fork)](https://github.com/qmk/qmk_firmware/)

## What is QMK Firmware?
## QMK 固件是什么?

QMK (*Quantum Mechanical Keyboard*) is an open source community that maintains QMK Firmware, QMK Toolbox, qmk.fm, and these docs. QMK Firmware is a keyboard firmware based on the [tmk\_keyboard](http://github.com/tmk/tmk_keyboard) with some useful features for Atmel AVR controllers, and more specifically, the [OLKB product line](http://olkb.com), the [ErgoDox EZ](http://www.ergodox-ez.com) keyboard, and the [Clueboard product line](http://clueboard.co/). It has also been ported to ARM chips using ChibiOS. You can use it to power your own hand-wired or custom keyboard PCB.
QMK (*Quantum Mechanical Keyboard*) 是一个维护QMK固件的开源社区，QMK 工具箱，qmk.fm，这些文档。QMK 固件是基于 [tmk_keyboard](http://github.com/tmk/tmk_keyboard) 的键盘固件，具有 Atmel AVR 控制器的一些有用功能，更具体地说，[OLKB](http://olkb.com) 产品线，ErgoDox EZ键盘，[ErgoDox EZ](http://www.ergodox-ez.com) 键盘，[Clueboard](http://clueboard.co/) 产品线，它也被使用 ChibiOS 移植到 ARM 芯片上，你可以使用在自己的手工布线或自定义 PCB 的键盘上。

## How to Get It
## 如何获得它

If you plan on contributing a keymap, keyboard, or features to QMK, the easiest thing to do is [fork the repo through Github](https://github.com/qmk/qmk_firmware#fork-destination-box), and clone your repo locally to make your changes, push them, then open a [Pull Request](https://github.com/qmk/qmk_firmware/pulls) from your fork.
如果您打算向 QMK 贡献一个按键映射，键盘或特性，最简单的方法是通过 Github fork 这个[仓库](https://github.com/qmk/qmk_firmware#fork-destination-box)，并且克隆仓库到本地进行更改，推送它们，然后从你 fork 的仓库 [Pull Request](https://github.com/qmk/qmk_firmware/pulls) 。

Otherwise, you can either download it directly ([zip](https://github.com/qmk/qmk_firmware/zipball/master), [tar](https://github.com/qmk/qmk_firmware/tarball/master)), or clone it via git (`git@github.com:qmk/qmk_firmware.git`), or https (`https://github.com/qmk/qmk_firmware.git`).
否则，您可以直接下载 ([zip](https://github.com/qmk/qmk_firmware/zipball/master), [tar](https://github.com/qmk/qmk_firmware/tarball/master))，或通过 git(git@github.com:qmk/qmk_firmware.git) 或者 https (https://github.com/qmk/qmk_firmware.git) 克隆它 。

## How to Compile
## 如何编译

Before you are able to compile, you'll need to [install an environment](getting_started_build_tools.md) for AVR or/and ARM development. Once that is complete, you'll use the `make` command to build a keyboard and keymap with the following notation:
在你能够编译之前，怒需要为 AVR 或 ARM 开发[安装](getting_started_build_tools.md)一个环境。一旦完成，你就可以使用 `make` 命令用以下表示法构建键盘和按键映射：

    make planck/rev4:default

This would build the `rev4` revision of the `planck` with the `default` keymap. Not all keyboards have revisions (also called subprojects or folders), in which case, it can be omitted:
这将使用默认的按键映射构建 `planck` 的 `rev4` 修订版。并非所有键盘都有修订版（也称为子项目或文件夹），在这种情况下，它可以省略：

    make preonic:default

## How to Customize
## 如何定制

QMK has lots of [features](features.md) to explore, and a good deal of [reference documentation](http://docs.qmk.fm) to dig through. Most features are taken advantage of by modifying your [keymap](keymap.md), and changing the [keycodes](keycodes.md).
QMK 有许多值得探索的[特点](features.md)，以及大量的[参考文档](http://docs.qmk.fm)。通过修改按键映射和更改键码可以充分利用大多数功能。