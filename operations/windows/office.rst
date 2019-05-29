Office 自定义部署
==========


使用自动部署工具自定义部署 ``office`` 工具.

1. 制作配置文件

使用`在线工具`_, 制作配置文件并导出.


2. 下载部署工具

下载`部署工具`_并解压.

3. 下载安装文件

打开 CMD 或 Powershell 并切换到工具与配置文件目录.

下载安装文件::

    PS G:\packages\office> .\setup.exe /download .\Configuration.xml

4. 部署 Office

下载完成后, 运行命令部署 Office 软件::

    PS G:\packages\office> .\setup.exe /configure .\Configuration.xml


.. _在线工具: https://config.office.com/
.. _部署工具: https://www.microsoft.com/en-us/download/details.aspx?id=49117
