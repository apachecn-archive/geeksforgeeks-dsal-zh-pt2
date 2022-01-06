# 迪尔沃斯定理

> 原文:[https://www.geeksforgeeks.org/dilworths-theorem/](https://www.geeksforgeeks.org/dilworths-theorem/)

设 S 是有限的[部分有序集](https://en.wikipedia.org/wiki/Partially_ordered_set)。**最大反链的大小等于最小链盖的大小。这就是所谓的[迪尔沃斯定理](https://en.wikipedia.org/wiki/Dilworth%27s_theorem)。它是以数学家罗伯特·p·迪尔沃斯(1950)的名字命名的。**

有限部分有序集 S 的宽度是 S 中反链的最大尺寸，换句话说，有限部分有序集 S 的宽度是覆盖 S 所需的最小链数，即使得 S 的任何元素都在至少一个链中的最小链数。

**链**的定义:部分有序集中的[链](http://aleph.math.louisville.edu/teaching/2009FA-681/notes-091119.pdf)是元素的子集，所有元素都可以相互比较。
**反链**的定义:一个[反链](https://en.wikipedia.org/wiki/Antichain)是元素的子集，没有两个元素可以互相比较。

示例:

```
Let S be the set of divisors of 30, with divisibility as the partial order. 
Then the following chains cover S : 
{1, 2, 6, 30}, {3, 15}, {5, 10}

And {2, 3, 5} is an antichain of length 3\. 
It is not immediately obvious, but the chain cover is minimal (though not unique), 
and the antichain is maximal (though not unique). 

So both definitions of width give 3 for this partially ordered set. 
```

**迪尔沃斯定理的证明:**
最简单的证明是通过对集合大小的归纳。设 d 为 S 的最大反链的大小，证明将表明 S 可以被 d 链覆盖。基本情况是微不足道的。所以假设结果已经被证明适用于所有小于 s 的集合。

首先，如果 S 的两个元素没有可比性，那么 S 本身就是一个反链，它可以被长度为 1 的 d = |S|链覆盖，所以结果成立。否则，设 M 为极小元素(m <= z 为所有可比 z)，M 为极大元素(z <= M 为所有可比 z)。让 T = S –{ M，M}。如果 T 中最大的反链的大小< = d–1，那么 T 可以被 d–1 链覆盖，所以 S 可以被那些加上链{m，M}的链覆盖，结果将被 S 证明。

现在，假设 T 中最大的反链的大小为 d(不能再大了，因为 T 是 S 的子集)。称之为反链 a。

其余证明的想法是:画出 S 的哈斯图，其中最大的反链由一个水平条带组成。把长条下面的东西和长条上面的东西都拿走，用感应用链条把这些盖住，然后把链条穿过长条连接在一起。

也就是说，构建这两个集合

S <sup>+</sup> = {x 属于 S:x > = a 对于某些 A 属于 A}
S<sup>–</sup>= { x 属于 S:x < = a 对于某些 A 属于 A }

那么 S<sup>+</sup>U<sup>–</sup>一定是 S 的全部，因为如果不是，那么 A 就不会是 S 中最大的反链，而 S<sup>+</sup>U<sup>–</sup>= A，因为如果 x 在交集中，那么 a < = x < = b 对于某些元素 A，b 属于 A，所以 A 和 b 在及物性上是可比较的，所以唯一的可能是 a = b，它们都等于 x。

由于 M 和 M 不在 A 中，必然是和 M 不属于 S+，M 不属于 S-所以两个集合)，且严格小于 S，归纳假设适用于 S<sup>–</sup>和 S <sup>+</sup> 两者，所以它们都被 d 链覆盖，每个链必须恰好包含 A 的一个元素，称它们为 C<sub>A</sub>T6–和 C<sub>A</sub>T10】+。现在我们可以通过链条 C<sub>a</sub><sup>–</sup>U { a } U C<sub>a</sub><sup>+</sup>将这些封面缝合在一起，得到所有 S 的封面。这个盖子有 d 链，所以结果是通过归纳得出的。

***代码来说明上面的例子:***
最长增子序列(LIS)的经典 O(N lg N)算法可以看作是迪尔沃斯定理的一个应用。参见此处。

参考资料: [Youtube 视频](https://www.youtube.com/watch?v=1-NW2fKIyLQ)