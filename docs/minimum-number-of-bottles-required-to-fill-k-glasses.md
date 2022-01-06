# 灌装 K 型玻璃杯所需的最小瓶子数量

> 原文:[https://www . geeksforgeeks . org/最低灌装量-k-glass/](https://www.geeksforgeeks.org/minimum-number-of-bottles-required-to-fill-k-glasses/)

给定 N 个有水的玻璃杯，并列出它们各自的容量。任务是找到准确填充 K 型玻璃杯所需的最小瓶子数量。每瓶容量为 100 个单位。

**示例:**

> **输入:** N = 4，K = 3，arr[] = {200，150，140，300}
> **输出:** 5
> 我们要正好填 3 个杯子。
> 所以我们填 140，150，200，总和是 490，所以这个需要 5 瓶。
> **输入:** N = 5，K = 4，arr[] = {1，2，3，2，1}
> **输出:** 1

**方法:**要准确填写 K 眼镜，取容量最小的 K 眼镜。所以对于这种给定容量的列表。最终答案将是**(1st k 玻璃杯容量之和)/(1 瓶容量)**的上限值。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// function to calculate minimum glasses
double Min_glass(int n, int k,
                            int a[])
{
    // sort the array based on
    // their capacity

    int sum = 0;

    // taking sum of capacity
    // of first k glasses
    for (int i = 0; i < k; i++)
        sum += a[i];

    // calculate the answer
    double ans = ceil((double)sum /
                            (double)100);

    return ans;
}

// Driver code
int main()
{

    int n = 4;
    int k = 3;
    int a[] = { 200, 150, 140, 300 };
    sort(a, a+n);
    cout << Min_glass(n, k, a);

    return 0;
}

// This code is contributed by target_2.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
import java.util.*;

class GFG
{
// function to calculate minimum glasses
public static double Min_glass(int n, int k,
                            int[] a)
{
    // sort the array based on
    // their capacity

    int sum = 0;

    // taking sum of capacity
    // of first k glasses
    for (int i = 0; i < k; i++)
        sum += a[i];

    // calculate the answer
    double ans = Math.ceil((double)sum /
                            (double)100);

    return ans;
}

// Driver code
public static void main(String[] args)
{
    int n = 4;
    int k = 3;
    int[] a = { 200, 150, 140, 300 };
    Arrays.sort(a);
    System.out.println(Min_glass(n, k, a));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
from math import ceil

# Function to calculate minimum glasses
def Min_glass(n, k, a):

    # sort the array based on their capacity
    a.sort()

    # calculate the answer
    return ceil(sum(a[:k]) / 100)

# Driver code
if __name__ == "__main__":

    n, k = 4, 3
    a = [200, 150, 140, 300] 

    print(Min_glass(n, k, a))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the
// above approach
using System;

class GFG
{
// function to calculate minimum glasses
public static double Min_glass(int n, int k,
                               int []a)
{
    // sort the array based on
    // their capacity

    int sum = 0;

    // taking sum of capacity
    // of first k glasses
    for (int i = 0; i < k; i++)
        sum += a[i];

    // calculate the answer
    double ans = Math.Ceiling((double)sum /
                              (double)100);

    return ans;
}

// Driver code
public static void Main()
{
    int n = 4;
    int k = 3;
    int[] a = { 200, 150, 140, 300 };
    Array.Sort(a);
    Console.WriteLine(Min_glass(n, k, a));
}
}

// This code is contributed
// by Soumik Mondal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// function to calculate minimum glasses
function Min_glass($n, $k, $a)
{
    // sort the array based on
    // their capacity
    sort($a);

    $sum = 0;

    // taking sum of capacity
    // of first k glasses
    for ($i = 0; $i < $k; $i++)
        $sum += $a[$i];

    // calculate the answer
    $ans = ceil($sum /100);

    return $ans;
}

// Driver code
$n = 4;
$k = 3;
$a = array( 200, 150, 140, 300 );

echo Min_glass($n, $k, $a);

// This code is contributed
// by akt_mit
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the
// above approach

// Function to calculate minimum glasses
function Min_glass(n, k, a)
{

    // Sort the array based on
    // their capacity
    var sum = 0;

    // Taking sum of capacity
    // of first k glasses
    for(var i = 0; i < k; i++)
        sum += a[i];

    // Calculate the answer
    var ans = parseInt(Math.ceil(sum / 100));

    return ans;
}

// Driver Code
var n = 4;
var k = 3;
var a = [ 200, 150, 140, 300 ];
a.sort();

document.write(Min_glass(n, k, a));

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
5
```