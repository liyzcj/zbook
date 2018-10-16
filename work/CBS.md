# CBS APPLICATION



## etrace

```shell
etrace -add 20 -s diameteradapter -t 620 -f -c CallingNumber=1620490637	
```


## gdr

```shell
drcli -c drstate -l -g  ## list nodes
drcli -c drstate -r -g  ## reset State
```

```shell
nodecli      ## 节点交互
lsn          ##  列出节点信息
```



## HACS

### 添加浮动ip资源

1. 添加浮动ip资源

   ```shell
   crm configure primitive billing_dfloatip_ip ocf:users:hwIPaddr \
   	params ip="10.19.112.138" cidr_netmask="255.255.255.0" broadcast="10.19.112.255" ping_timeout="1" ping_pktcount="2" OnStopFail="ignore" \
   	meta migration-threshold="0" failover-max-count="3" \
   	op start interval="0" timeout="30" \
   	op stop interval="0" timeout="20" \
   	op monitor interval="5" timeout="60"
   ```

2. 添加资源组

   ```shell
   crm configure group billing_dr_grp billing_dfloatip_ip \
   	meta target-role="Started"
   ```

3. 创建共存关系

   ```shell
   crm configure colocation billing_dfloatip_col inf: billing_dr_grp:Started billing_db_grp:Started
   ```


## I2000

### I2000 网页端口号

```shell
端口号可以通过“$I2000_HOME/I2000/run/etc/oms.xml”的“httpsPort”字段查询到。
```

### 浏览器配置

> 如果浏览器无法显示该页面，请在浏览器中选择“工具 > Internet 选项”，选择“高级”页签，在“设置”区域框中勾选“安全”节点下的“使用 TLS 1.1”和“使用 TLS 1.2”。



### i2kadm

检查所有进程状态

```shell
i2kadm status [all|dmu...]
```

停止进程

```shell
i2kadm stop [all|dmu...]
```

启动进程

```shell
i2kadm start [all|dmu...]
```



## ideploy

### 安装时权限回收问题

执行安装任务完毕时会回收权限，所以不要在对一个节点执行安装任务的时候再执行另一个任务。

解决办法： 

修改文件夹权限，以下所有文件夹权限需为 755

> /home 
>
> /home/deploy 
>
> /home/deploy/breeze
>
> /home/deploy/breeze/ideploy



## uniangent


```shell
cp $UNIAGENT_HOME/data/uniagent/uniagent.data $UNIAGENT_HOME/data/uniagent/uniagent.data.bak0606

vim $UNIAGENT_HOME/data/uniagent/uniagent.data

su - uniagent

$UNIAGENT_HOME/bin/wrapper.sh restart
```



## GMDB

### 导出表结构

```shell
gmdcp -c MDB_USR_701/Huawei_123@ipc -e -s MDB_USR_701 -d -feedback 1
```

## Agilit 平台


### 发布配置信息

```shell
cfgadmin
rls -all
yes
```



### 启动和停止应用

```shell
start_onip.sh           # 生产端主机正常启动
start_onip.sh -s        # 生产端备机启动
start_onip.sh -d -a     # A-S 容灾端启动
```

停止：

```shell
stop_onip.sh -f         # 强制停止
```


