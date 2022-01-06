# 二叉树的计数

> 原文:[https://www.geeksforgeeks.org/enumeration-of-binary-trees/](https://www.geeksforgeeks.org/enumeration-of-binary-trees/)

如果每个节点都被分配了一个标签，二叉树就被标记，如果节点没有被分配任何标签，二叉树就不被标记。

```
Below two are considered same unlabelled trees
    o                 o
  /   \             /   \ 
 o     o           o     o 

Below two are considered different labelled trees
    A                C
  /   \             /  \ 
 B     C           A    B 
```

**有 n 个节点可以有多少个不同的未标记二叉树？**

```
For n  = 1, there is only one tree
   o

For n  = 2, there are two trees
   o      o
  /        \  
 o          o

For n  = 3, there are five trees
    o      o           o         o      o
   /        \         /  \      /         \
  o          o       o    o     o          o
 /            \                  \        /
o              o                  o      o
```

其思想是考虑左右子树中节点的所有可能的计数对，并将特定对的计数相乘。最后，添加所有对的结果。

```
For example, let T(n) be count for n nodes.
T(0) = 1  [There is only 1 empty tree]
T(1) = 1
T(2) = 2

T(3) =  T(0)*T(2) + T(1)*T(1) + T(2)*T(0) = 1*2 + 1*1 + 2*1 = 5

T(4) =  T(0)*T(3) + T(1)*T(2) + T(2)*T(1) + T(3)*T(0)
     =  1*5 + 1*2 + 2*1 + 5*1 
     =  14 
```

以上模式基本代表了[第 n 个加泰罗尼亚数字](https://www.geeksforgeeks.org/program-nth-catalan-number/)。前几个加泰罗尼亚数字是 1 1 2 5 14 42 132 429 1430 4862、…
![T(n)=\sum_{i=1}^{n}T(i-1)T(n-i)=\sum_{i=0}^{n-1}T(i)T(n-i-1)=C_n    ](img/92a2c57ce1ae2c402c005ad3d00977a4.png "Rendered by QuickLaTeX.com")
这里，
T(i-1)代表左边子树上的节点数
T(n I-1)代表右边子树上的节点数

第 n 个加泰罗尼亚数字也可以用直接公式计算。

```
   T(n) = (2n)! / (n+1)!n!
```

具有 n 个节点的二分搜索法树的数量也与未标记树的数量相同。原因很简单，在 BST 中，我们也可以将任何键作为根，如果根是排序顺序中的第 I 个键，那么 i-1 个键可以放在一边，而(n-i)个键可以放在另一边。

**有 n 个节点的有标签二叉树可以有多少棵？**
要计数已标记的树，我们可以对未标记的树使用上面的计数。思路很简单，每一个有 n 个节点的无标签树都可以创建 n 个！通过给所有节点分配不同的标签排列来创建不同的标签树。

因此，

```
Number of Labelled Trees = (Number of unlabelled trees) * n!
                       = [(2n)! / (n+1)!n!]  × n!
```

比如 n = 3，就有 5 * 3！= 5*6 = 30 个不同的标签树

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息