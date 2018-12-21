reStructuredText
=====================

reStructuredText 以行为间隔, 每隔一行为一个段落。

行内标记
---------------------

+----------+--------------------------+-------------------------+------------------------------------------+
| **功能** | **代码**                 | **结果**                | 附加代码                                 |
+----------+--------------------------+-------------------------+------------------------------------------+
| 斜体     | \*emphasis*              | *emphasis*              | ~                                        |
+----------+--------------------------+-------------------------+------------------------------------------+
| 加粗     | \**emphasis**            | **emphasis**            | ~                                        |
+----------+--------------------------+-------------------------+------------------------------------------+
| 解释     | \`interpreted`           | `interpreted`           | ~                                        |
+----------+--------------------------+-------------------------+------------------------------------------+
| 代码     | \``code``                | ``code``                | ~                                        |
+----------+--------------------------+-------------------------+------------------------------------------+
| 参考     | \google_                 | google_                 | ``.. _google: http://google.com/``       |
+----------+--------------------------+-------------------------+------------------------------------------+
| 短语参考 | \`this google`_          | `this google`_          | ``.. _A google: http://google.com/``     |
+----------+--------------------------+-------------------------+------------------------------------------+
| 间接参考 | \`search engine`__       | `search engine`__       | ``__ google_``                           |
+----------+--------------------------+-------------------------+------------------------------------------+
| 替换     | \|biohazard|             | |biohazard|             | ``.. |biohazard| image:: biohazard.png`` |
+----------+--------------------------+-------------------------+------------------------------------------+
| 脚注     | footnote reference \[1]_ | footnote reference [1]_ | ``.. [1] This is a footnote ref``        |
+----------+--------------------------+-------------------------+------------------------------------------+
| 引用     | \[CIT2002]_              | [CIT2002]_              | ``.. [CIT2002] This is a Citation.``     |
+----------+--------------------------+-------------------------+------------------------------------------+
| 超链接   | http://google.com/       | http://google.com/      | ~                                        |
+----------+--------------------------+-------------------------+------------------------------------------+

.. [CIT2002] This is a Citation
.. [1] A footnote reference.

官方文档：行内标记_

.. _行内标记: http://docutils.sourceforge.net/docs/ref/rst/restructuredtext.html#inline-markup
.. _google: http://google.com/
.. _this google: http://google.com/
__ google_
.. |biohazard| image:: biohazard.png

标题
---------------------

使用以下任何一个符号生成标题：

``= - ` : ' " ~ ^ _ * + # < >``

例如::

    一级标题
    ======================
    二级标题
    ----------------------
    三级标题
    ''''''''''''''''''''''
    

官方文档：段落_

.. _段落: http://docutils.sourceforge.net/docs/ref/rst/restructuredtext.html#sections

列表
----------------------

无序列表
''''''''''''''''''''''

``- something`` or ``+ something`` or ``* somthing``

例如::

    - option1
    - option2
    + something1
    + something2
    * something2
结果:

- option1
- option2
+ something1
+ something2
* something2

有序列表
'''''''''''''''''''''''

``1. somthing`` or ``#. somthing``
例如::

    1. something1
    2. something2
    #. something else
结果:

1. something1
2. something2
#. something else

定义列表
'''''''''''''''''''''''

示例::

    what
        this is a english word.
    apple
        this is a kind of fruit.
结果:
what
    this is a english word.
apple
    this is a kind of fruit.

域列表
'''''''''''''''''''''''

示例::

    :Authors:
        Alex, Tony.
    :Version: 1.1 Alpha
    :Dedication: To my father.
结果:

:Authors:
    Alex, Tony.
:Version: 1.1 Alpha
:Dedication: To my father.

选项列表
''''''''''''''''''''''''
示例::

    -a           command-line option"a"
    -b file      options and arguments
    --long       long options
    /V           DOS option
结果:

-a           command-line option"a"
-b file      options and arguments
--long       long options
/V           DOS option

官方文档：列表_

.. _列表: http://docutils.sourceforge.net/docs/ref/rst/restructuredtext.html#bullet-lists

代码块
----------------------

基本代码块
''''''''''''''''''''''

一段文字跟在 ``::`` 之后, 可以作为文字块。快内的文字必须比块之外的文字多一个缩进。若想退出块,
只需要缩进与之前的文字并齐即可。

例如:

    \:: 

       for i in range(20):
            pass

结果:

:: 

    for i in range(20):
        pass

``::`` 同样可以在一段的最后, 如果在一段的最后, 则会被显示为一个 ``:``, 并且下一行
作为块, 使用这种格式非常方便。 
例如:
    
    这是一个代码块\::

        print('hello')
结果:

这是一个代码块::
    
    print('hello')

块会一直存在直到缩进变为和块之外的文本相同, 块才会结束::
 
      We start here 
    and continue here 
  and end here. 

如果不缩进, 也可以使用行引用符号, 在每一行之前加 ``>`` ,例如::

> Useful for quotes from email and  is
> for Haskell literate programming.

行块
'''''''''''''''''''''''''

行块属于引用, 代码不会高亮。
例如::

    | Line blocks are useful for addresses, 
    | verse, and adornment-free lists. 
    | 
    | Each new line begins with a 
    | vertical bar ("|"). 
    |     Line breaks and initial indents 
    |     are preserved. 
    | Continuation lines are wrapped 
    portions of long lines; they begin 
    with spaces in place of vertical bars.

结果:

| Line blocks are useful for addresses, 
| verse, and adornment-free lists. 
| 
| Each new line begins with a 
| vertical bar ("|"). 
|     Line breaks and initial indents 
|     are preserved. 
| Continuation lines are wrapped 
  portions of long lines; they begin 
  with spaces in place of vertical bars.

缩进块
'''''''''''''''''''''''''''

缩进块只需要进行简单的缩进, 同样不会高亮, 属于引用。 例如:

    简单的缩进也可以作为块。

测试代码块
'''''''''''''''''''''''''''

测试代码块由 ``>>>`` 符号开始, 直到一个空行结束。

例如:
    \>>> print "This is a doctest block."

    This is a doctest block.

结果:

>>> print "This is a doctest block." 
This is a doctest block.

.. attention::

    attention

.. warning::

    warning

.. note::

    note

.. tip::

    tip