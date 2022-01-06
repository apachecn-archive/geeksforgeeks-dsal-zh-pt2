# 计算子阵列的数量，使得子阵列中存在的元素的平均值大于子阵列中不存在的元素的平均值

> 原文:[https://www . geesforgeks . org/count-子阵列的数量-子阵列中存在的元素的平均值大于子阵列中不存在的元素的平均值/](https://www.geeksforgeeks.org/count-the-number-of-sub-arrays-such-that-the-average-of-elements-present-in-the-sub-array-is-greater-than-that-not-present-in-the-sub-array/)

给定整数数组 **arr[]** ，任务是计算子数组的数量，使得子数组中存在的元素的平均值大于子数组中不存在的元素的平均值。
**例:**

> **输入:** arr[] = {6，3，5}
> **输出:** 3
> 子数组分别为{6}、{5}和{6，3，5}，因为它们的平均值
> 分别大于{3，5}、{6，3}和{}。
> **输入:** arr[] = {2，1，4，1}
> **输出:** 5

**方法:**通过计算给定数组的[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)可以很容易地解决这个问题。前缀和数组的第元素的*将包含直到第 *i* 个元素的和。因此，任何两个索引 *i* 和 *j* 之间的元素之和都可以使用前缀和数组来找到。使用嵌套循环，找到所有可能的子数组，使其平均和大于数组中不存在的元素的平均值。
以下是上述方法的实施:* 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of sub-arrays
// such that the average of elements present
// in the sub-array is greater than the
// average of the elements not present
// in the sub-array
int countSubarrays(int a[], int n)
{
    // Initialize the count variable
    int count = 0;

    // Initialize prefix sum array
    int pre[n + 1] = { 0 };

    // Preprocessing prefix sum
    for (int i = 1; i < n + 1; i++) {
        pre[i] = pre[i - 1] + a[i - 1];
    }

    for (int i = 1; i < n + 1; i++) {
        for (int j = i; j < n + 1; j++) {

            // Calculating sum and count
            // to calculate averages
            int sum1 = pre[j] - pre[i - 1], count1 = j - i + 1;
            int sum2 = pre[n] - sum1, count2 = ((n - count1) == 0) ? 1 : (n - count1);

            // Calculating averages
            int includ = sum1 / count1;
            int exclud = sum2 / count2;

            // Increment count if including avg
            // is greater than excluding avg
            if (includ > exclud)
                count++;
        }
    }

    return count;
}

// Driver code
int main()
{
    int arr[] = { 6, 3, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countSubarrays(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the count of sub-arrays
// such that the average of elements present
// in the sub-array is greater than the
// average of the elements not present
// in the sub-array
static int countSubarrays(int a[], int n)
{
    // Initialize the count variable
    int count = 0;

    // Initialize prefix sum array
    int []pre = new int[n + 1];
    Arrays.fill(pre, 0);

    // Preprocessing prefix sum
    for (int i = 1; i < n + 1; i++)
    {
        pre[i] = pre[i - 1] + a[i - 1];
    }

    for (int i = 1; i < n + 1; i++)
    {
        for (int j = i; j < n + 1; j++)
        {

            // Calculating sum and count
            // to calculate averages
            int sum1 = pre[j] - pre[i - 1], count1 = j - i + 1;
            int sum2 = pre[n] - sum1, count2 =
                ((n - count1) == 0) ? 1 : (n - count1);

            // Calculating averages
            int includ = sum1 / count1;
            int exclud = sum2 / count2;

            // Increment count if including avg
            // is greater than excluding avg
            if (includ > exclud)
                count++;
        }
    }
    return count;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 6, 3, 5 };
    int n = arr.length;
    System.out.println(countSubarrays(arr, n));
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of sub-arrays
# such that the average of elements present
# in the sub-array is greater than the
# average of the elements not present
# in the sub-array
def countSubarrays(a, n):

    # Initialize the count variable
    count = 0

    # Initialize prefix sum array
    pre = [0 for i in range(n + 1)]

    # Preprocessing prefix sum
    for i in range(1, n + 1):
        pre[i] = pre[i - 1] + a[i - 1]

    for i in range(1, n + 1):
        for j in range(i, n + 1):

            # Calculating sum and count
            # to calculate averages
            sum1 = pre[j] - pre[i - 1]
            count1 = j - i + 1
            sum2 = pre[n] - sum1

            if n-count1 == 0:
                count2 = 1
            else:
                count2 = n - count1

            # Calculating averages
            includ = sum1 // count1
            exclud = sum2 // count2

            # Increment count if including avg
            # is greater than excluding avg
            if (includ > exclud):
                count += 1

    return count

# Driver code
arr = [6, 3, 5 ]
n = len(arr)
print(countSubarrays(arr, n))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of sub-arrays
// such that the average of elements present
// in the sub-array is greater than the
// average of the elements not present
// in the sub-array
static int countSubarrays(int []a, int n)
{
    // Initialize the count variable
    int count = 0;

    // Initialize prefix sum array
    int []pre = new int[n + 1];
    Array.Fill(pre, 0);

    // Preprocessing prefix sum
    for (int i = 1; i < n + 1; i++)
    {
        pre[i] = pre[i - 1] + a[i - 1];
    }

    for (int i = 1; i < n + 1; i++)
    {
        for (int j = i; j < n + 1; j++)
        {

            // Calculating sum and count
            // to calculate averages
            int sum1 = pre[j] - pre[i - 1], count1 = j - i + 1;
            int sum2 = pre[n] - sum1, count2 =
                ((n - count1) == 0) ? 1 : (n - count1);

            // Calculating averages
            int includ = sum1 / count1;
            int exclud = sum2 / count2;

            // Increment count if including avg
            // is greater than excluding avg
            if (includ > exclud)
                count++;
        }
    }
    return count;
}

// Driver code
public static void Main()
{
    int []arr = { 6, 3, 5 };
    int n = arr.Length;
    Console.WriteLine(countSubarrays(arr, n));
}
}

// This code is contributed by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count of sub-arrays
// such that the average of elements present
// in the sub-array is greater than the
// average of the elements not present
// in the sub-array
function countSubarrays($a, $n)
{
    // Initialize the count variable
    $count = 0;

    // Initialize prefix sum array
    $pre = array_fill(0, $n + 1, 0);

    // Preprocessing prefix sum
    for ($i = 1; $i < $n + 1; $i++)
    {
        $pre[$i] = $pre[$i - 1] + $a[$i - 1];
    }

    for ($i = 1; $i < $n + 1; $i++)
    {
        for ($j = $i; $j < $n + 1; $j++)
        {

            // Calculating sum and count
            // to calculate averages
            $sum1 = $pre[$j] - $pre[$i - 1] ;
            $count1 = $j - $i + 1;
            $sum2 = $pre[$n] - $sum1;
            $count2 = (($n - $count1) == 0) ?
                   1 : ($n - $count1);

            // Calculating averages
            $includ = floor($sum1 / $count1);
            $exclud = floor($sum2 / $count2);

            // Increment count if including avg
            // is greater than excluding avg
            if ($includ > $exclud)
                $count++;
        }
    }

    return $count;
}

// Driver code
$arr = array( 6, 3, 5 );

$n = count($arr) ;

echo countSubarrays($arr, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the count of sub-arrays
// such that the average of elements present
// in the sub-array is greater than the
// average of the elements not present
// in the sub-array
function countSubarrays(a, n)
{
    // Initialize the count variable
    let count = 0;

    // Initialize prefix sum array
    let pre = new Uint8Array(n + 1);

    // Preprocessing prefix sum
    for (let i = 1; i < n + 1; i++) {
        pre[i] = pre[i - 1] + a[i - 1];
    }

    for (let i = 1; i < n + 1; i++) {
        for (let j = i; j < n + 1; j++) {

            // Calculating sum and count
            // to calculate averages
            let sum1 = pre[j] - pre[i - 1], count1 = j - i + 1;
            let sum2 = pre[n] - sum1, count2 = ((n - count1) == 0) ? 1 : (n - count1);

            // Calculating averages
            let includ = Math.floor(sum1 / count1);
            let exclud = Math.floor(sum2 / count2);

            // Increment count if including avg
            // is greater than excluding avg
            if (includ > exclud)
                count++;
        }
    }

    return count;
}

// Driver code
    let arr = [ 6, 3, 5 ];
    let n = arr.length;
    document.write(countSubarrays(arr, n));

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N^2)其中 n 是数组的长度。