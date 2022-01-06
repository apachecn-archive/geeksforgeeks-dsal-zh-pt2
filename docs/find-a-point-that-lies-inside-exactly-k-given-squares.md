# 找到正好位于 K 个给定正方形内的点

> 原文:[https://www . geeksforgeeks . org/find-a-a-point-the-in-the-恰好位于-k-给定方块内/](https://www.geeksforgeeks.org/find-a-point-that-lies-inside-exactly-k-given-squares/)

给定一个整数 **K** 和一个数组 **arr** ，每个数组的元素 **x** 表示一个正方形，其两个顶点为 **(0，0)** 和 **(x，x)** 。任务是找到一个恰好位于 **K** 方块中的点。
**示例:**

> **输入:** arr[] = {1，2，3，4}，K = 2
> **输出:** (3，3)
> 点(3，3)仅位于第三和第四个正方形内。
> **输入:** arr[] = {8，1，55，90}，K = 3
> **输出:** (8，8)

**方法:**因为所有的正方形都有一个公共的角点(0，0)，所以位于任何正方形中的任何点也将位于任何更大的正方形中。因此，我们可以简单地打印出 Kth 最大广场的另一角。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

int PointInKSquares(int n, int a[], int k)
{
    sort(a, a + n);
    return a[n - k];
}

// Driver Program to test above function
int main()
{
    int k = 2;
    int a[] = { 1, 2, 3, 4 };
    int n = sizeof(a) / sizeof(a[0]);

    int x = PointInKSquares(n, a, k);
    cout << "(" << x << ", " << x << ")";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

import java.io.*;
import java.util.*;
class GFG {

static int PointInKSquares(int n, int a[], int k)
{
    Arrays.sort(a);
    return a[n - k];
}

// Driver Program to test above function

    public static void main (String[] args) {
            int k = 2;
    int []a = { 1, 2, 3, 4 };
    int n = a.length;

    int x = PointInKSquares(n, a, k);
    System.out.println( "(" + x + ", " + x +")");

    }
}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python 3 implementation of the
# above approach
def PointInKSquares(n, a, k) :

    a.sort()
    return a[n - k]

# Driver Code
if __name__ == "__main__" :

    k = 2
    a = [1, 2, 3, 4]
    n = len(a)

    x = PointInKSquares(n, a, k)
    print("(", x, ",", x, ")")

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

static int PointInKSquares(int n,
                           int []a, int k)
{
    Array.Sort(a);
    return a[n - k];
}

// Driver Code
public static void Main (String[] args)
{
    int k = 2;
    int []a = { 1, 2, 3, 4 };
    int n = a.Length;

    int x = PointInKSquares(n, a, k);
    Console.WriteLine("(" + x + ", " + x +")");
}
}

// This code is contributed
// by Arnab Kundu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

function PointInKSquares($n, $a, $k)
{
    sort($a);
    return $a[$n - $k];
}

// Driver Code
$k = 2;
$a = array(1, 2, 3, 4);
$n = sizeof($a);

$x = PointInKSquares($n, $a, $k);
echo "(" . $x . ", " . $x . ")";

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

function PointInKSquares(n, a, k)
{
    a.sort();
    return a[n - k];
}

// Driver Program to test above function

    let k = 2;
    let a = [ 1, 2, 3, 4 ];
    let n = a.length;

    let x = PointInKSquares(n, a, k);
    document.write("(" + x + ", " + x + ")");

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
(3, 3)
```