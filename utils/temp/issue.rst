TEMP issues
============================

1. Cmder 下使用 virtualenv

在Cmder 的 Powershell 中使用virtualenv, 无法进入虚拟环境。 由于prompt被cmder设置为常量。

解决办法：

在cmder 的配置文件 ``profile.ps1`` 中加入::

    $env:VIRTUAL_ENV_DISABLE_PROMPT = 1