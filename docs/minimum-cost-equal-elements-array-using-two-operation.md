# 使用两次运算使数组的所有元素相等的最小成本

> 原文:[https://www . geeksforgeeks . org/最小成本-相等元素-数组-使用两次运算/](https://www.geeksforgeeks.org/minimum-cost-equal-elements-array-using-two-operation/)

给定 n 个正整数的数组 arr[]。允许两种操作:

*   **操作 1 :** 选取任意两个指标，一个指标的值增加 1，另一个指标的值减少 1。这将花费**一辆**。

*   **操作 2 :** 选取任意一个指标，将其值增加 1。这将花费 **b** 。

任务是找到使数组中所有元素相等的最小代价。
示例:

```
Input : n = 4, a = 2, b = 3
        arr[] = { 3, 4, 2, 2 }
Output : 5
Perform operation 2 on 3rd index 
(0 based indexing). It will cost 2.
Perform operation 1 on index 1 (decrease) 
and index 2 (increase). It will cost 3.

Input : n = 3, a = 2, b = 1
        arr[] = { 5, 5, 5 }
Output : 0
```

**逼近:**观察，最终数组不会有大于给定数组最大元素的元素，因为没有意义增加所有元素。此外，它们将大于原始数组中的最小元素。现在，迭代需要相等的最终数组元素的所有可能值，并检查必须执行多少第二种类型的操作。对于 I 元素(这是最终数组元素的可能值之一)，该数字是(n * I–s)，其中 s 是数组中所有数字的总和。最终数组中 I 元素的第一种运算的次数可以通过以下方式得到:

```
for (int j = 0; j < n; j++)
  op1 += max(0, a[j] - i)
```

每次迭代结束时，只需检查新值 ans =(n * I–s)* b+op1 * a 是否小于 ans 的上一个值。如果少了，更新最终 ans。
以下是上述方法的实施。

## C++

```
// CPP Program to find the minimum cost to equal
// all elements of array using two operation
#include <bits/stdc++.h>
using namespace std;

// Return the minimum cost required
int minCost(int n, int arr[], int a, int b)
{
    int sum = 0, ans = INT_MAX;
    int maxval = 0;

    // finding the maximum element and sum of the array.
    for (int i = 0; i < n; i++) {
        sum += arr[i];
        maxval = max(maxval, arr[i]);
    }

    // for each of the possible value
    for (int i = 1; i <= maxval; i++) {
        int op1 = 0;

        // finding the number of operation 1 required
        for (int j = 0; j < n; j++)
            op1 += max(0, arr[j] - i);

        // finding the minimum cost.
        if (sum <= n * i)
            ans = min(ans, (n * i - sum) * b + op1 * a);
    }

    return ans;
}

// Driven Code
int main()
{
    int n = 4, a = 2, b = 3;
    int arr[] = { 3, 4, 2, 2 };

    cout << minCost(n, arr, a, b) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the minimum cost
// to equal all elements of array using
// two operation
import java.lang.*;

class GFG {

    // Return the minimum cost required
    static int minCost(int n, int arr[],
                                 int a, int b)
    {
        int sum = 0, ans = Integer.MAX_VALUE;
        int maxval = 0;

        // finding the maximum element and
        // sum of the array.
        for (int i = 0; i < n; i++) {
            sum += arr[i];
            maxval = Math.max(maxval, arr[i]);
        }

        // for each of the possible value
        for (int i = 1; i <= maxval; i++) {
            int op1 = 0;

            // finding the number of operation
            // 1 required
            for (int j = 0; j < n; j++)
                op1 += Math.max(0, arr[j] - i);

            // finding the minimum cost.
            if (sum <= n * i)
                ans = Math.min(ans, (n * i - sum)
                                  * b + op1 * a);
        }

        return ans;
    }

    // Driven Code
    public static void main(String [] args)
    {
        int n = 4, a = 2, b = 3;
        int arr[] = { 3, 4, 2, 2 };

        System.out.println(minCost(n, arr, a, b));
    }
}

// This code is contributed by Smitha.
```

## 蟒蛇 3

```
# Python 3 Program to find the minimum
# cost to equal all elements of array
# using two operation
import sys

# Return the minimum cost required
def minCost(n, arr, a, b):

    sum = 0
    ans = sys.maxsize
    maxval = 0

    # finding the maximum element and
    # sum of the array.
    for i in range(0, n) :
        sum += arr[i]
        maxval = max(maxval, arr[i])

    # for each of the possible value
    for i in range(0, n) :
        op1 = 0

        # finding the number of operation
        # 1 required
        for j in range(0, n) :
            op1 += max(0, arr[j] - i)

        # finding the minimum cost.
        if (sum <= n * i):
            ans = min(ans, (n * i - sum)
                          * b + op1 * a)

    return ans

# Driven Code
n = 4
a = 2
b = 3
arr = [3, 4, 2, 2]
print(minCost(n, arr, a, b))

# This code is contributed by Smitha
```

## C#

```
// C# Program to find the minimum
// cost to equal all elements of
// array using two operation
using System;

class GFG {

    // Return the minimum cost required
    static int minCost(int n, int [] arr,
                            int a, int b)
    {
        int sum = 0, ans = int.MaxValue;
        int maxval = 0;

        // finding the maximum element and
        // sum of the array.
        for (int i = 0; i < n; i++) {
            sum += arr[i];
            maxval = Math.Max(maxval, arr[i]);
        }

        // for each of the possible value
        for (int i = 1; i <= maxval; i++) {
            int op1 = 0;

            // finding the number of operation
            // 1 required
            for (int j = 0; j < n; j++)
                op1 += Math.Max(0, arr[j] - i);

            // finding the minimum cost.
            if (sum <= n * i)
                ans = Math.Min(ans, (n * i - sum)
                                  * b + op1 * a);
        }

        return ans;
    }

    // Driven Code
    public static void Main()
    {
        int n = 4, a = 2, b = 3;
        int []arr= { 3, 4, 2, 2 };

        Console.Write(minCost(n, arr, a, b));
    }
}

// This code is contributed by Smitha
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP Program to find the minimum cost
// to equal all elements of array using
// two operation

// Return the minimum cost required
function minCost($n, $arr, $a, $b)
{
    $sum = 0; $ans = PHP_INT_MAX;
    $maxval = 0;

    // finding the maximum element and
    // sum of the array.
    for ($i = 0; $i < $n; $i++) {
        $sum += $arr[$i];
        $maxval = max($maxval, $arr[$i]);
    }

    // for each of the possible value
    for ($i = 1; $i <= $maxval; $i++) {
        $op1 = 0;

        // finding the number of operation
        // 1 required
        for ($j = 0; $j < $n; $j++)
            $op1 += max(0, $arr[$j] - $i);

        // finding the minimum cost.
        if ($sum <= $n * $i)
            $ans = min($ans, ($n * $i - $sum)
                           * $b + $op1 * $a);
    }

    return $ans;
}

// Driven Code
    $n = 4; $a = 2; $b = 3;
    $arr= array(3, 4, 2, 2 );

    echo minCost($n, $arr, $a, $b) ,"\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// javascript Program to find the minimum cost
// to equal all elements of array using
// two operation

    // Return the minimum cost required
    function minCost(n , arr , a , b)
    {
        var sum = 0, ans = Number.MAX_VALUE;
        var maxval = 0;

        // finding the maximum element and
        // sum of the array.
        for (i = 0; i < n; i++) {
            sum += arr[i];
            maxval = Math.max(maxval, arr[i]);
        }

        // for each of the possible value
        for (i = 1; i <= maxval; i++) {
            var op1 = 0;

            // finding the number of operation
            // 1 required
            for (j = 0; j < n; j++)
                op1 += Math.max(0, arr[j] - i);

            // finding the minimum cost.
            if (sum <= n * i)
                ans = Math.min(ans, (n * i - sum) * b + op1 * a);
        }

        return ans;
    }

    // Driven Code

        var n = 4, a = 2, b = 3;
        var arr = [ 3, 4, 2, 2 ];

        document.write(minCost(n, arr, a, b));
// This code contributed by umadevi9616
</script>
```

**Output:** 

```
5
```