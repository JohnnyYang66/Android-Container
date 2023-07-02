## 测试环境

ubuntu-20.04.6-desktop-amd64



## 安装

终于弄好了，坑太多了，总结一下

①先进行正常步骤

```Bash
sudo apt install waydroid
```

然后参考这篇文章https://github.com/waydroid/waydroid/issues/215

到官网

[Index of /project/waydroid/images (sourceforge.net)](https://jaist.dl.sourceforge.net/project/waydroid/images/)

下载镜像，解压放在这里(system那个我下载的vanilla）

```Bash
/usr/share/waydroid-extra/images$ ls -l |grep img
-rw-r--r-- 1 eton eton 1738235904 Oct 21 17:01 system.img
-rw-r--r-- 1 eton eton  324395008 Oct 22 00:46 vendor.img
```

现在可以开始

```Bash
sudo waydroid init -f
```

②先安装pip，然后参考这篇文章，安装这个

[Failed to start Clipboard manager service, check logs · Issue #276 · waydroid/waydroid (github.com)](https://github.com/waydroid/waydroid/issues/276)

```Bash
pip install pyclip
```

③参考这篇文章，这么做（否则ui打不开），我自己是用虚拟机的

[Get Waydroid to work through a VM - Waydroid](https://docs.waydro.id/faq/get-waydroid-to-work-through-a-vm)

vim一下 /var/lib/waydroid/waydroid.cfg

```Bash
# 在properties下面添加
ro.hardware.gralloc=default
ro.hardware.egl=swiftshader
```

然后

```Bash
sudo waydroid upgrade -o
```

下面这一点应该可以略过

（其实我还做了这一步，参考了这篇文章，之前不能打开界面，改完之后能打开了但是黑屏，后面我也没改回去）

https://github.com/waydroid/waydroid/issues/61

```Bash
# https://github.com/waydroid/waydroid/issues/61

# Editing /var/lib/waydroid/waydroid_base.prop fixed this problem for my RX 6600 XT. However, hardware acceleration would be disabled. Not so usable.

ro.hardware.gralloc=default
ro.hardware.egl=mesa
```

之后启动黑屏了，啥也没有

④注销，出去在选项里面把ubuntu换成wayland这个

参考了这篇文章：

[WAYLAND_DISPLAY is not set, defaulting to "wayland-0" · Issue #771 · waydroid/waydroid (github.com)](https://github.com/waydroid/waydroid/issues/771)

⑤正常步骤

看安装和用法这里

[Waydroid - Arch Linux 中文维基 (archlinuxcn.org)](https://wiki.archlinuxcn.org/wiki/Waydroid)

```Bash
waydroid session start
```

另一个窗口：

```Bash
waydroid show-full-ui
```

可以进入shell安装东西

```Bash
waydroid shell
waydroid app install $path_to_apk
waydroid app launch $package-name #Can be retrieved with `waydroid app list`
```

唉，真是够麻烦的