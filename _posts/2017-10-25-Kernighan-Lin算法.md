---
title: Kernighan-Lin 算法描述
description: 对该算法简单描述
categories:
 - 图论
tags: algorithm cv
---
## 目的
本算法是求解二分图的一种贪心算法。G = (V, E)假设图G的节点为V， 带权值的边为E，算法的目的就是要在G中寻找一种分割将图分解为两个相同
的或者近似相同的两个子集A， B，且这种分割能够保持A，B之间的连线（子图分割的解S）权值之和最小。
该算法实际上是一种贪心算法，通过交换A B子图中的某些节点不断迭代优化某一值使得算法的解S最优。

## 设定
a为A集合的子集， 其中Ia是内部节点链接权重之和， Ea是内部节点与B集合之间链接权重之和。
而Da = Ea - Ia。同理，对于B集合也有Db = Eb - Ib。
而交换节点带来的损失以下式进行衡量， 其中Cab代表A、B两个集合之间的连接。
Told - Tnew = Da + Db - 2Cab
KL算法就是在不断迭代节点交换，使得Told - Tnew增大
## 伪代码
```shell
function Kernighan-Lin(G(V,E)):
  determine a balanced initial partition of the nodes into sets A and B
  do
    compute D values for all a in A and b in B
    let gv, av, and bv be empty lists
    for (n := 1 to |V|/2)
      find a from A and b from B, such that g = D[a] + D[b] - 2*c(a, b) is maximal
      remove a and b from further consideration in this pass
      add g to gv, a to av, and b to bv
      update D values for the elements of A = A \ a and B = B \ b
    end for
    find k which maximizes g_max, the sum of gv[1],...,gv[k]
    if (g_max > 0) then
      Exchange av[1],av[2],...,av[k] with bv[1],bv[2],...,bv[k]
    until (g_max <= 0)
  return G(V,E)
```
---
