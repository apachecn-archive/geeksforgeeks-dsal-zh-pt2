# 总和小于或等于给定总和的最大总和子阵列

> 原文:[https://www . geesforgeks . org/max-sum-subarray-sum-less-equal-given-sum/](https://www.geeksforgeeks.org/maximum-sum-subarray-sum-less-equal-given-sum/)

给定一组非负整数和一个和。我们必须找到最大和小于或等于阵列中给定和的子阵列的和。

(注意:给定数组只包含非负整数。)

**示例:**

```
Input : arr[] = { 1, 2, 3, 4, 5 }
        sum = 11
Output : 10
Subarray having maximum sum is { 1, 2, 3, 4 }

Input : arr[] = { 2, 4, 6, 8, 10 }
        sum = 7
Output : 6
Subarray having maximum sum is { 2, 4 } or { 6 }
```

**天真方法:**我们可以通过运行两个循环来找到子阵列的最大和。但是时间复杂度会是 O(N*N)。

**有效方法:**通过使用[滑动窗口](https://www.geeksforgeeks.org/window-sliding-technique/)可以找到具有最大和的子阵列。如果 curr_sum 小于 sum，则包含数组元素。如果大于总和，则从 curr_sum 中的开始处移除元素。(这仅在非负元素的情况下有效。)

## C++

```
// C++ program to find subarray having
// maximum sum less than or equal to sum
#include <bits/stdc++.h>
using namespace std;

// To find subarray with maximum sum
// less than or equal to sum
int findMaxSubarraySum(int arr[], int n, int sum)
{
    // To store current sum and
    // max sum of subarrays
    int curr_sum = arr[0], max_sum = 0, start = 0;

    // To find max_sum less than sum
    for (int i = 1; i < n; i++) {

        // Update max_sum if it becomes
        // greater than curr_sum
        if (curr_sum <= sum)
            max_sum = max(max_sum, curr_sum);

        // If curr_sum becomes greater than
        // sum subtract starting elements of array
        while (start < i && curr_sum + arr[i] > sum) {
            curr_sum -= arr[start];
            start++;
        }

        // If cur_sum becomes negative then start new subarray
        if (curr_sum < 0)
        {
            curr_sum = 0;
        }

        // Add elements to curr_sum
        curr_sum += arr[i];

    }

    // Adding an extra check for last subarray
    if (curr_sum <= sum)
        max_sum = max(max_sum, curr_sum);

    return max_sum;
}

// Driver program to test above function
int main()
{
    int arr[] = {6, 8, 9};
    int n = sizeof(arr) / sizeof(arr[0]);
    int sum = 20;

    cout << findMaxSubarraySum(arr, n, sum);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find subarray having
// maximum sum less than or equal to sum
public class Main {

    // To find subarray with maximum sum
    // less than or equal to sum
    static int findMaxSubarraySum(int arr[],
                             int n, int sum)
    {
    // To store current sum and
    // max sum of subarrays
    int curr_sum = arr[0], max_sum = 0, start = 0;

    // To find max_sum less than sum
    for (int i = 1; i < n; i++) {

        // Update max_sum if it becomes
        // greater than curr_sum
        if (curr_sum <= sum)
           max_sum = Math.max(max_sum, curr_sum);

        // If curr_sum becomes greater than
        // sum subtract starting elements of array
        while (curr_sum + arr[i] > sum && start < i) {
            curr_sum -= arr[start];
            start++;
        }

        // Add elements to curr_sum
        curr_sum += arr[i];
    }

    // Adding an extra check for last subarray
    if (curr_sum <= sum)
        max_sum = Math.max(max_sum, curr_sum);

    return max_sum;
    }

    // Driver program to test above function
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3, 4, 5 };
        int n = arr.length;
        int sum = 11;

        System.out.println(findMaxSubarraySum(arr, n, sum));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find subarray having
# maximum sum less than or equal to sum

# To find subarray with maximum sum
# less than or equal to sum
def findMaxSubarraySum(arr, n, sum):

    # To store current sum and
    # max sum of subarrays
    curr_sum = arr[0]
    max_sum = 0
    start = 0;

    # To find max_sum less than sum
    for i in range(1, n):

        # Update max_sum if it becomes
        # greater than curr_sum
        if (curr_sum <= sum):
            max_sum = max(max_sum, curr_sum)

        # If curr_sum becomes greater than sum
        # subtract starting elements of array
        while (curr_sum + arr[i] > sum and start < i):
            curr_sum -= arr[start]
            start += 1

        # Add elements to curr_sum
        curr_sum += arr[i]

    # Adding an extra check for last subarray
    if (curr_sum <= sum):
        max_sum = max(max_sum, curr_sum)

    return max_sum

# Driver Code
if __name__ == '__main__':
    arr = [6, 8, 9]
    n = len(arr)
    sum = 20

    print(findMaxSubarraySum(arr, n, sum))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find subarray
// having maximum sum less
//than or equal to sum
using System;

public class GFG
{

    // To find subarray with maximum
    // sum less than or equal
    // to sum
    static int findMaxSubarraySum(int []arr,
                             int n, int sum)
    {    // To store current sum and
    // max sum of subarrays
    int curr_sum = arr[0], max_sum = 0, start = 0;

    // To find max_sum less than sum
    for (int i = 1; i < n; i++) {

        // Update max_sum if it becomes
        // greater than curr_sum
        if (curr_sum <= sum)
           max_sum = Math.Max(max_sum, curr_sum);

        // If curr_sum becomes greater than
        // sum subtract starting elements of array
        while (curr_sum + arr[i] > sum && start < i) {
            curr_sum -= arr[start];
            start++;
        }

        // Add elements to curr_sum
        curr_sum += arr[i];
    }

    // Adding an extra check for last subarray
    if (curr_sum <= sum)
        max_sum = Math.Max(max_sum, curr_sum);

    return max_sum;
    }

    // Driver Code
    public static void Main()
    {
        int []arr = {1, 2, 3, 4, 5};
        int n = arr.Length;
        int sum = 11;

        Console.Write(findMaxSubarraySum(arr, n, sum));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find subarray having
// maximum sum less than or equal to sum

// To find subarray with maximum sum
// less than or equal to sum
function findMaxSubarraySum(&$arr, $n, $sum)
{
    // To store current sum and
    // max sum of subarrays
    $curr_sum = $arr[0];
    $max_sum = 0;
    $start = 0;

    // To find max_sum less than sum
    for ($i = 1; $i < $n; $i++)
    {

        // Update max_sum if it becomes
        // greater than curr_sum
        if ($curr_sum <= $sum)
        $max_sum = max($max_sum, $curr_sum);

        // If curr_sum becomes greater than
        // sum subtract starting elements of array
        while ($curr_sum + $arr[$i] > $sum &&
                             $start < $i)
        {
            $curr_sum -= $arr[$start];
            $start++;
        }

        // Add elements to curr_sum
        $curr_sum += $arr[$i];
    }

    // Adding an extra check for last subarray
    if ($curr_sum <= $sum)
        $max_sum = max($max_sum, $curr_sum);

    return $max_sum;
}

// Driver Code
$arr = array(6, 8, 9);
$n = sizeof($arr);
$sum = 20;

echo findMaxSubarraySum($arr, $n, $sum);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript program to find subarray having
// maximum sum less than or equal to sum

// To find subarray with maximum sum
// less than or equal to sum
function findMaxSubarraySum(arr, n, sum)
{

    // To store current sum and
    // max sum of subarrays
    let curr_sum = arr[0], max_sum = 0,
        start = 0;

    // To find max_sum less than sum
    for(let i = 1; i < n; i++)
    {

        // Update max_sum if it becomes
        // greater than curr_sum
        if (curr_sum <= sum)
            max_sum = Math.max(max_sum, curr_sum);

        // If curr_sum becomes greater than
        // sum subtract starting elements of array
        while (curr_sum + arr[i] > sum && start < i)
        {
            curr_sum -= arr[start];
            start++;
        }

        // Add elements to curr_sum
        curr_sum += arr[i];
    }

    // Adding an extra check for last subarray
    if (curr_sum <= sum)
        max_sum = Math.max(max_sum, curr_sum);

    return max_sum;
}

// Driver code
let arr = [ 6, 8, 9 ];
let n = arr.length;
let sum = 20;

document.write(findMaxSubarraySum(arr, n, sum));

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
17
```

**时间复杂度:** O(N*log(N))

**辅助空间:** O(1)

如果给定了一个包含所有类型(正、负或零)元素的数组，我们可以使用前缀和集合，最坏情况下的时间复杂度是 O(n.log(n))。为了更清楚地了解这种方法，可以使用集合文章来参考小于或等于 k 的最大子阵和。

本文由**核素**投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。