# 去掉 atmost 一个元素后最大化子阵和

> 原文:[https://www . geeksforgeeks . org/maximum-max-subarray-sum-remove-Atmos-one-element/](https://www.geeksforgeeks.org/maximize-the-maximum-subarray-sum-after-removing-atmost-one-element/)

给定一个由 **N** 个整数组成的数组 **arr[]** 。任务是首先找到最大子数组和，然后从子数组中最多移除一个元素。如果有多个子阵列具有最大子阵列总和，则最多移除单个元素，使得移除后的最大总和最大化。任务是最大化移除后获得的总和。
**注意:**你必须首先找到最大的子数组和，然后在必要时从那个子数组中移除元素。此外，在移除之后，子阵列大小应该至少为 1。
**示例:**

> **输入:** arr[] = {1，2，3，-2，3}
> **输出:** 9
> 最大子阵和由子阵{2，3，-2，3}
> 给出，因此，我们可以去掉-2 来进一步最大化子阵和。
> **输入:** arr[] = {-1，-2}
> **输出:** -1
> 最大子阵列和来自子阵列{-1}，无需移除。

**逼近**:用[卡丹算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)求最大子阵和。一旦找到和，重新应用[卡丹的算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)找到最大和，并做一些小的改变。在循环中使用两个额外的变量， **cnt** 和 **mini** 。变量 **cnt** 统计子阵列中的元素数量， **mini** 存储与最大子阵列具有相同和的所有子阵列中的最小值。如果由此获得的最小元素小于 **0** ，那么只有我们从子阵列中移除一个元素，否则我们不移除。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum sub-array sum
int maxSubArraySum(int a[], int size)
{

    // Initialized
    int max_so_far = INT_MIN, max_ending_here = 0;

    // Traverse in the array
    for (int i = 0; i < size; i++) {

        // Increase the sum
        max_ending_here = max_ending_here + a[i];

        // If sub-array sum is more than the previous
        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;

        // If sum is negative
        if (max_ending_here < 0)
            max_ending_here = 0;
    }
    return max_so_far;
}

// Function that returns the maximum sub-array sum
// after removing an element from the same sub-array
int maximizeSum(int a[], int n)
{
    int cnt = 0;
    int mini = INT_MAX;
    int minSubarray = INT_MAX;

    // Maximum sub-array sum using Kadane's Algorithm
    int sum = maxSubArraySum(a, n);

    int max_so_far = INT_MIN, max_ending_here = 0;

    // Re-apply Kadane's with minor changes
    for (int i = 0; i < n; i++) {

        // Increase the sum
        max_ending_here = max_ending_here + a[i];
        cnt++;
        minSubarray = min(a[i], minSubarray);

        // If sub-array sum is greater than the previous
        if (sum == max_ending_here) {

            // If elements are 0, no removal
            if (cnt == 1)
                mini = min(mini, 0);

            // If elements are more, then store
            // the minimum value in the sub-array
            // obtained till now
            else
                mini = min(mini, minSubarray);
        }

        // If sum is negative
        if (max_ending_here < 0) {

            // Re-initialize everything
            max_ending_here = 0;
            cnt = 0;
            minSubarray = INT_MAX;
        }
    }

    return sum - mini;
}

// Driver code
int main()
{
    int a[] = { 1, 2, 3, -2, 3 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << maximizeSum(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the maximum sub-array sum
static int maxSubArraySum(int a[], int size)
{

    // Initialized
    int max_so_far = Integer.MIN_VALUE,
        max_ending_here = 0;

    // Traverse in the array
    for (int i = 0; i < size; i++)
    {

        // Increase the sum
        max_ending_here = max_ending_here + a[i];

        // If sub-array sum is more than the previous
        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;

        // If sum is negative
        if (max_ending_here < 0)
            max_ending_here = 0;
    }
    return max_so_far;
}

// Function that returns the maximum sub-array sum
// after removing an element from the same sub-array
static int maximizeSum(int a[], int n)
{
    int cnt = 0;
    int mini = Integer.MAX_VALUE;
    int minSubarray = Integer.MAX_VALUE;

    // Maximum sub-array sum
    // using Kadane's Algorithm
    int sum = maxSubArraySum(a, n);

    int max_so_far = Integer.MIN_VALUE,
        max_ending_here = 0;

    // Re-apply Kadane's with minor changes
    for (int i = 0; i < n; i++)
    {

        // Increase the sum
        max_ending_here = max_ending_here + a[i];
        cnt++;
        minSubarray = Math.min(a[i], minSubarray);

        // If sub-array sum is greater than the previous
        if (sum == max_ending_here)
        {

            // If elements are 0, no removal
            if (cnt == 1)
                mini = Math.min(mini, 0);

            // If elements are more, then store
            // the minimum value in the sub-array
            // obtained till now
            else
                mini = Math.min(mini, minSubarray);
        }

        // If sum is negative
        if (max_ending_here < 0)
        {

            // Re-initialize everything
            max_ending_here = 0;
            cnt = 0;
            minSubarray = Integer.MAX_VALUE;
        }
    }

    return sum - mini;
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 1, 2, 3, -2, 3 };
    int n = a.length;
    System.out.println(maximizeSum(a, n));
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys;

# Function to return the maximum sub-array sum
def maxSubArraySum(a, size) :

    # Initialized
    max_so_far = -(sys.maxsize - 1);
    max_ending_here = 0;

    # Traverse in the array
    for i in range(size) :

        # Increase the sum
        max_ending_here = max_ending_here + a[i];

        # If sub-array sum is more than the previous
        if (max_so_far < max_ending_here) :
            max_so_far = max_ending_here;

        # If sum is negative
        if (max_ending_here < 0) :
            max_ending_here = 0;

    return max_so_far;

# Function that returns the maximum
# sub-array sum after removing an
# element from the same sub-array
def maximizeSum(a, n) :

    cnt = 0;
    mini = sys.maxsize;
    minSubarray = sys.maxsize;

    # Maximum sub-array sum using
    # Kadane's Algorithm
    sum = maxSubArraySum(a, n);

    max_so_far = -(sys.maxsize - 1);
    max_ending_here = 0;

    # Re-apply Kadane's with minor changes
    for i in range(n) :

        # Increase the sum
        max_ending_here = max_ending_here + a[i];
        cnt += 1;
        minSubarray = min(a[i], minSubarray);

        # If sub-array sum is greater
        # than the previous
        if (sum == max_ending_here) :

            # If elements are 0, no removal
            if (cnt == 1) :
                mini = min(mini, 0);

            # If elements are more, then store
            # the minimum value in the sub-array
            # obtained till now
            else :
                mini = min(mini, minSubarray);

        # If sum is negative
        if (max_ending_here < 0) :

            # Re-initialize everything
            max_ending_here = 0;
            cnt = 0;
            minSubarray = sys.maxsize;

    return sum - mini;

# Driver code
if __name__ == "__main__" :

    a = [ 1, 2, 3, -2, 3 ];
    n = len(a)

    print(maximizeSum(a, n));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the maximum sub-array sum
static int maxSubArraySum(int []a, int size)
{

    // Initialized
    int max_so_far = int.MinValue,
        max_ending_here = 0;

    // Traverse in the array
    for (int i = 0; i < size; i++)
    {

        // Increase the sum
        max_ending_here = max_ending_here + a[i];

        // If sub-array sum is more than the previous
        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;

        // If sum is negative
        if (max_ending_here < 0)
            max_ending_here = 0;
    }
    return max_so_far;
}

// Function that returns the maximum sub-array sum
// after removing an element from the same sub-array
static int maximizeSum(int []a, int n)
{
    int cnt = 0;
    int mini = int.MaxValue;
    int minSubarray = int.MaxValue;

    // Maximum sub-array sum
    // using Kadane's Algorithm
    int sum = maxSubArraySum(a, n);

    int max_so_far = int.MinValue,
        max_ending_here = 0;

    // Re-apply Kadane's with minor changes
    for (int i = 0; i < n; i++)
    {

        // Increase the sum
        max_ending_here = max_ending_here + a[i];
        cnt++;
        minSubarray = Math.Min(a[i], minSubarray);

        // If sub-array sum is greater than the previous
        if (sum == max_ending_here)
        {

            // If elements are 0, no removal
            if (cnt == 1)
                mini = Math.Min(mini, 0);

            // If elements are more, then store
            // the minimum value in the sub-array
            // obtained till now
            else
                mini = Math.Min(mini, minSubarray);
        }

        // If sum is negative
        if (max_ending_here < 0)
        {

            // Re-initialize everything
            max_ending_here = 0;
            cnt = 0;
            minSubarray = int.MaxValue;
        }
    }

    return sum - mini;
}

// Driver code
public static void Main(String[] args)
{
    int []a = { 1, 2, 3, -2, 3 };
    int n = a.Length;
    Console.WriteLine(maximizeSum(a, n));
}
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the maximum sub-array sum
function maxSubArraySum($a, $size)
{

    // Initialized
    $max_so_far = PHP_INT_MIN;
    $max_ending_here = 0;

    // Traverse in the array
    for ( $i = 0; $i < $size; $i++)
    {

        // Increase the sum
        $max_ending_here = $max_ending_here + $a[$i];

        // If sub-array sum is more than the previous
        if ($max_so_far < $max_ending_here)
            $max_so_far = $max_ending_here;

        // If sum is negative
        if ($max_ending_here < 0)
            $max_ending_here = 0;
    }
    return $max_so_far;
}

// Function that returns the maximum sub-array sum
// after removing an element from the same sub-array
function maximizeSum($a, $n)
{
    $cnt = 0;
    $mini = PHP_INT_MAX;
    $minSubarray = PHP_INT_MAX;

    // Maximum sub-array sum using Kadane's Algorithm
    $sum = maxSubArraySum($a, $n);

    $max_so_far = PHP_INT_MIN;
    $max_ending_here = 0;

    // Re-apply Kadane's with minor changes
    for ($i = 0; $i < $n; $i++)
    {

        // Increase the sum
        $max_ending_here = $max_ending_here + $a[$i];
        $cnt++;
        $minSubarray = min($a[$i], $minSubarray);

        // If sub-array sum is greater than the previous
        if ($sum == $max_ending_here)
        {

            // If elements are 0, no removal
            if ($cnt == 1)
                $mini = min($mini, 0);

            // If elements are more, then store
            // the minimum value in the sub-array
            // obtained till now
            else
                $mini = min($mini, $minSubarray);
        }

        // If sum is negative
        if ($max_ending_here < 0)
        {

            // Re-initialize everything
            $max_ending_here = 0;
            $cnt = 0;
            $minSubarray = PHP_INT_MAX;
        }
    }
    return $sum - $mini;
}

    // Driver code
    $a = array( 1, 2, 3, -2, 3 );
    $n = sizeof($a) / sizeof($a[0]);
    echo maximizeSum($a, $n);

// This code is contributed by Tushil.
?>
```

## java 描述语言

```
<script>
// Java script implementation of the approach

// Function to return the maximum sub-array sum
function maxSubArraySum(a,size)
{

    // Initialized
    let max_so_far = Number.MIN_VALUE,
        max_ending_here = 0;

    // Traverse in the array
    for (let i = 0; i < size; i++)
    {

        // Increase the sum
        max_ending_here = max_ending_here + a[i];

        // If sub-array sum is more than the previous
        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;

        // If sum is negative
        if (max_ending_here < 0)
            max_ending_here = 0;
    }
    return max_so_far;
}

// Function that returns the maximum sub-array sum
// after removing an element from the same sub-array
function maximizeSum(a,n)
{
    let cnt = 0;
    let mini = Number.MAX_VALUE;
    let minSubarray = Number.MAX_VALUE;

    // Maximum sub-array sum
    // using Kadane's Algorithm
    let sum = maxSubArraySum(a, n);

    let max_so_far = Number.MIN_VALUE,
        max_ending_here = 0;

    // Re-apply Kadane's with minor changes
    for (let i = 0; i < n; i++)
    {

        // Increase the sum
        max_ending_here = max_ending_here + a[i];
        cnt++;
        minSubarray = Math.min(a[i], minSubarray);

        // If sub-array sum is greater than the previous
        if (sum == max_ending_here)
        {

            // If elements are 0, no removal
            if (cnt == 1)
                mini = Math.min(mini, 0);

            // If elements are more, then store
            // the minimum value in the sub-array
            // obtained till now
            else
                mini = Math.min(mini, minSubarray);
        }

        // If sum is negative
        if (max_ending_here < 0)
        {

            // Re-initialize everything
            max_ending_here = 0;
            cnt = 0;
            minSubarray = Integer.MAX_VALUE;
        }
    }

    return sum - mini;
}

// Driver code

    let a = [ 1, 2, 3, -2, 3 ];
    let n = a.length;
    document.write(maximizeSum(a, n));

// This code is contributed by sravan kumar Gottumukkala
</script>
```

**Output:** 

```
9
```