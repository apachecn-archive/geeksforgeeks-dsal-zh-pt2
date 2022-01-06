# 要移除的元素的最小数量，使得剩余元素的总和等于 k

> 原文:[https://www . geeksforgeeks . org/待移除元素的最小数量，使得剩余元素的总和等于 k/](https://www.geeksforgeeks.org/minimum-number-of-elements-to-be-removed-such-that-the-sum-of-the-remaining-elements-is-equal-to-k/)

给定一个整数数组 **arr[]** 和一个整数 **k** ，任务是找到需要从数组中移除的整数的最小数量，使得剩余元素的总和等于 **k** 。如果我们不能得到所需的金额，打印 **-1** 。
**举例:**

> **输入:** arr[] = {1，2，3}，k = 3
> **输出:** 1
> 要么移除 1 和 2 以将数组减少到{3}
> ，要么移除 3 以获得数组{1，2}。两者的总和相等，即 3
> 但移除 3 只需要一次移除。
> **输入:** arr[] = {1，3，2，5，6}，k = 5
> **输出:** 3

**方法:**思路是使用滑动窗口和变量 **j** 初始化为 0， **min_num** 存储答案，**求和**存储当前求和。继续将数组的元素加到变量**和**上，直到大于等于 k，如果等于 k，那么更新 **min_num** 为 min_num 和(n -(i+1) +j) 的**最小值，其中 n 为数组中的整数个数，I 为当前索引，否则大于 k， 然后通过从 sum 中移除数组的值开始递减 sum，直到 sum 变得小于或等于 k，同时增加 **j** 的值，如果 sum 等于 k，则再次更新 **min_num** 。 重复整个过程，直到数组结束。
以下是上述方法的实施:** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum number of
// integers that need to be removed from the
// array to form a sub-array with sum k
int FindMinNumber(int arr[], int n, int k)
{
    int i = 0;
    int j = 0;

    // Stores the minimum number of
    // integers that need to be removed
    // from the array
    int min_num = INT_MAX;

    bool found = false;

    int sum = 0;

    while (i < n) {

        sum = sum + arr[i];

        // If current sum is equal to
        // k, update min_num
        if (sum == k) {
            min_num = min(min_num, ((n - (i + 1)) + j));
            found = true;
        }

        // If current sum is greater than k
        else if (sum > k) {

            // Decrement the sum until it
            // becomes less than or equal to k
            while (sum > k) {
                sum = sum - arr[j];
                j++;
            }
            if (sum == k) {
                min_num = min(min_num, ((n - (i + 1)) + j));
                found = true;
            }
        }

        i++;
    }

    if (found)
        return min_num;

    return -1;
}

// Driver code
int main()
{
    int arr[] = { 1, 3, 2, 5, 6 };
    int n = sizeof(arr) / sizeof(int);
    int k = 5;

    cout << FindMinNumber(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the minimum number of
// integers that need to be removed from the
// array to form a sub-array with sum k
static int FindMinNumber(int arr[], int n, int k)
{
    int i = 0;
    int j = 0;

    // Stores the minimum number of
    // integers that need to be removed
    // from the array
    int min_num = Integer.MAX_VALUE;

    boolean found = false;

    int sum = 0;

    while (i < n)
    {

        sum = sum + arr[i];

        // If current sum is equal to
        // k, update min_num
        if (sum == k)
        {
            min_num = Math.min(min_num,
                             ((n - (i + 1)) + j));
            found = true;
        }

        // If current sum is greater than k
        else if (sum > k)
        {

            // Decrement the sum until it
            // becomes less than or equal to k
            while (sum > k)
            {
                sum = sum - arr[j];
                j++;
            }
            if (sum == k)
            {
                min_num = Math.min(min_num,
                                 ((n - (i + 1)) + j));
                found = true;
            }
        }

        i++;
    }

    if (found)
        return min_num;

    return -1;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 3, 2, 5, 6 };
    int n = arr.length;
    int k = 5;

    System.out.println(FindMinNumber(arr, n, k));
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum number of
# integers that need to be removed from the
# array to form a sub-array with Sum k
def FindMinNumber(arr, n, k):
    i = 0
    j = 0

    # Stores the minimum number of
    # integers that need to be removed
    # from the array
    min_num = 10**9

    found = False

    Sum = 0

    while (i < n):

        Sum = Sum + arr[i]

        # If current Sum is equal to
        # k, update min_num
        if (Sum == k):
            min_num = min(min_num,
                        ((n - (i + 1)) + j))
            found = True

        # If current Sum is greater than k
        elif (Sum > k):

            # Decrement the Sum until it
            # becomes less than or equal to k
            while (Sum > k):
                Sum = Sum - arr[j]
                j += 1
            if (Sum == k):
                min_num = min(min_num,
                            ((n - (i + 1)) + j))
                found = True

        i += 1

    if (found):
        return min_num

    return -1

# Driver code
arr = [1, 3, 2, 5, 6]
n = len(arr)
k = 5

print(FindMinNumber(arr, n, k))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the minimum number of
// integers that need to be removed from the
// array to form a sub-array with sum k
static int FindMinNumber(int[] arr, int n, int k)
{
    int i = 0;
    int j = 0;

    // Stores the minimum number of
    // integers that need to be removed
    // from the array
    int min_num = int.MaxValue;

    bool found = false;

    int sum = 0;

    while (i < n)
    {

        sum = sum + arr[i];

        // If current sum is equal to
        // k, update min_num
        if (sum == k)
        {
            min_num = Math.Min(min_num,
                            ((n - (i + 1)) + j));
            found = true;
        }

        // If current sum is greater than k
        else if (sum > k)
        {

            // Decrement the sum until it
            // becomes less than or equal to k
            while (sum > k)
            {
                sum = sum - arr[j];
                j++;
            }
            if (sum == k)
            {
                min_num = Math.Min(min_num,
                                ((n - (i + 1)) + j));
                found = true;
            }
        }

        i++;
    }

    if (found)
        return min_num;

    return -1;
}

// Driver code
public static void Main()
{
    int[] arr = { 1, 3, 2, 5, 6 };
    int n = arr.Length;
    int k = 5;

    Console.WriteLine(FindMinNumber(arr, n, k));
}
}

// This code is contributed by Code_Mech
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
// Function to return the minimum number of
// integers that need to be removed from the
// array to form a sub-array with sum k
function FindMinNumber($arr,$n,$k)
{
    $i = 0;
    $j = 0;

    // Stores the minimum number of
    // integers that need to be removed
    // from the array
    $min_num = PHP_INT_MAX;

    $found = false;

    $sum = 0;

    while ($i < $n)
    {

        $sum = $sum + $arr[$i];

        // If current sum is equal to
        // k, update min_num
        if ($sum == $k)
        {
            $min_num = min($min_num,
                            (($n - ($i + 1)) + $j));
            $found = true;
        }

        // If current sum is greater than k
        else if ($sum > $k)
        {

            // Decrement the sum until it
            // becomes less than or equal to k
            while ($sum > $k)
            {
                $sum = $sum - $arr[$j];
                $j++;
            }
            if ($sum == $k)
            {
                $min_num =min($min_num,
                                (($n - ($i + 1)) + $j));
                $found = true;
            }
        }

        $i++;
    }

    if ($found)
        return $min_num;

    return -1;
}

// Driver code
$arr = array( 1, 3, 2, 5, 6 );
$n = sizeof($arr);
$k = 5;

echo(FindMinNumber($arr, $n, $k));

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the minimum number of
// integers that need to be removed from the
// array to form a sub-array with sum k
function FindMinNumber(arr,n,k)
{
    let i = 0;
    let j = 0;

    // Stores the minimum number of
    // integers that need to be removed
    // from the array
    let min_num = Number.MAX_VALUE; 
    let found = false;
    let sum = 0;
    while (i < n)
    {

        sum = sum + arr[i];

        // If current sum is equal to
        // k, update min_num
        if (sum == k)
        {
            min_num = Math.min(min_num,
                             ((n - (i + 1)) + j));
            found = true;
        }

        // If current sum is greater than k
        else if (sum > k)
        {

            // Decrement the sum until it
            // becomes less than or equal to k
            while (sum > k)
            {
                sum = sum - arr[j];
                j++;
            }
            if (sum == k)
            {
                min_num = Math.min(min_num,
                                 ((n - (i + 1)) + j));
                found = true;
            }
        }

        i++;
    }

    if (found)
        return min_num;

    return -1;
}

// Driver code
let arr = [1, 3, 2, 5, 6 ];
let n = arr.length;
let k = 5;
document.write(FindMinNumber(arr, n, k));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
3
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)