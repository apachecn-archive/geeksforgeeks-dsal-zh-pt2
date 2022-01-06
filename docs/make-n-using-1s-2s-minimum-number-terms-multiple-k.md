# 用最小项数为 k 倍数的 1s 和 2s 做 n

> 原文:[https://www . geesforgeks . org/make-n-using-1s-2s-最小数量-术语-multiple-k/](https://www.geeksforgeeks.org/make-n-using-1s-2s-minimum-number-terms-multiple-k/)

给定两个正整数 **n** 和 **k** 。n 可以用多种方式表示为 1 和 2 的和，使用多个项。任务是找到 1 和 2 的最小项数，用于计算 n 的和，并且项数必须是 k 的倍数。如果不存在这样的项数，请打印“-1”。
**例:**

```
Input : n = 10, k = 2
Output : 6
10 can be represented as 2 + 2 + 2 + 2 + 1 + 1.
Number of terms used are 6 which is multiple of 2.

Input : n = 11, k = 4
Output : 8
10 can be represented as 2 + 2 + 2 + 1 + 1 + 1 + 1 + 1
Number of terms used are 8 which is multiple of 4.
```

注意，当 1 被相加 n 次时，表示 n 为 1 和 2s 之和的最大项数是 n。此外，术语的最小数量将是 2 的 n/2 倍，并且添加了 n%2 倍的 1。所以，从最小项数迭代到最大项数，检查是否有 k 的倍数

## C++

```
// C++ program to find minimum multiple of k
// terms used to make sum n using 1s and 2s.
#include<bits/stdc++.h>
using namespace std;

// Return minimum multiple of k terms used to
// make sum n using 1s and 2s.
int minMultipleK(int n, int k)
{
    // Minimum number of terms required to make
    // sum n using 1s and 2s.
    int min = (n / 2) + (n % 2);

    // Iterate from Minimum to maximum to find
    // multiple of k. Maximum number of terns is
    // n (Sum of all 1s)
    for (int i = min; i <= n; i++)
        if (i % k == 0)
            return i;

    return -1;
}

// Driven Program
int main()
{
    int n = 10, k = 2;
    cout << minMultipleK(n, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum
// multiple of k terms used to
// make sum n using 1s and 2s.
import java.io.*;

class GFG
{

// Return minimum multiple of
// k terms used to make sum n
// using 1s and 2s.
static int minMultipleK(int n,
                        int k)
{
    // Minimum number of terms
    // required to make sum n
    // using 1s and 2s.
    int min = (n / 2) + (n % 2);

    // Iterate from Minimum to
    // maximum to findmultiple of k.
    // Maximum number of terms is
    // n (Sum of all 1s)
    for (int i = min; i <= n; i++)
        if (i % k == 0)
            return i;

    return -1;
}

// Driver Code
public static void main (String[] args)
{
    int n = 10, k = 2;
    System.out.println( minMultipleK(n, k));
}
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python3 program to find minimum multiple of k
# terms used to make sum n using 1s and 2s.

# Return minimum multiple of k terms
# used to make sum n using 1s and 2s.
def minMultipleK( n, k):

    # Minimum number of terms required
    # to make sum n using 1s and 2s.
    min = (n // 2) + (n % 2)

    # Iterate from Minimum to maximum to find
    #multiple of k. Maximum number of terns is
    # n (Sum of all 1s)
    for i in range(min, n + 1):
        if (i % k == 0):
            return i

    return -1

# Driver Code
if __name__=="__main__":

    n = 10
    k = 2
    print (minMultipleK(n, k))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find minimum
// multiple of k terms used to
// make sum n using 1s and 2s.
using System;

class GFG
{

// Return minimum multiple of
// k terms used to make sum n
// using 1s and 2s.
static int minMultipleK(int n,
                        int k)
{
    // Minimum number of terms
    // required to make sum n
    // using 1s and 2s.
    int min = (n / 2) + (n % 2);

    // Iterate from Minimum to
    // maximum to findmultiple of k.
    // Maximum number of terms is
    // n (Sum of all 1s)
    for (int i = min; i <= n; i++)
        if (i % k == 0)
            return i;

    return -1;
}

// Driver Code
public static void Main ()
{
    int n = 10, k = 2;
    Console.WriteLine( minMultipleK(n, k));
}
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum multiple of
// k terms used to make sum n using 1s and 2s.

// Return minimum multiple of k terms used
// to make sum n using 1s and 2s.
function minMultipleK($n, $k)

{
    // Minimum number of terms required
    // to make sum n using 1s and 2s.
    $min = ($n / 2) + ($n % 2);

    // Iterate from Minimum to maximum to
    // findmultiple of k. Maximum number
    // of terms is n (Sum of all 1s)
    for ($i = $min; $i <= $n; $i++)
        if ($i % $k == 0)
            return $i;

    return -1;
}

// Driver Code
$n = 10; $k = 2;
echo(minMultipleK($n, $k));

// This code is contributed
// by Mukul singh.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Return minimum multiple of
// k terms used to make sum n
// using 1s and 2s.
function minMultipleK(n, k)
{

    // Minimum number of terms 
    // required to make sum n 
    // using 1s and 2s.
    let min = (n / 2) + (n % 2);

    // Iterate from Minimum to 
    // maximum to findmultiple of k. 
    // Maximum number of terms is
    // n (Sum of all 1s)
    for (let i = min; i <= n; i++)
        if (i % k == 0)
            return i;

    return -1;
}

// Driver Code

    let n = 10, k = 2;
    document.write( minMultipleK(n, k));

       // This code is contributed by splevel62.
</script>
```

**输出:**

```
6
```

本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。