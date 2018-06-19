# Linux Command

Some commands used frequently in Linux.



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

## verification

- md5sum
- sha256sum

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

## ACL Permission
[setfacl命令](http://man.linuxde.net/setfacl)


## Default Editor

```shell
update-alternatives --config editor
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
