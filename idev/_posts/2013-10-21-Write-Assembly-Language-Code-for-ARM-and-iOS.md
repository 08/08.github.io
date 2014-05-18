---
layout: post_idev
title: Write Assembly language code for ARM and iOS
author: Ethan
---

为ARM写汇编代码主要下面有三种方式:

  1. 内联汇编 --嵌入到C/C++/Objective-C代码中
  2. 纯汇编代码 --命名为".s"格式的文件，添加到Xcode项目中
  3. 通过外部的汇编编译器生成目标文件连接到项目中， 比如使用[FASMARM][FASMARM]	


接下来你需要了解写ARM汇编的一些基本知识，可以参考:

  * [Coranac's Whirlwind Tour of ARM Assembly][A very good but old intro]
  * [Thumb-2 instructions at DaveSpace's Introduction to arm][A recent intro including Thumb-2 instructions]
  *	[BraveGNU's Embedded Programming with the GNU Toolchain][Another good intro]
  * [WebShaker's Begin Programming Assembler with GCC][A brief introduction]
  * [Ethernut's ARM GCC Inline Assembler Cookbook][if you specifically want to use GCC inline assembler]

[FASMARM]: http://arm.flatassembler.net/
[A very good but old intro]: http://www.coranac.com/tonc/text/asm.htm
[A recent intro including Thumb-2 instructions]: http://www.davespace.co.uk/arm/introduction-to-arm/index.html
[Another good intro]: http://www.bravegnu.org/gnu-eprog/index.html
[A brief introduction]: http://pulsar.webshaker.net/2011/04/01/begin-programming-assembler-with-gcc/#more-873
[if you specifically want to use GCC inline assembler]: http://www.ethernut.de/en/documents/arm-inline-asm.html