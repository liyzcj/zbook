# Numpy

Numpy 由 `np` 表示：

```python
import numpy as np
```

## Search
---
`np.flatnonzero`(**`a`**) : 返回非零值的索引

```python
>>> x = np.arange(-2, 3)
>>> x
array([-2, -1,  0,  1,  2])
>>> np.flatnonzero(x)
array([0, 1, 3, 4])
```
和以下命令相同：
```python
np.nonzero(np.ravel(x))[0]
```
---
`np.argmax`(**`a, axis=None, out=None`**) : 返回最大值的索引

```python
>>> a = np.arange(6).reshape(2,3)
>>> a
array([[0, 1, 2],
       [3, 4, 5]])
>>> np.argmax(a)
5
>>> np.argmax(a, axis=0)
array([1, 1, 1])
>>> np.argmax(a, axis=1)
array([2, 2])
```

## Sort

---

`np.bincount`(**`x, weights=None, minlength=0`**) : 返回数组中非负`int` 类型的个数，从0到n，没有就返回零。

```python
>>> np.bincount(np.arange(5))
array([1, 1, 1, 1, 1])
>>> np.bincount(np.array([0, 1, 1, 3, 2, 1, 7]))
array([1, 3, 1, 1, 0, 0, 0, 1])
```

## Matrix

`np.array_split`(**`ary, indices_or_sections, axis=0`**) : 分割矩阵

```python
>>> x = np.arange(8.0)
>>> np.array_split(x, 3)
    [array([ 0.,  1.,  2.]), array([ 3.,  4.,  5.]), array([ 6.,  7.])]

>>> x = np.arange(7.0)
>>> np.array_split(x, 3)
    [array([ 0.,  1.,  2.]), array([ 3.,  4.]), array([ 5.,  6.])]
```
---

`np.concatenate`(**`(a1, a2, ...), axis=0, out=None`**) : 拼接矩阵

```python
>>> a = np.array([[1, 2], [3, 4]])
>>> b = np.array([[5, 6]])
>>> np.concatenate((a, b), axis=0)
array([[1, 2],
       [3, 4],
       [5, 6]])
>>> np.concatenate((a, b.T), axis=1)
array([[1, 2, 5],
       [3, 4, 6]])
>>> np.concatenate((a, b), axis=None)
array([1, 2, 3, 4, 5, 6])
```
---
`np.hstack`(**`tuple | list`**) : 列方向堆栈，列拼接，相当于`np.stack([a,b], axis=1)`;

```python
>>> a = np.array((1,2,3))
>>> b = np.array((2,3,4))
>>> np.hstack((a,b))
array([1, 2, 3, 2, 3, 4])
>>> a = np.array([[1],[2],[3]])
>>> b = np.array([[2],[3],[4]])
>>> np.hstack((a,b))
array([[1, 2],
       [2, 3],
       [3, 4]])
```
---
`numpy.stack`(**`arrays, axis=0, out=None`**) : 按指定轴连接数组;

```python
>>> arrays = [np.random.randn(3, 4) for _ in range(10)]
>>> np.stack(arrays, axis=0).shape
(10, 3, 4)
>>> np.stack(arrays, axis=1).shape
(3, 10, 4)
>>> np.stack(arrays, axis=2).shape
(3, 4, 10)
>>> a = np.array([1, 2, 3])
>>> b = np.array([2, 3, 4])
>>> np.stack((a, b))
array([[1, 2, 3],
       [2, 3, 4]])
>>> np.stack((a, b), axis=-1)
array([[1, 2],
       [2, 3],
       [3, 4]])
```
---