Linux
================

linux commands.

g++ 编译 c++11
------------------

使用 ``g++`` 编译 ``c++``::

    g++ -g Wall -std=c++11 filename -o output_name

可以直接将命令写进 ``Makefile`` ::

    all:
        g++ -g -std=c++11 filename -o output_name

.. hint:: ``-g`` 指示编译时显示调试信息.
