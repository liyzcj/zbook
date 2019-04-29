Python
==========================

.. contents::
  :local:
  :backlinks: top

文件操作
-------------------------

``Python`` 通过 ``open(filname, flag)`` 函数打开一个文件, 返回一个文件对象, 并通过对象对文件进行操作. 

:filename:  要打开的文件
:flag:      标志, 控制对文件的权限

标志包括 ``a, w, r, b, t, +, x``.

``a``: 添加; 打开文件, 并将指针置于文件末尾.

``w``: 写入; 打开文件, 并将指针置于文件开头. 不存则会创建文件.

``r``: 读取; 打开文件, 并将指针置于文件开头

``b``: 是否以二进制的方式读写.

``t``: 以 ``str`` 的方式读写, 默认.

``+``: 将权限提高为读写.

``x``: 创建文件, 如果文件存在则报错. 有写权限.

读取方法
''''''''''''''''''''''''''

从文件中读取:

file.read(size)
  如果 ``size`` 未指定, 返回读取整个文件. ``size`` **包含 ``\n``**.

file.readline()
  返回一行数据, **包含 ``\n``**.

file.readlines(size)
  返回在 ``size`` 内行的列表,  如果未指定, 返回包含全部行的列表, 每个元素 **包含 ``\n``**. ``size`` **不包含 ``\n``**.

.. attention:: 

  注意, ``size`` 指的是字符数.

此外还可以将文件对象当作迭代器读取::

  with open(filename, 'r') as f:
    for line in f:
      ...

写入方法
'''''''''''''''''''''''''''

往文件写入:

file.write(content)
  ``content`` 必须是字符串.

file.writelines(content)
  ``content`` 可以是字符串或着列表.

其他
''''''''''''''''''''''''''

除了写入和读取方法, 还有对指针的操作方法:

file.seek(offset, position=1)
  移动文件指针.

:offset: 偏移量; 单位为字符, 可正可负数.
:position: 相对位置; ``0`` - 文件开头; ``1`` - 当前位置; ``2`` - 文件结尾.

.. important:: 只有以二进制方式打开时, 才可以使用负偏移量.

file.tell()
  返回当前指针相对于文件头的位置, 即第几个字符. 例如从开头读取 ``6`` 个字符, 则返回 ``7``.

file.close()
  清空 ``buffer``, 关闭文件.

除了方法, 文件对象还有属性:

file.mode
  返回打开文件的标记.

Utils
--------------------------

Assertion
''''''''''''''''''''''''''

断言可以用来判断, 确保程序运行正确.

断言二维列表::

  assert isinstance(input_data[0], list)


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