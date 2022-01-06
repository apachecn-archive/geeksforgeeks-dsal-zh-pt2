# 通过移动线段中心的最大可能交点

> 原文:[https://www . geeksforgeeks . org/移动线段中心最大可能相交数/](https://www.geeksforgeeks.org/maximum-possible-intersection-by-moving-centers-of-line-segments/)

给定 X 轴上的三个点，表示三条线段的中心。线段的长度也给出为 l。任务是将给定线段的中心移动 K 的距离，以最大化三条线之间的相交长度。
**例:**

> **输入:** c1 = 1，c2 = 2，c3 = 3，L = 1，K = 0
> **输出:** 0
> 由于没有可以移动的中心，所以三段{(0.5，1.5)，(1.5，2.5)，(2.5，3.5)}之间没有交集。
> **输入:** c1 = 1，c2 = 2，c3 = 3，L = 1，K = 1
> **输出:** 1
> 中心的 1 和 3 可以分别向前和向前移动 1 个单位，与中心 2 重叠

线段如下:

1.  线段 1:(中心 1-1/2，中心 1+1/2)
2.  线段 2:(中心 2-1/2，中心 2+1/2)
3.  线段 3:(中心 3-1/2，中心 3+1/2)

**方法:**首先对中心进行排序，因为中间线段永远不会移动，因为左右线段总是可以到达其中心附近以增加相交长度。将处理三起案件:

*   **情况 1:** 在这样的场景中，当左右中心之间的距离大于等于 2*K+L 时，交点将始终为零。没有重叠是可能的，因为即使在移动两个中心仍然有 K 距离之后，它们将远离 L 或更大的距离。
*   **情况 2:** 在这种情况下，当左右中心之间的距离大于或等于 2*K 时，存在一个等于**(2 * K –(中心[2]–中心[0]–长度))**的交点，可以用简单的数学计算出来。
*   **情况 3:** 当左右中心之间的距离小于 2*K 时，在这种情况下，两个中心可以与中间中心重合。因此，交点是 l。

以下是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to print the maximum intersection
int max_intersection(int* center, int length, int k)
{
    sort(center, center + 3);

    // Case 1
    if (center[2] - center[0] >= 2 * k + length) {
        return 0;
    }

    // Case 2
    else if (center[2] - center[0] >= 2 * k) {
        return (2 * k - (center[2] - center[0] - length));
    }

    // Case 3
    else
        return length;
}

// Driver Code
int main()
{
    int center[3] = { 1, 2, 3 };
    int L = 1;
    int K = 1;
    cout << max_intersection(center, L, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation
// of above approach
import java.util.*;

class GFG
{

// Function to print the
// maximum intersection
static int max_intersection(int center[],
                            int length, int k)
{
    Arrays.sort(center);

    // Case 1
    if (center[2] - center[0] >= 2 * k + length)
    {
        return 0;
    }

    // Case 2
    else if (center[2] - center[0] >= 2 * k)
    {
        return (2 * k - (center[2] -
                center[0] - length));
    }

    // Case 3
    else
        return length;
}

// Driver Code
public static void main(String args[])
{
    int center[] = { 1, 2, 3 };
    int L = 1;
    int K = 1;
    System.out.println( max_intersection(center, L, K));
}
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to print the maximum intersection
def max_intersection(center, length, k):

    center.sort();

    # Case 1
    if (center[2] - center[0] >= 2 * k + length):
        return 0;

    # Case 2
    elif (center[2] - center[0] >= 2 * k):
        return (2 * k - (center[2] - center[0] - length));

    # Case 3
    else:
        return length;

# Driver Code
center = [1, 2, 3];
L = 1;
K = 1;
print(max_intersection(center, L, K));

# This code is contributed
# by mits
```

## C#

```
// C# implementation
// of above approach
using System;

class GFG
{

// Function to print the
// maximum intersection
static int max_intersection(int []center,
                            int length, int k)
{
    Array.Sort(center);

    // Case 1
    if (center[2] - center[0] >= 2 * k + length)
    {
        return 0;
    }

    // Case 2
    else if (center[2] -
             center[0] >= 2 * k)
    {
        return (2 * k - (center[2] -
                         center[0] - length));
    }

    // Case 3
    else
        return length;
}

// Driver Code
public static void Main()
{
    int []center = { 1, 2, 3 };
    int L = 1;
    int K = 1;
    Console.WriteLine(max_intersection(center, L, K));
}
}

// This code is contributed
// by Subhadeep Gupta
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation
// of above approach

// Function to print the
// maximum intersection
function max_intersection($center,
                          $length, $k)
{
    sort($center);

    // Case 1
    if ($center[2] -
        $center[0] >= 2 * $k + $length)
    {
        return 0;
    }

    // Case 2
    else if ($center[2] -
             $center[0] >= 2 * $k)
    {
        return (2 * $k - ($center[2] -
             $center[0] - $length));
    }

    // Case 3
    else
        return $length;
}

// Driver Code
$center = array(1, 2, 3);
$L = 1;
$K = 1;
echo max_intersection($center, $L, $K);

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation
// of above approach

// Function to print the
// maximum intersection
function max_intersection(center,length, k)
{
    center.sort();

    // Case 1
    if (center[2] - center[0] >= 2 * k + length)
    {
        return 0;
    }

    // Case 2
    else if (center[2] - center[0] >= 2 * k)
    {
        return (2 * k - (center[2] -
                center[0] - length));
    }

    // Case 3
    else
        return length;
}

// driver program

    let center = [ 1, 2, 3 ];
    let L = 1;
    let K = 1;
    document.write( max_intersection(center, L, K));

</script>
```

**Output:** 

```
1
```