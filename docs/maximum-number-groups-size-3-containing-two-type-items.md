# 包含两类物品的 3 号组的最大数量

> 原文:[https://www . geesforgeks . org/最大数量-组-大小-3-包含-两种类型-项目/](https://www.geeksforgeeks.org/maximum-number-groups-size-3-containing-two-type-items/)

给定项目 A 的 n 个实例和项目 b 的 m 个实例。找到可以使用这些项目形成的大小为 3 的组的最大数量，使得所有组都包含两种类型的项目，即， 一个组不应包含所有类型 A 的项目或所有类型 B 的项目。
形成的组中类型 A 的项目总数必须小于或等于 n。
形成的组中类型 B 的项目总数必须小于或等于 m。
**示例:**

```
Input : n = 2 and m = 6.
Output : 2
In group 1, one item of type A and two items of
type B. Similarly, in the group 2, one item of 
type A and two items of type B.
We have used 2 (<= n) items of type A and 4 (<= m)
items of type B.

Input : n = 4 and m = 5.
Output : 3
In group 1, one item of type A and two items of type B.
In group 2, one item of type B and two items of type A.
In group 3, one item of type A and two items of type B.
We have used 4 (<= n) items of type A and 5 (<= 5)
items of type B.
```

观察:
1。如果 m > = 2n，将有 n 个可能的组。或者有 m 组可能，如果 n > = 2m。
2。假设 n = 3，m = 3，那么项目 A 的一个实例将与项目 B 的两个实例组成一个组，项目 B 的一个实例将与项目 A 的两个实例组成一个组。因此，最多可以有两个组。所以，在给定 n 和 m 的情况下，用 m 和 m 除以 3，求出这类条件的总数。在此之后，每种类型可以剩下 0、1、2 个实例。为了找到左侧实例的组数:
a)如果 n = 0 或 m = 0，0 组是可能的。
b)如果 n + m > = 3，则只能有 1 组。
解决这个问题的算法:
1。如果 n > = 2m，最大组数= n.
2。否则如果 m > = 2n，最大组数= m
3。否则 If (m + n) % 3 == 0，最大组数=(m+n)/3；
4。否则最大组数= (n + m)/3。并设置 n = n%3 和 m = m%3。
a) If n！= 0 & & m！= 0 & & (n + m) > = 3，最大组数加 1。
以下是上述思路的实现:

## C++

```
// C++ program to calculate
// maximum number of groups
#include<bits/stdc++.h>

using namespace std;

// Implements above mentioned steps.
int maxGroup(int n, int m)
{
    if (n >= 2 * m)
        return n;
    if (m >= 2 * n)
        return m;
    if ((m + n) % 3 == 0)
        return (m + n)/3;

    int ans = (m + n)/3;
    m %= 3;
    n %= 3;

    if (m && n && (m + n) >= 3)
        ans++;

    return ans;
}

// Driver code
int main()
{
    int n = 4, m = 5;
    cout << maxGroup(n, m) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate
// maximum number of groups
import java.io.*;

public class GFG{

// Implements above mentioned steps.
static int maxGroup(int n, int m)
{
    if (n >= 2 * m)
        return n;
    if (m >= 2 * n)
        return m;
    if ((m + n) % 3 == 0)
        return (m + n) / 3;

    int ans = (m + n) / 3;
    m %= 3;
    n %= 3;

    if (m > 0 && n > 0 && (m + n) >= 3)
        ans++;

    return ans;
}

    // Driver code
    static public void main (String[] args)
    {
            int n = 4, m = 5;
    System.out.println(maxGroup(n, m));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to calculate maximum
# number of groups

# Implements above mentioned steps
def maxGroup(n, m):

    if n >= 2 * m:
        return n
    if m >= 2 * n:
        return m
    if (m + n) % 3 == 0:
        return (m + n) // 3
    ans = (m + n) // 3
    m = m % 3
    n = n % 3

    if m and n and (m + n) >= 3:
        ans += 1
    return ans

# Driver Code
n, m = 4, 5
print(maxGroup(n, m))

# This code is contributed
# by Mohit kumar 29
```

## C#

```
// C# program to calculate
// maximum number of groups
using System;

public class GFG{

// Implements above mentioned steps.
static int maxGroup(int n, int m)
{
    if (n >= 2 * m)
        return n;
    if (m >= 2 * n)
        return m;
    if ((m + n) % 3 == 0)
        return (m + n) / 3;

    int ans = (m + n) / 3;
    m %= 3;
    n %= 3;

    if (m > 0 && n > 0 && (m + n) >= 3)
        ans++;

    return ans;
}

    // Driver code
    static public void Main ()
    {
        int n = 4, m = 5;
        Console.WriteLine(maxGroup(n, m));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate
// maximum number of groups

// Implements above mentioned steps.
function maxGroup($n, $m)
{
    if ($n >= 2 * $m)
        return n;
    if ($m >= 2 * $n)
        return m;
    if ((($m + $n) % 3) == 0)
        return ($m + $n) / 3;

    $ans = ($m + $n) / 3;
    $m %= 3;
    $n %= 3;

    if ($m && $n && ($m + $n) >= 3)
        $ans++;

    return $ans;
}

// Driver code
$n = 4; $m = 5;
echo maxGroup($n, $m) ;

// This code is contributed
// by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find Cullen number

// Implements above mentioned steps.
function maxGroup(n, m)
{
    if (n >= 2 * m)
        return n;
    if (m >= 2 * n)
        return m;
    if ((m + n) % 3 == 0)
        return (m + n) / 3;

    let ans = (m + n) / 3;
    m %= 3;
    n %= 3;

    if (m > 0 && n > 0 && (m + n) >= 3)
        ans++;

    return ans;
}

// Driver Code
    let n = 4, m = 5;
    document.write(maxGroup(n, m));

// This code is contributed by chinmoy1997pal.
</script>
```

**输出:**

```
3
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)
本文由[**Anuj Chauhan(Anuj 0503)**](https://web.facebook.com/anuj0503)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。