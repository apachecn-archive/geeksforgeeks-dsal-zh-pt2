# 可添加到集合中的最大差异元素

> 原文:[https://www . geesforgeks . org/最大差异-可以添加到集合中的元素/](https://www.geeksforgeeks.org/maximum-difference-elements-that-can-added-to-a-set/)

给定一个包含 N 个元素的集合，只有当元素 Z > 0 可以表示为|X-Y|其中 X 和 Y 已经存在于集合中时，才允许向该集合中添加元素 Z > 0。添加元素 Z 后，可以将其用作集合的元素来添加新元素。找出以这种方式可以添加的元素的最大数量。
**例** :

```
Input : set = {2, 3}
Output : 1
The only element that can be added is 1.

Input : set = {4, 6, 10}
Output : 2
The 2 elements that can be added are 
(6-4) = 2 and (10-2) = 8.
```

这个问题基于以下观察:

*   可以插入的最大元素必须小于集合中的当前最大元素，因为两个整数的差不能超过任何整数。
*   您插入的每个数字都必须是给定数组 gcd 的倍数。因为在任何一步，X 和 Y 都是 gcd 的倍数，(X-Y)也将是 gcd 的倍数。
*   您可以插入小于最大元素的 gcd 的所有倍数。
*   小于或等于最大可被 gcd 整除的项数是 floor (max/gcd)，这将是执行所有插入后集合中元素的总数，我们需要去掉原始 N 个元素的计数才能得到我们的答案。

以下是上述方法的实现:

## C++

```
// CPP program to find the maximum number
// of elements that can be added to a set
// such that it is the absolute difference
// of 2 elements already in the set

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum number
// of elements that can be added to a set
// such that it is the absolute difference
// of 2 elements already in the set
int maxNewElements(int a[], int n)
{
    int gcd = a[0];

    int mx = a[0];

    for (int i = 1; i < n; i++) {
        gcd = __gcd(gcd, a[i]);
        mx = max(mx, a[i]);
    }

    int total_terms = mx / gcd;

    return total_terms - n;
}

// Driver Code
int main()
{
    int a[] = { 4, 6, 10 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << maxNewElements(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum number
// of elements that can be added to a set
// such that it is the absolute difference
// of 2 elements already in the set

import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{

static int __gcd(int a, int b) {
   if (b==0) return a;
   return __gcd(b,a%b);
}
// Function to find the maximum number
// of elements that can be added to a set
// such that it is the absolute difference
// of 2 elements already in the set
static int maxNewElements(int []a, int n)
{
    int gcd = a[0];

    int mx = a[0];

    for (int i = 1; i < n; i++) {
        gcd = __gcd(gcd, a[i]);
        mx = Math.max(mx, a[i]);
    }

    int total_terms = mx / gcd;

    return total_terms - n;
}

// Driver Code
public static void main(String args[])
{
    int a[] = { 4, 6, 10 };
    int n = a.length;
    System.out.print(maxNewElements(a, n));
}
}
```

## 蟒蛇 3

```
# Python3 program to find the maximum number
# of elements that can be added to a set
# such that it is the absolute difference
# of 2 elements already in the set

# from math lib import gcd method
from math import gcd

# Function to find the maximum number
# of elements that can be added to a set
# such that it is the absolute difference
# of 2 elements already in the set
def maxNewElements(a, n) :

    __gcd = a[0]

    mx = a[0]

    for i in range(1, n) :
        __gcd = gcd(__gcd,a[i])
        mx = max(mx, a[i])

    total_terms = mx / __gcd

    return total_terms - n

# Driver code
if __name__ == "__main__" :

    a = [ 4, 6, 10 ]

    n = len(a)

    print(int(maxNewElements(a,n)))

# This code is contributed by
# ANKITRAI1
```

## C#

```
// C# program to find the maximum
// number of elements that can be
// added to a set such that it is
// the absolute difference of 2
// elements already in the set
class GFG
{

static int __gcd(int a, int b)
{
    if (b == 0) return a;
    return __gcd(b, a % b);
}

// Function to find the maximum number
// of elements that can be added to a set
// such that it is the absolute difference
// of 2 elements already in the set
static int maxNewElements(int[] a, int n)
{
    int gcd = a[0];

    int mx = a[0];

    for (int i = 1; i < n; i++)
    {
        gcd = __gcd(gcd, a[i]);
        mx = System.Math.Max(mx, a[i]);
    }

    int total_terms = mx / gcd;

    return total_terms - n;
}

// Driver Code
static void Main()
{
    int[] a = { 4, 6, 10 };
    int n = a.Length;
    System.Console.WriteLine(maxNewElements(a, n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the maximum number
// of elements that can be added to a set
// such that it is the absolute difference
// of 2 elements already in the set

function __gcd($a, $b)
{
    if ($b == 0)
        return $a;
    return __gcd($b, $a % $b);
}

// Function to find the maximum number
// of elements that can be added to
// a set such that it is the absolute
// difference of 2 elements already in
// the set
function maxNewElements($a, $n)
{
    $gcd = $a[0];

    $mx = $a[0];

    for ($i = 1; $i < $n; $i++)
    {
        $gcd = __gcd($gcd, $a[$i]);
        $mx = max($mx, $a[$i]);
    }

    $total_terms = $mx / $gcd;

    return $total_terms - $n;
}

// Driver Code
$a = array(4, 6, 10 );
$n = sizeof($a);
echo maxNewElements($a, $n);

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>
    // Javascript program to find the maximum
    // number of elements that can be
    // added to a set such that it is
    // the absolute difference of 2
    // elements already in the set

    function __gcd(a, b)
    {
        if (b == 0) return a;
            return __gcd(b, a % b);
    }

    // Function to find the maximum number
    // of elements that can be added to a set
    // such that it is the absolute difference
    // of 2 elements already in the set
    function maxNewElements(a, n)
    {
        let gcd = a[0];

        let mx = a[0];

        for (let i = 1; i < n; i++)
        {
            gcd = __gcd(gcd, a[i]);
            mx = Math.max(mx, a[i]);
        }

        let total_terms = parseInt(mx / gcd, 10);

        return total_terms - n;
    }

    let a = [ 4, 6, 10 ];
    let n = a.length;
    document.write(maxNewElements(a, n));

    // This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N*LogN)