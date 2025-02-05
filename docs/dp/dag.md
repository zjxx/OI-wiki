## 定义

DAG 即 [有向无环图](../graph/dag.md)，一些实际问题中的二元关系都可使用 DAG 来建模，从而将这些问题转化为 DAG 上的最长（短）路问题。

## 解释

以这道题为例子，来分析一下 DAG 建模的过程。

???+note " 例题 [UVa 437 巴比伦塔 The Tower of Babylon](https://cn.vjudge.net/problem/UVA-437)"
    有 $n (n\leqslant 30)$ 种砖块，已知三条边长，每种都有无穷多个。要求选一些立方体摞成一根尽量高的柱子（每个砖块可以自行选择一条边作为高），使得每个砖块的底面长宽分别严格小于它下方砖块的底面长宽，求塔的最大高度。

## 过程

### 建立 DAG

由于每个砖块的底面长宽分别严格小于它下方砖块的底面长宽，因此不难将这样一种关系作为建图的依据，而本题也就转化为最长路问题。

也就是说如果砖块 $j$ 能放在砖块 $i$ 上，那么 $i$ 和 $j$ 之间存在一条边 $(i, j)$，且边权就是砖块 $j$ 所选取的高。

本题的另一个问题在于每个砖块的高有三种选法，怎样建图更合适呢？

不妨将每个砖块拆解为三种堆叠方式，即将一个砖块分解为三个砖块，每一个拆解得到的砖块都选取不同的高。

初始的起点是大地，大地的底面是无穷大的，则大地可达任意砖块，当然我们写程序时不必特意写上无穷大。

假设有两个砖块，三条边分别为 $31, 41, 59$ 和 $33, 83, 27$，那么整张 DAG 应该如下图所示。

![](./images/dag-babylon.png)

图中蓝色实线框所表示的是一个砖块拆解得到的一组砖块，之所以用 $\{\}$ 表示底面边长，是因为砖块一旦选取了高，底面边长就是无序的。

图中黄色虚线框表示的是重复计算部分，可以采用 [记忆化搜索](./memo.md) 的方法来避免重复计算。

### 转移

题目要求的是塔的最大高度，已经转化为最长路问题，其起点上文已指出是大地，那么终点呢？显然终点已经自然确定，那就是某砖块上不能再搭别的砖块的时候。

下面我们开始考虑转移方程。

设 $d(i,r)$ 表示第 $i$ 块砖块在最上面，且采取第 $r$ 种堆叠方式时的最大高度。那么有如下转移方程：

$$
d(i, r) = \max\left\{d(j, r') + h\right\}
$$

其中 $j$ 是所有那些在砖块 $i$ 以 $r$ 方式堆叠时可放上的砖块，$r'$ 对应 $j$ 此时的摆放方式，$h$ 对应砖块 $i$ 采用第 $r$ 种堆叠方式时的高度。

??? note "实现"
    ```cpp
    --8<-- "docs/dp/code/dag/dag_1.cpp"
    ```
