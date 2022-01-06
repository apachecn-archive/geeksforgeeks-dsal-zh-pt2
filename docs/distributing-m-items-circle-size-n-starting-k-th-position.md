# 从第 K 个位置

开始，将 M 个物品分布在一个大小为 N 的圆内

> 原文:[https://www . geesforgeks . org/distribution-m-items-circle-size-n-start-k-th-position/](https://www.geeksforgeeks.org/distributing-m-items-circle-size-n-starting-k-th-position/)

M 个物品将在一个大小为 n 的圆圈中交付。如果我们从给定的位置 k 开始，请找到第 M 个物品将被交付的位置。请注意，物品分布在从 k 开始的相邻位置。
**示例:**

```
Input : N = 5 // Size of circle
        M = 2 // Number of items
        K = 1 // Starting position
Output : 2
The first item will be given to 1st 
position. Second (or last) item will 
be delivered to 2nd position

Input : N = 5 
        M = 8 
        K = 2
Output : 4
The last item will be delivered to 
4th position
```

我们检查要分发的项目数量是否大于我们在当前循环中的剩余位置。如果是，那么我们只需返回 m+k–1(我们从 k 开始以相同的周期分发物品)。否则，我们在完成当前周期后计算剩余物品的数量，并返回剩余物品的模型。
以下是上述思路的实现

## C++

```
// C++ program to find the position where
// last item is delivered.
#include <bits/stdc++.h>
using namespace std;

// n ==> Size of circle
// m ==> Number of items
// k ==> Initial position
int lastPosition(int n, int m, int k)
{
    // n - k + 1 is number of positions
    // before we reach beginning of circle
    // If m is less than this value, then
    // we can simply return (m-1)th position
    if (m <= n - k + 1)
        return m + k - 1;

    // Let us compute remaining items before
    // we reach beginning.
    m = m - (n - k + 1);

    // We compute m % n to skip all complete
    // rounds. If we reach end, we return n
    // else we return m % n
    return (m % n == 0) ? n : (m % n);
}

// Driver code
int main()
{
    int n = 5;
    int m = 8;
    int k = 2;
    cout << lastPosition(n, m, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the position where
// last item is delivered.
class GFG {

    // n ==> Size of circle
    // m ==> Number of items
    // k ==> Initial position
    static int lastPosition(int n, int m, int k)
    {

        // n - k + 1 is number of positions
        // before we reach beginning of circle
        // If m is less than this value, then
        // we can simply return (m-1)th position
        if (m <= n - k + 1)
            return m + k - 1;

        // Let us compute remaining items before
        // we reach beginning.
        m = m - (n - k + 1);

        // We compute m % n to skip all complete
        // rounds. If we reach end, we return n
        // else we return m % n
        return (m % n == 0) ? n : (m % n);
    }

    // Driver Program to test above function
    public static void main(String arg[])
    {
        int n = 5;
        int m = 8;
        int k = 2;
        System.out.print(lastPosition(n, m, k));
    }
}

// This code is contributed by Anant Agarwal.
```

## 计算机编程语言

```
# Python program to find the position where
# last item is delivered.

# n ==> Size of circle
# m ==> Number of items
# k ==> Initial position
def lastPosition(n, m, k):

    # n - k + 1 is number of positions
    # before we reach beginning of circle
    # If m is less than this value, then
    # we can simply return (m-1)th position
    if (m <= n - k + 1):
       return m + k - 1

    # Let us compute remaining items before
    # we reach beginning.
    m = m - (n - k + 1)

    # We compute m % n to skip all complete
    # rounds. If we reach end, we return n
    # else we return m % n
    if(m % n == 0):
        return n
    else:
        return m % n

# Driver code
n = 5
m = 8
k = 2
print lastPosition(n, m, k)

# This code is contributed by Sachin Bisht
```

## C#

```
// C# program to find the position where
// last item is delivered.
using System;

class GFG {

    // n ==> Size of circle
    // m ==> Number of items
    // k ==> Initial position
    static int lastPosition(int n, int m, int k)
    {

        // n - k + 1 is number of positions
        // before we reach beginning of circle
        // If m is less than this value, then
        // we can simply return (m-1)th position
        if (m <= n - k + 1)
            return m + k - 1;

        // Let us compute remaining items before
        // we reach beginning.
        m = m - (n - k + 1);

        // We compute m % n to skip all complete
        // rounds. If we reach end, we return n
        // else we return m % n
        return (m % n == 0) ? n : (m % n);
    }

    // Driver Program to test above function
    public static void Main()
    {
        int n = 5;
        int m = 8;
        int k = 2;

        Console.WriteLine(lastPosition(n, m, k));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// position where last item
// is delivered.

// n ==> Size of circle
// m ==> Number of items
// k ==> Initial position

function lastPosition($n, $m, $k)
{
    // n - k + 1 is number of
    // positions before we reach
    // beginning of circle.
    // If m is less than this value,
    // then we can simply return
    // (m-1)th position
    if ($m <= $n - $k + 1)
    return $m + $k - 1;

    // Let us compute remaining items
    // before we reach beginning.
    $m = $m - ($n - $k + 1);

    // We compute m % n to skip
    // all complete rounds. If we
    // reach end, we return n
    // else we return m % n
    return ($m % $n == 0) ? $n : ($m % $n);
}

// Driver code
$n = 5;
$m = 8;
$k = 2;
echo lastPosition($n, $m, $k);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// Javascript program to find the
// position where last item
// is delivered.

// n ==> Size of circle
// m ==> Number of items
// k ==> Initial position

function lastPosition(n, m, k)
{

    // n - k + 1 is number of
    // positions before we reach
    // beginning of circle.
    // If m is less than this value,
    // then we can simply return
    // (m-1)th position
    if (m <= n - k + 1)
    return m + k - 1;

    // Let us compute remaining items
    // before we reach beginning.
    m = m - (n - k + 1);

    // We compute m % n to skip
    // all complete rounds. If we
    // reach end, we return n
    // else we return m % n
    return (m % n == 0) ? n : (m % n);
}

// Driver code
let n = 5;
let m = 8;
let k = 2;
document.write(lastPosition(n, m, k));

// This code is contributed by _saurabh_jaiswal
</script>
```

**输出:**

```
4
```

**时间复杂度** : O(1)
本文由**萨达克·科利**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。