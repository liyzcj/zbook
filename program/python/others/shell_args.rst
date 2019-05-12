命令行参数
===============

命令行参数指在命令行运行 python 脚本时所传递给脚本的参数.

参数传递
----------
python 的命令行参数传递由 ``sys`` 模块完成, ``sys.argv`` 是一个保存了所有参数的 List.

在命令行运行 python 脚本::

  python script [arg1, arg2, arg3, ...]

其中, ``sys.argv[0]`` 即第 0 个参数为 ``script`` . 

参数解析(内建)
-----------

参数解析可以由手动写代码完成, 但是比较繁琐, python 已经提供了封装好的参数解析模块.

参数解析的方法主要有如下几种:

+------------+-----------------------------+------+
| 方法       | 介绍                        | 模块 |
+------------+-----------------------------+------+
|   getopt   | 与 C 中的 ``getopt()`` 等价 | 内建 |
+------------+-----------------------------+------+
| optparse   | python2.7 以后不建议使用    | 内建 |
+------------+-----------------------------+------+
| argparse   | 基于 ``optparse`` 的新版本  | 内建 |
+------------+-----------------------------+------+
| tensorflow | ``tensorflow`` 解析专用     | 其他 |
+------------+-----------------------------+------+
| docopt     | ``__doc__`` 自动生成解析    | 其他 |
+------------+-----------------------------+------+
| click      | todo                        | 其他 |
+------------+-----------------------------+------+

.. hint:: 如果没有特殊要求, 推荐使用内建 ``argparse`` .

getopt
'''''''''''

getopt 主要提供两个函数以及一个异常判断.

1. 第一个函数是 getopt

::
  
  getopt.getopt(args, options[, long_options])

:args: 需要解析的参数列表, 一般是 ``sys.argv[1:]``
:options: 字符串, 短选项. 如果某一项需要参数, 则在后面加 ``:`` 
:long_options: 字符串列表, 长选项. 如果需要参数在后面加 ``=``
:返回值: 返回两部分, 第一个部分是 (options, value) 列表; 第二部分是解析后剩下的参数.

示例代码::

  import sys
  from getopt import getopt
  from getopt import GetoptError

  print(f"sys.argv : {sys.argv}")
  long_option = ['opt1', 'opt2=']
  result = getopt(sys.argv[1:], 'opt:', long_option)
  print(f"result: {result}")

运行结果::

  PS D:\znote> python.exe test.py -p -t tt --opt1 --opt2 oo2 other1 -o
  sys.argv : ['test.py', '-p', '-t', 'tt', '--opt1', '--opt2', 'oo2', 'other1', '-o']
  result: ([('-p', ''), ('-t', 'tt'), ('--opt1', ''), ('--opt2', 'oo2')], ['other1', '-o'])

.. attention:: 需要解析的选项不能在其他选项后面, 否则会抛出异常.

由上面的结果可以看到, 要使用解析得到的结果还需要一定的代码处理才能使用, 并不方便.

2. getopt 提供的第二个函数是 gnu_getopt

::

  getopt.gnu_getopt(args, options[, long_options])

gnu_getopt 可以解决参数解析顺序的问题, 使得参数的顺序可以随意. 带来的缺点就是其他参数不能有短选项, 
例如上述示例中的 `-s` 在 gnu_getopt 中就会抛出异常.


3. getopt 提供一个异常

::

  getopt.GetoptError

当一个必要的参数未传入或着一个选项无法识别时抛出此异常.


optparse
'''''''''''

optparse 在 python2.7 以后已经弃用, 而且将来可能会删除.

argparse 基于 optparse 并有很多优势:

- 处理位置参数
- 支持子命令
- 允许自定义前缀
- 能够处理 ``zero-or-more`` 或 ``one-or-more`` 参数
- 产生更多帮助信息
- 更简单的接口与使用方法

更多详见 `PEP 389`_

参考: `Why use argparse rather than optparse?`_

argparse
'''''''''''

argparse 使用分为三个步骤:

1. 创建 ``ArgumentParser`` 对象
2. 使用 ``add_argument()`` 添加参数选项
3. 使用 ``parse_args()`` 解析参数

创建对象::

  parser = argparse.ArgumentParser()


可选关键字参数:

:prog: 脚本名称 (default: sys.argv[0])
:usage: 帮助信息 (default: 自动生成)
:description: 显示在帮助之前的描述 (default: none)
:epilog: 显示在帮助之后的文本 (default: none)
:parents: 包含多个ArgumentParser对象的List, 同样需要被解析的参数.
:formatter_class: 一个格式化帮助信息的类
:prefix_chars: 包含可选参数前缀的 Set (default: ‘-‘)
:fromfile_prefix_chars: 从文件读取参数的前缀 (default: none)
:argument_default: 参数全局默认值 (default: None)
:conflict_handler: 解决冲突选项的策略 (usually unnecessary)
:add_help: 增加 -h/--help 选项 (default: True)
:allow_abbrev:  允许长选项缩写, 3.5 版本加入. (default: True)

详见 `ArgumentParser objects`_

增加可选参数::

  ArgumentParser.add_argument(name or flags...[key args])

参数:

:name or flags: 名称或flag. 例如 ``foo, -f, --foo`` 
:action: 当参数传入时执行的动作. (default: store)
:nargs: 选项消耗的参数个数.
:const: 一个常量, 用于 ``action`` 与 ``nargs``
:default: 选项未提供时的默认值
:type: 参数的类型
:choices: 允许的参数的容器
:required: 是否允许省略(仅可选参数)
:help: 参数的简短描述
:metavar: 帮助中显示的名称
:dest: 解析后变量的名称.

详见 `the-add-argument-method`_

简单示例::

  import argparse

  parser = argparse.ArgumentParser(description="This is a example.")
  parser.parse_args()

.. hint:: 如果没有传递参数给 ``parse_args()`` 函数, 则默认解析 ``sys.argv`` .

默认拥有 ``-h`` 或 ``--help`` 选项::

  PS D:\znote> python.exe test.py -h
  usage: test.py [-h]

  This is a example.

  optional arguments:
    -h, --help  show this help message and exit


位置参数
"""""""""""

位置参数意思就是像函数参数那样根据位置确定传入的参数而不需要指定选项, 
argparse 可以很方便的实现这一点::

  import argparse

  parser = argparse.ArgumentParser(description="This is a example.")
  parser.add_argument('loc1', help='这是第一个参数.')
  args = parser.parse_args()
  print(args.loc1)

运行代码并传入参数::

  PS D:\znote> python.exe test.py one
  one

查看帮助选项::

  PS D:\znote> python.exe test.py -h
  usage: test.py [-h] loc1

  This is a example.

  positional arguments:
    loc1        这是第一个参数.

  optional arguments:
    -h, --help  show this help message and exit

默认接受的参数是 string 类型的, 我们也可以为位置参数添加数据类型::

  import argparse

  parser = argparse.ArgumentParser(description="This is a example.")
  parser.add_argument('squre', help='这是第一个参数.', type=int)
  args = parser.parse_args()
  print(args.squre ** 2)

.. attention:: 帮助信息并不会自动提示数据类型.

可选参数
""""""""""""

可选参数同样使用 ``add_argument()`` 函数添加. 现在让我们来看看怎么添加可选参数::

  import argparse

  parser = argparse.ArgumentParser(description="求平方")
  parser.add_argument('--verbose', action = 'store_true', help="提高输出显示等级")
  args = parser.parse_args()
  if args.verbose:
    print("输出打开.")

输出::

  PS D:\znote> python.exe test.py --verbose
  输出打开.

这里采用了一个 ``action`` 参数, 提供了一个 ``store_true`` 动作, 表明 ``verbose`` 选项
指定时 ``verbose`` 选项设为 ``True`` 否则设为 ``False`` .

动作类型
""""""""""

action 参数提供了 **八** 种类型的动作, 除此之外也可以自定义动作.

+--------------+----------------------------------------+
| 动作         | 介绍                                   |
+--------------+----------------------------------------+
|     store    | 默认动作, 直接存储到变量, 消耗一个参数 |
+--------------+----------------------------------------+
| store_const  | 配合const, 将const存进变量, 不消耗参数 |
+--------------+----------------------------------------+
| store_true   | 存储 True 进变量, 未指定存储 False     |
+--------------+----------------------------------------+
| append       | 将参数 Append 到一个 List 对象         |
+--------------+----------------------------------------+
| append_const | 配合const, 将常量 Append 到 List       |
+--------------+----------------------------------------+
| count        | 统计参数出现的次数                     |
+--------------+----------------------------------------+
| help         | 打印 help, ArgumentParser 默认有一个   |
+--------------+----------------------------------------+
| version      | 配合 version, 打印 version 并退出      |
+--------------+----------------------------------------+

详见 `action`_

nargs
"""""""""

nargs 参数代表消耗参数的个数. 可取的值有如下几种:

- ``N`` : 一个整型数字, 代表消耗参数的个数.

这会将消耗的参数保存为 List 存进变量中, 即使 ``N = 1``, 所以等于 1 时与默认也不相同.

- ``?`` : 判断形式

若选项后有参数, 则保存参数进变量; 若选项后没有参数, 则保存 const 参数的值进变量; 若选项
没有出现, 则保存 default 的值进参数.

常用的方法时重定向输入输出文件::

  >>> parser = argparse.ArgumentParser()
  >>> parser.add_argument('infile', nargs='?', type=argparse.FileType('r'),
                      default=sys.stdin)
  >>> parser.add_argument('outfile', nargs='?', type=argparse.FileType('w'),
                      default=sys.stdout)
  >>> parser.parse_args(['input.txt', 'output.txt'])
  Namespace(infile=<_io.TextIOWrapper name='input.txt' encoding='UTF-8'>,
          outfile=<_io.TextIOWrapper name='output.txt' encoding='UTF-8'>)
  >>> parser.parse_args([])
  Namespace(infile=<_io.TextIOWrapper name='<stdin>' encoding='UTF-8'>,
          outfile=<_io.TextIOWrapper name='<stdout>' encoding='UTF-8'>)

- ``*`` : 将选项后的所有参数存进 List 变量

- ``+`` : 像 ``*`` 一样, 但是不少于一个参数.

- argparse.REMAINDER : 所有剩余的参数存进 List 变量

type
""""""""

类型转换, 将收到的字符串参数转换为特定类型::

  >>> parser = argparse.ArgumentParser()
  >>> parser.add_argument('foo', type=int)
  >>> parser.add_argument('bar', type=open)
  >>> parser.parse_args('2 temp.txt'.split())
  Namespace(bar=<_io.TextIOWrapper name='temp.txt' encoding='UTF-8'>, foo=2)


为了方便打开各种类型的文件, ``argparse`` 提供了 ``FileType`` 类型接受 ``mode=, bufsize=, encoding= and errors=``
参数来传递给 ``open()`` 函数. 例如::

  >>> parser = argparse.ArgumentParser()
  >>> parser.add_argument('bar', type=argparse.FileType('w'))
  >>> parser.parse_args(['out.txt'])
  Namespace(bar=<_io.TextIOWrapper name='out.txt' encoding='UTF-8'>)

.. hint:: type 可以接受任何以字符串为输入, 返回一个值的函数.

choices
""""""""""

``choices`` 可以对输入的参数进行限定. 

将一组可选的值作为 List 传递给 ``choices`` , 注意应与 ``type`` 指定的类型相同.

::

  >>> parser = argparse.ArgumentParser(prog='doors.py')
  >>> parser.add_argument('door', type=int, choices=range(1, 4))
  >>> print(parser.parse_args(['3']))
  Namespace(door=3)
  >>> parser.parse_args(['4'])
  usage: doors.py [-h] {1,2,3}
  doors.py: error: argument door: invalid choice: 4 (choose from 1, 2, 3)

dest
"""""""""""

dest 指定了保存变量的名称.

argparse 提供的其他函数见: `other-utilities`_

参数解析(其他)
---------------

tensorflow
'''''''''''

``tensorflow`` 里的参数解析是 ``tensorflow.app.flags``, 是基于 ``argparse`` 再封装的专门给
``tensorflow`` 应用提供的参数解析模块. 配合 ``tensorflow.app`` 使用.

使用方法也非常简单::

  import tensorflow as tf

  flags = tf.app.flags

  flags.DEFINE_string(flag_name, default_value, docstring)

``tensorflow`` 提供了四种类型的参数::

  DEFINE_string(flag_name, default_value, docstring)
  DEFINE_integer(flag_name, default_value, docstring)
  DEFINE_boolean(flag_name, default_value, docstring)
  DEFINE_float(flag_name, default_value, docstring)

使用简单, 在传递参数后, 参数变量保存在 ``flags.FLAGS`` 内.

.. hint:: FLAGS 是全局变量, 在任何位置都可以使用.

最后配合 ``tf.app.run()`` , 运行定义的 ``main()`` 函数.

docopt
""""""""

与 ``argparse`` 定义参数并自动生成帮助文本不同, ``docopt`` 是根据特定的格式从 ``__doc__`` 
描述中自动生成参数解析.

`docopt`_

click
"""""""""

``click`` 是可交互式的参数传递模块, 可以实时的将参数交互式的传递给程序.

`click`_

.. _click: https://palletsprojects.com/p/click/
.. _docopt: http://docopt.org/
.. _Why use argparse rather than optparse?: https://stackoverflow.com/questions/3217673/why-use-argparse-rather-than-optparse
.. _PEP 389: https://www.python.org/dev/peps/pep-0389/
.. _ArgumentParser objects: https://docs.python.org/3/library/argparse.html#argumentparser-objects
.. _action: https://docs.python.org/3/library/argparse.html#action
.. _the-add-argument-method: https://docs.python.org/3/library/argparse.html#the-add-argument-method
.. _other-utilities: https://docs.python.org/3/library/argparse.html#other-utilities

