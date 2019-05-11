Powershell
=============

Powershell 常用命令.

配置文件
---------

配置文件类似于 ``bash`` 的 ``.bashrc``, 在终端打开时首先运行.

Powershell 默认的配置文件路径保存在 `PROFILE` 变量中::

  λ  $PROFILE
  C:\Users\liyz0\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1

Utils
---------

.. sidebar:: 注意

   不要忘记 ``;``.

添加目录到环境变量 ``PATH`` 中::

  $Env:path=$Env:Path+";new_path"

.. tip:: 
  
  如果想要添加的环境变量永久生效, 可以将语句写到 $PROFILE 配置文件中.增加路径到 ``PATH`` 变量中::
