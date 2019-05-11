Numpy
==========================

.. contents::
  :local:
  :backlinks: top

矩阵操作
---------

Padding 操作::

  numpy.pad(arr, shape, mode, value)

shape 代表 pad 的形状:

- shape 为标量则代表所有维度的前后,
- shape 为一维(a,b)则分别代表所有维度的 前和 后.
- shape 与arr 维度数相同, 则代表每个维度的前后.

详见 `numpy.pad`_

.. _numpy.pad: https://docs.scipy.org/doc/numpy/reference/generated/numpy.pad.html?highlight=pad#numpy.pad


拆分操作::

  numpy.split(ary, indices_or_sections, axis=0)

将数组拆分成多个数组, 根据提供的索引.

详见 `numpy.split`_

.. _numpy.split: https://docs.scipy.org/doc/numpy/reference/generated/numpy.split.html?highlight=split#numpy-split

Utils
--------------------------

矩阵属性
''''''''''''''''''''''''''

``numpy.ndarray`` 的属性:

:ndim:      维度个数
:shape:     数组形状
:size:      元素个数
:dtype:     元素类型

.. code:: python
  
  assert arr.ndim == 2
  arr.shape
  arr.size
  arr.dtype