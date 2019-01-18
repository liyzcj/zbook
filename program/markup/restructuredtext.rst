reStructuredText
=====================

.. contents::

.. section-numbering::

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
| 公式     | \:math:`x\\in\\mathbb{W}`|  :math:`x\in\mathbb{W}` | ~                                        |
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

单独的一行 ``-------``, 会渲染为分割线:

------------------------

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

有序列表
'''''''''''''''''''''''

以数字或字母之后根一个圆点、右括号或被括号包围。以下所有的形式都可以识别:
例如::

    1. 数字

    A. 小写字母
        可以有多行

        可以有几个段落。

    a. 小写字母

        3. 以不同的数字开始的子列表
        4. 确保数字的顺序是对的

    I. 大写罗马数字

    i. 小写罗马数字

    (1) 又是数字

    1) 还是数字

结果:

1. 数字

A. 小写字母
   可以有多行

   可以有几个段落。

a. 小写字母

   3. 以不同的数字开始的子列表
   4. 确保数字的顺序是对的

I. 大写罗马数字

i. 小写罗马数字

(1) 又是数字

1) 还是数字

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

字段列表
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

.. note::

    reStructuredText 中注册的字段如下

    - 字段名 "Author": 作者元素
    - "Authors": 作者.
    - "Organization": 组织.
    - "Contact": 联系方式.
    - "Address": 地址.
    - "Version": 版本.
    - "Status": 状态.
    - "Date": 日期.
    - "Copyright": 版权.
    - "Dedication": 主题.
    - "Abstract": 主题.

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

.. tip::

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

官方文档: `代码块 <http://docutils.sourceforge.net/docs/ref/rst/restructuredtext.html#literal-blocks>`_

--------------------

表格
--------------------

表格包含简单表格和复杂表格, 简单表格格式简单, 但是表达内容有限, 复杂表格则相反。

简单表格
'''''''''''''''''''''

简单表格由等号 ``=`` 以及 ``-`` 组成。``=`` 用于表格的顶部和底部边框, 也可用于分隔可选标题行。
``-`` 则用于单行中连接列::

    =====  =====  ======
       Inputs     Output
    ------------  ------
      A      B    A or B
    =====  =====  ======
    False  False  False
    True   False  True
    False  True   True
    True   True   True
    =====  =====  ======

=====  =====  ======
   Inputs     Output
------------  ------
  A      B    A or B
=====  =====  ======
False  False  False
True   False  True
False  True   True
True   True   True
=====  =====  ======

复杂表格
'''''''''''''''''''''

网格表格通过字符”-“、”=”、”|”和”+”被描述为一个视觉网格::

    +--------------+----------+-----------+-----------+
    | row 1, col 1 | column 2 | column 3  | column 4  |
    +--------------+----------+-----------+-----------+
    | row 2        |                                  |
    +--------------+----------+-----------+-----------+
    | row 3        |          |           |           |
    +--------------+----------+-----------+-----------+

.. tip::

    复杂表格可以使用专门的 生成器_ 生成。 

.. _生成器: http://www.tablesgenerator.com/

指令
--------------------------

指令是reStructuredText的扩展机制，一种添加支持新结构而不用添加新的
语法（指令支持额外的本地语法）的方法。

.. hint:: 

    指令的参数由 字段列表_ 组成。

语法树::

    +-------+-------------------------------+
    | ".. " | directive type "::" directive |
    +-------+ block                         |
            |                               |
            +-------------------------------+

官方文档：`指令 <http://docutils.sourceforge.net/docs/ref/rst/directives.html#id28>`_

警告
''''''''''''''''''''''''''

- attention

    .. attention:: 注意

- caution

    .. caution:: 小心

- danger

    .. danger:: 危险
    
- error

    .. error:: 错误

- hint

    .. hint:: 提示

- important

    .. important:: 重要

- note

    .. note:: 通知
    
- tip

    .. tip:: 小技巧
    
- warning

    .. warning:: 警告
        
图片
'''''''''''''''''''''''

语法::

    .. image:: picture.jpeg
        :height: 100px
        :width: 200 px
        :scale: 50 %
        :alt: alternate text
        :align: right

- ``alt``: *text*   简单图片介绍
- ``height``: *length*  图片的高度
- ``width``: *length* or *percentage*  长度单位或百分比： 图片的宽度。
- ``scale``: *integer percentage* 整数百分比：图片的缩放比例
- ``align``: *top*, *middle*, *bottom*, *left*, *center*, or *right*：图片的位置。
- ``target``: *url* : 图片指向的超链接。

正文元素
'''''''''''''''''''''''''

话题
+++++++++++++++++++++++++

一个话题类似于一个包含标题或自包含章节而无子章节的引用块。
使用话题指令来表示一个与文档流程隔离的自包含的想法::

    .. topic:: Topic Title

        之后的所缩进行包含话题的正文
        并不解释为正文元素

侧边栏
+++++++++++++++++++++++++

侧边栏类似正好在其他文档内的小型、平行文档，提供关联或引用材料。 侧边栏通常通过边框和漂浮偏移
到页面的旁边。侧边栏也可以连接到内容在文档主文之外的脚注::

    .. sidebar:: Sidebar Title
        :subtitle: Optional Sidebar Subtitle

        Subsequent indented lines comprise
        the body of the sidebar, and are
        interpreted as body elements.

``subtitle``: *text* : 侧边栏子标题

.. sidebar:: Sidebar Title
   :subtitle: Optional Sidebar Subtitle

   Subsequent indented lines comprise
   the body of the sidebar, and are
   interpreted as body elements.

代码
+++++++++++++++++++++++++++

代码块已经可以实现基本的代码高亮, 使用代码指令可以指定代码语言, 从而被高亮语法器解析::

    .. code:: python

        def my_function():
            "just a test"
            print 8/2

.. code:: python

  def my_function():
      "just a test"
      print 8/2

数学公式
+++++++++++++++++++++++++++

数学公式默认使用MathJax::

    .. math::

        α_t(i) = P(O_1, O_2, … O_t, q_t = S_i λ)

.. math::

  α_t(i) = P(O_1, O_2, … O_t, q_t = S_i λ)


引言
++++++++++++++++++++++++++++

引言是一个简短的铭文, 通常在文章的开头::

    .. epigraph::

        No matter where you go, there you are.

        -- Buckaroo Banzai

.. epigraph::

   No matter where you go, there you are.

   -- Buckaroo Banzai

文档部分
'''''''''''''''''''''''''''''

目录
++++++++++++++++++++++++++++

``contents`` 指令在文档中生成一个目录::

    .. contents::
        :depth: 2
        :local: 
        :backlinks:
        :class:

参数:

- ``depth`` : *integer*  , 目录的深度, 默认不限深度。
- ``local`` : *flag*  , 生成一个本地目录。条目只包含指定标题的章节的子标题。如果没有显式指定标题，目录没有标题。
- ``backlinks`` : *entry* , *top*, *无* : 是否从章节标题反向链接到目录。
- ``class`` : *text* , 在主题元素上设置类属性。

章节自动编号
+++++++++++++++++++++++++++++

``sectnum`` 或者 ``section-autonumbering``

参数:

- ``depth`` : *integer*, 目录深度
- ``prefix`` : *string*, 任意的字符串，用于生成章节前缀。
- ``suffix`` : *string*, 任意后缀, 默认为空
- ``start`` : *integer*, 用于第一个章节的值