# 最大偶数和子序列

> 原文:[https://www.geeksforgeeks.org/maximum-even-sum-subsequence/](https://www.geeksforgeeks.org/maximum-even-sum-subsequence/)

给定一个由 n 个正整数和负整数组成的数组，找到具有最大偶数和的子序列，并显示该偶数和。
**例:**

```
Input: arr[] = {-2, 2, -3, 1, 3}
Output: 6
Explanation: The longest subsequence
with even sum is 2, 1 and 3.

Input: arr[] = {-2, 2, -3, 4, 5}
Output: 8
Explanation: The longest subsequence
with even sum is 2,-3,4 and 5
```

解决问题的方法可以简化为几点:
1)将所有正数相加
2)如果总和是偶数，那么这将是最大可能总和
3)如果总和不是偶数，那么要么从中减去一个正奇数，要么加上一个负奇数。
—求负奇数的最大最大奇数，因此和+a[I](因为 a[I]本身是负的)
—求正奇数的最小最大奇数，因此是 sun-a[I]。
—两个结果的最大值即为答案。
以下是上述方法的实施

## C++

```
// CPP program to find longest even sum
// subsequence.
#include <bits/stdc++.h>
using namespace std;

// Returns sum of maximum even sum subsequence
int maxEvenSum(int arr[], int n)
{
    // Find sum of positive numbers
    int pos_sum = 0;
    for (int i = 0; i < n; ++i)
        if (arr[i] > 0)
            pos_sum += arr[i];

    // If sum is even, it is our
    // answer
    if (pos_sum % 2 == 0)
        return pos_sum;

    // Traverse the array to find the
    // maximum sum by adding a positive
    // odd or subtracting a negative odd
    int ans = INT_MIN;
    for (int i = 0; i < n; ++i) {
        if (arr[i] % 2 != 0) {
            if (arr[i] > 0)
                ans = max(ans, pos_sum - arr[i]);
            else
                ans = max(ans, pos_sum + arr[i]);
        }
    }

    return ans;
}

// driver program
int main()
{
    int a[] = { -2, 2, -3, 1 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << maxEvenSum(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find longest
// even sum subsequence.
class MaxevenSum
{

    // Returns sum of maximum even sum
    // subsequence
    static int maxEvenSum(int arr[], int n)
    {
        // Find sum of positive numbers
        int pos_sum = 0;
        for (int i = 0; i < n; ++i)
            if (arr[i] > 0)
                pos_sum += arr[i];

        // If sum is even, it is our
        // answer
        if (pos_sum % 2 == 0)
            return pos_sum;

        // Traverse the array to find the
        // maximum sum by adding a
        // positive odd or subtracting a
        // negative odd
        int ans = Integer.MIN_VALUE;
        for (int i = 0; i < n; ++i) {
            if (arr[i] % 2 != 0) {
                if (arr[i] > 0)
                    ans = ans>(pos_sum - arr[i]) ?
                          ans:(pos_sum - arr[i]);
                else
                    ans = ans>(pos_sum + arr[i]) ?
                          ans:(pos_sum + arr[i]);
            }
        }  

        return ans;
    }

    // driver program  
    public static void main(String s[])
    {
        int a[] = {-2, 2, -3, 1};

        System.out.println(maxEvenSum(a, a.length));   

    }
}
// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python 3 program to find longest
# even sum subsequence.
INT_MIN = -100000000

# Returns sum of maximum even
# sum subsequence
def maxEvenSum(arr, n):

    # Find sum of positive numbers
    pos_sum = 0
    for i in range(n):
        if (arr[i] > 0):
            pos_sum += arr[i]

    # If sum is even, it is our answer
    if (pos_sum % 2 == 0):
        return pos_sum

    # Traverse the array to find the
    # maximum sum by adding a positive
    # odd or subtracting a negative odd
    ans = INT_MIN;
    for i in range(n):
        if (arr[i] % 2 != 0):
            if (arr[i] > 0):
                ans = max(ans, pos_sum - arr[i])
            else:
                ans = max(ans, pos_sum + arr[i])
    return ans

# Driver Code
a = [-2, 2, -3, 1]
n = len(a)
print(maxEvenSum(a, n))

# This code is contributed by sahilshelangia
```

## C#

```
// C# program to find longest
// even sum subsequence.
using System;

class GFG {

    // Returns sum of maximum even sum
    // subsequence
    static int maxEvenSum(int []arr, int n)
    {

        // Find sum of positive numbers
        int pos_sum = 0;
        for (int i = 0; i < n; ++i)
            if (arr[i] > 0)
                pos_sum += arr[i];

        // If sum is even, it is our
        // answer
        if (pos_sum % 2 == 0)
            return pos_sum;

        // Traverse the array to find the
        // maximum sum by adding a
        // positive odd or subtracting a
        // negative odd
        int ans = int.MinValue;

        for (int i = 0; i < n; ++i)
        {
            if (arr[i] % 2 != 0)
            {
                if (arr[i] > 0)
                    ans = (ans > (pos_sum - arr[i]))
                         ? ans : (pos_sum - arr[i]);
                else
                    ans = (ans > (pos_sum + arr[i]))
                         ? ans : (pos_sum + arr[i]);
            }
        }

        return ans;
    }

    // driver program
    public static void Main()
    {
        int []a = {-2, 2, -3, 1};

        Console.WriteLine(maxEvenSum(a, a.Length));

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find longest
// even sum subsequence.

// Returns sum of maximum even
// sum subsequence
function maxEvenSum( $arr, $n)
{
    // Find sum of positive numbers
    $pos_sum = 0;
    for ( $i = 0; $i < $n; ++$i)
        if ($arr[$i] > 0)
            $pos_sum += $arr[$i];

    // If sum is even, it is our
    // answer
    if ($pos_sum % 2 == 0)
        return $pos_sum;

    // Traverse the array to find
    // the maximum sum by adding
    // a positive odd or
    // subtracting a negative odd
    $ans = PHP_INT_MIN;
    for ( $i = 0; $i < $n; ++$i) {
        if ($arr[$i] % 2 != 0) {
            if ($arr[$i] > 0)
                $ans = max($ans,
                 $pos_sum - $arr[$i]);
            else
                $ans = max($ans,
                 $pos_sum + $arr[$i]);
        }
    }

    return $ans;
}

// driver program
    $a = array( -2, 2, -3, 1 );
    $n = count($a);
    echo maxEvenSum($a, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// javascript program to find longest
// even sum subsequence.

    // Returns sum of maximum even sum
    // subsequence
    function maxEvenSum(arr , n)
    {

        // Find sum of positive numbers
        var pos_sum = 0;
        for (i = 0; i < n; ++i)
            if (arr[i] > 0)
                pos_sum += arr[i];

        // If sum is even, it is our
        // answer
        if (pos_sum % 2 == 0)
            return pos_sum;

        // Traverse the array to find the
        // maximum sum by adding a
        // positive odd or subtracting a
        // negative odd
        var ans = Number.MIN_VALUE;
        for (i = 0; i < n; ++i) {
            if (arr[i] % 2 != 0) {
                if (arr[i] > 0)
                    ans = ans > (pos_sum - arr[i]) ? ans : (pos_sum - arr[i]);
                else
                    ans = ans > (pos_sum + arr[i]) ? ans : (pos_sum + arr[i]);
            }
        }

        return ans;
    }

    // driver program
    var a = [ -2, 2, -3, 1 ];
    document.write(maxEvenSum(a, a.length));

// This code is contributed by Rajput-Ji
</script>
```

输出:

```
2
```

时间复杂度:O(n)
辅助空间:O(1)
本文由 [**Raj**](https://www.facebook.com/raja.vikramaditya.7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。