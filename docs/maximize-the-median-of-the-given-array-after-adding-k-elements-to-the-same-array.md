# 将 K 个元素添加到同一个数组后，给定数组的中值最大化

> 原文:[https://www . geeksforgeeks . org/将 k 个元素添加到同一个数组后，给定数组的中值最大化/](https://www.geeksforgeeks.org/maximize-the-median-of-the-given-array-after-adding-k-elements-to-the-same-array/)

给定一个由 **N** 元素组成的数组 **arr[]** 和一个整数 **K** ，其中 **K < N** 。任务是将 **K** 个整数元素插入到同一个数组中，使得结果数组的中值最大化。打印最大化中间值。
**举例:**

> **输入:** arr[] = {3，2，3，4，2}，k = 2
> **输出:** 3
> {2，2，3，3，4，5，5}可以是一次这样的以 3 为中值的结果数组。
> **输入:** arr[] = {3，2，3，4，2}，k = 3
> **输出:** 3.5

**方法:**为了最大化结果数组的中值，所有需要插入的元素必须大于数组中的最大元素。插入这些元素后，数组的新大小将是**大小= N + K** 。对数组进行排序，如果**的大小为奇数**则数组的中值为 **arr【大小/2】**，否则为 **(arr【(大小/2)–1】+arr【大小/2】)/2**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximized median
float getMaxMedian(int arr[], int n, int k)
{
    int size = n + k;

    // Sort the array
    sort(arr, arr + n);

    // If size is even
    if (size % 2 == 0) {
        float median = (float)(arr[(size / 2) - 1]
                               + arr[size / 2])
                       / 2;
        return median;
    }

    // If size is odd
    float median = arr[size / 2];
    return median;
}

// Driver code
int main()
{
    int arr[] = { 3, 2, 3, 4, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;
    cout << getMaxMedian(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

// Java implementation of the approach
class GFG
{

    // Function to return the maximized median
    static double getMaxMedian(int[] arr, int n, int k)
    {
        int size = n + k;

        // Sort the array
        Arrays.sort(arr);

        // If size is even
        if (size % 2 == 0)
        {
            double median = (double) (arr[(size / 2) - 1]
                    + arr[size / 2])
                    / 2;
            return median;
        }

        // If size is odd
        double median1 = arr[size / 2];
        return median1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = {3, 2, 3, 4, 2};
        int n = arr.length;
        int k = 2;
        System.out.print((int)getMaxMedian(arr, n, k));

    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the maximized median
def getMaxMedian(arr, n, k):
    size = n + k

    # Sort the array
    arr.sort(reverse = False)

    # If size is even
    if (size % 2 == 0):
        median = (arr[int(size / 2) - 1] +
                  arr[int(size / 2)]) / 2
        return median

    # If size is odd
    median = arr[int(size / 2)]
    return median

# Driver code
if __name__ == '__main__':
    arr = [3, 2, 3, 4, 2]
    n = len(arr)
    k = 2
    print(getMaxMedian(arr, n, k))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
using System.Linq;

class GFG
{

// Function to return the maximized median
static double getMaxMedian(int []arr, int n, int k)
{
    int size = n + k;

    // Sort the array
    Array.Sort(arr);

    // If size is even
    if (size % 2 == 0)
    {
        double median = (double)(arr[(size / 2) - 1]
                            + arr[size / 2])
                    / 2;
        return median;
    }

    // If size is odd
    double median1 = arr[size / 2];
    return median1;
}

// Driver code
static void Main()
{
    int []arr = { 3, 2, 3, 4, 2 };
    int n = arr.Length;
    int k = 2;
    Console.WriteLine(getMaxMedian(arr, n, k));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
// Function to return the maximized median
function getMaxMedian($arr, $n, $k)
{
    $size = $n + $k;

    // Sort the array
    sort($arr, $n);

    // If size is even
    if ($size % 2 == 0)
    {
        $median = (float)($arr[($size / 2) - 1] +
                          $arr[$size / 2]) / 2;
        return $median;
    }

    // If size is odd
    $median = $arr[$size / 2];
    return $median;
}

// Driver code
$arr = array( 3, 2, 3, 4, 2 );
$n = sizeof($arr);
$k = 2;
echo(getMaxMedian($arr, $n, $k));

// This code is Contributed by Code_Mech.
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the maximized median
function getMaxMedian(arr, n, k) {
    let size = n + k;

    // Sort the array
    arr.sort((a, b) => a - b);

    // If size is even
    if (size % 2 == 0) {
        let median = (arr[Math.floor(size / 2) - 1] +
        arr[Math.floor(size / 2)]) / 2;
        return median;
    }

    // If size is odd
    let median = arr[Math.floor(size / 2)];
    return median;
}

// Driver code

let arr = [3, 2, 3, 4, 2];
let n = arr.length;
let k = 2;
document.write(getMaxMedian(arr, n, k));

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
3
```