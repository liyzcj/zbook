PANDAS
==========================

DataFrame 操作
---------------------------

数据替换
'''''''''''''''''''''''''''

1. 对整个|df|的值进行替换, ``inplace`` 代表是否改变源数据::

    df.replace(to_replace, value, inplace = True)

2. 对某一列的值进行替换::

    df["col"].replace(to_replace, value, inplace = True)

3. 多个值替换, 可以使用 **列表** 或者 **字典** 替换.

- 列表替换::

    df.replace(['a',1], ['b',2], inplace = True)

- 字典替换::

    df.replace({'a':'b', 1:2}, inplace = True)

.. tip:: 使用列表时, 也可以将多个值替换为一个值.

4. 正则表达式替换, 使用正则表达式也可以同时替换多个值::

    df.replace('[a-z]', 'aphabet', regex = True)

5. 部分替换, 有时候不想全部替换, 例如将 ``go up`` 中的 ``up`` 替换为 ``down`` ::

    df['col'] = df['col'].str.replace('up', 'down')

.. note::

    部分替换没有 ``inplace`` 参数, 所以想要替换源数据需要赋值操作.
    **注意赋值时选择为某一列赋值**


