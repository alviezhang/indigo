---
layout: post
title: 修复LaunchPad空文件夹
description:
tags: Mac
blog: true
---

在终端执行

    defaults write com.apple.dock ResetLaunchPad -bool true; killall Dock

  

另外[Sorty][]这个App也能解决这个问题。

[参考链接][]

[Sorty]: http://wiles.dk/   "Sorty for OS X"
[参考链接]: http://forums.macrumors.com/showthread.php?t=1760552#2

