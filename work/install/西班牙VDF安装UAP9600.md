## 安装服务端

1. 上传安装包至I2000

   > 上传 UAP9600_NMU_V100R003C35.zip 到ideploy 的pkg目录
   >
   > **注意，SUSE11的操作系统 安装R3C35SPC008;    SUSE12的操作系统 安装R3C57 **

2. 创建任务

   创建安装任务，选择nmu节点。

3. 配置NMU

   填写ip地址等参数。

4. 执行安装任务

   安装任务报错：远程无响应。

   > 修改sshd配置文件：/etc/sshd_config
   >
   > **ListenAddress 0.0.0.0** ## 配置任何ip都可以连接。

5. 更新至R3C35SPC008

   >1. 上传UAP9600_V100R003C35SPC008.zip至NMU主节点。
   >
   >2. 解压
   >
   >   检查是否有热补丁`DSP PATCH`若存在，执行`RMV PATCH`，再执行`RMV PKG`删除补丁包
   >
   >3. root用户执行`./Install_bin.sh`升级 
   >
   >```shell
   >nmustatus ## 查看nmu状态
   >```
   >
   >

6. 安装客户端LMT

   解压客户端，并执行Install.bat 安装Windows客户端。

   **注意，如果使用管理员账户安装，则需要管理员账户启动才能正常使用。**

7. 配置PMU

   1. `ADD UNSVR`配置PMU信息。
   2. `ADD APP`增加PMU模块进程。