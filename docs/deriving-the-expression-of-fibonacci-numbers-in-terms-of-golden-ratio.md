# 用黄金分割率推导斐波那契数的表达式

> 原文:[https://www . geeksforgeeks . org/推导黄金分割率中斐波那契数的表达式/](https://www.geeksforgeeks.org/deriving-the-expression-of-fibonacci-numbers-in-terms-of-golden-ratio/)

**先决条件:** [生成函数](https://en.wikipedia.org/wiki/Generating_function)[斐波那契数](https://www.geeksforgeeks.org/interesting-facts-fibonacci-numbers/)[寻找斐波那契数的方法](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。

利用[生成函数](https://en.wikipedia.org/wiki/Generating_function)求解著名且有用的[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)递推的方法，本文已经讨论过了。

**生成函数**是解决各种数学问题的强大工具，包括计数问题。它是一个正式的幂级数。例如，在计算问题时，我们经常对寻找大小物体的数量感兴趣![n](img/42ce0a847b20a2f8a781c8a50bdab975.png "Rendered by QuickLaTeX.com")。在这种情况下，我们定义一个幂级数，简单来说就是一个无限项多项式，其中![nth](img/44b991dc2175a809c6a2e3e44fc1b4cc.png "Rendered by QuickLaTeX.com")次项的系数是序列的![nth](img/44b991dc2175a809c6a2e3e44fc1b4cc.png "Rendered by QuickLaTeX.com")项。这有助于我们发现许多有趣而重要的结果。需要注意的是，在使用母函数时，我们一般使用母函数幂级数中的系数，很少使用级数中的变量。在这个职位上，我们也将这样做。某些 a <sub>n</sub> 的普通生成函数是:

> ![\mathcal{G}(a_{n};x) = \sum_{n=0}^{\infty}a_{n}x^n](img/984edab8825dfa724f9699e44c225c4e.png "Rendered by QuickLaTeX.com")

[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)是数学中的基本数列之一，人们已经发现了许多方法来找出这个数列的高阶项。这篇文章讨论了这样一种方法。

让我们首先为斐波那契数定义一个生成函数，然后将该函数简化以得到一个递归。利用这一点，扩展简化并将其分解为部分分数，然后使用两个标准幂级数，然后将它们结合起来，得出斐波那契数列![ith](img/117450c664a576148a7d81723ff2e253.png "Rendered by QuickLaTeX.com")项的惊人结果。

让我们将生成函数![\mathcal{F}](img/e754af8d99b13e8aed0be468d0cc98b4.png "Rendered by QuickLaTeX.com")定义为

> ![\mathcal{F}(z) = \sum_{i=0}^{\infty}F_{i}z^i](img/4710e995370d982af46cd5e417c7e78d.png "Rendered by QuickLaTeX.com")
> 
> ![\mathcal{F}(z) = 0 + z + z^2 + 2z^3 + 3z^4 + 5z^5 + 8z^6 + ... \infty](img/cdc6099f5ee87c596fc1532bcc14f4ac.png "Rendered by QuickLaTeX.com")，
> 
> 其中![F_{i}](img/ac443dffc4a5e3517cd38a00baeffaa9.png "Rendered by QuickLaTeX.com")是第 I 个斐波那契数。

因为，

![\mathcal{F}(z) = z + z^2 + 2z^3 + 3z^4 + 5z^5 + 8z^6 + ... \infty](img/7a1292fab36d7becc02589e0e9f72080.png "Rendered by QuickLaTeX.com")。

![\mathcal{F}(z) = z + (1 + 0)z^2 + (1 + 1)z^3 + (2 + 1)z^4 + (3 + 2)z^5 + (5 + 3)z^6 + ... \infty](img/7601447b5a8d85b531eba1eeaca9dfe9.png "Rendered by QuickLaTeX.com")。

重新排列我们得到的，

![\mathcal{F}(z) = z + [z^2 + z^3 + 2z^4 + 3z^5 + 5z^6 + ... \infty] + [0 + z^3 + z^4 + 2z^5 + 3z^6 + ... \infty]](img/12e090d559b564effa3b75bafe1c2ec9.png "Rendered by QuickLaTeX.com")。

用通用术语来说，

![\mathcal{F}(z) = z + (z)[z + z^2 + 2z^3 + 3z^4 + 5z^5 + ... \infty]](img/391fe8b7aa0e0aa497213d62a9bdba44.png "Rendered by QuickLaTeX.com")
![+ (z^2)[0 + z^1 + z^2 + z^3 + 3z^4 + ... \infty]](img/d0e877b5453783d6a16ef2b299b79fa9.png "Rendered by QuickLaTeX.com")

进一步简化，得到下面的函数。

![\mathcal{F}(z) = z + z\mathcal{F}(z) + z^2\mathcal{F}(z)](img/95f1cece4116b736a83df1a6c9ff8000.png "Rendered by QuickLaTeX.com")。

求解![\mathcal{F}(z)](img/b08e269ef2fb3336bac4e396ce370d60.png "Rendered by QuickLaTeX.com")，我们得到:

![\mathcal{F}(z) = \frac{z}{1-z-z^2}](img/170d89953800f4c387bd029e841dffd0.png "Rendered by QuickLaTeX.com")。

通过以上运算，我们得到以下公式:

> ![1-z-z^2 = -(z + \phi)(z + \widehat{\phi})](img/3f7879766e64c3e643270c1c4b5bfbe6.png "Rendered by QuickLaTeX.com")，
> 
> 其中，![\phi = \frac{1+\sqrt{5}}{2}](img/8d138b2efa47b8a98fa45276f7016f1e.png "Rendered by QuickLaTeX.com")和![\widehat{\phi} = \frac{1-\sqrt{5}}{2}](img/373cdf713c6e9982215179a85ced20dc.png "Rendered by QuickLaTeX.com")。

因此，

![\mathcal{F}(z) = \frac{-z}{(z + \phi)(z + \widehat{\phi})}](img/d114c7542e4d53e65a959f21fe1798f3.png "Rendered by QuickLaTeX.com")
还要注意的是，

![\phi\widehat{\phi} = -1](img/066d9034734a63a174334c6e00ed0e1d.png "Rendered by QuickLaTeX.com")。

因此，保持上面表达式中的关系，我们得到，

![\mathcal{F}(z) = \frac{z}{(1-z\phi)(1 - z\widehat{\phi})}](img/9af6c68f83debb6b9eb7a2991eb39da4.png "Rendered by QuickLaTeX.com")。

现在，上面表达式的右边可以分成部分分数，

![\mathcal{F}(z) = \frac{1}{\sqrt{5}}\left [ \frac{1}{(1-\phi z)} - \frac{1}{(1-\widehat{\phi} z)}\right ]](img/58db6900b02ada2ad2c4665a1ee7a00f.png "Rendered by QuickLaTeX.com")。

在两个分数上使用[展开](https://en.wikipedia.org/wiki/Series_expansion)，

![\frac{1}{(1-\phi z)} = 1 + \phi z + \phi ^2 z^2 + \phi ^3 z^3 + ... \infty = \sum_{i=0}^{\infty}\phi ^iz^i](img/c6d0117677352d036fbbbffe54d6a8c5.png "Rendered by QuickLaTeX.com")。

同样的，

![\frac{1}{(1-\widehat{\phi} z)} = 1 + \widehat{\phi} z + \widehat{\phi} ^2 z^2 + \widehat{\phi} ^3 z^3 + ... \infty = \sum_{i=0}^{\infty}\widehat{\phi} ^iz^i](img/8a57f4fd03d451d116d1e3fbbaa50f7f.png "Rendered by QuickLaTeX.com")。

因此，

![\mathcal{F}(z) = \sum_{i=0}^{\infty}\frac{1}{\sqrt{5}}(\phi ^iz^i - \widehat{\phi} ^iz^i)](img/8a8375f44039cd67b061752990ee3857.png "Rendered by QuickLaTeX.com")。

因此，

![F_{i} = \frac{1}{\sqrt{5}}(\phi ^i - \widehat{\phi} ^i)](img/9fc4276f6968cd699cd41c1ac9e3e3be.png "Rendered by QuickLaTeX.com")。

现在，

![\left | \phi \right |  < 1](img/8a10646f6ee90224e9856a7e7b46ce6a.png "Rendered by QuickLaTeX.com")，

还有，

![\left | \frac{\widehat{\phi} ^i}{\sqrt{5}} \right | < \left | \frac{\phi ^i}{\sqrt{5}} \right | < \frac{1}{2}](img/f24608212002b9f78a57c59f5d5ff3ed.png "Rendered by QuickLaTeX.com")

利用以上两个事实，可以有把握地得出结论

> ![F_{i} = \frac{\phi ^i}{\sqrt{5}}](img/8191801f3d3a904298a44e779c750a8c.png "Rendered by QuickLaTeX.com")，四舍五入到最接近的整数。

[利用黄金分割比](https://www.geeksforgeeks.org/find-nth-fibonacci-number-using-golden-ratio/)求第 n 个斐波那契数就是这个公式的应用之一。