# 欧几里德引理

> 原文:[https://www.geeksforgeeks.org/euclids-lemma/](https://www.geeksforgeeks.org/euclids-lemma/)

给我们两个数字 x 和 y，我们知道一个数字 p 除以它们的乘积。我们能肯定地说 p 也分其中一个吗？

答案是否定的，比如考虑 x = 15，y = 6，p = 9。p 将乘积除以 15*6，但没有将它们中的任何一个分开。

**如果 p 是素数呢？**
**欧几里德引理**指出，如果一个素数 p 除了两个数(x*y)的乘积，它必须至少除其中一个数。

例如 x = 15，y = 6，p = 5。p 除积 15*6，它也除 15。

这个想法很简单，因为 p 是质数，所以不能分解。所以它要么完全存在于 x 中，要么存在于 y 中。

**欧几里德引理的推广:**
如果 p 除 x*y，p 相对于 x 是素数，那么 p 必须除 y，上例中，5 相对于 6 是素数，因此它必须除 15。

**参考:**T2[https://en.wikipedia.org/wiki/Euclid's_lemma](https://en.wikipedia.org/wiki/Euclid's_lemma)

如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论