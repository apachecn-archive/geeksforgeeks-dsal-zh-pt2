# 可被给定数 k 整除的数组的最小和最大元素

> 原文:[https://www . geeksforgeeks . org/可被给定数字 k 整除的最小和最大数组元素/](https://www.geeksforgeeks.org/minimum-and-maximum-element-of-an-array-which-is-divisible-by-a-given-number-k/)

给定一个数组，任务是找出数组中可被给定数 k 整除的最小和最大元素
**示例:**

```
Input: arr[] = {12, 1235, 45, 67, 1}, k=5
Output: Minimum = 45, Maximum = 1235

Input: arr[] = {10, 1230, 45, 67, 1}, k=10
Output: Minimum = 10, Maximum = 1230
```

**进场:**

1.  取一个存储最小元素的 min 变量，用 INT_MAX 初始化，与数组的每个元素进行比较，更新下一个可被 k 整除的最小元素。
2.  取一个存储最大元素的 max 变量，用 INT_MIN 初始化，与数组的每个元素进行比较，更新下一个可被 k 整除的最大元素。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum element
int getMin(int arr[], int n, int k)
{
    int res = INT_MAX;
    for (int i = 0; i < n; i++) {
        if (arr[i] % k == 0)
            res = min(res, arr[i]);
    }
    return res;
}

// Function to find the maximum element
int getMax(int arr[], int n, int k)
{
    int res = INT_MIN;
    for (int i = 1; i < n; i++) {
        if (arr[i] % k == 0)
            res = max(res, arr[i]);
    }
    return res;
}

// Driver code
int main()
{
    int arr[] = { 10, 1230, 45, 67, 1 };
    int k = 10;
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Minimum element of array which is divisible by k: "
         << getMin(arr, n, k) << "\n";
    cout << "Maximum element of array which is divisible by k: "
         << getMax(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation of the above approach

class GFG {

// Function to find the minimum element
    static int getMin(int arr[], int n, int k) {
        int res = Integer.MAX_VALUE;
        for (int i = 0; i < n; i++) {
            if (arr[i] % k == 0) {
                res = Math.min(res, arr[i]);
            }
        }
        return res;
    }

// Function to find the maximum element
    static int getMax(int arr[], int n, int k) {
        int res = Integer.MIN_VALUE;
        for (int i = 1; i < n; i++) {
            if (arr[i] % k == 0) {
                res = Math.max(res, arr[i]);
            }
        }
        return res;
    }

// Driver code
    public static void main(String[] args) {
        int arr[] = {10, 1230, 45, 67, 1};
        int k = 10;
        int n = arr.length;
        System.out.println("Minimum element of array which is divisible by k: "
                + getMin(arr, n, k));
        System.out.println("Maximum element of array which is divisible by k: "
                + getMax(arr, n, k));
    }
}
//This code contribute by Shikha Singh
```

## 蟒蛇 3

```
# Python 3 implementation of the
# above approach
import sys

# Function to find the minimum element
def getMin(arr, n, k):

    res = sys.maxsize
    for i in range(n):
        if (arr[i] % k == 0):
            res = min(res, arr[i])
    return res

# Function to find the maximum element
def getMax(arr, n, k):

    res = 0
    for i in range(1, n):
        if (arr[i] % k == 0):
            res = max(res, arr[i])
    return res

# Driver code
if __name__ == "__main__":

    arr = [ 10, 1230, 45, 67, 1 ]
    k = 10
    n = len(arr)
    print("Minimum element of array which",
          "is divisible by k: ", getMin(arr, n, k))
    print( "Maximum element of array which",
           "is divisible by k: ", getMax(arr, n, k))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
// Function to find the minimum element
static int getMin(int []arr, int n, int k)
{
    int res = int.MaxValue;
    for (int i = 0; i < n; i++)
    {
        if (arr[i] % k == 0)
        {
            res = Math.Min(res, arr[i]);
        }
    }
    return res;
}

// Function to find the maximum element
static int getMax(int []arr, int n, int k)
{
    int res = int.MinValue;
    for (int i = 1; i < n; i++)
    {
        if (arr[i] % k == 0)
        {
            res = Math.Max(res, arr[i]);
        }
    }
    return res;
}

// Driver code
static public void Main ()
{
    int []arr = {10, 1230, 45, 67, 1};
    int k = 10;
    int n = arr.Length;
    Console.WriteLine("Minimum element of array " +
                      "which is divisible by k: " +
                                getMin(arr, n, k));
    Console.WriteLine("Maximum element of array " +
                      "which is divisible by k: " +
                                getMax(arr, n, k));
}
}

// This code is contributes by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to find the minimum element
function getMin($arr, $n, $k)
{
    $res = PHP_INT_MAX;
    for ($i = 0; $i < $n; $i++)
    {
        if ($arr[$i] % $k == 0)
            $res = min($res, $arr[$i]);
    }
    return $res;
}

// Function to find the maximum element
function getMax($arr, $n, $k)
{
    $res = PHP_INT_MIN;
    for ($i = 1; $i < $n; $i++)
    {
        if ($arr[$i] % $k == 0)
            $res = max($res, $arr[$i]);
    }
    return $res;
}

// Driver code
$arr = array( 10, 1230, 45, 67, 1 );
$k = 10;
$n = sizeof($arr);
echo "Minimum element of array which is " .
     "divisible by k: ", getMin($arr, $n, $k) , "\n";
echo "Maximum element of array which is " .
     "divisible by k: ", getMax($arr, $n, $k);

// This code is contributed by akt_mit
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

// Function to find the minimum element
function getMin(arr, n, k)
{
    let res = Number.MAX_VALUE;
    for (let i = 0; i < n; i++) {
        if (arr[i] % k == 0)
            res = Math.min(res, arr[i]);
    }
    return res;
}

// Function to find the maximum element
function getMax(arr, n, k)
{
    let res = Number.MIN_VALUE;
    for (let i = 1; i < n; i++) {
        if (arr[i] % k == 0)
            res = Math.max(res, arr[i]);
    }
    return res;
}

// Driver code
    let arr = [ 10, 1230, 45, 67, 1 ];
    let k = 10;
    let n = arr.length;
    document.write("Minimum element of array which is divisible by k: "
         + getMin(arr, n, k) + "<br>");
    document.write("Maximum element of array which is divisible by k: "
         + getMax(arr, n, k));

</script>
```

**Output:** 

```
Minimum element of array which is divisible by k: 10
Maximum element of array which is divisible by k: 1230
```