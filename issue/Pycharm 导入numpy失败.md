# Pycharm 导入numpy失败



使用conda新建了一个非系统默认环境， 并安装了numpy。

然后再pycharm使用该环境的解释器，运行代码结果显示导入numpy失败。

> 日志：
>
> Traceback (most recent call last):
>
>   File "C:\Users\liyz0\Miniconda3\envs\ann\lib\site-packages\numpy\core\__init__.py", line 16, in <module>
>
> ​    from . import multiarray
>
> ImportError: DLL load failed: 找不到指定的模块。
>
>  
>
> During handling of the above exception, another exception occurred:
>
>
>
> Traceback (most recent call last):
>
>   File "C:/Users/liyz0/Desktop/sos/lab2/test.py", line 1, in <module>
>
> ​    import numpy as np
>
>   File "C:\Users\liyz0\Miniconda3\envs\ann\lib\site-packages\numpy\__init__.py", line 142, in <module>
>
> ​    from . import add_newdocs
>
>   File "C:\Users\liyz0\Miniconda3\envs\ann\lib\site-packages\numpy\add_newdocs.py", line 13, in <module>
>
> ​    from numpy.lib import add_newdoc
>
>   File "C:\Users\liyz0\Miniconda3\envs\ann\lib\site-packages\numpy\lib\__init__.py", line 8, in <module>
>
> ​    from .type_check import *
>
>   File "C:\Users\liyz0\Miniconda3\envs\ann\lib\site-packages\numpy\lib\type_check.py", line 11, in <module>
>
> ​    import numpy.core.numeric as _nx
>
>   File "C:\Users\liyz0\Miniconda3\envs\ann\lib\site-packages\numpy\core\__init__.py", line 26, in <module>
>
> ​    raise ImportError(msg)
>
> ImportError: 
>
> Importing the multiarray numpy extension module failed.  Most
>
> likely you are trying to import a failed build of numpy.
>
> If you're working with a numpy git repo, try `git clean -xdf` (removes all
>
> files not under version control).  Otherwise reinstall numpy.
>
>  
>
> Original error was: DLL load failed: 找不到指定的模块。



在pycharm的python console 里导入numpy仍然失败，原因相同。



在pycharm外，使用vscode 还是直接使用python编译都可以编译成功。

最后将环境下的`library/bin`目录加入系统环境变量才能成功运行。至今不知道为什么。