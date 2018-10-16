# flowtest

Mediation上创建eventlinkuser用户
使用root用户执行如下命令创建eventlinkuser用户：

```shell
 groupadd sftpgroup
 mkdir -p /home/eventlinkuser
 useradd -d /home/eventlinkuser -s /usr/bin/csh -g sftpgroup -m eventlinkuser
 chown -R eventlinkuser:sftpgroup /home/eventlinkuser
 passwd eventlinkuser
```

备机创建相同groupid和userid的用户：
```shell
 groupadd -g 7832 sftpgroup
 mkdir -p /home/eventlinkuser
 useradd -u 7832 -d /home/eventlinkuser -s /usr/bin/csh -g sftpgroup -m eventlinkuser
 chown -R eventlinkuser:sftpgroup /home/eventlinkuser
 passwd eventlinkuser
 passwd eventlinkuser
```
