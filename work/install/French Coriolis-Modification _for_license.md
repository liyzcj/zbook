# Modification for License



## The modification below must be performed on every bmp node

1. Use **bmpapp** user login bmp node.
2. Use command below edit the file “**cbs.license.net.xml**”

```shell
vi $HOME/config/release/lic/cbs.license.net.xml
```

3.       Find the parameter below and modify the parameter **servAddr** to `10002@10.100.3.96`

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

**After modified the file, use command below restart the bmpapp**

```shell
stop_bmp.sh;start_bmp.sh
```



## Modification On CBS web

1. Use **101** user login CBS web <https://10.100.3.109:28081>
2. Choose `Billing Configuration` > `System-Level Configuration` > `System Configuration Item Instance`
3. click button `create`. Type the information below.

> `Service Module`: choose **BM**
> `Submodule`: **cm_gramework**
> `Parameter Category`: **licenseconfigitem**
> `Parameter Name`: **isexectaks**
> `Parameter Value`: **True**

4. click `save`

