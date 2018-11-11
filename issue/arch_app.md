
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

---

## 硬盘异响

安装`arch`以后， 硬盘偶尔会吱吱的响。 `google`查了以下， 有人说是硬盘省电模式的问题。

首先安装`hdparm`:

```shell
yay -S hdparm
```

执行命令检查硬盘参数：
```shell
> sudo hdparm -B /dev/sda

/dev/sda:
 APM_level      = 128
```
一般硬盘出厂的默认参数就是128。

> APM=1 --最小电源模式，工作时耗电量最低，硬盘的性能最低。  
> APM=[2...127] --次小电源模式，比上一等级的耗电量和性能都稍有提升。  
> APM=128 --平衡电源/性能模式，一般也是硬盘出厂时的默认电源模式。  
> APM=[129...253] --高性能模式，耗电量和磁盘性能进一步提升。  
> APM=254 --最高性能模式  
> APM=255 --APM电源管理关闭模式，在此模式下，硬盘性能等同与APM=254，但是不一定每一个硬盘都支持。

执行命令修改为 254 ：
```shell
sudo hdparm -B 254 /dev/sda
```

修改之后重启还是会恢复 128 ，可以使用`udev` 的规则设置默认值。

```
> cat /etc/udev/rules.d/69-hdparm.rules
ACTION=="add|change", KERNEL=="sd[a-z]", ATTR{queue/rotational}=="1", RUN+="/usr/bin/hdparm -B 254 -S 0 /dev/%k"
```
---