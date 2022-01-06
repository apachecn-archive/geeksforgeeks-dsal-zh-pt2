# 仅使用阵列元素均衡阵列

> 原文:[https://www . geesforgeks . org/equal-array-use-array-elements/](https://www.geeksforgeeks.org/equalize-array-using-array-elements/)

给定一个整数数组，任务是计算最小操作数来均衡数组(使所有数组元素相同)。如果无法均衡，则返回-1。为了均衡一个数组，我们需要将数值从较大的数字移动到较小的数字。操作次数等于移动次数。
**例:**

```
Input :  arr[] = {1, 3, 2, 0, 4}
Output : 3
We can equalize the array by making value
of all elements equal to 2\. To achieve this
we need to do minimum 3 operations (moving
Moving 1 value from arr[1] to arr[0]
Moving 2 values from arr[4] to arr[3]

Input : arr[] = {1, 7, 1}
Output : 4 
```

**方法 1(简单):**首先是蛮力方法，我们固定一个元素，然后检查相邻元素，然后借用(或给出)所需的操作量。在这种方法中，我们将需要两个循环，第一个循环用于固定数组的元素，第二个循环用于检查当前元素的其他相邻元素是否能够在均衡数组中做出贡献。该解的时间复杂度为 O(n<sup>2</sup>)；
**方法二(高效):**
1)求**和**数组元素。如果总和% n 不为 0，则返回-1。
2)计算平均值或均衡值，如**等式** = sum/n
3)遍历数组。对于每个元素 **arr[i]** 计算 **eq** 和 **arr[i]** 之间差值的绝对值。并记录这些差异的总和。让这个和成为**微分和**。
4)返回 diff_sum / 2。

## C++

```
// C++ program to find minimum operations
// needed to equalize an array.
#include <bits/stdc++.h>
using namespace std;

// Returns minimum operations needed to
// equalize an array.
int minOperations(int arr[], int n)
{
    // Compute sum of array elements
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    // If average of array is not integer,
    // then it is not possible to equalize
    if (sum % n != 0)
        return -1;

    // Compute sum of absolute differences
    // between array elements and average
    // or equalized value
    int diff_sum = 0;
    int eq = sum / n;
    for (int i = 0; i < n; i++)
        diff_sum += abs(arr[i] - eq);

    return (diff_sum / 2);
}

// Driver code
int main()
{
    int arr[] = { 5, 3, 2, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << minOperations(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum operations
// needed to equalize an array.
public class Equalize_Array {

    // Returns minimum operations needed to
    // equalize an array.
    static int minOperations(int arr[], int n)
    {
        // Compute sum of array elements
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += arr[i];

        // If average of array is not integer,
        // then it is not possible to equalize
        if (sum % n != 0)
            return -1;

        // Compute sum of absolute differences
        // between array elements and average
        // or equalized value
        int diff_sum = 0;
        int eq = sum / n;
        for (int i = 0; i < n; i++)
            diff_sum += Math.abs(arr[i] - eq);

        return (diff_sum / 2);
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 5, 3, 2, 6 };
        int n = arr.length;
        System.out.println(minOperations(arr, n));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 program to find minimum
# operations needed to equalize an array.

# Returns minimum operations needed
# to equalize an array.
def minOperations(arr, n):

    # Compute sum of array elements
    sum = 0
    for i in range(0,n):
        sum += arr[i]

    # If average of array is not integer,
    # then it is not possible to equalize
    if sum % n != 0:
        return -1

    # Compute sum of absolute differences
    # between array elements and average
    # or equalized value
    diff_sum = 0
    eq = sum / n
    for i in range(0, n):
        diff_sum += abs(arr[i] - eq)

    return int(diff_sum / 2)

# Driver code
arr = [5, 3, 2, 6 ]
n = len(arr)
print(minOperations(arr, n))

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// C# program to find minimum operations
// needed to equalize an array.
using System;

class Equalize_Array {

    // Returns minimum operations needed to
    // equalize an array.
    static int minOperations(int []arr, int n)
    {
        // Compute sum of array elements
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += arr[i];

        // If average of array is not integer,
        // then it is not possible to equalize
        if (sum % n != 0)
            return -1;

        // Compute sum of absolute differences
        // between array elements and average
        // or equalized value
        int diff_sum = 0;
        int eq = sum / n;
        for (int i = 0; i < n; i++)
            diff_sum += Math.Abs(arr[i] - eq);

        return (diff_sum / 2);
    }

    // Driver code
    public static void Main()
    {
        int []arr = {5, 3, 2, 6};
        int n = arr.Length;
        Console.WriteLine(minOperations(arr, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum
// operations needed to
// equalize an array.

// Returns minimum operations
// needed to equalize an array.
function minOperations($arr, $n)
{
    // Compute sum of
    // array elements
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
        $sum += $arr[$i];

    // If average of array is
    // not integer, then it is
    // not possible to equalize
    if ($sum % $n != 0)
        return -1;

    // Compute sum of absolute
    // differences between array
    // elements and average or
    // equalized value
    $diff_sum = 0;
    $eq = $sum / $n;
    for ($i = 0; $i < $n; $i++)
        $diff_sum += abs($arr[$i] -
                         $eq);

    return ($diff_sum / 2);
}

// Driver code
$arr = array(5, 3, 2, 6);
$n = count($arr);
echo minOperations($arr, $n);

// This code is contributed
// by anuj_67.
?>
```

## java 描述语言

```
<script>

    // JavaScript program to find minimum operations
    // needed to equalize an array.

    // Returns minimum operations needed to
    // equalize an array.
    function minOperations(arr, n)
    {
        // Compute sum of array elements
        let sum = 0;
        for (let i = 0; i < n; i++)
            sum += arr[i];

        // If average of array is not integer,
        // then it is not possible to equalize
        if (sum % n != 0)
            return -1;

        // Compute sum of absolute differences
        // between array elements and average
        // or equalized value
        let diff_sum = 0;
        let eq = parseInt(sum / n, 10);
        for (let i = 0; i < n; i++)
            diff_sum += Math.abs(arr[i] - eq);

        return parseInt(diff_sum / 2, 10);
    }

    let arr = [5, 3, 2, 6];
    let n = arr.length;
    document.write(minOperations(arr, n));

</script>
```

**输出:**

```
3
```

本文由 **Mohak Agrawal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。