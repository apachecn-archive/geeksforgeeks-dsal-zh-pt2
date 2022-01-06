# 满足给定条件的子阵列最大尺寸

> 原文:[https://www . geeksforgeeks . org/满足给定条件的子数组的最大大小/](https://www.geeksforgeeks.org/maximum-size-of-sub-array-that-satisfies-the-given-condition/)

给定整数数组 **arr[]** 。任务是返回最大大小子数组的长度，以便满足以下任一条件:

1.  当 **k 为奇数时 **arr[k] > arr[k + 1]** ，当 **k 为偶数时 **arr[k] < arr[k + 1]** 。****
2.  当 **k 为偶数**时 **arr[k] > arr[k + 1]** ，当 **k 为奇数**时 **arr[k] < arr[k + 1]** 。

**示例:**

> **输入:** arr[] = {9，4，2，10，7，8，8，1，9}
> **输出:** 5
> 所需子阵列为{4，2，10，7，8}，满足第一个条件。
> **输入:** arr[] = {4，8，12，16}
> **输出:** 2

**方法:**因为只需要相邻元素之间的比较。因此，如果用 **-1，0，1** 来表示比较，那么我们需要最长的交替序列 **1，-1，1，…，-1** (从 1 或-1 开始)，其中:

*   0 -> arr[i] = arr[i + 1]
*   1 -> arr[i] > arr[i + 1]
*   -1 -> arr[i] < arr[i + 1]

例如，如果我们有一个数组 **arr[] = {9，4，2，10，7，8，8，1，9}** ，那么比较将是 **{1，1，-1，1，-1，1，0，0，-1，1}** ，所有可能的子数组是 **{1}** ， **{1，-1，1，-1}** ， **{0}** ， **{-1，1}** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function that compares a and b
int cmp(int a, int b)
{
    return (a > b) - (a < b);
}

// Function to return length of longest subarray
// that satisfies one of the given conditions
int maxSubarraySize(int arr[], int n)
{
    int ans = 1;
    int anchor = 0;

    for (int i = 1; i < n; i++)
    {
        int c = cmp(arr[i - 1], arr[i]);
        if (c == 0)
            anchor = i;
        else if (i == n - 1 ||
                 c * cmp(arr[i], arr[i + 1]) != -1)
        {
            ans = max(ans, i - anchor + 1);
            anchor = i;
        }
    }

    return ans;
}

// Driver Code
int main()
{
    int arr[] = {9, 4, 2, 10, 7, 8, 8, 1, 9};
    int n = sizeof(arr) / sizeof(arr[0]);

    // Print the required answer
    cout << maxSubarraySize(arr, n);
}

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

// Function that compares a and b
static int cmp(int a, int b)
{
    if(a > b)
        return 1;
    else if(a == b)
        return 0;
    else
        return -1;
}

// Function to return length of longest subarray
// that satisfies one of the given conditions
static int maxSubarraySize(int []arr, int n)
{
    int ans = 1;
    int anchor = 0;

    for (int i = 1; i < n; i++)
    {
        int c = cmp(arr[i - 1], arr[i]);
        if (c == 0)
            anchor = i;
        else if (i == n - 1 ||
                c * cmp(arr[i], arr[i + 1]) != -1)
        {
            ans = Math.max(ans, i - anchor + 1);
            anchor = i;
        }
    }

    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int []arr = {9, 4, 2, 10, 7, 8, 8, 1, 9};
    int n = arr.length;

    // Print the required answer
    System.out.println(maxSubarraySize(arr, n));
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that compares a and b
def cmp(a, b):
    return (a > b) - (a < b)

# Function to return length of longest subarray
# that satisfies one of the given conditions
def maxSubarraySize(arr):
    N = len(arr)
    ans = 1
    anchor = 0

    for i in range(1, N):
        c = cmp(arr[i - 1], arr[i])
        if c == 0:
            anchor = i
        elif i == N - 1 or c * cmp(arr[i], arr[i + 1]) != -1:
            ans = max(ans, i - anchor + 1)
            anchor = i
    return ans

# Driver program
arr = [9, 4, 2, 10, 7, 8, 8, 1, 9]

# Print the required answer
print(maxSubarraySize(arr))
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that compares a and b
static int cmp(int a, int b)
{
    if(a > b)
        return 1;
    else if(a == b)
        return 0;
    else
        return -1;
}

// Function to return length of longest subarray
// that satisfies one of the given conditions
static int maxSubarraySize(int []arr, int n)
{
    int ans = 1;
    int anchor = 0;

    for (int i = 1; i < n; i++)
    {
        int c = cmp(arr[i - 1], arr[i]);
        if (c == 0)
            anchor = i;
        else if (i == n - 1 ||
                c * cmp(arr[i], arr[i + 1]) != -1)
        {
            ans = Math.Max(ans, i - anchor + 1);
            anchor = i;
        }
    }

    return ans;
}

// Driver Code
static void Main()
{
    int []arr = {9, 4, 2, 10, 7, 8, 8, 1, 9};
    int n = arr.Length;

    // Print the required answer
    Console.WriteLine(maxSubarraySize(arr, n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that compares a and b
function cmp($a, $b)
{
    return ($a > $b) - ($a < $b);
}

// Function to return length of longest subarray
// that satisfies one of the given conditions
function maxSubarraySize($arr)
{
    $N = sizeof($arr);
    $ans = 1;
    $anchor = 0;

    for ($i = 1; $i < $N; $i++)
    {
        $c = cmp($arr[$i - 1], $arr[$i]);
        if ($c == 0)
            $anchor = $i;

        else if ($i == $N - 1 or
                 $c * cmp($arr[$i],
                          $arr[$i + 1]) != -1)
        {
            $ans = max($ans, $i - $anchor + 1);
            $anchor = $i;
        }
    }    
    return $ans;
}

// Driver Code
$arr = array(9, 4, 2, 10, 7, 8, 8, 1, 9);

// Print the required answer
echo maxSubarraySize($arr);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// javascript implementation of the approach
    // Function that compares a and b
    function cmp(a , b) {
        if (a > b)
            return 1;
        else if (a == b)
            return 0;
        else
            return -1;
    }

    // Function to return length of longest subarray
    // that satisfies one of the given conditions
    function maxSubarraySize(arr , n) {
        var ans = 1;
        var anchor = 0;

        for (i = 1; i < n; i++) {
            var c = cmp(arr[i - 1], arr[i]);
            if (c == 0)
                anchor = i;
            else if (i == n - 1 || c * cmp(arr[i], arr[i + 1]) != -1) {
                ans = Math.max(ans, i - anchor + 1);
                anchor = i;
            }
        }

        return ans;
    }

    // Driver Code

        var arr = [ 9, 4, 2, 10, 7, 8, 8, 1, 9 ];
        var n = arr.length;

        // Print the required answer
        document.write(maxSubarraySize(arr, n));

// This code contributed by aashish1995
</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(N)，其中 N 是数组的长度
T3】空间复杂度: O(1)