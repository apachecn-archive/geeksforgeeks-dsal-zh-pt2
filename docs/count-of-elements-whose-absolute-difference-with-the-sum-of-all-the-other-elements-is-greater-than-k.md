# 与所有其他元素之和的绝对差大于 k 的元素计数

> 原文:[https://www . geesforgeks . org/元素计数-其与所有其他元素之和的绝对差值大于-k/](https://www.geeksforgeeks.org/count-of-elements-whose-absolute-difference-with-the-sum-of-all-the-other-elements-is-greater-than-k/)

给定一个由 **N** 个整数和一个整数 **K** 组成的数组 **arr[]** ，任务是找出数组中异常的数量。异常是指其与数组中所有其他数字的绝对差值大于 **K** 的数字。找出异常的数量。

**示例:**

> **输入:** arr[] = {1，3，5}，k = 1
> **输出:** 2
> 1 和 3 为异常。
> | 1 –( 3+5)| = 7>1
> | 3 –( 1+5)| = 3>1
> 
> **输入:** arr[] = {7，1，8}，k = 5
> **输出:** 1

**方法:**求所有数组元素的和并存储在 **sum** 中，现在对于数组的每个元素 **arr[i]** 如果 **arr[i]** 与**sum–arr[I]**的绝对差是 **> k** ，那么就是异常。统计数组中的所有异常，最后打印结果。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the number of anomalies
static int countAnomalies(int arr[],
                          int n, int k)
{

    // To store the count of anomalies
    int cnt = 0;

    // To store the sum of the array elements
    int i, sum = 0;

    // Find the sum of the array elements
    for (i = 0; i < n; i++)
        sum += arr[i];

    // Count the anomalies
    for (i = 0; i < n; i++)
        if (abs(arr[i] -
               (sum - arr[i])) > k)
            cnt++;

    return cnt;
}

// Driver code
int main()
{
    int arr[] = { 1, 3, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 1;
    cout << countAnomalies(arr, n, k);
}

// This code is contributed
// by Code_Mech
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the number of anomalies
    static int countAnomalies(int arr[], int n, int k)
    {

        // To store the count of anomalies
        int cnt = 0;

        // To store the sum of the array elements
        int i, sum = 0;

        // Find the sum of the array elements
        for (i = 0; i < n; i++)
            sum += arr[i];

        // Count the anomalies
        for (i = 0; i < n; i++)
            if (Math.abs(arr[i] - (sum - arr[i])) > k)
                cnt++;

        return cnt;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 3, 5 };
        int n = arr.length;
        int k = 1;
        System.out.print(countAnomalies(arr, n, k));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the
# number of anomalies
def countAnomalies(arr, n, k):

    # To store the count of anomalies
    cnt = 0

    # To store the Sum of
    # the array elements
    i, Sum = 0, 0

    # Find the Sum of the array elements
    for i in range(n):
        Sum += arr[i]

    # Count the anomalies
    for i in range(n):
        if (abs(arr[i] - (Sum - arr[i])) > k):
            cnt += 1

    return cnt

# Driver code
arr = [1, 3, 5]
n = len(arr)
k = 1
print(countAnomalies(arr, n, k))

# This code is contributed
# by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the number of anomalies
    static int countAnomalies(int[] arr, int n, int k)
    {

        // To store the count of anomalies
        int cnt = 0;

        // To store the sum of the array elements
        int i, sum = 0;

        // Find the sum of the array elements
        for (i = 0; i < n; i++)
            sum += arr[i];

        // Count the anomalies
        for (i = 0; i < n; i++)
            if (Math.Abs(arr[i] - (sum - arr[i])) > k)
                cnt++;

        return cnt;
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 1, 3, 5 };
        int n = arr.Length;
        int k = 1;
        Console.WriteLine(countAnomalies(arr, n, k));
    }
}

// This code is contributed by Code_Mech.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return
// the number of anomalies
function countAnomalies($arr, $n, $k)
{

    // To store the count of anomalies
    $cnt = 0;

    // To store the sum of
    // the array elements
    $sum = 0;

    // Find the sum of the array elements
    for ($i = 0; $i < $n; $i++)
        $sum += $arr[$i];

    // Count the anomalies
    for ($i = 0; $i < $n; $i++)
        if (abs($arr[$i] -
               ($sum - $arr[$i])) > $k)
            $cnt++;

    return $cnt;
}

// Driver code
$arr = array(1, 3, 5);
$n = count($arr);
$k = 1;

echo countAnomalies($arr, $n, $k);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the number of anomalies
function countAnomalies(arr, n, k)
{

    // To store the count of anomalies
    var cnt = 0;

    // To store the sum of the array elements
    var i, sum = 0;

    // Find the sum of the array elements
    for(i = 0; i < n; i++)
        sum += arr[i];

    // Count the anomalies
    for(i = 0; i < n; i++)
        if (Math.abs(arr[i] - (sum - arr[i])) > k)
            cnt++;

    return cnt;
}

// Driver code
var arr = [ 1, 3, 5 ];
var n = arr.length;
var k = 1;

document.write(countAnomalies(arr, n, k));

// This code is contributed by umadevi9616

</script>
```

**Output:** 

```
2
```