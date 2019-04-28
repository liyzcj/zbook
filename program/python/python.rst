Python
==========================

.. contents::
    :local:
    :backlinks: top

Utils
--------------------------

pickle
''''''''''''''''''''''''''
  
  **Python object serialization: Python对象序列化**

``pickle`` 模块用来方便的将对象保存为文件, 用于重复使用.

.. note:: ``Python2`` 中为 ``cPickle`` 模块, 在 ``Python3`` 中为 ``pickle`` 模块.

保存
""""""""""""""""""""""""""

保存对象::

  pickle.dump(obj, file, protocol=None, *, fix_imports=True)

.. sidebar:: 协议兼容

  当 ``protocol < 3`` 时, ``Python3`` 保存的 ``pkl`` 文件才能在 ``Python2`` 中载入.

:fix_imports: 是否与 ``Python2`` 名称兼容.
:protocol: 存储协议 ``[0, 4]`` 五种

在 ``Python2`` 中, 对象以字符保存, 可以使用 ``w`` 或着 ``wb``::
  
  with open(filename, 'wb') as f:
    cPickle.dump(obj, f)

或着::

  with open(filename, 'w') as f:
    cPickle.dump(obj, f)

在 ``Python3`` 中, 对象以二进制保存, 只能使用 ``wb`` 保存::

    with open(filename, 'wb') as f:
      cPickle.dump(obj, f, protocol=2)

载入
""""""""""""""""""""""""""

载入对象::

  pickle.load(file, *, fix_imports=True, encoding="ASCII", errors="strict")

:fix_imports: 是否与 ``Python2`` 名称兼容.
:encoding: ``Python2`` 的解码方式

在 ``Python2`` 中载入对象可以使用 ``rb`` 或着 ``r``::

  with open(filename, 'r') as f:
    obj = cPickle.load(f)

在 ``Python3`` 中载入对象只能使用 ``rb`` 无论是 ``Python2`` 还时 ``Python3`` 生成的 ``pkl``::

  with open(filename, 'rb') as f:
    obj = pickle.load(f)