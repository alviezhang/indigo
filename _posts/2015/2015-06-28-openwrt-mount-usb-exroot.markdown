---
layout: post
title: "OpenWrt挂载USB存储设置exroot"
date: 2015-06-28
description:
tags: OpenWrt
blog: true
---

#### 设备信息

`TP-Link WR-720N Version: 4.0`

`OpenWrt Barrier Breaker 14.07 / LuCI Trunk (0.12+svn-r10530)`

#### 步骤

- 安装所需要的软件包

~~~sh
opkg update
opkg install block-mount kmod-usb-storage kmod-fs-ext4
reboot
~~~

- 挂载USB分区（假设对应分区为`/dev/sda1`）

~~~sh
mkdir /mnt/usb
mount -t ext4 /dev/sda1 /mnt/usb
~~~

- 编辑`fstab`

~~~
config 'global'
option  anon_swap   '0'
option  anon_mount  '0'
option  auto_swap   '1'
option  auto_mount  '1'
option  delay_root  '5'
option  check_fs    '0'

config 'mount'
option  target  '/'
option  device  /dev/sda1
option  enabled '1'
option  fstype  ext4
option  options rw,sync
option  enabled_fsck    0
~~~

- 拷贝root文件到USB文件系统中

~~~sh
mkdir /tmp/cproot
mount --bind / /tmp/cproot
tar -C /tmp/cproot -cvf - . | tar -C /mnt/usb -xvf -
sync ; umount /mnt/usb
umount /tmp/cproot
~~~

- `reboot`，搞定

----------

上面只记录了操作过程，想了解更多请参考官方文档[Rootfs on External Storage (extroot)](http://wiki.openwrt.org/doc/howto/extroot)
