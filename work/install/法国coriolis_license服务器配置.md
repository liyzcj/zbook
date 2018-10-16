# 法国coriolis_license管理工具

## 获取license管理工具

`license管理工具`随版本包发布，在版本包内找到相应版本的license管理工具安装文件。

- `windows`： “AdaptiveLMV\*_ZIP_INS_WIN32_\*.zip”或“adaptivelm-win32_\*\*\*-release.zip”
- `Linux`： “AdaptiveLMV\*\_ZIP\_INS\_SUSE10\_X8664\_\*.tar.gz”

本次使用的是Windows版本的管理工具。

## 安装license管理工具

直接将`AdaptiveLMV100R003C06SPC013_ZIP_INS_WIN32_X8632_20150617.zip`解压到安装路径。运行文件夹内的`start.bat`即可。

**注意**：需要32位的`jdk`，否则在登录license服务器时会闪退。

## 检查服务器是否正常

使用`license`账户登录后台。运行一下命令查看进程：

```shell
ps -u license |grep -v pts
PID TTY          TIME CMD
23764 ?        00:00:03 proxy
23957 ?        00:00:00 logalarm
```

运行一下命令查看日志：

```shell
cd $LIC_HOME/log/
vim proxy.log
vim logalarm.log
```

如果没有错误，则license服务器正常。

## 连接 License 服务器

1. 右键`License server`点击`Add server`。

`Server name`随意填写license服务器名称。例如`license_server`。

`IP&Port`填写IP地址和端口号。

>  IP 地址和端口号可以在日志 `proxy.log`里查看。也可以在`conf/config.ini`文件内查看。

确定连接。

2. 连接成功后，右键`Login Server`，登录license 服务器。

> **默认账户名**： Administrator

> **默认密码**：hw124426

## 获取公钥文件

<http://w3.huawei.com/dominoapp/isc/license/libvcg.nsf/fmlibvcg?OpenForm>

点击链接申请产品公钥。填入以下信息。

> Operation Type：LIB Recovery
>
> Product Line： 软件公司Software Company
>
> Product Name：CBS
>
> Product Version：V500R005
>
> Application Model：Client-Server
>
> LIB Version：1.2
>
> LIB&VCG Deliveries：server_suse10_so_x8664_suse10 
>
> **LIB&VCG Deliveries**选择符合服务器设备的公钥。

## 使用管理工具加载公钥文件



右键服务器`Add Product`增加产品。选择公钥文件-->`Advanced`，将`Work Mode`设置为Request License Mode。

>- 工作模式配置为“Configure License Mode”时，表示为License资源离线配置模式。
>在这种管理模式下，License由License server统一管理。通过License管理工具在License服务器上为各个设备分配指定的License。设备通过连接到服务器来查询已分配给自己的License，服务器返回为设备配置的License。License只能在服务器侧进行修改，License客户端不能主动向Server请求。各设备的License总和不能超出管理员指定的授权数。
>
>- 工作模式配置为“Request License Mode”时，表示为License资源共享竞争模式。
在这种管理模式下，License由License server统一管理。服务器提供一定数量的License，各个设备在需要License时向License服务器申请，不再使用时主动释放，以达到License在各客户端的设备间充分的共享。OCS License资源项的管理采用该种模式。

`OK`-->`YES`。

加载公钥文件后，选择右键`start Product`启动产品。

## 加载 License 文件

1. **上传**：右键产品，选择`Upload License File`，选择 License 文件。
2. **激活**：右键 License 文件，选择`Activate File`，然后选择`Yes`。

## 开启 License 功能


### 修改bmpapp 配置文件

1. 使用**bmpapp**用户登录bmp节点。
2. 使用以下命令编辑文件 “**cbs.license.net.xml**”。

```shell
vi $HOME/config/release/lic/cbs.license.net.xml
```

3. 找到下面的参数并修改 **servAddr** 为 `10002@10.100.3.96`（端口号@IP地址）

```xml
<product name="OCS">
    <!--basic configure item-->
    <basic>
        <!-- product version -->
        <productVer>V500R005</productVer>
        <!-- work mode, 1: request license mode; 2: configure license mode -->
        <workMode>1</workMode>
        <!-- esn, if this item is null, it will take node number as esn. -->
        <esn></esn>
        <!-- license server address("port@ipaddress" or "port1@ipaddress1;port2@ipaddress2", only support IPV4) -->
        <servAddr>10200@10.137.7.223</servAddr>
    </basic>
```

---

**修改完每个bmp节点的配置文件后，重启bmp**

```shell
stop_bmp.sh;start_bmp.sh
```



### CBM web修改

1. 使用**101**账户登录 CBS web <https://10.100.3.109:28081>
2. 选择 `Billing Configuration` > `System-Level Configuration` > `System Configuration Item Instance`
3. 点击 `create`. 输入以下信息 

> `Service Module`: choose **BM**  
> `Submodule`: **cm_gramework **   
> `Parameter Category`: **licenseconfigitem **   
> `Parameter Name`: **isexectaks**  
> `Parameter Value`: **True**  

4. 点击 `save`

