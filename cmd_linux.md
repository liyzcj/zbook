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
echo 'eval "$(rbenv init -)"' >> ~/.bashrc # zsh
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
