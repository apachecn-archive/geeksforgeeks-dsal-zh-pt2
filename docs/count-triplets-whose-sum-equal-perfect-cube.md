# 计算所有和等于一个完美立方体的三胞胎

> 原文:[https://www . geesforgeks . org/count-triplets-what-sum-equal-perfect-cube/](https://www.geeksforgeeks.org/count-triplets-whose-sum-equal-perfect-cube/)

给定一个 n 个整数的数组，计算其和等于完美立方体的所有不同三元组，即对于任何 I，j，k(i < j < k) satisfying the condition that a[i] + a[j] + a[j] = X <sup>3</sup> ，其中 X 是任何整数。3 ≤ n ≤ 1000，1 ≤ a[i，j，k] ≤ 5000

**示例:**

```
Input:
N = 5
2 5 1 20 6
Output:
3
Explanation:
There are only 3 triplets whose total sum is a perfect cube.
Indices  Values SUM
0 1 2    2 5 1   8
0 1 3    2 5 20  27
2 3 4    1 20 6  27
Since 8 and 27 are perfect cube of 2 and 3.
```

**天真的方法**是通过使用 3 个嵌套循环迭代所有可能的数字，并检查它们的和是否是一个完美的立方体。这种方法会非常慢，因为时间复杂度会上升到 0(n<sup>3</sup>)。

一种有效的方法是使用动态规划和基础数学。根据给定的条件，三个正整数的和不大于 15000。因此，在 1 到 15000 的范围内，可能只有 24 个(15000 <sup>1/3</sup> )立方体。
现在，我们可以借助上述信息做得更好，而不是迭代所有的三元组。修正了前两个索引 I 和 j，这样我们就可以迭代所有 24 个可能的立方体，而不是迭代所有 k(j < k ≤ n)，对于每个立方体，(假设 P)检查**P –( a[I]+a[j])**在 a[j+1，j+2，… n]中出现了多少次。
但是如果我们计算一个数字的出现次数，比如说 K 在一个[j+1，j+2，… n]中的出现次数，那么这将再次被认为是缓慢的方法，并且肯定会给出 TLE。所以我们必须想一个不同的方法。
现在来看一个动态规划。因为所有数字都小于 5000，n 最多为 1000。因此，我们可以将 DP 数组计算为，
**DP[I][K]:= K 在 A[i，i+1，i+2 … n]** 中的出现次数

## C++

```
// C++ program to calculate all triplets whose
// sum is perfect cube.
#include <bits/stdc++.h>
using namespace std;

int dp[1001][15001];

// Function to calculate all occurrence of
// a number in a given range
void computeDpArray(int arr[], int n)
{
    for (int i = 0; i < n; ++i) {
        for (int j = 1; j <= 15000; ++j) {

            // if i == 0
            // assign 1 to present state
            if (i == 0)
                dp[i][j] = (j == arr[i]);

            // else add +1 to current state with
            // previous state
            else
                dp[i][j] = dp[i - 1][j] + (arr[i] == j);
        }
    }
}

// Function to calculate triplets whose sum
// is equal to the perfect cube
int countTripletSum(int arr[], int n)
{
    computeDpArray(arr, n);

    int ans = 0;  // Initialize answer
    for (int i = 0; i < n - 2; ++i) {
        for (int j = i + 1; j < n - 1; ++j) {
            for (int k = 1; k <= 24; ++k) {
                int cube = k * k * k;

                int rem = cube - (arr[i] + arr[j]);

                // count all occurrence of third triplet
                // in range from j+1 to n
                if (rem > 0)
                    ans += dp[n - 1][rem] - dp[j][rem];
            }
        }
    }
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 2, 5, 1, 20, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countTripletSum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code for Count all triplets whose
// sum is equal to a perfect cube
import java.util.*;

class GFG {

    public static int dp[][];

    // Function to calculate all occurrence of
    // a number in a given range
    public static void computeDpArray(int arr[], int n)
    {
        for (int i = 0; i < n; ++i) {
            for (int j = 1; j <= 15000; ++j) {

                // if i == 0
                // assign 1 to present state

                if (i == 0 && j == arr[i])
                    dp[i][j] = 1;
                else if(i==0)
                     dp[i][j] = 0;

                // else add +1 to current state
                // with previous state
                else if(arr[i] == j)
                    dp[i][j] = dp[i - 1][j] + 1;
                else
                    dp[i][j] = dp[i - 1][j];
            }
        }
    }

    // Function to calculate triplets whose sum
    // is equal to the perfect cube
    public static int countTripletSum(int arr[], int n)
    {
        computeDpArray(arr, n);

        int ans = 0;  // Initialize answer
        for (int i = 0; i < n - 2; ++i) {
            for (int j = i + 1; j < n - 1; ++j) {
                for (int k = 1; k <= 24; ++k) {
                    int cube = k * k * k;

                    int rem = cube - (arr[i] + arr[j]);

                    // count all occurrence of
                    // third triplet in range
                    // from j+1 to n
                    if (rem > 0)
                        ans += dp[n - 1][rem] - dp[j][rem];
                }
            }
        }
        return ans;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int arr[] = { 2, 5, 1, 20, 6 };
        int n = arr.length;
        dp = new int[1001][15001];

        System.out.println(countTripletSum(arr, n));

    }
}

// This code is contributed by Arnav Kr. Mandal.   
```

## 蟒蛇 3

```
# Python 3 program to calculate all
# triplets whose sum is perfect cube.

dp = [[0 for i in range(15001)]
         for j in range(1001)]

# Function to calculate all occurrence
# of a number in a given range
def computeDpArray(arr, n):
    for i in range(n):
        for j in range(1, 15001, 1):

            # if i == 0
            # assign 1 to present state
            if (i == 0):
                dp[i][j] = (j == arr[i])

            # else add +1 to current state with
            # previous state
            else:
                dp[i][j] = dp[i - 1][j] + (arr[i] == j)

# Function to calculate triplets whose
# sum is equal to the perfect cube
def countTripletSum(arr, n):
    computeDpArray(arr, n)

    ans = 0 # Initialize answer
    for i in range(0, n - 2, 1):
        for j in range(i + 1, n - 1, 1):
            for k in range(1, 25, 1):
                cube = k * k * k

                rem = cube - (arr[i] + arr[j])

                # count all occurrence of third
                # triplet in range from j+1 to n
                if (rem > 0):
                    ans += dp[n - 1][rem] - dp[j][rem]

    return ans

# Driver code
if __name__ == '__main__':
    arr = [2, 5, 1, 20, 6]
    n = len(arr)
    print(countTripletSum(arr, n))

# This code is contributed by
# Sahil_Shelangia
```

## C#

```
// C# Code for Count all triplets whose
// sum is equal to a perfect cube
using System;

class GFG
{

public static int [,]dp;

// Function to calculate all occurrence
// of a number in a given range
public static void computeDpArray(int []arr,
                                  int n)
{
    for (int i = 0; i < n; ++i)
    {
        for (int j = 1; j <= 15000; ++j)
        {

            // if i == 0
            // assign 1 to present state

            if (i == 0 && j == arr[i])
                dp[i, j] = 1;
            else if(i == 0)
                dp[i, j] = 0;

            // else add +1 to current state
            // with previous state
            else if(arr[i] == j)
                dp[i, j] = dp[i - 1, j] + 1;
            else
                dp[i, j] = dp[i - 1, j];
        }
    }
}

// Function to calculate triplets whose
// sum is equal to the perfect cube
public static int countTripletSum(int []arr,
                                  int n)
{
    computeDpArray(arr, n);

    int ans = 0; // Initialize answer
    for (int i = 0; i < n - 2; ++i)
    {
        for (int j = i + 1; j < n - 1; ++j)
        {
            for (int k = 1; k <= 24; ++k)
            {
                int cube = k * k * k;

                int rem = cube - (arr[i] + arr[j]);

                // count all occurrence of
                // third triplet in range
                // from j+1 to n
                if (rem > 0)
                    ans += dp[n - 1, rem] -
                           dp[j, rem];
            }
        }
    }
    return ans;
}

// Driver Code
public static void Main()
{
    int []arr = { 2, 5, 1, 20, 6 };
    int n = arr.Length;
    dp = new int[1001, 15001];

    Console.Write(countTripletSum(arr, n));
}
}

// This code is contributed
// by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate all triplets
// whose sum is perfect cube.

$dp = array_fill(0, 1001,
      array_fill(0, 15001, NULL));

// Function to calculate all occurrence
// of a number in a given range
function computeDpArray(&$arr, $n)
{
    global $dp;
    for ($i = 0; $i < $n; ++$i)
    {
        for ($j = 1; $j <= 15000; ++$j)
        {

            // if i == 0
            // assign 1 to present state
            if ($i == 0)
                $dp[$i][$j] = ($j == $arr[$i]);

            // else add +1 to current state with
            // previous state
            else
                $dp[$i][$j] = $dp[$i - 1][$j] +
                             ($arr[$i] == $j);
        }
    }
}

// Function to calculate triplets whose
// sum is equal to the perfect cube
function countTripletSum(&$arr, $n)
{
    global $dp;
    computeDpArray($arr, $n);

    $ans = 0; // Initialize answer
    for ($i = 0; $i < $n - 2; ++$i)
    {
        for ($j = $i + 1; $j < $n - 1; ++$j)
        {
            for ($k = 1; $k <= 24; ++$k)
            {
                $cube = $k * $k * $k;

                $rem = $cube - ($arr[$i] + $arr[$j]);

                // count all occurrence of third
                // triplet in range from j+1 to n
                if ($rem > 0)
                    $ans += $dp[$n - 1][$rem] -
                            $dp[$j][$rem];
            }
        }
    }
    return $ans;
}

// Driver code
$arr = array(2, 5, 1, 20, 6);
$n = sizeof($arr);
echo countTripletSum($arr, $n);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// JavaScript Code for Count all triplets whose
// sum is equal to a perfect cube
        let dp = new Array(1001);

        // Loop to create 2D array using 1D array
        for (var i = 0; i < dp.length; i++) {
            dp[i] = new Array(2);
        }

    // Function to calculate all occurrence of
    // a number in a given range
    function computeDpArray(arr, n)
    {
        for (let i = 0; i < n; ++i) {
            for (let j = 1; j <= 15000; ++j) {

                // if i == 0
                // assign 1 to present state

                if (i == 0 && j == arr[i])
                    dp[i][j] = 1;
                else if(i==0)
                     dp[i][j] = 0;

                // else add +1 to current state
                // with previous state
                else if(arr[i] == j)
                    dp[i][j] = dp[i - 1][j] + 1;
                else
                    dp[i][j] = dp[i - 1][j];
            }
        }
    }

    // Function to calculate triplets whose sum
    // is equal to the perfect cube
    function countTripletSum(arr, n)
    {
        computeDpArray(arr, n);

        let ans = 0;  // Initialize answer
        for (let i = 0; i < n - 2; ++i)
        {
            for (let j = i + 1; j < n - 1; ++j)
            {
                for (let k = 1; k <= 24; ++k)
                {
                    let cube = k * k * k;

                    let rem = cube - (arr[i] + arr[j]);

                    // count all occurrence of
                    // third triplet in range
                    // from j+1 to n
                    if (rem > 0)
                        ans += dp[n - 1][rem] - dp[j][rem];
                }
            }
        }
        return ans;
    }

// Driver Code
        let arr = [ 2, 5, 1, 20, 6 ];
        let n = arr.length;
        dp = new Array(1001);

        // Loop to create 2D array using 1D array
        for (var i = 0; i < dp.length; i++)
        {
            dp[i] = new Array(2);
        }

        document.write(countTripletSum(arr, n));

// This code is contributed by susmitakundugoaldanga.
</script>
```

**输出:**

```
 3
```

**时间复杂度:**O(N<sup>2</sup>* 24)
T5】辅助空间: O(10 <sup>7</sup>

本文由 [Shubham Bansal](https://www.quora.com/profile/Shubham-Bansal-209) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。