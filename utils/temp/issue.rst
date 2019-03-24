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

3. windows python virtualenv 下 spyder 打不开

在 virtualenv 中使用 ``pip install spyder`` 后运行 ``spyder3.exe`` 没有反应.

在python 终端中运行如下代码::

    from spyder.app import start
    start.main()

报错, ModuleNotFoundError: No module named 'PyQt5.QtWebKitWidgets'

解决办法: 运行 ``pip install PyQtWebEngine`` 解决. 运行 ``spyder3.exe`` 正常.