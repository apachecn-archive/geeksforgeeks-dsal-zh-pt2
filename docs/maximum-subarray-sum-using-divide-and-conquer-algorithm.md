# 使用分治算法的最大子阵和

> 原文:[https://www . geesforgeks . org/maximum-subarray-sum-使用分治算法/](https://www.geeksforgeeks.org/maximum-subarray-sum-using-divide-and-conquer-algorithm/)

给你一个一维数组，它可以包含正整数和负整数，求具有最大和的相邻数的子数组的和。

例如，如果给定的数组是{-2，-5， **6，-2，-3，1，5** ，-6}，那么最大子数组和是 7(参见突出显示的元素)。

**天真的方法**是运行两个循环。外部循环选择开始元素，内部循环找到外部循环选择的第一个元素的最大可能和，并将该最大值与总最大值进行比较。最后，返回整体最大值。朴素方法的时间复杂度是 O(n^2).

使用**分治**方法，我们可以在 O(nLogn)时间内找到最大子阵和。下面是分治算法。

1.  将给定的数组分成两半
2.  返回以下三个中的最大值
    *   左半部分的最大子阵列和(进行递归调用)
    *   右半部分的最大子阵列和(进行递归调用)
    *   最大子阵列和，使得子阵列穿过中点

第 2.a 和 2.b 行是简单的递归调用。如何求最大子阵和使得子阵过中点？我们可以很容易地在线性时间内找到交和。思路很简单，先求从中点开始到中点左边某点结束的最大和，然后求从中点+ 1 开始到中点+ 1 右边某点结束的最大和。最后，将两者结合起来，返回左、右和两者结合之间的最大值。

下面是上述方法的实现:

## C++

```
// A Divide and Conquer based program for maximum subarray
// sum problem
#include <limits.h>
#include <stdio.h>

// A utility function to find maximum of two integers
int max(int a, int b) { return (a > b) ? a : b; }

// A utility function to find maximum of three integers
int max(int a, int b, int c) { return max(max(a, b), c); }

// Find the maximum possible sum in arr[] auch that arr[m]
// is part of it
int maxCrossingSum(int arr[], int l, int m, int h)
{
    // Include elements on left of mid.
    int sum = 0;
    int left_sum = INT_MIN;
    for (int i = m; i >= l; i--) {
        sum = sum + arr[i];
        if (sum > left_sum)
            left_sum = sum;
    }

    // Include elements on right of mid
    sum = 0;
    int right_sum = INT_MIN;
    for (int i = m + 1; i <= h; i++) {
        sum = sum + arr[i];
        if (sum > right_sum)
            right_sum = sum;
    }

    // Return sum of elements on left and right of mid
    // returning only left_sum + right_sum will fail for
    // [-2, 1]
    return max(left_sum + right_sum, left_sum, right_sum);
}

// Returns sum of maximum sum subarray in aa[l..h]
int maxSubArraySum(int arr[], int l, int h)
{
    // Base Case: Only one element
    if (l == h)
        return arr[l];

    // Find middle point
    int m = (l + h) / 2;

    /* Return maximum of following three possible cases
            a) Maximum subarray sum in left half
            b) Maximum subarray sum in right half
            c) Maximum subarray sum such that the subarray
       crosses the midpoint */
    return max(maxSubArraySum(arr, l, m),
               maxSubArraySum(arr, m + 1, h),
               maxCrossingSum(arr, l, m, h));
}

/*Driver program to test maxSubArraySum*/
int main()
{
    int arr[] = { 2, 3, 4, 5, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int max_sum = maxSubArraySum(arr, 0, n - 1);
    printf("Maximum contiguous sum is %d\n", max_sum);
    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Divide and Conquer based Java
// program for maximum subarray sum
// problem
import java.util.*;

class GFG {

    // Find the maximum possible sum in arr[]
    // such that arr[m] is part of it
    static int maxCrossingSum(int arr[], int l, int m,
                              int h)
    {
        // Include elements on left of mid.
        int sum = 0;
        int left_sum = Integer.MIN_VALUE;
        for (int i = m; i >= l; i--) {
            sum = sum + arr[i];
            if (sum > left_sum)
                left_sum = sum;
        }

        // Include elements on right of mid
        sum = 0;
        int right_sum = Integer.MIN_VALUE;
        for (int i = m + 1; i <= h; i++) {
            sum = sum + arr[i];
            if (sum > right_sum)
                right_sum = sum;
        }

        // Return sum of elements on left
        // and right of mid
        // returning only left_sum + right_sum will fail for
        // [-2, 1]
        return Math.max(left_sum + right_sum,
                        Math.max(left_sum, right_sum));
    }

    // Returns sum of maximum sum subarray
    // in aa[l..h]
    static int maxSubArraySum(int arr[], int l, int h)
    {
        // Base Case: Only one element
        if (l == h)
            return arr[l];

        // Find middle point
        int m = (l + h) / 2;

        /* Return maximum of following three
        possible cases:
        a) Maximum subarray sum in left half
        b) Maximum subarray sum in right half
        c) Maximum subarray sum such that the
        subarray crosses the midpoint */
        return Math.max(
            Math.max(maxSubArraySum(arr, l, m),
                     maxSubArraySum(arr, m + 1, h)),
            maxCrossingSum(arr, l, m, h));
    }

    /* Driver program to test maxSubArraySum */
    public static void main(String[] args)
    {
        int arr[] = { 2, 3, 4, 5, 7 };
        int n = arr.length;
        int max_sum = maxSubArraySum(arr, 0, n - 1);

        System.out.println("Maximum contiguous sum is "
                           + max_sum);
    }
}
// This code is contributed by Prerna Saini
```

## 计算机编程语言

```
# A Divide and Conquer based program
# for maximum subarray sum problem

# Find the maximum possible sum in
# arr[] auch that arr[m] is part of it

def maxCrossingSum(arr, l, m, h):

    # Include elements on left of mid.
    sm = 0
    left_sum = -10000

    for i in range(m, l-1, -1):
        sm = sm + arr[i]

        if (sm > left_sum):
            left_sum = sm

    # Include elements on right of mid
    sm = 0
    right_sum = -1000
    for i in range(m + 1, h + 1):
        sm = sm + arr[i]

        if (sm > right_sum):
            right_sum = sm

    # Return sum of elements on left and right of mid
    # returning only left_sum + right_sum will fail for [-2, 1]
    return max(left_sum + right_sum, left_sum, right_sum)

# Returns sum of maximum sum subarray in aa[l..h]
def maxSubArraySum(arr, l, h):

    # Base Case: Only one element
    if (l == h):
        return arr[l]

    # Find middle point
    m = (l + h) // 2

    # Return maximum of following three possible cases
    # a) Maximum subarray sum in left half
    # b) Maximum subarray sum in right half
    # c) Maximum subarray sum such that the
    #     subarray crosses the midpoint
    return max(maxSubArraySum(arr, l, m),
               maxSubArraySum(arr, m+1, h),
               maxCrossingSum(arr, l, m, h))

# Driver Code
arr = [2, 3, 4, 5, 7]
n = len(arr)

max_sum = maxSubArraySum(arr, 0, n-1)
print("Maximum contiguous sum is ", max_sum)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// A Divide and Conquer based C#
// program for maximum subarray sum
// problem
using System;

class GFG {

    // Find the maximum possible sum in arr[]
    // such that arr[m] is part of it
    static int maxCrossingSum(int[] arr, int l, int m,
                              int h)
    {
        // Include elements on left of mid.
        int sum = 0;
        int left_sum = int.MinValue;
        for (int i = m; i >= l; i--) {
            sum = sum + arr[i];
            if (sum > left_sum)
                left_sum = sum;
        }

        // Include elements on right of mid
        sum = 0;
        int right_sum = int.MinValue;
        ;
        for (int i = m + 1; i <= h; i++) {
            sum = sum + arr[i];
            if (sum > right_sum)
                right_sum = sum;
        }

        // Return sum of elements on left
        // and right of mid
        // returning only left_sum + right_sum will fail for
        // [-2, 1]
        return Math.Max(left_sum + right_sum,
                        Math.Max(left_sum, right_sum));
    }

    // Returns sum of maximum sum subarray
    // in aa[l..h]
    static int maxSubArraySum(int[] arr, int l, int h)
    {

        // Base Case: Only one element
        if (l == h)
            return arr[l];

        // Find middle point
        int m = (l + h) / 2;

        /* Return maximum of following three
        possible cases:
        a) Maximum subarray sum in left half
        b) Maximum subarray sum in right half
        c) Maximum subarray sum such that the
        subarray crosses the midpoint */
        return Math.Max(
            Math.Max(maxSubArraySum(arr, l, m),
                     maxSubArraySum(arr, m + 1, h)),
            maxCrossingSum(arr, l, m, h));
    }

    /* Driver program to test maxSubArraySum */
    public static void Main()
    {
        int[] arr = { 2, 3, 4, 5, 7 };
        int n = arr.Length;
        int max_sum = maxSubArraySum(arr, 0, n - 1);

        Console.Write("Maximum contiguous sum is "
                      + max_sum);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A Divide and Conquer based program
// for maximum subarray sum problem

// Find the maximum possible sum in arr[]
// such that arr[m] is part of it
function maxCrossingSum(&$arr, $l, $m, $h)
{
    // Include elements on left of mid.
    $sum = 0;
    $left_sum = PHP_INT_MIN;
    for ($i = $m; $i >= $l; $i--)
    {
        $sum = $sum + $arr[$i];
        if ($sum > $left_sum)
        $left_sum = $sum;
    }

    // Include elements on right of mid
    $sum = 0;
    $right_sum = PHP_INT_MIN;
    for ($i = $m + 1; $i <= $h; $i++)
    {
        $sum = $sum + $arr[$i];
        if ($sum > $right_sum)
        $right_sum = $sum;
    }

    // Return sum of elements on left
    // and right of mid
    // returning only left_sum + right_sum will fail for [-2, 1]
    return max($left_sum + $right_sum, $left_sum, $right_sum);
}

// Returns sum of maximum sum
// subarray in aa[l..h]
function maxSubArraySum(&$arr, $l, $h)
{
    // Base Case: Only one element
    if ($l == $h)
        return $arr[$l];

    // Find middle point
    $m = intval(($l + $h) / 2);

    /* Return maximum of following three possible cases
        a) Maximum subarray sum in left half
        b) Maximum subarray sum in right half
        c) Maximum subarray sum such that the
        subarray crosses the midpoint */
    return max(maxSubArraySum($arr, $l, $m),
            maxSubArraySum($arr, $m + 1, $h),
            maxCrossingSum($arr, $l, $m, $h));
}

// Driver Code
$arr = array(2, 3, 4, 5, 7);
$n = count($arr);
$max_sum = maxSubArraySum($arr, 0, $n - 1);
echo "Maximum contiguous sum is " . $max_sum;

// This code is contributed by rathbhupendra, Aadil
?>
```

## java 描述语言

```
<script>
    // A Divide and Conquer based program for maximum subarray
    // sum problem

    // A utility function to find maximum of two integers
    function max(a,b) { return (a > b) ? a : b; }

    // A utility function to find maximum of three integers
    function max(a,b,c) { return Math.max(Math.max(a, b), c); }

    // Find the maximum possible sum in arr[] auch that arr[m]
    // is part of it
    function maxCrossingSum(arr, l, m,h)
    {
        // Include elements on left of mid.
        let sum = 0;
        let left_sum = Number.MIN_VALUE;
        for (let i = m; i >= l; i--) {
            sum = sum + arr[i];
            if (sum > left_sum)
                left_sum = sum;
        }

        // Include elements on right of mid
        sum = 0;
        let right_sum = Number.MIN_VALUE;
        for (let i = m + 1; i <= h; i++) {
            sum = sum + arr[i];
            if (sum > right_sum)
                right_sum = sum;
        }

        // Return sum of elements on left and right of mid
        // returning only left_sum + right_sum will fail for
        // [-2, 1]
        return max(left_sum + right_sum, left_sum, right_sum);
    }

    // Returns sum of maximum sum subarray in aa[l..h]
    function maxSubArraySum(arr, l,h)
    {
        // Base Case: Only one element
        if (l == h)
            return arr[l];

        // Find middle point
        let m = parseInt((l + h) / 2, 10);

        /* Return maximum of following three possible cases
                a) Maximum subarray sum in left half
                b) Maximum subarray sum in right half
                c) Maximum subarray sum such that the subarray
        crosses the midpoint */
        return max(maxSubArraySum(arr, l, m),
                maxSubArraySum(arr, m + 1, h),
                maxCrossingSum(arr, l, m, h));
    }

    let arr = [ 2, 3, 4, 5, 7 ];
    let n = arr.length;
    let max_sum = maxSubArraySum(arr, 0, n - 1);
    document.write("Maximum contiguous sum is " + max_sum);

  // This code is contributed by vaibhavrabadiya117. 
</script>
```

**Output**

```
Maximum contiguous sum is 21n
```

**时间复杂度:** maxSubArraySum()是递归方法，时间复杂度可以表示为以下递归关系。
T(n)= 2T(n/2)+θ(n)
以上递归类似于[合并排序](http://geeksquiz.com/merge-sort/)，可以用递归树法或者 Master 法求解。它属于主方法的情况二，递推的解是θ(nLogn)。

[**这个问题的卡丹算法**](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/) 需要 0(n)个时间。因此，卡丹的算法比分治法更好，但这个问题可以被认为是展示分治力量的一个很好的例子。上面简单的方法将数组分成两半，将时间复杂度从 O(n^2 降低到了零。

**参考文献:**
[Clifford Stein，Thomas H. Cormen，Charles E. Leiserson，Ronald L.](http://www.flipkart.com/introduction-algorithms-8120340078/p/itmczynzhyhxv2gs?pid=9788120340077&affid=sandeepgfg) 算法导论
如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论。