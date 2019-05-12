进度条
==========

进度条可以方便的观察程序运行的进展, 并进行时间的估算.

自己实现
-----------

利用 ``print()`` 可以方便的实现简单进度条. 

比如利用将 '\r' 传递给 ``print()`` 来刷新当前行的输出::

  print(i, end='\r')

或着直接不换行, 在后面继续输出:

  >>> print('#', end='')
  ##########


自己实现进度条比较简陋也不方便, 利用封装好的模块可以实现方便又复杂的进度条.

比较常用的进度条模块有两个:

- tqdm
- progressbar

tqdm
-----------

tqdm 在阿拉伯语中意思为 "进展" (taqadum) 并且是西班牙语 "我很爱你" 的缩写.(te quiero demasiado)

命令行
''''''''''''

tqdm 简单易用, 仅仅需要在循环外包裹一个 ``tqdm`` 对象::

  >>> from tqdm import tqdm
  >>> from time import sleep

  >>> for _ in tqdm(range(10), ncols=100):
  >>>   sleep(1)
  100%|█████████████| 10/10 [00:10<00:00,  1.00s/it]

.. attention:: windows 上最好指定 ``ncols`` ,设置进度条宽度, 否则容易出bug

tqdm 类提供了许多属性与方法控制进度条的显示: `tqdm`_

gui
'''''''''''''

``tqdm`` 还提供了 ``gui`` 版本的进度条, 但是需要 ``matplotlib`` 支持::

  from tqdm import tqdm_gui
  from time import sleep

  for i in tqdm_gui(range(10), ncols=100):
    sleep(1)

快捷方法:
''''''''''''''

tqdm 还提供了许多快捷方法来简单的实现进度条:

+--------------------------+-------------------------------------+
| 快捷方法                 | 完整语法                            |
+--------------------------+-------------------------------------+
|  trange(*args, **kwargs) | tqdm(range(args), *kwargs)          |
+--------------------------+-------------------------------------+
| tgrange(*args, **kwargs) | tqdm_gui(range(args), *kwargs)      |
+--------------------------+-------------------------------------+
| tnrange(*args, **kwargs) | tqdm_notebook(range(args), *kwargs) |
+--------------------------+-------------------------------------+

示例::

  >>> from tqdm import trange
  >>> from time import sleep

  >>> for i in trange(10, ncols=50):
  >>>   sleep(1)
  100%|█████████████| 10/10 [00:10<00:00,  1.00s/it]

progressbar
-------------

progressbar 的用法和 tqdm 类似, 也是使用一个类接受可迭代对象作为参数.

::

  import time
  from progressbar import ProgressBar
  
  total = 1000
  
  def dosomework():
    time.sleep(0.01)
  
  progress = ProgressBar()
  for i in progress(range(100)):
    dosomework()

也可以使用 update() 方法来更新进度条::

  import sys, time
  from progressbar import ProgressBar

  total = 100
  
  def dosomework():
    time.sleep(0.01)
  
  pbar = ProgressBar().start()
  for i in range(100):
    pbar.update(int((i / (total - 1)) * 100))
    dosomework()
  pbar.finish()


自定义插件
''''''''''''

如果需要也可以自己定义进度条插件::

  import  time
  from progressbar import *
  
  total = 100
  
  def dosomework():
    time.sleep(0.01)
  
  widgets = ['Progress: ',Percentage(), ' ', Bar('#'),' ', Timer(),
            ' ', ETA(), ' ', FileTransferSpeed()]
  pbar = ProgressBar(widgets=widgets, maxval=10*total).start()
  for i in range(total):
    # do something
    pbar.update(10 * i + 1)
    dosomework()

输出::

  PS D:\znote> ######### | Elapsed Time: 0:00:01 ETA:  0:00:00 904.70  B/s

插件参数含义:

- ``Progress`` : 进度条前的文字
- ``Percentage`` : 显示百分比
- ``Bar('#')`` : 进度条形状
- ``ETA()`` : 预计剩余时间
- ``Timer()`` : 显示已用时间

`progressbar`_


.. _progressbar: https://progressbar-2.readthedocs.io/en/latest/
.. _tqdm: https://tqdm.github.io/docs/tqdm/
