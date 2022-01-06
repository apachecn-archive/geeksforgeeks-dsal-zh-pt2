# 最多去除一个元素的最大和子阵列

> 原文:[https://www . geesforgeks . org/max-sum-subarray-remove-one-element/](https://www.geeksforgeeks.org/maximum-sum-subarray-removing-one-element/)

给定一个数组，我们需要找到最大和子数组，去掉一个元素也是可以得到最大和的。

**示例:**

```
Input  : arr[] = {1, 2, 3, -4, 5}
Output : 11
Explanation : We can get maximum sum subarray by
removing -4.

Input  : arr[] = [-2, -3, 4, -1, -2, 1, 5, -3]
Output : 9
Explanation : We can get maximum sum subarray by
removing -2 as, [4, -1, 1, 5] summing 9, which is 
the maximum achievable sum.
```

如果没有应用元素移除条件，我们可以使用卡丹算法来解决这个问题，但是这里也可以移除一个元素来增加最大和。这种情况可以用两个数组来处理，前向数组和后向数组，这些数组分别存储从起始到第 I 个索引，以及从第 I 个索引到结束的当前最大子数组和。
在下面的代码中，编写了两个循环，首先一个循环在 fw[]中存储正向最大电流和，另一个循环在 bw[]中存储反向最大电流和。获取当前最大值和上升值与卡丹的算法相同。
现在，当两个数组都被创建时，我们可以将它们用于一个元素移除条件，如下所示，在每个索引 I 处，忽略第 I 个元素后的最大子数组和将是 fw[i-1] + bw[i+1]，因此我们循环所有可能的 I 值，并在其中选择最大值。

解的总时间复杂度和空间复杂度为 O(N)

## C++

```
// C++ program to get maximum sum subarray removing
// at-most one element
#include <bits/stdc++.h>
using namespace std;

// Method returns maximum sum of all subarray where
// removing one element is also allowed
int maxSumSubarrayRemovingOneEle(int arr[], int n)
{
    // Maximum sum subarrays in forward and backward
    // directions
    int fw[n], bw[n];

    // Initialize current max and max so far.
    int cur_max = arr[0], max_so_far = arr[0];

    // calculating maximum sum subarrays in forward
    // direction
    fw[0] = arr[0];
    for (int i = 1; i < n; i++)
    {
        cur_max = max(arr[i], cur_max + arr[i]);
        max_so_far = max(max_so_far, cur_max);

        // storing current maximum till ith, in
        // forward array
        fw[i] = cur_max;
    }

    // calculating maximum sum subarrays in backward
    // direction
    cur_max = max_so_far = bw[n-1] = arr[n-1];
    for (int i = n-2; i >= 0; i--)
    {
        cur_max = max(arr[i], cur_max + arr[i]);
        max_so_far = max(max_so_far, cur_max);

        // storing current maximum from ith, in
        // backward array
        bw[i] = cur_max;
    }

    /* Initializing final ans by max_so_far so that,
        case when no element is removed to get max sum
        subarray is also handled */
    int fans = max_so_far;

    // choosing maximum ignoring ith element
    for (int i = 1; i < n - 1; i++)
        fans = max(fans,max(0, fw[i - 1]) +max(0, bw[i + 1]));
  // In this condition we are checking when removing the ith element
  //so checking the max(0,left)+max(0,right), because maybe left<0 || right<0 so it wont contribute to the answer
        if(fans==0){
          // if no positive element in array so return max_element
            return *max_element(arr,arr+n);
        }
    return fans;

}

// Driver code to test above methods
int main()
{
    int arr[] = {-2, -3, 4, -1, -2, 1, 5, -3};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << maxSumSubarrayRemovingOneEle(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to get maximum sum subarray
// removing at-most one element
class GFG {

    // Method returns maximum sum of all subarray where
    // removing one element is also allowed
    static int maxSumSubarrayRemovingOneEle(int arr[],
                                                 int n)
    {

        // Maximum sum subarrays in forward and
        // backward directions
        int fw[] = new int[n];
        int bw[] = new int[n];

        // Initialize current max and max so far.
        int cur_max = arr[0], max_so_far = arr[0];

        // calculating maximum sum subarrays in forward
        // direction
        fw[0] = arr[0];

        for (int i = 1; i < n; i++) {

            cur_max = Math.max(arr[i], cur_max + arr[i]);
            max_so_far = Math.max(max_so_far, cur_max);

            // storing current maximum till ith, in
            // forward array
            fw[i] = cur_max;
        }

        // calculating maximum sum subarrays in backward
        // direction
        cur_max = max_so_far = bw[n - 1] = arr[n - 1];

        for (int i = n - 2; i >= 0; i--) {

            cur_max = Math.max(arr[i], cur_max + arr[i]);
            max_so_far = Math.max(max_so_far, cur_max);

            // storing current maximum from ith, in
            // backward array
            bw[i] = cur_max;
        }

        /* Initializing final ans by max_so_far so that,
        case when no element is removed to get max sum
        subarray is also handled */
        int fans = max_so_far;

        // choosing maximum ignoring ith element
        for (int i = 1; i < n - 1; i++)
            fans = Math.max(fans, fw[i - 1] + bw[i + 1]);

        return fans;
    }

    // Driver code
    public static void main(String arg[])
    {
        int arr[] = { -2, -3, 4, -1, -2, 1, 5, -3 };
        int n = arr.length;

        System.out.print(maxSumSubarrayRemovingOneEle(
                                             arr, n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 计算机编程语言

```
# Python program to get maximum sum subarray removing
# at-most one element

# Method returns maximum sum of all subarray where
# removing one element is also allowed
def maxSumSubarrayRemovingOneEle(arr, n):
    # Maximum sum subarrays in forward and backward
    # directions
    fw = [0 for k in range(n)]
    bw = [0 for k in range(n)]

    # Initialize current max and max so far.
    cur_max, max_so_far = arr[0], arr[0]
    fw[0] = cur_max

    # calculating maximum sum subarrays in forward
    # direction
    for i in range(1,n):
        cur_max = max(arr[i], cur_max + arr[i])
        max_so_far = max(max_so_far, cur_max)

        # storing current maximum till ith, in
        # forward array
        fw[i] = cur_max

    # calculating maximum sum subarrays in backward
    # direction
    cur_max = max_so_far = bw[n-1] = arr[n-1]
    i = n-2
    while i >= 0:
        cur_max = max(arr[i], cur_max + arr[i])
        max_so_far = max(max_so_far, cur_max)

        # storing current maximum from ith, in
        # backward array
        bw[i] = cur_max
        i -= 1

    #  Initializing final ans by max_so_far so that,
    #  case when no element is removed to get max sum
    #  subarray is also handled
    fans = max_so_far

    #  choosing maximum ignoring ith element
    for i in range(1,n-1):
        fans = max(fans, fw[i - 1] + bw[i + 1])

    return fans

#  Driver code to test above methods
arr = [-2, -3, 4, -1, -2, 1, 5, -3]
n = len(arr)
print  maxSumSubarrayRemovingOneEle(arr, n)

# Contributed by: Afzal_Saan
```

## C#

```
// C# program to get maximum sum subarray
// removing at-most one element
using System;
class GFG {

    // Method returns maximum sum of all subarray where
    // removing one element is also allowed
    static int maxSumSubarrayRemovingOneEle(int []arr,
                                                int n)
    {

        // Maximum sum subarrays in forward and
        // backward directions
        int []fw = new int[n];
        int []bw = new int[n];

        // Initialize current max and max so far.
        int cur_max = arr[0], max_so_far = arr[0];

        // calculating maximum sum subarrays in forward
        // direction
        fw[0] = arr[0];

        for (int i = 1; i < n; i++) {

            cur_max = Math.Max(arr[i], cur_max + arr[i]);
            max_so_far = Math.Max(max_so_far, cur_max);

            // storing current maximum till ith, in
            // forward array
            fw[i] = cur_max;
        }

        // calculating maximum sum subarrays in backward
        // direction
        cur_max = max_so_far = bw[n - 1] = arr[n - 1];

        for (int i = n - 2; i >= 0; i--) {

            cur_max = Math.Max(arr[i], cur_max + arr[i]);
            max_so_far = Math.Max(max_so_far, cur_max);

            // storing current maximum from ith, in
            // backward array
            bw[i] = cur_max;
        }

        /* Initializing final ans by max_so_far so that,
        case when no element is removed to get max sum
        subarray is also handled */
        int fans = max_so_far;

        // choosing maximum ignoring ith element
        for (int i = 1; i < n - 1; i++)
            fans = Math.Max(fans, fw[i - 1] + bw[i + 1]);

        return fans;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { -2, -3, 4, -1, -2, 1, 5, -3 };
        int n = arr.Length;

        Console.WriteLine(maxSumSubarrayRemovingOneEle(
                                            arr, n));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to get maximum
// sum subarray removing
// at-most one element

// Method returns maximum sum
// of all subarray where removing
// one element is also allowed
function maxSumSubarrayRemovingOneEle( $arr, $n)
{
    // Maximum sum subarrays in
    // forward and backward directions
    $fw = array(); $bw = array();

    // Initialize current
    // max and max so far.
    $cur_max = $arr[0];
    $max_so_far = $arr[0];

    // calculating maximum sum
    // subarrays in forward direction
    $fw[0] = $arr[0];
    for ($i = 1; $i < $n; $i++)
    {
        $cur_max = max($arr[$i],
                       $cur_max + $arr[$i]);
        $max_so_far = max($max_so_far,
                          $cur_max);

        // storing current maximum till
        // ith, in forward array
        $fw[$i] = $cur_max;
    }

    // calculating maximum sum
    // subarrays in backward direction
    $cur_max = $max_so_far =
    $bw[$n - 1] = $arr[$n - 1];
    for ( $i = $n - 2; $i >= 0; $i--)
    {
        $cur_max = max($arr[$i],
                       $cur_max + $arr[$i]);
        $max_so_far = max($max_so_far,
                          $cur_max);

        // storing current maximum from
        // ith, in backward array
        $bw[$i] = $cur_max;
    }

    /* Initializing final ans by
        max_so_far so that, case
        when no element is removed
        to get max sum subarray is
        also handled */
    $fans = $max_so_far;

    // choosing maximum
    // ignoring ith element
    for ($i = 1; $i < $n - 1; $i++)
        $fans = max($fans, $fw[$i - 1] +
                           $bw[$i + 1]);

    return $fans;
}

// Driver Code
$arr = array(-2, -3, 4, -1,
             -2, 1, 5, -3);
$n = count($arr);
echo maxSumSubarrayRemovingOneEle($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to get maximum sum subarray
// removing at-most one element

// Method returns maximum sum of all subarray where
// removing one element is also allowed
function maxSumSubarrayRemovingOneEle(arr, n)
{

    // Maximum sum subarrays in forward and
    // backward directions
    let fw = [];
    let bw = [];

    // Initialize current max and max so far.
    let cur_max = arr[0], max_so_far = arr[0];

    // calculating maximum sum subarrays in forward
    // direction
    fw[0] = arr[0];

    for(let i = 1; i < n; i++)
    {
        cur_max = Math.max(arr[i], cur_max + arr[i]);
        max_so_far = Math.max(max_so_far, cur_max);

        // Storing current maximum till ith,
        // in forward array
        fw[i] = cur_max;
    }

    // Calculating maximum sum subarrays
    // in backward direction
    cur_max = max_so_far = bw[n - 1] = arr[n - 1];

    for(let i = n - 2; i >= 0; i--)
    {
        cur_max = Math.max(arr[i], cur_max + arr[i]);
        max_so_far = Math.max(max_so_far, cur_max);

        // Storing current maximum from ith, in
        // backward array
        bw[i] = cur_max;
    }

    /* Initializing final ans by max_so_far so that,
    case when no element is removed to get max sum
    subarray is also handled */
    let fans = max_so_far;

    // Choosing maximum ignoring ith element
    for(let i = 1; i < n - 1; i++)
        fans = Math.max(fans, fw[i - 1] +
                              bw[i + 1]);

    return fans;
}

// Driver Code
let arr = [ -2, -3, 4, -1, -2, 1, 5, -3 ];
let n = arr.length;

document.write(
    maxSumSubarrayRemovingOneEle(arr, n));

</script>
```

**输出:**

```
9
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)

本文由 [**Vinish Thanai**](https://www.linkedin.com/in/vinish-thanai/) 投稿，如果你喜欢 GeeksforGeeks 并且愿意投稿，也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章，或者把文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。