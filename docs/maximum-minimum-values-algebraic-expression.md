# 代数表达式的最大值和最小值

> 原文:[https://www . geesforgeks . org/maximum-minimum-values-代数-expression/](https://www.geeksforgeeks.org/maximum-minimum-values-algebraic-expression/)

给定形式的代数表达式(x<sub>1</sub>+x<sub>2</sub>+x<sub>3</sub>+。。。+x<sub>n</sub>)*(y<sub>1</sub>+y<sub>2</sub>+。。。+ y <sub>m</sub> )和
(n + m)整数。使用给定的
整数求表达式的最大值和最小值。

> 约束:
> n<= 50
> m<= 50
> -50<= x1，x2，..x<sub>n</sub>T8 = 50

**例:**

```
Input : n = 2, m = 2
        arr[] = {1, 2, 3, 4}
Output : Maximum : 25 
         Minimum : 21
The expression is (x1 + x2) * (y1 + y2) and
the given integers are 1, 2, 3 and 4\. Then
maximum value is (1 + 4) * (2 + 3) = 25 
whereas minimum value is (4 + 3) * (2 + 1) 
= 21.

Input : n = 3, m = 1
        arr[] = {1, 2, 3, 4}
Output : Maximum : 24 
         Minimum : 9
```

一个**简单的解决方案**就是考虑 n 个数和剩余 m 个数的所有可能组合，计算它们的值，从中可以推导出最大值和最小值。
下面是一个**高效解决方案**。
这个想法是基于有限的 n，m，x1，x2，..y1，y2，..假设 S 是表达式中所有(n + m)个数的和，X 是表达式左边 n 个数的和。显然，表达式右边的 m 个数之和将表示为(S–X)。从给定的(n + m)个数中可以有许多可能的 X 值，因此问题简化为简单地迭代 X 的所有值，并跟踪 X *(S–X)的最小值和最大值。
现在，这个问题相当于找到 X 的所有可能值。由于给定的数字在-50 到 50 的范围内，并且(n + m)的最大值是 100，X 将位于-2500 到 2500 之间，这导致 X 的总值为 5000。我们将使用动态编程方法来解决这个问题。考虑一个 dp[i][j]数组，它的值可以是 1 或 0，其中 1 表示通过从(n + m)个数字中选择 I 个数字，X 可以等于 j，否则为 0。那么对于每个数字 k，如果 dp[i][j]是 1，那么 dp[i + 1][j + k]也是 1，其中 k 属于给定的(n + m)个数字。因此，通过遍历所有 k，我们可以通过选择总共 n 个数字来确定 X 的值是否可达
下面是上述方法的实现。

## C++

```
// CPP program to find the maximum
// and minimum values of an Algebraic
// expression of given form
#include <bits/stdc++.h>
using namespace std;

#define INF 1e9
#define MAX 50

int minMaxValues(int arr[], int n, int m)
{
    // Finding sum of array elements
    int sum = 0;
    for (int i = 0; i < (n + m); i++) {
        sum += arr[i];

        // shifting the integers by 50
        // so that they become positive
        arr[i] += 50;
    }

// dp[i][j] represents true if sum
// j can be reachable by choosing
// i numbers
bool dp[MAX+1][MAX * MAX + 1];

    // initialize the dp array to 01
    memset(dp, 0, sizeof(dp));

    dp[0][0] = 1;

    // if dp[i][j] is true, that means
    // it is possible to select i numbers
    // from (n + m) numbers to sum upto j
    for (int i = 0; i < (n + m); i++) {

        // k can be at max n because the
        // left expression has n numbers
        for (int k = min(n, i + 1); k >= 1; k--) {
            for (int j = 0; j < MAX * MAX + 1; j++) {
                if (dp[k - 1][j])
                    dp[k][j + arr[i]] = 1;
            }
        }
    }

    int max_value = -INF, min_value = INF;

    for (int i = 0; i < MAX * MAX + 1; i++) {

        // checking if a particular sum
        // can be reachable by choosing
        // n numbers
        if (dp[n][i]) {

            // getting the actual sum as
            // we shifted the numbers by
            /// 50 to avoid negative indexing
            // in array
            int temp = i - 50 * n;
            max_value = max(max_value, temp * (sum - temp));
            min_value = min(min_value, temp * (sum - temp));
        }
    }
    cout << "Maximum Value: " << max_value
         << "\n"
         << "Minimum Value: "
         << min_value << endl;
}

// Driver Code
int main()
{
    int n = 2, m = 2;
    int arr[] = { 1, 2, 3, 4 };
    minMaxValues(arr, n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum
// and minimum values of an Algebraic
// expression of given form
import java.io.*;
import java.lang.*;

public class GFG {

    static double INF = 1e9;
    static int MAX = 50;

    static void minMaxValues(int []arr, 
                              int n, int m)
    {

        // Finding sum of array elements
        int sum = 0;
        for (int i = 0; i < (n + m); i++)
        {
            sum += arr[i];

            // shifting the integers by 50
            // so that they become positive
            arr[i] += 50;
        }

        // dp[i][j] represents true if sum
        // j can be reachable by choosing
        // i numbers
        boolean dp[][] = 
             new boolean[MAX+1][MAX * MAX + 1];

        dp[0][0] = true;

        // if dp[i][j] is true, that means
        // it is possible to select i numbers
        // from (n + m) numbers to sum upto j
        for (int i = 0; i < (n + m); i++) {

            // k can be at max n because the
            // left expression has n numbers
            for (int k = Math.min(n, i + 1); k >= 1; k--) 
            {
                for (int j = 0; j < MAX * MAX + 1; j++)
                {
                    if (dp[k - 1][j])
                        dp[k][j + arr[i]] = true;
                }
            }
        }

        double max_value = -1 * INF, min_value = INF;

        for (int i = 0; i < MAX * MAX + 1; i++)
        {

            // checking if a particular sum
            // can be reachable by choosing
            // n numbers
            if (dp[n][i]) {

                // getting the actual sum as
                // we shifted the numbers by
                /// 50 to avoid negative indexing
                // in array
                int temp = i - 50 * n;
                max_value = Math.max(max_value, temp *
                                        (sum - temp));

                min_value = Math.min(min_value, temp * 
                                        (sum - temp));
            }
        }

        System.out.print("Maximum Value: " + 
                     (int)max_value + "\n" + 
          "Minimum Value: " + (int)min_value + "\n");
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 2, m = 2;
        int []arr = { 1, 2, 3, 4 };
        minMaxValues(arr, n, m);
    }
}

// This code is contributed by Manish Shaw
// (manishshaw1)
```

## 蟒蛇 3

```
# Python3 program to find the 
# maximum and minimum values 
# of an Algebraic expression 
# of given form
def minMaxValues(arr, n, m) :     
    # Finding sum of
    # array elements
    sum = 0
    INF = 1000000000
    MAX = 50
    for i in range(0, (n + m)) :
        sum += arr[i]

        # shifting the integers by 50
        # so that they become positive
        arr[i] += 50

    # dp[i][j] represents true 
    # if sum j can be reachable
    # by choosing i numbers
    dp = [[0 for x in range(MAX * MAX + 1)]
                  for y in range( MAX + 1)]

    dp[0][0] = 1

    # if dp[i][j] is true, that 
    # means it is possible to 
    # select i numbers from (n + m)
    # numbers to sum upto j
    for i in range(0, (n + m)) : 

        # k can be at max n because the
        # left expression has n numbers
        for k in range(min(n, i + 1), 0, -1) :
            for j in range(0, MAX * MAX + 1) :
                if (dp[k - 1][j]) :
                    dp[k][j + arr[i]] = 1

    max_value = -1 * INF 
    min_value = INF

    for i in range(0, MAX * MAX + 1) :

        # checking if a particular 
        # sum can be reachable by 
        # choosing n numbers
        if (dp[n][i]) :

            # getting the actual sum 
            # as we shifted the numbers 
            # by 50 to avoid negative 
            # indexing in array
            temp = i - 50 * n
            max_value = max(max_value, 
                         temp * (sum - temp))

            min_value = min(min_value,
                         temp * (sum - temp))

    print ("Maximum Value: {}\nMinimum Value: {}"
                 .format(max_value, min_value))

# Driver Code
n = 2
m = 2
arr = [ 1, 2, 3, 4 ]

minMaxValues(arr, n, m) 

# This code is contributed by 
# Manish Shaw(manishshaw1)
```

## C#

```
// C# program to find the maximum
// and minimum values of an Algebraic
// expression of given form
using System;
using System.Collections.Generic;

class GFG {

    static double INF = 1e9;
    static int MAX = 50;

    static void minMaxValues(int []arr, int n, int m)
    {

        // Finding sum of array elements
        int sum = 0;
        for (int i = 0; i < (n + m); i++)
        {
            sum += arr[i];

            // shifting the integers by 50
            // so that they become positive
            arr[i] += 50;
        }

    // dp[i][j] represents true if sum
    // j can be reachable by choosing
    // i numbers
        bool[,] dp = new bool[MAX+1, MAX * MAX + 1];

        dp[0,0] = true;

        // if dp[i][j] is true, that means
        // it is possible to select i numbers
        // from (n + m) numbers to sum upto j
        for (int i = 0; i < (n + m); i++) {

            // k can be at max n because the
            // left expression has n numbers
            for (int k = Math.Min(n, i + 1); k >= 1; k--) 
            {
                for (int j = 0; j < MAX * MAX + 1; j++)
                {
                    if (dp[k - 1,j])
                        dp[k,j + arr[i]] = true;
                }
            }
        }

        double max_value = -1 * INF, min_value = INF;

        for (int i = 0; i < MAX * MAX + 1; i++)
        {

            // checking if a particular sum
            // can be reachable by choosing
            // n numbers
            if (dp[n,i]) {

                // getting the actual sum as
                // we shifted the numbers by
                /// 50 to avoid negative indexing
                // in array
                int temp = i - 50 * n;
                max_value = Math.Max(max_value, temp *
                                          (sum - temp));

                min_value = Math.Min(min_value, temp * 
                                          (sum - temp));
            }
        }

        Console.WriteLine("Maximum Value: " + max_value
         + "\n" + "Minimum Value: " + min_value + "\n");
    }

    // Driver Code
    public static void Main()
    {
        int n = 2, m = 2;
        int []arr = { 1, 2, 3, 4 };
        minMaxValues(arr, n, m);
    }
}

// This code is contributed by Manish Shaw
// (manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the 
// maximum and minimum values 
// of an Algebraic expression 
// of given form
function minMaxValues($arr, $n, $m)
{         
    // Finding sum of
    // array elements
    $sum = 0;
    $INF = 1000000000;
    $MAX = 50;
    for ($i = 0; $i < ($n + $m); $i++)
    {
        $sum += $arr[$i];

        // shifting the integers by 50
        // so that they become positive
        $arr[$i] += 50;
    }

    // dp[i][j] represents true 
    // if sum j can be reachable
    // by choosing i numbers
    $dp = array();

    // new bool[MAX+1, MAX * MAX + 1];
    for($i = 0; $i < $MAX + 1; $i++)
    {
        for($j = 0; $j < $MAX * $MAX + 1; $j++)
            $dp[$i][$j] = 0; 
    }

    $dp[0][0] = 1;

    // if dp[i][j] is true, that 
    // means it is possible to 
    // select i numbers from (n + m)
    // numbers to sum upto j
    for ($i = 0; $i < ($n + $m); $i++) 
    {

        // k can be at max n because the
        // left expression has n numbers
        for ($k = min($n, $i + 1); 
                      $k >= 1; $k--) 
        {
            for ($j = 0; $j < $MAX * 
                              $MAX + 1; $j++)
            {
                if ($dp[$k - 1][$j])
                    $dp[$k][$j + $arr[$i]] = 1;
            }
        }
    }

    $max_value = -1 * $INF; 
    $min_value = $INF;

    for ($i = 0; $i < $MAX * $MAX + 1; $i++)
    {

        // checking if a particular 
        // sum can be reachable by 
        // choosing n numbers
        if ($dp[$n][$i]) 
        {

            // getting the actual sum 
            // as we shifted the numbers 
            // by 50 to avoid negative 
            // indexing in array
            $temp = $i - 50 * $n;
            $max_value = max($max_value, $temp *
                                ($sum - $temp));

            $min_value = min($min_value, $temp * 
                                ($sum - $temp));
        }
    }

    echo ("Maximum Value: ". $max_value. "\n". 
          "Minimum Value: ". $min_value. "\n");
}

// Driver Code
$n = 2;
$m = 2;
$arr = [ 1, 2, 3, 4 ];

minMaxValues($arr, $n, $m); 

// This code is contributed by 
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// Javascript program to find the maximum
// and minimum values of an Algebraic
// expression of given form

var INF  = 1000000000
var MAX = 50

function minMaxValues(arr, n, m)
{
    // Finding sum of array elements
    var sum = 0;
    for (var i = 0; i < (n + m); i++) {
        sum += arr[i];

        // shifting the integers by 50
        // so that they become positive
        arr[i] += 50;
    }

// dp[i][j] represents true if sum
// j can be reachable by choosing
// i numbers
var dp = Array.from(Array(MAX+1), ()=> Array(MAX*MAX + 1).fill(0));

    dp[0][0] = 1;

    // if dp[i][j] is true, that means
    // it is possible to select i numbers
    // from (n + m) numbers to sum upto j
    for (var i = 0; i < (n + m); i++) {

        // k can be at max n because the
        // left expression has n numbers
        for (var k = Math.min(n, i + 1); k >= 1; k--) {
            for (var j = 0; j < MAX * MAX + 1; j++) {
                if (dp[k - 1][j])
                    dp[k][j + arr[i]] = 1;
            }
        }
    }

    var max_value = -INF, min_value = INF;

    for (var i = 0; i < MAX * MAX + 1; i++) {

        // checking if a particular sum
        // can be reachable by choosing
        // n numbers
        if (dp[n][i]) {

            // getting the actual sum as
            // we shifted the numbers by
            /// 50 to avoid negative indexing
            // in array
            var temp = i - 50 * n;
            max_value = Math.max(max_value, temp * (sum - temp));
            min_value = Math.min(min_value, temp * (sum - temp));
        }
    }
    document.write( "Maximum Value: " + max_value
         + "<br>"
         + "Minimum Value: "
         + min_value );
}

// Driver Code
var n = 2, m = 2;
var arr =[1, 2, 3, 4];
minMaxValues(arr, n, m);

</script>
```

**Output :** 

```
Maximum Value: 25
Minimum Value: 21
```

这种方法的运行时复杂度为 0(MAX * MAX *(n+m)<sup>2</sup>)。