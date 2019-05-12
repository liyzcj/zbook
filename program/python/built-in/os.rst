os
========

.. code-block:: python

  import os

- 创建文件夹

::

  os.mkdir(path, mode=0777)

如果需要创建的文件夹的父文件夹不存在, 则需要递归创建::

  os.makedirs(path, mode=0777)

- 连接目录

::

  os.path.join(path, *args)

- 判断文件或目录是否存在

::

  os.path.exists(path)

- 调用系统指令

::

  os.system(command) # 不返回信息
  result = os.popen(command) # 返回输出信息
  print(result.read())
  