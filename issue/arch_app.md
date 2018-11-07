
# ISSUE for Arch linux Applications

## xmind

**Description**: 从AUR安装的xmind无法打开。 //java terminate code 1

**Detail**:
1. 直接使用yay安装xmind， 自动安装openjdk 依赖。无法打开， 提示错误 ”java terminate code 1“。

```shell
yay -S xmind
```

2. 删除xmind，并手动安装jdk， 再重新安装xmind。  （当前版本jdk为jdk11）

```shell
yay -S jdk
yay -S xmind
```
3. 在命令行内运行xmind， 报错找不到module “java se.ee"

编辑 `/usr/share/xmind/XMind/XMind.ini`，去掉最后一行`--add-modules=java.se.ee`， 报不知名错误， 让查看日志。

4. 查看java文档，发现java11 取消了java.se.ee模块。 卸载 `java11`, 安装`java8`。（由于xmind依赖，无法先删除java11,故先安装java8, 然后再删除java11。

```shell
yay -S jdk8
yay -Rsn java11
```

5. 命令行启动xmind，报错无法识别`java.se.ee`。 执行 第三部的删除模块。 成功打开