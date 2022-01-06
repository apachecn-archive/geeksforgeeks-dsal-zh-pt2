# 猜测确认的方法

> 原文:[https://www . geesforgeks . org/猜测和确认方法/](https://www.geeksforgeeks.org/method-of-guessing-and-confirming/)

这个方法背后的基本思路是**猜测答案**，然后**通过归纳证明正确。**此方法可用于解决任何复发。如果一个解决方案被猜测，然后试图归纳验证我们的猜测，通常要么证明会成功(在这种情况下，我们完成了)，要么证明会失败(在这种情况下，失败将帮助我们完善我们的猜测)。

例如，考虑循环:![T(N) = √N*T(√N) + N](img/c22e879fe3f7aa83b36b77d81f6ab97c.png "Rendered by QuickLaTeX.com")。这不符合[主定理](https://www.geeksforgeeks.org/analysis-algorithm-set-4-master-method-solving-recurrences/)所要求的形式。仔细观察递归给我们的印象是类似于分治法(把问题潜水到 *√N* 子问题中，每个子问题都有大小 *√N* )。可以看出，递归第一级子问题的规模为 *N* 。所以，让我们猜测一下![T(N) = O(N*log N)](img/38e7d6996751aa67a435a041b528c64a.png "Rendered by QuickLaTeX.com")，然后试着证明这个猜测是正确的。

我们先来证明一个上限:

> ![T(N) \le cN*logN:](img/acaaaf18deb766a49f9b4a2fd087b50e.png "Rendered by QuickLaTeX.com")
> 
> ![T(N) = √N*T(√N) + N](img/c22e879fe3f7aa83b36b77d81f6ab97c.png "Rendered by QuickLaTeX.com")
> 
> ![T(N) \le √N* c√N*log√N + N](img/dccba4bbfc4f388cef09ca355fb40718.png "Rendered by QuickLaTeX.com")
> 
> ![T(N) = N* clog√N + N](img/3d5e178e1f73cd9ccd71c4711426d8c1.png "Rendered by QuickLaTeX.com")
> 
> ![T(N) = N*1/2*c*log N + N](img/d0db3a044277b07bc06a4839d544b26d.png "Rendered by QuickLaTeX.com")
> 
> ![T(N) \le cN*log N](img/b1e11babd2019284a37868a38e615794.png "Rendered by QuickLaTeX.com")

最后一个不等式只假设![1 \le 1/2*clog N](img/2c7d40e6bb23af3372c98569181ac614.png "Rendered by QuickLaTeX.com")。如果 *N* 足够大，并且对于任何常数 c，无论多小，这都是正确的。

从上面的证明可以看出，我们的猜想对于上限是正确的。现在，让我们证明这个递归的下界:

> ![T(N) = √N*T(√N) + N](img/c22e879fe3f7aa83b36b77d81f6ab97c.png "Rendered by QuickLaTeX.com")
> 
> ![T(N) \ge  √N* k√N*log√N + N](img/b0f0137245091bc696106914877c1ee0.png "Rendered by QuickLaTeX.com")
> 
> ![T(N) = N* klog√N + N](img/8db33a80e6914620aa5139d30cfaf1b8.png "Rendered by QuickLaTeX.com")
> 
> ![T(N) = N*1/2*k*log N + N](img/d068f027a74972cd13a3f0b16f0f9d45.png "Rendered by QuickLaTeX.com")
> 
> ![T(N) \ge  N*k*log N](img/33a206e3389f4db098e2006222399740.png "Rendered by QuickLaTeX.com")

最后一个不等式只假设![1 \ge  1/2*k*log N](img/903198139ffe4b0b65b400f800436eab.png "Rendered by QuickLaTeX.com")。如果 *N* 足够大并且对于任何常数 k，这是不正确的

从上面的证明可以看出，我们的猜想对于下界是不正确的。

从上面的讨论可以理解![Θ(N*log N)](img/5d02a5f16159bbc73ef52839d89585de.png "Rendered by QuickLaTeX.com")太大了。但是![Θ(N)](img/3fec4c6b6aee024ff6a7bd29fafedd4f.png "Rendered by QuickLaTeX.com")呢？下界很容易直接证明:

> ![T(N) = √N*T(√N) + N \ge  N](img/4172ea019ce3e6d3527a5cf80da73384.png "Rendered by QuickLaTeX.com")

现在，让我们证明这个θ(N)的上限:
![T(N) = √N*T(√N) + N\\ \le √N*c√N + N\\ = N c+ N\\ = N (c + 1)\\ \nleq cN](img/2c5ca09368867a217c34f3f2cd3342a8.png "Rendered by QuickLaTeX.com")

从上面的归纳可以理解为![Θ(N)](img/3fec4c6b6aee024ff6a7bd29fafedd4f.png "Rendered by QuickLaTeX.com")太小，![Θ(N*log N)](img/5d02a5f16159bbc73ef52839d89585de.png "Rendered by QuickLaTeX.com")太大。所以，我们需要比 N 大，比![N*log N](img/2ea3b974e3b23a237a936336eacae76a.png "Rendered by QuickLaTeX.com")小的东西？![N*√log N](img/d7ec389854b4dfe3e9f0464d18d74742.png "Rendered by QuickLaTeX.com")怎么样？

证明![N*√log N](img/d7ec389854b4dfe3e9f0464d18d74742.png "Rendered by QuickLaTeX.com")的上限:

> ![T(N) = √N*T(√N) + N](img/c22e879fe3f7aa83b36b77d81f6ab97c.png "Rendered by QuickLaTeX.com")
> 
> ![T(N) \le √n*c√N*√(log √N) + N](img/2d253f6539f63997e23c00061549522f.png "Rendered by QuickLaTeX.com")
> 
> ![T(N) = N* 1/√2 *c*log √N + N](img/9584c124d8250e01cf8bf65987566e89.png "Rendered by QuickLaTeX.com")
> 
> ![T(N) \le N*c*log √N](img/646614862631c8d1d3ffcb64c65a8ab2.png "Rendered by QuickLaTeX.com")

证明![N*√log N](img/d7ec389854b4dfe3e9f0464d18d74742.png "Rendered by QuickLaTeX.com")的下限:

> ![T(N) = √N*T(√N) + N](img/c22e879fe3f7aa83b36b77d81f6ab97c.png "Rendered by QuickLaTeX.com")
> 
> ![T(N) \ge  √N*k√N*√(log√N) + N](img/236bf5afaf7617680cba79eda9daf1e9.png "Rendered by QuickLaTeX.com")
> 
> ![T(N) = N*1/√2*k*log √N + N](img/5f0848970789610b4293bc6a0ac57760.png "Rendered by QuickLaTeX.com")
> 
> ![T(N) \ngeq N*k*log √N](img/668244242a8f81f50d1c524d4ac001c8.png "Rendered by QuickLaTeX.com")

最后一步不管用。所以，![Θ(N*√log N)](img/59b69f1a6010015c39fe9150466734e5.png "Rendered by QuickLaTeX.com")不起作用。N 和![N*log N](img/2ea3b974e3b23a237a936336eacae76a.png "Rendered by QuickLaTeX.com")之间还有什么？![N*log(log N)](img/61302b4be2e17c5ba9d9540f734e316b.png "Rendered by QuickLaTeX.com")怎么样？

证明![N*log(log N)](img/61302b4be2e17c5ba9d9540f734e316b.png "Rendered by QuickLaTeX.com")的上限:

> ![T(N) = √N*T(√N) + N](img/c22e879fe3f7aa83b36b77d81f6ab97c.png "Rendered by QuickLaTeX.com")
> ![T(N) \le √N*c√N*log(log √N) + N](img/fac61d4c99511ad588b47cbd2b862847.png "Rendered by QuickLaTeX.com")
> ![T(N) = N*clog(log N) - cN + N](img/131d81c40a6570cb8c63cdcc84ef049c.png "Rendered by QuickLaTeX.com")
> ![T(N) \le N*clog(log N), if \ c\ge 1](img/ae54058d12c3036811d8016248089b02.png "Rendered by QuickLaTeX.com")

证明![N*log(log N)](img/61302b4be2e17c5ba9d9540f734e316b.png "Rendered by QuickLaTeX.com")的下限:

> ![T(N) = √N*T(√N) + N](img/c22e879fe3f7aa83b36b77d81f6ab97c.png "Rendered by QuickLaTeX.com")
> 
> ![T(N) \ge  √N*k√N*log(log √N) + N](img/914ca10a790caae0ee59169253befba7.png "Rendered by QuickLaTeX.com")
> 
> ![T(N) = N*k*log(log N) - kN + N](img/908836c9e07a20f026ab9d16b3bc0827.png "Rendered by QuickLaTeX.com")
> 
> ![T(N) \ge  N*klog(log N), if \ k \le 1](img/820f1db4ec1f43a4bad80e540f4ccb0d.png "Rendered by QuickLaTeX.com")

从以上证明可以看出![T(N) \le N*clog(log N), if \ c \ge  1](img/46bc217380ad041634608501263efdbd.png "Rendered by QuickLaTeX.com")和![T(N) \ge  N*klog(log N), if \ k \le 1](img/820f1db4ec1f43a4bad80e540f4ccb0d.png "Rendered by QuickLaTeX.com")。
从技术上来说，我们仍然缺少两个证据中的基本情况，但是我们可以相当有信心在这一点上![T(N) = Θ(N*log(log N))](img/e506c3b986d9d5152b4acd10f9312d0e.png "Rendered by QuickLaTeX.com")。