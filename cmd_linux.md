# Linux Command

Some commands used frequently in Linux.

## Linux

### 查看占用大小并排序

```shell
du -sm * | sort -rn ## 正序
du -sm * | sort -n  ## 倒序
```

### 关机和重启

关机

```shell
halt ## 马上关机
poweroff ## 马上关机
shutdown -h now ## 马上关机
shutdown -h 10 ## 十分钟后关机
shutdown -c ## 取消shutdown计划
```

重启

```shell
reboot
shutdown -r now ## 马上重启
shutdown -r 10 ## 过十分钟重启
shutdown -r 21:52 ## 在特定时间重启
```

### Default Editor

```shell
update-alternatives --config editor
```

### ACL Permission
[setfacl命令](http://man.linuxde.net/setfacl)

### verification

- md5sum
- sha256sum

## apt

| command          | function                                |
| ---------------- | --------------------------------------- |
| apt install      | Install a package                       |
| apt remove       | Remove a package                        |
| apt purge        | Remove package with configuration       |
| apt update       | Refreshes repository index              |
| apt upgrade      | Upgrade all upgradable packages         |
| apt autoremove   | Removes unwanted packages               |
| apt full-upgrade | Upgrade with auto-handling dependencies |
| apt search       | Search package                          |
| apt show         | show package details                    |

------------------------
| new command      | function           |
| ---------------- | :----------------- |
| apt list         | List packages      |
| apt edit-sources | Edits sources list |


## git

```shell
# list configuration
git config --list
git config --global user.name "alex"
git config --global user.email liyz0912@gmail.com
# difference tool
git config --global merge.tool vimdiff
# store username and password
git config --global credential.helper store
```

## ruby

### rbenv

#### Install

1. Clone rbenv into _~/.rbenv_.
```shell
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
# Optionally, try to compile dynamic bash extension to speed up rbenv.
cd ~/.rbenv && src/configure && make -C src
```

2. Add _~/.rbenv/bin_ to your $PATH
```shell
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc # bash
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.zshrc # zsh
```
3. Set up rbenv in your shell.

```shell
~/.rbenv/bin/rbenv init
```

4. Load rbenv automatically 

```shell
echo 'eval "$(rbenv init -)"' >> ~/.bashrc # bash
echo 'eval "$(rbenv init -)"' >> ~/.zashrc # zsh
```

#### rbenv-doctor

```shell
curl -fsSL https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-doctor | bash
```

#### ruby-build

Clone ruby-build to _~/.rbenv/plugins/ruby-build_

```shell
git clone git://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
```

#### use

| Command              | Function                       |
| -------------------- | ------------------------------ |
| rbenv install --list | List available version of ruby |
| rbenv versions       | List installed versions        |
| rbenv install 2.5.1  | Install a ruby                 |
| rbenv global 2.5.1   | Set global version             |
| rbenv local 2.5.1    | Set local version              |
| rbenv shell 2.5.1    | Set shell version              |

## conda

| Command                  | Function     |
| ------------------------ | ------------ |
| conda install python=x.x | 切换默认环境 |


## 用户管理

### 添加用户

```shell
adduser 
```

## 网络管理

```shell
hostname			## 查看主机名
ifconfig			## 查看网卡信息
ping				## 测试网络
route				## 查看路由表
netstat -ano		## 查看网络，路由和接口
netconfig			## 设置IP、子网掩码、网关、主DNS
```

### 网络重启，打开关闭

重启：

```shell
service network restart
rcnetwork restart
/etc/rc.d/network restart
```

打开关闭：

```shell
 service network start
 service network stop
 service network restart
```

### 网络配置文件

```shell
/etc/hosts		## 主机名对应信息
/etc/sysconfig/network ## 网络配置， 网卡路由等。
```

### 加路由

```cmd
route add 10.132.51.0 mask 255.255.255.0  10.1.228.243
```

### 添加浮动ip

```shell
# 添加
ifconfig eth0:0 10.19.244.148 netmask 255.255.255.0 up
# 删除
ifconfig eth0:0 down
```

## NFS 服务

### 配置服务端

修改 `/etc/exports`文件:

```shell
/home/  10.0.2.0/24(rw,sync,all_squash,anonuid=501,anongid=501)
```

> 共分为三部分，第一部分就是**本地要共享出去的目录**，第二部分为**允许访问的主机**（可以是一个IP也可以是一个IP段）第三部分就是小括号里面的，为一些**权限选项**。 
>
> 第三部分：
>
> `rw` ：读写； 
>
> `ro` ：只读； 
>
> `sync` ：同步模式，内存中数据时时写入磁盘；
>
> `async` ：不同步，把内存中数据定期写入磁盘中；
>
> `no_root_squash` ：加上这个选项后，root用户就会对共享的目录拥有至高的权限控制，就像是对本机的目录操作一样。不安全，不建议使用；
>
> `root_squash` ：和上面的选项对应，root用户对共享目录的权限不高，只有普通用户的权限，即限制了root；
>
> `all_squash` ：不管使用NFS的用户是谁，他的身份都会被限定成为一个指定的普通用户身份；
>
> `anonuid/anongid` ：要和root_squash 以及 all_squash一同使用，用于指定使用NFS的用户限定后的uid和gid，前提是本机的/etc/passwd中存在这个uid和gid。

### 使用NFS

开启：

```shell
service portmap start; service nfs start
## suse11
service nfsserver restart
```

客户端检测远程`nfs`服务：

```shell
showmount -e remote_ip_address
```

客户端挂载`nfs`:

```shell
mount -t nfs 10.0.2.69:/home /mnt
mount -t nfs -o nolock 10.0.2.69:/tmp /mnt/
```
> nolock 选项即在挂载nfs服务时，不加锁。
> 还可以把要挂载的nfs目录写到client上的/etc/fstab文件中，挂载时只需要mount -a即可。

```shell
cat /etc/fstab
10.0.2.69:/tmp          /mnt                 nfs     nolock          0 0
##　自动挂载
mount -a
```
服务端查看所有连接的`nfs`客户端：

```shell
showmount -a
## 查看版本等信息
nfsstat -m
```

### 不重启挂载

使用`exportfs`命令不需要重启nfs服务：

> NFS服务中还有一个常用的命令那就是exportfs，它的常用选项为[-aruv]。
>
> -a ：全部挂载或者卸载；
>
> -r ：重新挂载；
>
> -u ：卸载某一个目录；
>
> -v ：显示共享的目录；

```shell
exportfs -arv ## 修改exports文件后无需重启服务。
```

## 挂载

```shell
# 自动挂载
vim /etc/fstab
# 查看磁盘信息
fdisk -l 

# 查看挂载信息
df -h
# 开机脚本
vim /etc/init.d/boot.loacal
```
## LVM

### 创建lv

```shell
lvcreate -L 32m -n lv_i2k_flex vg_i2k
```

### 修改lv名字

```shell
lvrename 旧逻辑卷名 新逻辑卷名
lvrename /dev/vg_pro1/lv_fileserver2 /dev/vg_pro1/lv_fileserver1
```

