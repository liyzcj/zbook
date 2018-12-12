# Windows Command

some commands in windows Cmd or Powershell



## cmd

| command   | function                    |
| --------- | --------------------------- |
| `findstr` | Like grep in Linux          |
| `set`     | About environment variables |
| `where`   | Like which in Linux         |

### 网络

ipconfig dns:

```powershell
ipconfig /displaydns  显示dns缓存 
ipconfig /flushdns    刷新DNS记录 
ipconfig /renew       重请从DHCP服务器获得IP 
```





### WSL

```shell
debian config --default-user root
```

```powershell
wslconfig /l
```



## Powershell

### verification

```powershell
Get-FileHash _filename_ -Algorithm MD5
Get-FileHash _filename_ -Algorithm SHA256
```

```powershell
# 打开 Hyper-V -- powershell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
```

