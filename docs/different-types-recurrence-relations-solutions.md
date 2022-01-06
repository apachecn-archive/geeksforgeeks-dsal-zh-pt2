# 不同类型的递推关系及其求解

> 原文:[https://www . geesforgeks . org/different-type-recurrence-relations-solutions/](https://www.geeksforgeeks.org/different-types-recurrence-relations-solutions/)

在本文中，我们将看到如何使用不同的方法解决不同类型的递归关系。在理解本文之前，您应该对递归关系和不同的求解方法有所了解(参见:[最坏、平均和最佳情况](https://www.geeksforgeeks.org/analysis-of-algorithms-set-2-asymptotic-analysis/)、[渐近符号](https://www.geeksforgeeks.org/analysis-of-algorithms-set-3asymptotic-notations/)、[循环分析](https://www.geeksforgeeks.org/analysis-of-algorithms-set-4-analysis-of-loops/))。

**类型 1:分治递归关系–**
以下是一些基于分治的递归关系的例子。

```
T(n) = 2T(n/2) + cn
T(n) = 2T(n/2) + √n

```

使用 [**【主法】**](https://www.geeksforgeeks.org/analysis-algorithm-set-4-master-method-solving-recurrences/) 可以轻松解决这些类型的递归关系。
对于递推关系 T(n) = 2T(n/2) + cn，a = 2，b = 2，k =1。这里 logb(a) = log2(2) = 1 = k，因此复杂度为θ(nlog 2(n))。
类似于递推关系 T(n) = 2T(n/2) + √n，a = 2，b = 2，k =1/2 的值。这里 logb(a) = log2(2) = 1 > k，因此复杂度为θ(n)。

**类型 2:线性递归关系–**
以下是一些基于线性递归关系的递归关系的例子。

```
T(n) = T(n-1) + n for n>0 and T(0) = 1

```

这些类型的递归关系可以使用[替换方法](https://www.geeksforgeeks.org/analysis-algorithm-set-4-master-method-solving-recurrences/)轻松解决。
例如，

```
T(n) = T(n-1) + n
       = T(n-2) + (n-1) + n
       = T(n-k) + (n-(k-1))….. (n-1) + n

```

代入 k = n，我们得到

```
T(n) = T(0) + 1 + 2+….. +n = n(n+1)/2 = O(n^2) 

```

**类型 3:求解前的值替换–**
有时，递归关系无法使用替换、递归树或主方法等技术直接求解。因此，在求解前需要将递推关系转换成合适的形式。例如，

```
T(n) = T(√n) + 1

```

为了解决这种类型的复发，将 n = 2^m 代入公式:

```
T(2^m) = T(2^m /2) + 1
Let T(2^m) = S(m),
S(m) = S(m/2) + 1 

```

用主方法求解，我们得到

```
S(m) = Θ(logm)
As n = 2^m or m = log2(n),
T(n) = T(2^m) = S(m) = Θ(logm) = Θ(loglogn)

```

让我们根据所讨论的方法来讨论一些问题。

**Que–1。**汉诺塔问题的时间复杂度是多少？
(a)t(n)= o(sqrt(n))
(d)t(n)= o(n^2)
(c)t(n)= o(2^n)
(d)无

**解:**对于汉诺塔，T(n) = 2T(n-1) + c 对于 n > 1 和 T(1) = 1。解决这个问题，

```
T(n) = 2T(n-1) + c
        = 2(2T(n-2)+ c) + c  = 2^2*T(n-2) + (c + 2c)
       = 2^k*T(n-k) + (c + 2c + .. kc)
Substituting k = (n-1), we get
T(n) = 2^(n-1)*T(1) + (c + 2c + (n-1)c) = O(2^n)

```

**Que–2。**考虑以下递归:
T3】T(n)= 2 * T(ceil(sqrt(n)))+1，T(1)= 1T5】以下哪一项是正确的？
(A)T(n)=(loglog n)
(B)T(n)=(logn)
(C)T(n)=(sqrt(n))
(D)T(n)=(n)

**解:**为了求解这种类型的复发，将 n = 2^m 代入:

```
T(2^m) = 2T(2^m /2) + 1
Let T(2^m) = S(m),
S(m) = 2S(m/2) + 1 
Solving by master method, we get
S(m) = Θ(m)
As n = 2^m or m = log2n,
T(n) = T(2^m) = S(m) = Θ(m) = Θ(logn)

```