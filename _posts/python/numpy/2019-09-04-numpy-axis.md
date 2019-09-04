---
layout: article
title: numpy axis
permalink: /_posts/python/numpy/2019-09-04-numpy-axis 
tags: Numpy
aside:
  toc: true
sidebar:
  nav: Numpy
---

<!--more-->


在 `numpy` 中，有很多函数都涉及到了 `axis`，而且根据`aixs` 的取值不同，得到的结果也完成不同。为了清晰的说明这个问题，首先我们通过一个三维数组来展示 axis 是什么。

1. 首先随机生成一个三维数组。

```python
>>>import numpy as np
>>>a = np.random.randint(0, 5, [3, 2, 2])
array([[[0, 4],
        [2, 3]],
       [[3, 1],
        [0, 0]],
       [[2, 4],
        [3, 1]]])
```

此三维数组的形状用 `list` 表示为 `[3, 2, 2]`。`axis=0` 表示轴 `0`，即 `[3, 2, 2]` 下标 `0` 对应的那个维度；`axis=1` 表示轴` 1`，即 `[3, 2, 2]` 下标 1 对应的那个维度；`axis=2` 表示轴 `2`，即 `[3, 2, 2]` 下标` 2` 对应的那个维度。由于其形状使用` list` 或者` tuple `表示的，所以其下标也可以用负数来表示，因此 `axis=0` 与 `axis=-3` 等价；`axis=1` 与 `axis=-2` 等价；`axis=2` 与 `axis=-1` 等价。

在上面的三维数组中，`axis=0` 表示的方向是 `a[0]->a[1]->a[2]`；`axis=1` 表示的方向是 `a[0][0]->a[0][1]`，`a[1][0]->a[1][1]`，`a[2][0]->a[2][1]`；`axis=2` 表示的方向是`a[0][0][0]->a[0][0][1]`，`a[0][1][0]->a[0][1][1]`，`a[1][0][0]->a[1][0][1]`，`a[1][1][0]->a[1][1][1]`，`a[2][0][0]->a[2][0][1]`，`a[2][1][0]->a[2][1][1]`。

为了方便我们的理解，我们可以将三维数组看成是平面堆叠而成，`[[0, 4], [2, 3]]` 就表示第一个平面，`[[3, 1], [0, 0]]` 就表示第二个平面，而 `[[2, 4], [3, 1]]` 则表示第三个平面。而平面又可以看成是行堆叠而成的，在第一个平面中，`[0, 4]` 表示第一行, `[2, 3]` 表示第二行，其他平面同理。行又可以看成是单个点堆叠而成，在第一个平面的第一行中，`0` 表示第一个点，`4` 表示第二个点。

接下来，我们结合使用 `axis` 的相关函数来理解设置不同的 `axis` 时该如何操作数组，相关的函数通常有 `average()`，`max()`，`min()`，`sum()`，`sort()`，`prod()`。**如果这些函数没有指定 `axis` 参数，则默认对所有元素进行操作, `sort()` 除外，它默认是最大的`axis`。**

**`sum()`**

```python
>>>a.sum()
23
>>>a.sum(axis=0)
array([[5, 9],
       [5, 4]])
>>>a.sum(axis=1)
array([[2, 7],
       [3, 1],
       [5, 5]])
>>>a.sum(axis=2)
array([[4, 5],
       [4, 0],
       [6, 4]])
```

**`average()`**

```python
>>>np.average(a)
1.9166666666666667
>>>np.average(a, axis=0)
array([[1.66666667, 3.        ],
       [1.66666667, 1.33333333]])
>>>np.average(a, axis=1)
array([[1. , 3.5],
       [1.5, 0.5],
       [2.5, 2.5]])
>>>np.average(a, axis=2)
array([[2. , 2.5],
       [2. , 0. ],
       [3. , 2. ]])
```

**`min()`**

```python
>>>a.min()
0
>>>a.min(axis=0)
array([[0, 1],
       [0, 0]])
>>>a.min(axis=1)
array([[0, 3],
       [0, 0],
       [2, 1]])
>>>a.min(axis=2)
array([[0, 2],
       [1, 0],
       [2, 1]])
```

**`max()`**

```python
>>>a.max()
4
>>>a.max(axis=0)
array([[3, 4],
       [3, 3]])
>>>a.max(axis=1)
array([[2, 4],
       [3, 1],
       [3, 4]])
>>>a.max(axis=2)
array([[4, 3],
       [3, 0],
       [4, 3]])
```

**`sort()`**

```python
>>>np.sort(a)  # 默认以最大的 axis 进行排序，这里即 axis=2
array([[[0, 4],
        [2, 3]],
       [[1, 3],
        [0, 0]],
       [[2, 4],
        [1, 3]]])
>>>np.sort(a, axis=0)
array([[[0, 1],
        [0, 0]],
       [[2, 4],
        [2, 1]],
       [[3, 4],
        [3, 3]]])
>>>np.sort(a, axis=1)
array([[[0, 3],
        [2, 4]],
       [[0, 0],
        [3, 1]],
       [[2, 1],
        [3, 4]]])
>>>np.sort(a, axis=2)
array([[[0, 4],
        [2, 3]],
       [[1, 3],
        [0, 0]],
       [[2, 4],
        [1, 3]]])
```

**`prod()`**

```python
>>>np.prod(a)
0
>>>np.prod(a, axis=0)
array([[ 0, 16],
       [ 0,  0]])
>>>np.prod(a, axis=1)
array([[ 0, 12],
       [ 0,  0],
       [ 6,  4]])
>>>np.prod(a, axis=2)
array([[0, 6],
       [3, 0],
       [8, 3]])
```
