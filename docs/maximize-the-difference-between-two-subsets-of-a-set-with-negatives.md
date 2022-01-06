# 用否定最大化集合的两个子集之间的差异

> 原文:[https://www . geeksforgeeks . org/最大化带否定集合的两个子集之间的差异/](https://www.geeksforgeeks.org/maximize-the-difference-between-two-subsets-of-a-set-with-negatives/)

给定一组 n 大小的整数，任务是将这些整数分成两组 g1 和 g2，使得(g1 的元素之和)–(G2 的元素之和)变得最大。您的任务是打印结果的值。我们可以保留一个子集为空。
**例:**

> **输入:** 3，7，-4，10，-11，2
> T3】输出: 37
> 说明:
> g1: 3，7，10，2
> g2: -4，-11
> 结果=(3+7+10+2)–(-4+-11)= 22 –(-15)= 37
> **输入:** 2，2，-2，-2
> **输出:【T11**

其思想是根据它们的符号值对整数进行分组，即我们将正整数分组为 g1，将负整数分组为 g2。
因为，–(-G2)=+G2
所以，结果变成 g1 + |g2|。

## C++

```
// CPP program to make two subsets with
// maximum difference.
#include <bits/stdc++.h>
using namespace std;

int maxDiff(int arr[], int n)
{
    int sum = 0;

    // We move all negative elements into
    // one set. So we add negation of negative
    // numbers to maximize difference
    for (int i = 0; i < n; i++)
         sum = sum + abs(arr[i]);

    return sum;
}

// Driver Code
int main()
{
    int arr[] = { 3, 7, -4, 10, -11, 2 };
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << maxDiff(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to make two subsets with
// maximum difference.
import java.util.*;

class solution
{

static int maxDiff(int arr[], int n)
{
    int sum = 0;

    // We move all negative elements into
    // one set. So we add negation of negative
    // numbers to maximize difference
    for (int i = 0; i < n; i++)
        sum = sum + Math.abs(arr[i]);

    return sum;
}

// Driver Code
public static void main(String args[])
{
    int []arr = { 3, 7, -4, 10, -11, 2 };
    int n = arr.length;
    System.out.println(maxDiff(arr, n));
}
}
```

## 蟒蛇 3

```
# Python3 program to make two subsets
# with maximum difference.

def maxDiff(arr, n) :

    sum = 0

    # We move all negative elements into
    # one set. So we add negation of negative
    # numbers to maximize difference
    for i in range(n) :
        sum += abs(arr[i])

    return sum

# Driver Code
if __name__ == "__main__" :

    arr = [ 3, 7, -4, 10, -11, 2 ]
    n = len(arr)
    print(maxDiff(arr, n))

# This code is contributed by Ryuga
```

## C#

```
using System;

// C# program to make two subsets with
// maximum difference.

public class solution
{

public static int maxDiff(int[] arr, int n)
{
    int sum = 0;

    // We move all negative elements into
    // one set. So we add negation of negative
    // numbers to maximize difference 
    for (int i = 0; i < n; i++)
    {
        sum = sum + Math.Abs(arr[i]);
    }

    return sum;
}

// Driver Code
public static void Main(string[] args)
{
    int[] arr = new int[] {3, 7, -4, 10, -11, 2};
    int n = arr.Length;
    Console.WriteLine(maxDiff(arr, n));
}
}

  // This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to make two subsets
// with maximum difference.
function maxDiff($arr, $n)
{
    $sum = 0;

    // We move all negative elements
    // into one set. So we add negation
    // of negative numbers to maximize
    // difference
    for ($i = 0; $i < $n; $i++)
        $sum = $sum + abs($arr[$i]);

    return $sum;
}

// Driver Code
$arr = array( 3, 7, -4, 10, -11, 2 );
$n = sizeof($arr);
echo maxDiff($arr, $n);

// This code is contributed by Sachin.
?>
```

## java 描述语言

```
<script>
// javascript program to make two subsets with
// maximum difference.
function maxDiff(arr , n)
{
    var sum = 0;

    // We move all negative elements into
    // one set. So we add negation of negative
    // numbers to maximize difference
    for (i = 0; i < n; i++)
        sum = sum + Math.abs(arr[i]);

    return sum;
}

// Driver Code
var arr = [ 3, 7, -4, 10, -11, 2 ];
var n = arr.length;
document.write(maxDiff(arr, n));

// This code is contributed by Princi Singh
</script>
```

**Output:** 

```
37
```

**时间复杂度:** O(n)