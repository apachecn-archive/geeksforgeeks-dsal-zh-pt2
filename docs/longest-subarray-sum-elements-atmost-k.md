# 元素总和为“k”的最长子阵列

> 原文:[https://www . geesforgeks . org/long-subarray-sum-elements-atmat-k/](https://www.geeksforgeeks.org/longest-subarray-sum-elements-atmost-k/)

给定一个整数数组，我们的目标是找到最大子数组的长度，它的元素之和最多为‘k’，其中 k>0。

**示例:**

```
Input : arr[] = {1, 2, 1, 0, 1, 1, 0}, k = 4
Output : 5
Explanation:
 {1, 2, 1} => sum = 4, length = 3
 {1, 2, 1, 0}, {2, 1, 0, 1} => sum = 4, length = 4
 {1, 0, 1, 1, 0} =>5 sum = 3, length = 5
```

**方法 1(蛮力)**
找出所有和小于等于 k 的子阵，返回长度最大的一个。
时间复杂度:O(n^2)
**方法 2(高效):**
一种**高效的方法**是使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)。

1.  遍历数组并检查添加当前元素时其总和是否小于或等于 k。
2.  如果它小于 k，那么把它加到和上并增加计数。
3.  记录最大计数。

## C++

```
// A C++ program to find longest subarray with
// sum of elements at-least k.
#include <bits/stdc++.h>
using namespace std;

// function to find the length of largest subarray
// having sum atmost k.
int atMostSum(int arr[], int n, int k)
{
    int sum = 0;
    int cnt = 0, maxcnt = 0;

    for (int i = 0; i < n; i++) {

        // If adding current element doesn't
        // cross limit add it to current window
        if ((sum + arr[i]) <= k) {
            sum += arr[i];
            cnt++;
        }

        // Else, remove first element of current
        // window and add the current element
        else if(sum!=0)
        {
            sum = sum - arr[i - cnt] + arr[i];
        }

        // keep track of max length.
        maxcnt = max(cnt, maxcnt);
    }
    return maxcnt;
}

// Driver function
int main()
{
    int arr[] = {1, 2, 1, 0, 1, 1, 0};
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 4;

    cout << atMostSum(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find longest subarray with
// sum of elements at-least k.
import java.util.*;

class GFG {

    // function to find the length of largest
    // subarray having sum atmost k.
    public static int atMostSum(int arr[], int n,
                                        int k)
    {
        int sum = 0;
        int cnt = 0, maxcnt = 0;

        for (int i = 0; i < n; i++) {

            // If adding current element doesn't
            // cross limit add it to current window
            if ((sum + arr[i]) <= k) {
                sum += arr[i];
                cnt++;
            }

            // Else, remove first element of current
            // window.
            else if(sum!=0)
           {
            sum = sum - arr[i - cnt] + arr[i];
           }

            // keep track of max length.
            maxcnt = Math.max(cnt, maxcnt);
        }
        return maxcnt;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 1, 0, 1, 1, 0 };
        int n = arr.length;
        int k = 4;

        System.out.print(atMostSum(arr, n, k));

    }
}
// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 program to find longest subarray
# with sum of elements at-least k.

# function to find the length of largest
# subarray having sum atmost k.
def atMostSum(arr, n, k):
    _sum = 0
    cnt = 0
    maxcnt = 0

    for i in range(n):

        # If adding current element doesn't
        # Cross limit add it to current window
        if ((_sum + arr[i]) <= k):
            _sum += arr[i]
            cnt += 1

        # Else, remove first element of current
        # window and add the current element
        elif(sum != 0):
            _sum = _sum - arr[i - cnt] + arr[i]

        # keep track of max length.
        maxcnt = max(cnt, maxcnt)

    return maxcnt

# Driver function
arr = [1, 2, 1, 0, 1, 1, 0]
n = len(arr)
k = 4
print(atMostSum(arr, n, k))

# This code is contributed by "Abhishek Sharma 44"
```

## C#

```
// C# program to find longest subarray
// with sum of elements at-least k.
using System;

class GFG {

    // function to find the length of largest
    // subarray having sum atmost k.
    public static int atMostSum(int []arr, int n,
                                           int k)
    {
        int sum = 0;
        int cnt = 0, maxcnt = 0;

        for (int i = 0; i < n; i++) {

            // If adding current element doesn't
            // cross limit add it to current window
            if ((sum + arr[i]) <= k) {
                sum += arr[i];
                cnt++;
            }

            // Else, remove first element
            // of current window.
            else if(sum!=0)
            {
                sum = sum - arr[i - cnt] + arr[i];
            }

            // keep track of max length.
            maxcnt = Math.Max(cnt, maxcnt);
        }
        return maxcnt;
    }

    // Driver Code
    public static void Main()
    {
        int []arr = {1, 2, 1, 0, 1, 1, 0};
        int n = arr.Length;
        int k = 4;

        Console.Write(atMostSum(arr, n, k));

    }
}

// This code is contributed by Nitin Mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A PHP program to find longest
// subarray with sum of elements
// at-least k.

// function to find the length
// of largest subarray having
// sum atmost k.
function atMostSum(&$arr, $n, $k)
{
    $sum = 0;
    $cnt = 0;
    $maxcnt = 0;

    for($i = 0; $i < $n; $i++)
    {
        // If adding current element
        // doesn't cross limit add
        // it to current window
        if (($sum + $arr[$i]) <= $k)
        {
            $sum += $arr[$i] ;
            $cnt += 1 ;
        }

        // Else, remove first element
        // of current window and add
        // the current element
        else if($sum != 0)
            $sum = $sum - $arr[$i - $cnt] +
                               $arr[$i];

        // keep track of max length.
        $maxcnt = max($cnt, $maxcnt);
    }
    return $maxcnt;
}

// Driver Code
$arr = array(1, 2, 1, 0, 1, 1, 0);
$n = sizeof($arr);
$k = 4;

print(atMostSum($arr, $n, $k));

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
// A Javascript program to find longest subarray with
// sum of elements at-least k.

// function to find the length of largest subarray
// having sum atmost k.
function atMostSum(arr, n, k)
{
    let sum = 0;
    let cnt = 0, maxcnt = 0;

    for (let i = 0; i < n; i++) {

        // If adding current element doesn't
        // cross limit add it to current window
        if ((sum + arr[i]) <= k) {
            sum += arr[i];
            cnt++;
        }

        // Else, remove first element of current
        // window and add the current element
        else if(sum!=0)
        {
            sum = sum - arr[i - cnt] + arr[i];
        }

        // keep track of max length.
        maxcnt = Math.max(cnt, maxcnt);
    }
    return maxcnt;
}

// Driver function
    let arr = [1, 2, 1, 0, 1, 1, 0];
    let n = arr.length;
    let k = 4;

    document.write(atMostSum(arr, n, k));

</script>
```

**输出:**

```
5
```

**时间复杂度** : O(n)
本文由 **Kshitiz gupta** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。