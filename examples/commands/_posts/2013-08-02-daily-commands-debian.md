---
layout: nil
title: daily commands on debian
---

daily commands on debian

## "CDRom is not detected in Debian installer"
量产使用USB-DVD/CD安装debian的时候

## "Unable to resolve UUIDs"
对于经常折腾系统的同学，“Unable to resolve UUIDs”频繁出现, 需要删掉废弃的UUID
	＃ nano /etc/fstab


## debian wheezy driver

在一些配有旧款ATI显卡和Marvell Yukon网卡的笔记本装debian wheezy， 总会为装驱动而头疼。 我这里有一款10年产的hp 4411s 481，5月份折腾过。
弄了个64位版的,

首先看看显卡驱动,很多依赖文件都得装上
	＃ sudo apt-get fglrx-driver fglrx-control fglrx-glx-ia32 fglrx-atieventsd fglrx-modules-dkms
还有Kernel Header package和官方驱动[AMD 催化剂13.1 Linux x86 专利 显示驱动](http://www2.ati.com/drivers/legacy/amd-driver-installer-catalyst-13.1-legacy-linux-x86.x86_64.zip) ,
注意也许要手动添加headers的链接，比如这个：/lib/modules/3.2.0-4-amd64/build/include/linux/version.h
最后也许那些驱动装不了
还是看看内核编译的信息
	＃ cat /proc/version 
准备定制驱动和配置自己内核吧，呵呵。

对于网卡驱动，[kernel 2.6.x Linux Driver Install Package for Yukon Devices](http://www.marvell.com/support/downloads/driverDownload.do?driverId=153&action=1), 同样是问题多多。sk98lin driver也太古老了。

* [ubuntuforums](http://ubuntuforums.org/) 
* [launchpad](https://launchpad.net)
* [linuxquestions](http://www.linuxquestions.org/)
* [bugs.debian](http://bugs.debian.org/)
* [unix.stackexchange](http://unix.stackexchange.com/)
* [oldsite.debianhelp](http://oldsite.debianhelp.org/)
* [linuxsir](http://www.linuxsir.org/)

瞎折腾不是个好的学习方式，但就是折腾折腾世界就不一样了，为能折腾的同学干杯！说多了都是泪-_-^+，有木有!


