author: 2008verser

反常游戏、反 $Nim$ 游戏的 [定义](intro.md/#_3)。

以反 $Nim$ 游戏为例，这里给出反 $Nim$ 游戏的结论以及证明：

规定：字母 $N$ 和 $P$ 分别代表先手必胜与必败。

一个局面为 $N$ 态的充要条件是有至少一条出边连接至 $P$ 态。

一个局面为 $P$ 态的充要条件是每一条出边都连接到 $N$ 态。

## 反 Nim 游戏

为方便书写，用字母 $T$ 表示 $\oplus_{i=1}^{n}a_{i}$。

结论：

- 1、当全部 $a_{i}=1$，如果有奇数堆石子就为 $P$ 态，有偶数堆则为 $N$ 态。


- 2、当至少一个 $a_{i}>1$，$T\neq 0$ 时为 $N$ 态，否则为 $P$ 态。

证明 1：显然。

证明 2：

情况 $A$：若只有一个 **$a_{i}>1$（此时 $T$ 一定 $\neq 0$）**，则先手选择转移到全部 $a_{i}=1$ 的局面，并且先手可以在这次决策中控制转移后堆数的奇偶。

故这种情况 **是 $N$ 态**。

情况 $B$：（不考虑 $T$ 取值）有至少 2 个 $a_{i}>1$。

小情况 $a$：$T\neq 0$：通过 $Nim$ 游戏可知一定能够转移到 $T=0$ 的局面（小情况 $b$）。

小情况 $b$：$T=0$：

一方面可以转移到至少 2 个 $a_{i}>1,T\neq 0$ 的局面，即 $a$。

另一方面随着游戏进行（$a,b$ 循环），数量大于 1 的堆会逐渐减少，最终只剩一堆，这就变成了情况 $a$，为 $N$ 态。

观察情况 $b$，$b$ 能给对面 $N$ 态或至少 2 个 $a_{i}>1,T\neq 0$ 的局面，而 $a$ 仅能给对面 $T=0$ 的局面。

所以在情况 $b$ 下，小情况 $b$ 为 $N$ 态，$a$ 为 $P$ 态。

也就是说 **当至少 2 个 $a_{i}>1,T\neq 0$ 时为 N 态，否则为 $P$ 态。**

综合情况 $a$ 和情况 $b$ 的结论，2 得证。

综上，1 和 2 皆得证。结论得证。
