---
title: STM32LearningNoteOld
date: 2023-07-24 21:24:29
excerpt: ''
swiper: false
bgImg: []
swiperImg: ''
img: '' 
tags: [Archived]
---

# 记录这几天学习STM32的玄幻经历

第一天安装keil5，告诉我keil4没有卸载干净，需要先卸载keil4。清理了半天没找到在哪里有残留文件，遂手动解包配置，折腾一整天安装完成。

第二天测试例程发现烧不进去，检查pack安装无误，所有功能一切正常，全网搜不到相关错误遂转投STM32CubeIDE。之前安装过一次没有用过，这次安装完以后调试的时候无法使用，报错信息全网仅有5条全是unsolved。后来怀疑是之前安装的汉化包的问题，遂通宵重装系统(软件全安C盘了，所以重装系统花了好长时间)

第三天软件全部安装完毕，开始正式学习，从闪灯学起，遇到问题，一运行到HAL_Delay函数整个程序就莫名其妙卡死无法继续运行，结果烧进去例程就能正常运行。上网搜索竟然还有一大堆看起来很有道理的解释，比如ticktock中断优先级是15，闪灯时有其他的中断把函数阻塞了。研究了一整天未果，结果换了STM32F103C8T6就全好使了。开始怀疑是板子有问题

第四天培训完以后向老师说明，老师A说我心不诚，老师B说板子坏了的可能性很小，大多都是我软件配置有问题，让老师A帮忙看一下，但老师A着急吃饭，略微瞥了一眼说我配置有问题，遂回去研究了一整天时钟配置未果。

第五天开始向周围人请求解答，大家都忙，无人解答。樊佬抽了时间帮忙看了一下，说我配置没有问题。发现郑佬有相同的板子，将程序发给他烧进去就能用。确定板子损坏。

第六天更换了板子，一切正常。

自此，学习兴趣全无。
