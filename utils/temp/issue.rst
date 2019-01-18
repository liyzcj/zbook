TEMP issues
============================

1. Cmder 下使用 virtualenv

在Cmder 的 Powershell 中使用virtualenv, 无法进入虚拟环境。 由于prompt被cmder设置为常量。

解决办法：

在cmder 的配置文件 ``profile.ps1`` 中加入::

    $env:VIRTUAL_ENV_DISABLE_PROMPT = 1

2. Read the Docs 不显示公式.

不知道为什么, 本地能够编译出来公式, read the docs 托管的却不显示公式. sphinx 官方文档表示已经内置 mathjax, 
不需要再 Extension 里添加 mathjax.
 
原因可能是 read the docs 上的sphinx 版本较低?

解决办法: 在sphinx 配置文件里添加 'sphinx.ext.mathjax',