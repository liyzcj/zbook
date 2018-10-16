# CBS5.5 Debug日志分析

## BMP 日志

### debug 日志  

业务功能调测时常用的BMP的debug日志为“${HOME}/log/debug/bmp_debug.log”。另外，BMP启动或GUI界面抛出的一些异常可以通过查看“${HOME}/tomcat/logs/catalina.out”和“${HOME}/tomcat/logs/localhost.log  日志进行定位。

> BMP网元的debug日志获取办法如下：
>
> 1- 到指定log路径下 cd $HOME/log/debug
>
> 2- 删掉原有日志 rm bmp_debug.log.* 
>
> 3- 置空日志 echo " "> bmp_debug.log 
>
> **注意：bmp_debug.log文件的清理，请使用echo命令清空，不要使用rm操作。**
>
> **删除bmp_debug.log文件再重新创建，会导致bmp日志无法写入到文件中或写入日志内容不全。**
>
> **如果出现误删操作，在重启bmp后才能正常写入。**
>
> 4- 打开debug日志开关（以下命令操作后，输入y） logadm_bmp -on; 
>
> 5- 业务操作 
>
> 6- 根据关键信息(比如接口名或号码或账户)搜索日志，grep -li "XXXXX" bmp_debug.log*
>
> 7-关闭debug日志开关 logadm_bmp -off; 
>
> 8- 第6步搜索到的日志按“接口名_局点_问题描述_问题提交人工号_时间”命名发给问题定位人 

[BMP日志汇总](http://3ms.huawei.com/hi/group/2904915/wiki_4396997.html#1)

## CBP 日志

1. 进入日志目录

   ```shell
   su - cbpapp
   cd log/debug
   ```

   

2. 删除存在日志

   ```shell
   rm -rf *.dlog
   ```

3. 打开日志开关

   打开CBP上的debug日志命令： 

   ```shell
   logadm debug -p <pid> on -t <delay> 
   ## 该命令表示打开特定进程的debug日志，pid表示进程号，delay表示打开debug日志的时长。
   ```

   ```shell
   logadm debug -all on -t <delay> 
   ## 该命令表示打开所有进程的debug日志，delay表示打开debug日志的时长。
   ```

   常用命令：

   ```shell
   logadm debug -all on -t 3600
   ```

4. 业务操作

5. 关闭日志开关

   关闭CBP上的debug日志命令：

   ```shell
   logadm debug -p <pid> off 
   ## 该命令表示关闭特定进程的debug日志。
   ```

   ````shell
   logadm debug -all off 
   ## 该命令表示关闭所有进程的debug日志。
   ````

6. 日志分析流程

   在定位CBP上的问题时，可能会涉及多个日志。本节将介绍各日志分析的先后顺序。

   CBP的debug日志全部存放在“${BILLING_HOME}/log/debug”目录中，该目录下的debug日志命名规则为：`<Process Name>_<Identifier ID>.dlog`

   >  例如：OnlineRating_1900.dlog。

   业务功能调测时常用的CBP debug日志为：

   > - `GeneralMng_1100.dlog`：记录用户开户激活等业务的处理过程。 
   > - `OfflineRating_1800.dlog`：记录离线计费等业务的处理过程。 
   > - `OnlineRating_1900.dlog`：记录在线语音、短信计费等业务的处理过程。

   

