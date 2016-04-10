---
layout: post
title: 在AUR中创建软件包
tags:
  - Arch Linux
  - AUR
blog: true
---

身为Arch Linux/AUR用户好几年了，还未向社区贡献过什么东西。今天刚好用到的一个代理软件[Meow][]没在AUR中找到，就照着[Wiki][]创建了包[meow-proxy][]，下面是大致的步骤。

- 克隆git仓库

~~~ shell
git clone git+ssh://aur@aur.archlinux.org/meow-proxy.git
~~~

- 编辑PKGBUILD文件

写PKGBUILD时，首先参考了在Github上的已有的项目<https://github.com/aur-archive/meow-proxy>，这个包版本已经很老了，也无法在AUR中找到，于是根据最新的meow重新写了下source和sha1sum，后来发现生成的包只有当前Arch的包，于是参考了<https://aur.archlinux.org/packages/cow-proxy/>的PKGBUILD重新写了一下。

- 打包测试

使用makepkg在本地打包

~~~ shell
makepkg
~~~

- 生成.SRCINFO文件

~~~ shell
makepkg --printsrcinfo > .SRCINFO
~~~

- 提交git代码

将PKGBUILD、.SRCINFO和在PKGBUILD包含的本地source添加到git中，然后push代码。

运行`yaourt meow-proxy`，检查无误。

[Meow]: https://github.com/renzhn/MEOW "Meow proxy"

[Wiki]: https://wiki.archlinux.org/index.php/Arch_User_Repository#Creating_a_new_package

[meow-proxy]: https://aur.archlinux.org/packages/meow-proxy/


