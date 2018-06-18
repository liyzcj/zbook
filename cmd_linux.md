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

- #### md5sum
- #### sha256sum

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

