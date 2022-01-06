# 计算 GCD 等于给定数的自然数对

> 原文:[https://www . geesforgeks . org/count-pairs-natural-numbers-gcd-equal-given-number/](https://www.geeksforgeeks.org/count-pairs-natural-numbers-gcd-equal-given-number/)

给定三个正整数 **L** 、 **R** 、 **G** 。任务是找出 GCD(x，y) = G 且 x，y 位于 L 和 r 之间的对(x，y)的计数。
示例:

```
Input : L = 1, R = 11, G = 5
Output : 3
(5, 5), (5, 10), (10, 5) are three pair having GCD equal to 5 and lie between 1 and 11.
So answer is 3.

Input : L = 1, R = 10, G = 7
Output : 1
```

一个**简单的解决方法**是遍历【L，R】中的所有对。对于每一对，找到它的 GCD。如果 GCD 等于 g，则递增计数。最后返回计数。
一个**有效的解决方案**是基于这样一个事实，对于任何正整数对(x，y)来说，GCD 等于 g，x 和 y 应该被 g 整除
观察，L 和 R 之间最多会有(R–L)/g 的数可以被 g 整除
所以我们找到 L 和 R 之间可以被 g 整除的数。为此，我们从 ceil(L/g) * g 开始，在每一步递增 g，同时不超过 R，计算 GCD 等于 g 的数
同样，

```
ceil(L/g) * g = floor((L + g - 1) / g) * g.
```

以下是上述思路的实现:

## C++

```
// C++ program to count pair in range of natural
// number having GCD equal to given number.
#include <bits/stdc++.h>
using namespace std;

// Return the GCD of two numbers.
int gcd(int a, int b)
{
    return b ? gcd(b, a % b) : a;
}

// Return the count of pairs having GCD equal to g.
int countGCD(int L, int R, int g)
{
    // Setting the value of L, R.
    L = (L + g - 1) / g;
    R = R/ g;

    // For each possible pair check if GCD is 1.
    int ans = 0;
    for (int i = L; i <= R; i++)
        for (int j = L; j <= R; j++)
            if (gcd(i, j) == 1)
                ans++;

    return ans;
}

// Driven Program
int main()
{
    int L = 1, R = 11, g = 5;
    cout << countGCD(L, R, g) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count pair in
// range of natural number having
// GCD equal to given number.
import java.util.*;

class GFG {

// Return the GCD of two numbers.
static int gcd(int a, int b)
{
    return b > 0 ? gcd(b, a % b) : a;
}

// Return the count of pairs
// having GCD equal to g.
static int countGCD(int L, int R, int g) {

    // Setting the value of L, R.
    L = (L + g - 1) / g;
    R = R / g;

    // For each possible pair check if GCD is 1.
    int ans = 0;
    for (int i = L; i <= R; i++)
    for (int j = L; j <= R; j++)
        if (gcd(i, j) == 1)
        ans++;

    return ans;
}

// Driver code
public static void main(String[] args) {

    int L = 1, R = 11, g = 5;
    System.out.println(countGCD(L, R, g));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to count
# pair in range of natural
# number having GCD equal
# to given number.

# Return the GCD of two numbers.
def gcd(a,b):

    return gcd(b, a % b) if b>0 else a

# Return the count of pairs
# having GCD equal to g.
def countGCD(L,R,g):

    # Setting the value of L, R.
    L = (L + g - 1) // g
    R = R// g

    # For each possible pair
    # check if GCD is 1.
    ans = 0
    for i in range(L,R+1):
        for j in range(L,R+1):
            if (gcd(i, j) == 1):
                ans=ans +1

    return ans

# Driver code

L = 1
R = 11
g = 5

print(countGCD(L, R, g))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to count pair in
// range of natural number having
// GCD equal to given number.
using System;

class GFG {

// Return the GCD of two numbers.
static int gcd(int a, int b)
{
    return b > 0 ? gcd(b, a % b) : a;
}

// Return the count of pairs
// having GCD equal to g.
static int countGCD(int L, int R,
                    int g)
{

    // Setting the value of L, R.
    L = (L + g - 1) / g;
    R = R / g;

    // For each possible pair
    // check if GCD is 1.
    int ans = 0;
    for (int i = L; i <= R; i++)
    for (int j = L; j <= R; j++)
        if (gcd(i, j) == 1)
        ans++;

    return ans;
}

// Driver code
public static void Main()
{

    int L = 1, R = 11, g = 5;
    Console.WriteLine(countGCD(L, R, g));
}
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count pair
// in range of natural number
// having GCD equal to given number.

// Return the GCD of two numbers.
function gcd( $a, $b)
{
    return $b ? gcd($b, $a % $b) : $a;
}

// Return the count of pairs
// having GCD equal to g.
function countGCD( $L, $R, $g)
{

    // Setting the value of L, R.
    $L = ($L + $g - 1) / $g;
    $R = $R/ $g;

    // For each possible pair
    // check if GCD is 1.
    $ans = 0;
    for($i = $L; $i <= $R; $i++)
        for($j = $L; $j <= $R; $j++)
            if (gcd($i, $j) == 1)
                $ans++;

    return $ans;
}

    // Driver Code
    $L = 1;
    $R = 11;
    $g = 5;
    echo countGCD($L, $R, $g);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript program to count pair in
    // range of natural number having
    // GCD equal to given number.

    // Return the GCD of two numbers.
    function gcd(a, b)
    {
        return b > 0 ? gcd(b, a % b) : a;
    }

    // Return the count of pairs
    // having GCD equal to g.
    function countGCD(L, R, g)
    {

        // Setting the value of L, R.
        L = parseInt((L + g - 1) / g, 10);
        R = parseInt(R / g, 10);

        // For each possible pair
        // check if GCD is 1.
        let ans = 0;
        for (let i = L; i <= R; i++)
        for (let j = L; j <= R; j++)
            if (gcd(i, j) == 1)
            ans++;

        return ans;
    }

    let L = 1, R = 11, g = 5;
    document.write(countGCD(L, R, g));

</script>
```

输出:

```
3
```

本文由 [**Anuj Chauhan**](https://www.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。