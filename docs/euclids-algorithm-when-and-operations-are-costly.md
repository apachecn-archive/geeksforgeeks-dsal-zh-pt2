# 当%和/运算成本高时的欧几里德算法

> 原文:[https://www . geeksforgeeks . org/euclids-算法和操作成本高/](https://www.geeksforgeeks.org/euclids-algorithm-when-and-operations-are-costly/)

[欧几里德算法](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/)用于求两个数的 GCD。
算法主要有两个版本。
**版本 1(使用减法)**

## C

```
// Recursive function to return gcd of a and b
int gcd(int a, int b)
{
    if (a == b) 
       return a;

    return (a > b)? gcd(a-b, b): gcd(a, b-a);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive function to return gcd of a and b
static int gcd(int a, int b)
{
    if (a == b)
        return a;

    return (a > b) ? gcd(a - b, b) : gcd(a, b - a);
}

// This code is contributed by subham348.
```

## 蟒蛇 3

```
# Recursive function to return gcd of a and b
def gcd(a, b):
    if (a == b):
        return a

    return gcd(a-b, b) if (a > b) else gcd(a, b-a)

  # This code is contributed by subham348.
```

## C#

```
// Recursive function to return gcd of a and b
static int gcd(int a, int b)
{
    if (a == b)
        return a;

    return (a > b) ? gcd(a - b, b) : gcd(a, b - a);
}

// This code is contributed by subham348.
```

## java 描述语言

```
// Recursive function to return gcd of a and b
function gcd(a, b)
{
    if (a === b) 
       return a;

    return (a > b)? gcd(a-b, b): gcd(a, b-a);
}

// This code is contributed by subham348.
```

**版本 2(使用模运算符)**

## C

```
// Function to return gcd of a and b
int gcd(int a, int b)
{
    if (a == 0)
       return b;

    return gcd(b%a, a);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Function to return gcd of a and b
static int gcd(int a, int b)
{
    if (a == 0)
       return b;

    return gcd(b%a, a);
}

// This code is contributed by subham348.
```

## C#

```
// Function to return gcd of a and b
static int gcd(int a, int b)
{
    if (a == 0)
       return b;

    return gcd(b%a, a);
}

// This code is contributed by subham348.
```

## java 描述语言

```
// Function to return gcd of a and b
function gcd(a, b)
{
    if (a === 0)
       return b;

    return gcd(b%a, a);
}

// This code is contributed by subham348.
```

**以上两者哪个效率更高？**
版本 1 可以用线性时间找到 GCD，考虑一个给定数字比另一个大很多的情况。版本 2 显然更有效，因为递归调用更少，并且需要对数时间。
**考虑一个不允许模运算符的情况，我们能不能优化版本 1 让它工作得更快？**
下面是一些重要的观察。想法是使用按位运算符。我们可以用 x > > 1 找到 x/2。我们可以使用 x & 1 来检查 x 是奇数还是偶数。
如果 a 和 b 都是偶数，gcd(a，b) = 2*gcd(a/2，b/2)。
如果 a 为偶数，b 为奇数，则 gcd(a，b) = gcd(a/2，b)。
如果 a 为奇数，b 为偶数，则 gcd(a，b) = gcd(a，b/2)。
下面是 C++实现。

## C

```
// Efficient C++ program when % and / are not allowed
int gcd(int a, int b)
{
    // Base cases
    if (b == 0 || a == b) return a;
    if (a == 0) return b;

    // If both a and b are even, divide both a
    // and b by 2.  And multiply the result with 2
    if ( (a & 1) == 0 && (b & 1) == 0 )
       return gcd(a>>1, b>>1) << 1;

    // If a is even and b is odd, divide a by 2
    if ( (a & 1) == 0 && (b & 1) != 0 )
       return gcd(a>>1, b);

    // If a is odd and b is even, divide b by 2
    if ( (a & 1) != 0 && (b & 1) == 0 )
       return gcd(a, b>>1);

    // If both are odd, then apply normal subtraction
    // algorithm.  Note that odd-odd case always
    // converts odd-even case after one recursion
    return (a > b)? gcd(a-b, b): gcd(a, b-a);
}
```

本文由希瓦姆·阿格拉瓦尔编辑。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息