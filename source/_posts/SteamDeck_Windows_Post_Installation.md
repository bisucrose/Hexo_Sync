---
title: SteamDeck Tools
date: 2024-12-13 03:24:17
excerpt: ''
swiper: false
bgImg: []
swiperImg: ''
img: '' 
tags: [科普,搞机]
top: false
---

# SteamDeck安装Windows后的操作

## 前言

给SteamDeck安装Windows大大提高了SteamDeck的兼容性，个人感觉比SteamOS强了好几倍。但是发现很多人的SteamDeck都没有安装必要的插件，导致使用起来非常麻烦，所以写这篇文章来给大家安利一下好用的插件

## SteamDeck的Windows驱动

安装完Windows以后，各种驱动都没有打上，所有的驱动包可以在 [Steam 客服 :: Steam Deck - Windows 资源](https://help.steampowered.com/zh-cn/faqs/view/6121-ECCD-D643-BAA8) 处下载，注意现在SteamDeck已经有了OLED版本，需要下载对应的驱动并 **逐！个！安！装！**

## SteamDeck Tools

SteamDeck Tools集成了好几个模块，而且在不断更新。有了这个工具，Windows的日常使用体验其实就不输SteamOS了。GitHub下载链接在这里 [ayufan/steam-deck-tools: (Windows) Steam Deck Tools - Fan, Overlay, Power Control and Steam Controller for Windows](https://github.com/ayufan/steam-deck-tools) 有些地区可能需要加速，可以使用 [瓦特工具箱(Steam++官网) - Watt Toolkit](https://steampp.net/)

<span style="color:red">**注意：这个插件完全按照你的命令，操作不当可能会使你的Windows系统崩溃，甚至烧坏SteamDeck的硬件**</span>

### Fan Control

这个是控制SteamDeck风扇的小工具，里面内置了几个Profile。大家在安装完Windows的时候，会发现Windows系统下的风扇声音很大，这个里面的SteamOS的配置文件就是照搬了SteamOS的风扇温控曲线，建议平常使用选择SteamOS即可。Silent使用不当可能会使你的硬件过热，在某些早期机型上会使电源芯片脱焊。Max就是风扇开到最大，一般用不上。

### Performance Overlay

这个是在Windows上面模仿SteamOS上面显示性能参数的插件，基于RTSS（没安装或者没启动RTSS Service这个图标会变红），可以以浮窗形式显示各种参数，有几种模式，FPS，Detailed，Full啥的（忘记了），只有在打开游戏的时候才会调用。

### Power Control

用以实现SteamDeck里面按下三个点来控制功耗，帧率，CPU频率，GPU频率等。

### Steam Controller

这个用来模拟手柄，基于ViGemBus（没安装或者没启动这个图标会变红），Desktop模式就可以使用摇杆模拟鼠标，XBox，DS4模式可以模拟出来相应的手柄。背部按键也可以自定义，还有一些呼出屏幕键盘的快捷键设置等等。



## 安装SteamDeck Tool的注意事项

1. 网络环境不好可能会无法安装ViGemBus，请自行下载安装
2. RTSS安装完以后不会自行启动，请手动启动RTSS Service（在开始菜单里面），并设置开机自启动
3. 这几个插件都不会开机自启动，请手动设置Run at Startup
4. 请勾选这几个插件的 Use Kernel Drivers，否则会缺失功能
5. 调整手柄或者风扇可能会触发某些游戏的防作弊，~~我的这个是原神启动器，没试过~~



