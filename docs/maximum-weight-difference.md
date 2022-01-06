# 最大重量差

> 原文:[https://www.geeksforgeeks.org/maximum-weight-difference/](https://www.geeksforgeeks.org/maximum-weight-difference/)

给你一个数组 W[1]，W[2]，…，W[N]。在其中选择 K 个数字，使得所选数字之和与剩余数字之和之间的绝对差值尽可能大。
**例:**

```
Input : arr[] = [8, 4, 5, 2, 10]
            k = 2
Output: 17

Input : arr[] = [1, 1, 1, 1, 1, 1, 1, 1]
          k = 3
Output: 2
```

有两种可能得到想要的答案。这两个是:选择 **k** 个最大的数字或者选择 **k** 个最小的数字。根据给定的值选择最适合的选项。这是因为在某些情况下，最小 k 个数的和可以大于数组的其余部分，在某些情况下，最大 k 个数的和可以大于这些数的和的其余部分。
**进场:**

*   给定数组排序。
*   得到数组中所有数字的和，存储在 **sum** 中
*   获取数组的第一个 **k** 个数的和，并存储在 **sum1** 中
*   获取数组最后 **k** 个数字的和，并存储在 **sum2** 中
*   输出结果为: **max(abs(S1-(S-S1))、abs(S2-(S-S2)))**

## C++

```
// C++ Program to find maximum weight
// difference
#include <iostream>
#include <algorithm>
using namespace std;

// return the max value of two numbers

int solve(int array[], int n, int k)
{
    // sort the given array
    sort(array, array + n);

    // Initializing the value to 0
    int sum = 0, sum1 = 0, sum2 = 0;

    // Getting the sum of the array
    for (int i = 0; i < n; i++) {
        sum += array[i];
    }

    // Getting the sum of smallest k elements
    for (int i = 0; i < k; i++) {
        sum1 += array[i];
    }
    sort(array, array+n, greater<int>());
    // Getting the sum of k largest elements
    for (int i = 0; i < k; i++) {
        sum2 += array[i];
    }

    // Returning the maximum possible difference.
    return max(abs(sum1 - (sum - sum1)), abs(sum2 -
                                  (sum - sum2)));
}

// Driver function
int main()
{
    int k = 2;
    int array[] = { 8, 4, 5, 2, 10 };

    // calculate the numbers of elements in the array
    int n = sizeof(array) / sizeof(array[0]);

    // call the solve function
    cout << solve(array, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code for Maximum Weight Difference
import java.util.*;

class GFG {

    public static int solve(int array[], int n,
                                        int k)
    {
        // sort the given array
        Arrays.sort(array);

        // Initializing the value to 0
        int sum = 0, sum1 = 0, sum2 = 0;

        // Getting the sum of the array
        for (int i = 0; i < n; i++) {
            sum += array[i];
        }

        // Getting the sum of first k elements
        for (int i = 0; i < k; i++) {
            sum1 += array[i];
        }

        // Getting the sum of (n-k) elements
        for (int i = k; i < n; i++) {
            sum2 += array[i];
        }

        // Returning the maximum possible difference.
        return Math.max(Math.abs(sum1 - (sum - sum1)),
                       Math.abs(sum2 - (sum - sum2)));
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int k = 2;
        int array[] = { 8, 4, 5, 2, 10 };

        // calculate the numbers of elements
        // in the array
        int n = array.length;

        // call the solve function
        System.out.print(solve(array, n, k));

    }
}
// This code is contributed by Arnav Kr. Mandal.
```

## 计算机编程语言

```
def solve(array, k):

  # Sorting array
  array.sort()

  # Getting the sum of all the elements
  s = sum(array)

  # Getting the sum of smallest k elements
  s1 = sum(array[:k])

  # Getting the sum greatest k elements
  array.sort(reverse=True)
  s2 = sum(array[:k])

  # Returning the maximum possible difference
  return max(abs(s1-(s-s1)), abs(s2-(s-s2)))

# Driver function
k = 2
array =[8, 4, 5, 2, 10]
print(solve(array, k))
```

## C#

```
// C# Code for Maximum Weight Difference
using System;

class GFG {

    public static int solve(int []array, int n,
                                        int k)
    {

        // sort the given array
        Array.Sort(array);

        // Initializing the value to 0
        int sum = 0, sum1 = 0, sum2 = 0;

        // Getting the sum of the array
        for (int i = 0; i < n; i++) {
            sum += array[i];
        }

        // Getting the sum of first k elements
        for (int i = 0; i < k; i++) {
            sum1 += array[i];
        }

        // Getting the sum of (n-k) elements
        for (int i = k; i < n; i++) {
            sum2 += array[i];
        }

        // Returning the maximum possible difference.
        return Math.Max(Math.Abs(sum1 - (sum - sum1)),
                        Math.Abs(sum2 - (sum - sum2)));
    }

    /* Driver program to test above function */
    public static void Main()
    {
        int k = 2;
        int []array = { 8, 4, 5, 2, 10 };

        // calculate the numbers of elements
        // in the array
        int n = array.Length;

        // call the solve function
        Console.WriteLine(solve(array, n, k));

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find maximum weight
// difference

// return the max value of two numbers
function maxi($a, $b)
{
    if ($a > $b)
    {
        return $a;
    }
    else
    {
        return $b;
    }
}

function solve(&$arr, $n, $k)
{
    // sort the given array
    sort($arr);

    // Initializing the value to 0
    $sum = 0;
    $sum1 = 0;
    $sum2 = 0;

    // Getting the sum of the array
    for ($i = 0; $i < $n; $i++)
    {
        $sum += $arr[$i];
    }

    // Getting the sum of first k elements
    for ($i = 0; $i < $k; $i++)
    {
        $sum1 += $arr[$i];
    }

    // Getting the sum of (n-k) elements
    for ($i = $k; $i < $n; $i++)
    {
        $sum2 += $arr[$i];
    }

    // Returning the maximum possible difference.
    return maxi(abs($sum1 - ($sum - $sum1)),
                abs($sum2 - ($sum - $sum2)));
}

// DriverCode
$k = 2;
$arr = array(8, 4, 5, 2, 10 );

// calculate the numbers of
// elements in the array
$n = sizeof($arr);

// call the solve function
echo (solve($arr, $n, $k));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

    // JavaScript Code for Maximum Weight Difference

    function solve(array, n, k)
    {

        // sort the given array
        array.sort(function(a, b){return a - b});

        // Initializing the value to 0
        let sum = 0, sum1 = 0, sum2 = 0;

        // Getting the sum of the array
        for (let i = 0; i < n; i++) {
            sum += array[i];
        }

        // Getting the sum of first k elements
        for (let i = 0; i < k; i++) {
            sum1 += array[i];
        }

        // Getting the sum of (n-k) elements
        for (let i = k; i < n; i++) {
            sum2 += array[i];
        }

        // Returning the maximum possible difference.
        return Math.max(Math.abs(sum1 - (sum - sum1)),
                        Math.abs(sum2 - (sum - sum2)));
    }

    let k = 2;
    let array = [ 8, 4, 5, 2, 10 ];

    // calculate the numbers of elements
    // in the array
    let n = array.length;

    // call the solve function
    document.write(solve(array, n, k));

</script>
```

**Output**

```
17
```

本文由 [**里沙布·班萨尔**](https://www.linkedin.com/in/rishabh-bansal-9b4b71108/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。