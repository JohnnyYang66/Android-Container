## 安装

终于弄好了，这个坑也特别多，总结一下

①正常步骤，按照官网

[remote-android/redroid-doc: redroid (Remote-Android) is a multi-arch, GPU enabled, Android in Cloud solution. Track issues / docs here (github.com)](https://github.com/remote-android/redroid-doc)

```Bash
apt install linux-modules-extra-`uname -r`
modprobe binder_linux devices="binder,hwbinder,vndbinder"
modprobe ashmem_linux
```

②注意要安装下面这个版本，11.0.0的版本会报binder的错，我弄了一周多都没解决，12.0.0的版本会报奇怪的错，并且似乎具有破坏性，最后发现还是需要下面这个版本

```Bash
docker run -itd --rm --privileged \
    --pull always \
    -v ~/data12_64only:/data \
    -p 5555:5555 \
    --name redroid12_64only \
    redroid/redroid:12.0.0_64only-latest \
```

③安装adb和scrcpy。注意scrcpy要从snap里面装，不然版本不够新

```Bash
apt install adb
snap install scrcpy
```

④报了个No protocol specified的错，不过很好解决

[(60条消息) 报错No protocol specified解决办法_Anne332的博客-CSDN博客](https://blog.csdn.net/Anne332/article/details/118903921)

```Bash
# 新开一个窗口
xhost +
echo $DISPLAY
# 我的数字是0，是什么数字就填什么
export DISPLAY=:0 
```

⑤开启

```Bash
adb connect localhost:5555
/snap/bin/scrcpy -s localhost:5555
```

总结一下，之前一直在11.0.0版本（官方推荐）死磕，n多方法都解决不了问题。有人说换成12，但是还得是这个redroid12_64only才行。下次遇到问题得清醒一下，不能死磕。休息两天再换个思路