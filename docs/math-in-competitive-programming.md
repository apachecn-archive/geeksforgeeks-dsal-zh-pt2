# 必须为竞争性编程做数学

> 原文:[https://www . geesforgeks . org/math-in-competitive-programming/](https://www.geeksforgeeks.org/math-in-competitive-programming/)

**C** 竞争 **P** 编程( **CP** )通常不需要知道高级微积分或一些火箭科学。但是有些概念和技巧在大多数时候是足够的。你绝对可以在没有任何数学背景的情况下开始竞争性编码。但是当你深入 CP 的世界时，数学变得至关重要。您将遇到的大多数竞争性编码问题都有一些数学逻辑或技巧。我们学习的所有算法都是从数学的角度推导出来的。大多数时候，数学帮助我们在必要的时间限制内解决问题。

不可能在一篇文章中涵盖所有的主题，但是我们将研究竞争编码中一些最常见的数学概念。这些概念中的一些乍一看可能太难了，但是把它们应用到问题上会让你轻松一些。

还有一点，我只提到了你需要覆盖的东西和一些技巧，但是你可以借助其他在线资源来学习和练习它们。

![](img/e054780daae5d5be37c4111005a438af.png)

**1 .big integer〔t1〕**

例如[计算大数的阶乘](https://www.geeksforgeeks.org/factorial-large-number/)(假设 100)或输入长度约为 100000 位的大数。在 c++中，即使我们使用 long long int，也不可能存储这些数字。取这种数字的一种方法是，更明智地将它们放入一个数组中，使用 vector …每个数字都有一个数组索引，就像如果这个数字是 12345，那么 12345%10=5 将在索引[4]中，这个数字现在=12345/10=1234。现在 1234%10=4 将在[3]中，以此类推到 1%10=1 在[0]中，或者您也可以使用 string，这更容易，因为 char 数组只允许每个索引有 1 个字节，所以您不需要那些调制操作来将数字放入索引中。

Java 提供了 [Biginteger](https://www.geeksforgeeks.org/biginteger-class-in-java/) 类来处理这个。

**2。**[**GCD**](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/)**[**LCM**](https://www.geeksforgeeks.org/lcm-gq/)**[**欧几里德算法，扩展欧几里德算法**](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/)****

****GCD 和 LCM 的定义是众所周知的，(而且是在中学教的)我就跳过定义了。另外，由于 lcm(a，b) * gcd(a，b) = a*b，计算 gcd 相当于计算 lcm。****

****现在，我们如何计算两个数字的 GCD？****

****我们当然可以找到这两个数的因子，然后确定最高公因数。然而，随着数字变大(比如 155566328819)，因式分解变得无效。****

****这就是欧几里德算法拯救我们的地方。该算法使用易于证明的事实 gcd(a，b)=gcd(b，r)，其中 r 是 a 除以 b 时的余数，或者只是 a%b。****

## ****C****

```
**int GCD(int A, int B)
{
    if (B == 0)
        return A;
    else
        return GCD(B, A % B);
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**static int GCD(int A, int B)
{
    if (B == 0)
        return A;
    else
        return GCD(B, A % B);
}

// This code is contributed by susmitamittal1329.**
```

## ****蟒蛇 3****

```
**def GCD(A, B):
    if (B == 0):
        return A
    else:
        return GCD(B, A % B)

      # This code is contributed by subham348.**
```

## ****C#****

```
**static int GCD(int A, int B)
{
    if (B == 0)
        return A;
    else
        return GCD(B, A % B);
}

// This code is contributed by subham348.**
```

## ****java 描述语言****

```
**function GCD(A, B)
{
    if (B === 0)
        return A;
    else
        return GCD(B, A % B);
}

// This code is contributed by subham348.**
```

****我们能找到数字(x，y)使得 ux + vy = gcd(u，v)吗？。存在无限多对——这是贝佐特的引理。生成这种对的算法称为扩展欧几里德算法。****

******3。** [**厄拉多塞筛**](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) **和** [**分段筛**](https://www.geeksforgeeks.org/segmented-sieve/)****

****在某些问题中，快速生成素数是非常重要的。让我们开门见山，介绍一下厄拉多塞的筛子。你可以用厄拉多塞筛找出所有小于或等于给定数 N 的素数，或者找出一个数是否是素数。****

****厄拉多塞筛背后的基本思想是，在每次迭代中，一个质数被拾取，它的所有倍数被消除。消除过程完成后，所有剩余的未标记数字都是质数。假设我们想找到 2 到 50 之间的所有素数。从 2 到 50 迭代。我们从 2 开始。既然没查，那就是质数。现在检查除 2 以外的所有倍数。现在我们继续，到第三个。没有勾选，所以是质数。现在检查除 3 以外的所有 3 的倍数。现在转到第 4 步。我们看到这是选中的–这是 2 的倍数！所以 4 不是质数。我们继续这样做。****

## ****卡片打印处理机（Card Print Processor 的缩写）****

```
**void sieve(int N)
{
    bool isPrime[N + 1];
    for (int i = 0; i& lt; = N; ++i) {
        isPrime[i] = true;
    }

    isPrime[0] = false;
    isPrime[1] = false;

    for (int i = 2; i * i <= N; ++i) {

        // Mark all the multiples of i as composite numbers
        if (isPrime[i] == true) {
            for (int j = i * i; j <= N; j += i)
                isPrime[j] = false;
        }
    }
}**
```

****如果数量很大(比如 10^16)，在这种情况下，我们需要分段筛选。****

****[分段筛](https://www.geeksforgeeks.org/segmented-sieve/)的思路是划分范围【0..n-1]并逐个计算所有段中的素数。这个算法首先用 Simple Sieve 来寻找小于等于的素数？(n)。以下是分段筛选中使用的步骤。****

****1.使用 Simple Sieve 查找所有的素数直到‘n’的平方根，并将这些素数存储在数组“prime[]”中。将找到的素数存储在数组“prime[]”中。****

****2.我们需要范围[0]内的所有素数..n-1]。我们把这个范围分成不同的部分，这样每个部分的大小最多为？n****

****3.对每个细分市场执行以下操作[低..高]****

****创建数组标记[高-低+1]。这里我们只需要 O(x)空间，其中 x 是给定范围内的元素数。****

****迭代第 1 步中找到的所有素数。对于每个质数，标记其在给定范围内的倍数[低..高】。****

****在简单筛选中，我们需要 O(n)空间，这对于大 n 可能是不可行的。n)空间，我们一次处理较小的范围****

******4。模算术，** [**模幂**](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/) **和** [**模逆**](https://www.geeksforgeeks.org/multiplicative-inverse-under-modulo-m/)****

****当一个数除以另一个数时，模运算得到余数。它由%符号表示。****

****例子****

****假设你有两个数字 10 和 3。10%3 是 1，因为当 10 除以 3 时，余数是 1。****

****性能****

****1.(a+b)%c = (a%c+b%c)%c****

****2.(一？b)%c = ((a%c)？(b%c))%c****

****3.(一？b)%c = ((a%c)？(b%c)+c)%c****

****4.(a/b)%c = ((a%c)？(b%c))%c****

****这些属性是什么时候使用的？****

****假设 a = 10^12，b = 10^12，c = 10^9+7.你必须找到(a？b)%c .当你将 a 乘以 b，答案是 10^24，这与标准的整数数据类型不相符。因此，为了避免这种情况，我们使用了属性。(一？b)%c = ((a%c)？(b%c))%c****

****快速模幂运算****

****用模数 m/o(对数 b)计算 a^b，****

****它使用 b 的二进制扩展，非常简单。****

## ****卡片打印处理机（Card Print Processor 的缩写）****

```
**ll expo(ll a, ll b, ll m)
{
    if (b == 0)
        return 1;
    ll p = expo(a, b / 2, m) % m;
    p = (p * p) % m;

    return (b % 2 == 0) ? p : (a * p) % m;
}**
```

****现在，我们来谈谈[模逆](https://www.geeksforgeeks.org/multiplicative-inverse-under-modulo-m/)。****

****利用扩展欧氏算法，我们可以得到模 m 的逆****

## ****卡片打印处理机（Card Print Processor 的缩写）****

```
**// Returns modulo inverse of a with respect
// to m using extended Euclid Algorithm
// Assumption: a and m are coprimes, i.e.,
// gcd(a, m) = 1
int modInverse(int a, int m)
{
    int m0 = m;
    int y = 0, x = 1;

    if (m == 1)
      return 0;

    while (a > 1)
    {
        // q is quotient
        int q = a / m;
        int t = m;

        // m is remainder now, process same as
        // Euclid's algo
        m = a % m, a = t;
        t = y;

        // Update y and x
        y = x - q * y;
        x = t;
    }

    // Make x positive
    if (x < 0)
       x += m0;

    return x;
}**
```

****[费马小定理](https://www.geeksforgeeks.org/fermats-little-theorem/)给出了 gcd(a，p)=1 时的 a^(p-1)==a (mod p)，其中 p 是素数。因此，我们也可以通过快速取幂来计算 a(a^(p-2)的模逆。****

******5。** [**卢卡斯定理**](https://www.geeksforgeeks.org/compute-ncr-p-set-2-lucas-theorem/)****

****利用卢卡斯定理，我们可以非常快速地计算模 p (p 是素数)中的 nCr。Lucas 定理基本上表明，nCr 的值可以通过将 n(i)Cr(i)相乘的结果来计算，其中 n(i)和 r(i)分别是 n 和 r 的基 p 表示中的单个相同位置的数字。当 p 很小，n，r 很大时，这是非常有效的。我们可以用上面的代码预先计算阶乘和阶乘模 p 的倒数。****

******6。** [**中国剩余定理<**](https://www.geeksforgeeks.org/chinese-remainder-theorem-set-1-introduction/)****

****两个数(正整数)a 和 b 是相对素数(互为素数)，如果它们没有共同的素数因子。数字 m1，m2，…如果集合中任何两个不同的数字相对素数，则 mr 是成对的相对素数。中国剩余定理说，给定任何 r 对相对素数 m1，m2，…mr，以及任何数字 b1，b2，b3，..br，我们总能找到一个数字 M，它留下了剩余的 b1，b2，b3，..br 分别除以 m1、m2、…mr。****

****让我们求解 x == r (mod mi)，其中 mi 是成对互素。****

****(如果它们不是互质，就把它们分解成素数幂，如果有些是矛盾的，就没有解。)****

******7。** [**系列和序列**](https://www.geeksforgeeks.org/mathematics-sequence-series-and-summations/)****

****你只需要知道一些基本知识，比如:****

****什么是系列，它是否收敛到某个值？****

****了解三角函数、双曲线等著名级数****

****如何计算著名级数如(几何级数、调和级数)的有限极限****

****对于序列来说，基本上是一样的，你只需要知道基本知识。****

****(技巧:使用 [OEIS](https://oeis.org/A001597) 站点)****

****我们有时会遇到这样的情况:各种编码问题可以简化成一个数学公式，但往往发现这个公式并不那么简单。OEIS 来了，请求救援。我们可以计算初始指数的项，即 n=0，1，2，3，…..然后可以用 OEIS 找到数学表达式。****

******8。** [**加泰罗尼亚数字**](https://www.geeksforgeeks.org/program-nth-catalan-number/)****

****加泰罗尼亚数字是一个自然数序列，有助于解决许多计数问题。以 n=0 开头的术语有:1，1，2，5，14，42，132，429，1430 …等等。****

****基于加泰罗尼亚数字的问题可能会出现在许多编码比赛中。所以深入了解加泰罗尼亚数字总是一个加分点。****

****加泰罗尼亚数字在形成组合学问题的封闭解方面有广泛的应用。一些例子是:****

****1.使用“n”个节点可以形成的二分搜索法树的数量是第 n 个加泰罗尼亚数字。****

****2.n+2 边的凸多边形通过连接任意 2 条边可以被切割成 2 个或更多三角形的方法数是第 n 个加泰罗尼亚数。****

****3.匹配给定“n”对的可能副命题的数目的封闭解是第 n 个加泰罗尼亚数。****

******9。** [**鸽子洞原理**](https://www.geeksforgeeks.org/discrete-mathematics-the-pigeonhole-principle/)****

****鸽子洞原理是组合数学中一个强有力的工具。但是这个想法很简单，可以用下面这个奇特的问题来解释。想象一下，三只鸽子需要被放入两个鸽笼。能做到吗？答案是肯定的，但有一个问题。问题是，不管鸽子如何摆放，其中一个鸽笼必须容纳不止一只鸽子。****

****这个逻辑可以推广到更大的数字。鸽子洞原则规定，如果有 n 只以上的鸽子被放入 n 个鸽子洞，那么一些鸽子洞必须包含一只以上的鸽子。尽管这一原则显而易见，但其含义却令人震惊。****

****例如，考虑以下语句“如果从整数 1 到 8 中选择五个数字，那么其中两个必须加起来等于九。”****

****说明:每个数字都可以和另一个数字配对，加起来就是九。总共有四对这样的数字:1 和 8，2 和 7，3 和 6，最后是 4 和 5。这五个数字中的每一个都属于这四对中的一对。根据鸽子洞原理，两个数字必须来自同一个配对——根据构造，其总和为 9。****

******10。**[](https://www.geeksforgeeks.org/inclusion-exclusion-various-applications/)****夹杂物排除原则********

******包含排除原理是一个非常基本的计数定理，各种编程竞赛中的许多问题都是基于它，包含排除原理的一个正式解释如下:******

******将 A 视为对象的集合，将|A|视为 A 中的对象数，类似地，对于 B，则集合 A 和 B 的对象集合的基数(当 A 和 B 都不相交时)可以表示为(对于 2 个有限集合) :******

******|AUB| = |A| + |B|******

******但是如果集合不是不相交的呢？******

******然后我们需要在计算 A 和 B 的基数时减去计算了两次的公共对象，新的形式将变成:******

******| aub | = | a |+| b | | a’b |******

******这是包含-排除原则最基本的形式。******

******但是有 2 套以上，比如说 n 套。******

******那么它可以表述为:******

******(包括=相加，排除=相减)******

******|A1 U A2 U A3 …..U AN| =(包括每个集合的计数、排除成对集合的计数、包括三元组集合的计数、排除四元组集合的计数……直到第 n 个元组被包括(如果是奇数)或排除(如果是偶数))******

******即|A1 U A2 U A3 …..u AN | =(| A1 |+| A2 |+| A3 |+| A4 |…+| AN |)–(| A1∪A2 |+| A1∪A3 |+| A1∪A4 |..+所有组合)+(| A1∪A2∪A3 |…所有组合)………。等等。******

******这个列表不是详尽的，但是这些概念在代码部队、代码厨师等的竞赛中非常有用..所以，带上你的笔、纸和笔记本电脑，开始练习吧。******

******快乐编码！******