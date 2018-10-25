# SHELL PROGRAMMING

## 远程脚本

1. 建立信任关系

> - generate key with ssh-keygen
> - put the public key on remote
```shell
ssh-keygen
```
2. sftp命令  
General： sftp user@hostname "commad"  
sftp 有一个选项`-b`来处理批量命令
```shell
sftp -b command.file user@hostname
```
或者使用重定向输入命令。
```shell
sftp user@hostname << EOF
command 1
command 2
command 3
EOF
```

3. ssh命令  
General：ssh user@hostname "command"  
若有多个命令，与sftp相同可以使用重定向输入：
```shell
ssh user@hostname << EOF
command 1
command 2
command 3
EOF