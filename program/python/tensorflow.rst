TensorFlow
==========================

TensorFlow 优化
--------------------------

显存占用
'''''''''''''''''''''''''

增加环境变量, 控制可见GPU ::

  import os
  os.environ['CUDA_VISIBLE_DEVICES'] = '0'

随着进程逐渐增加显存占用, 而不是再初始化 ``Session`` 时一下占用所有空闲显存::

  config = tf.ConfigProto()
  config.gpu_options.allow_growth = True
  ## tf.Session()
  tf.Session(config = config)

TimeLine 查看运行时间线
''''''''''''''''''''''''''

使用 ``timeline`` 查看一个 ``step`` 的运行时间线, 并保存为 ``json`` 文件, 使用 ``chrome`` 查看时间线::

  from tensorflow.python.client import timeline

运行计算图之前定义 ``metadata`` 和 ``options``::

  run_metadata = tf.RunMetadata()
  run_options = tf.RunOptions(trace_level=tf.RunOptions.FULL_TRACE)

运行计算图时, 加上 ``metadata`` 和 ``options``::

  with tf.Session() as sess:
    result = sess.run(fetch, feed, options=run_options, run_metadata=run_metadata)

运行后, 创建 ``Timeline`` 对象, 并将数据写入 ``json`` 文件::

  fetched_timeline = timeline.Timeline(run_metadata.step_stats)
  # Chrome Trace 格式
  chrome_trace = fetched_timeline.generate_chrome_trace_format()
  # 保存, step 是当前的步数.
  with open('timeline_%d.json' % step, 'w') as f:
    f.write(chrome_trace)

保存后, 在 ``Chrome`` 输入::

  chrome://tracing/

最后点击 ``load`` 加载 ``timeline`` 文件.

TensorBoard
------------------------

``TensorBoard`` 是 ``TensorFlow`` 提供的可视化平台, 可以将训练模型时的各种数据以网页应用的方式直观的展示出来.
包括计算图, 运行时的标量, 变量, 嵌入层的映射等等.

使用方法
'''''''''''''''''''''''

首先定义一个 ``FileWriter``, 用来将 ``summary`` 数据写入文件::

  with tf.Session() as sess:
    writer = tf.summary.FileWriter(save_path, sess.graph)

常用参数:

:logdir:            保存路径
:graph:             一个图对象, 例如 ``sess.graph``.
:max_queue:         整数. 记录 ``summary`` 的队列大小.
:flush_secs:        多少秒将队列中的数据写入硬盘.

.. attention:: ``FileWriter`` 需要定义在初始化 ``Session()`` 以后.

.. _写入文件:

然后在每次运行计算图并获得 ``summary`` 的结果时, 将结果写入到文件::

  # summ 是运行 summary op 得到的结果
  writer.add_summary(summ, global_step=step)

在训练完成以后, ``save_path`` 目录下会出现 ``events`` 文件, 在命令行使用以下命令打开 ``TensorBoard`` 服务::

  tensorboard --logdir=save_path --host=127.0.0.1

--logdir    ``summary`` 保存路径
--host      主机IP地址

如果默认 ``host`` 地址即为 ``127.0.0.1`` 可以不添加 ``host`` 参数.

Summaries
'''''''''''''''''''''''

``TensorFlow`` 的 ``summary`` 是用来在 ``TensorBoard`` 中直观显示标量或者变量的.

.. important:: ``summary`` 也是计算图里的一个 ``operation``.

定义
"""""""""""""""""""""""

- 标量

首先在计算图中定义 ``summary``, 例如 ``Loss``::

  tf.summary.scalar(name="Loss", tensor=_loss)

合并
""""""""""""""""""""""""

定义完 ``summary`` 以后, 需要将操作合并到计算图中, 返回 ``summary op``.

将所有的 ``summary`` 合并到默认的计算图中::

  summ_op = tf.summary.merge_all()

运行与保存
"""""""""""""""""""""""""

最后和其他操作一样, 需要在 ``Session`` 里运行才能在 ``tensorboard`` 里看到结果.

::

  with tf.Session() as sess:
    result = sess.run(summ_op)

在得到结果后不要忘记将结果 写入文件_::

  writer.add_summary(summ, global_step=step)

词嵌入映射
'''''''''''''''''''''''''

词嵌入映射可以将 ``TensorFlow`` 的嵌入层学习到的变量降维后以 2D 或着 3D 的形式在
``TensorBoard`` 中展示出来.

.. hint:: ``TensorBoard`` 中提供的降维方式有 ``PCA`` 与 ``t-SNE``.

首先从 ``tensorboard`` 插件中导入 ``projector``::

  from tensorflow.contrib.tensorboard.plugins import projector

创建 ``projector_config`` 并增加 ``embedding`` 层, 通过名称指定 ``Tensor`` 变量::

  proj_config = projector.ProjectorConfig()
  embed = proj_config.embeddings.add()
  embed.tensor_name = train_model.embedding.name

如果需要显示单词在嵌入空间点上, 则需要指定单词表::

  embed.metadata_path = "vocab.tsv"

然后指定 ``writer`` 与 ``proj_config``, 即 ``summary`` 的 ``FileWriter``, 写入文件_.

.. important:: ``proj_config`` 会以文件形式写入 ``FileWriter`` 的相同目录下, 所以单词表的路径应该是 ``FileWriter`` 的相对路径.

将以上信息配置好以后, 就可以在 ``tensorboard`` 的 ``PROJECTOR`` 标签内查看映射.