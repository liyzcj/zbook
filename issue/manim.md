# Manim

The animation engin from 3b1b.

## ISSUE 1

默认预览功能下无法默认播放．
查看源码，manim是调用xdg-open来打开生成的视频文件．　由于默认的播放器是dragon, 不知道为什么dragon无法播放，　遂删除dragon. 默认播放器变成mpv, 解决．

## ISSUE 2
生成动画以后提示没有`play`命令．

查看源码，`play`命令是用来播放音频的，属于`sox`， 成功生成或失败生成的音频。
```shell
yay -S sox
```
安装sox解决。

## ISSUE 3
无法生成带有文字的动画， 由于没有安装`latex`:

```shell
yay -S texlive-most
```
安装`texlive-core` 和**经常使用的包**，开始只安装了`texlive-core`, 导致老是报错缺少`sty`文件。