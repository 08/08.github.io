---
layout: post
title: Auto Layout何时如何使用
author: Ethan
published: true
---

Auto Layout是一个以数学形式描述应用的用户界面元素布局的系统。它定义了如何限定独立元素或多个元素的构成体。使用Auto Layout可以创造出能对屏幕尺寸、设备方位和语言本地化的变化作出合理响应的多功能动态界面。

Auto Layout内置于Xcode 5的Interface Builder之中， 对iOS和OS X上的app都适用。使用Xcode 5创建新项目时默认使用Auto Layout。对于要迁移到Auto Layout上项目请参考[Adopting Auto Layout](https://developer.apple.com/library/ios/documentation/UserExperience/Conceptual/AutolayoutPG/AdoptingAutoLayout/AdoptingAutoLayout.html)

使用Interface Builder创建用户界面的一般流程：建立UI、调整位置、调整尺寸、定制视图和控制器。当你对位置和设置满意时，可以准备添加Auto Layout约束了，以便你建立的界面可以响应设备方位，屏幕尺寸和语言本地化的变化。

- 添加约束
- 添加控制器拖动和菜单选项约束
- 约束和帧各自独立更新

