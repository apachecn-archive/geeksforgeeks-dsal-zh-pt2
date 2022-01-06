# 没有两个元素相邻的最大和|集合 2

> 原文:[https://www . geesforgeks . org/maximum-sum-so-no-two-elements-neighbor-set-2/](https://www.geeksforgeeks.org/maximum-sum-such-that-no-two-elements-are-adjacent-set-2/)

给定一个正数数组，求一个子序列的最大和，条件是序列中没有 2 个数字在数组中是相邻的。所以 3 2 7 10 应该返回 13(3 和 10 的和)或者 3 2 5 10 7 应该返回 15(3、5 和 7 的和)。

**示例:**

```
Input :  arr[] = {3, 5, 3} 
Output : 6 
Explanation : 
Selecting indexes 0 and 2 will maximise the sum 
i.e 3+3 = 6

Input : arr[] = {2, 5, 2}
Output : 5 
```

在[之前的文章](https://www.geeksforgeeks.org/maximum-sum-such-that-no-two-elements-are-adjacent/)中，我们已经讨论了解决这个问题的有效方法。
但是，我们也可以使用*动态规划*方法来解决这个问题。
**动态规划法:**我们来决定‘DP’的状态。假设 dp[i]是从索引“I”开始到索引“N-1”结束的子阵列的最大可能和。现在，我们必须找到这个状态和低阶状态之间的递归关系。
在这种情况下，对于指数‘I’，我们将有两个选择。

```
1) Choose the current index:
   In this case, the relation will be dp[i] = arr[i] + dp[i+2]
2) Skip the current index:
   Relation will be dp[i] = dp[i+1]
```

我们将选择最大化我们结果的道路。
因此，最终关系将是:

```
dp[i] = max(dp[i+2]+arr[i], dp[i+1])
```

下面是上述方法的实现:

## C++

```
// C++ program to implement above approach

#include <bits/stdc++.h>
#define maxLen 10
using namespace std;

// variable to store states of dp
int dp[maxLen];

// variable to check if a given state
// has been solved
bool v[maxLen];

// Function to find the maximum sum subsequence
// such that no two elements are adjacent
int maxSum(int arr[], int i, int n)
{
    // Base case
    if (i >= n)
        return 0;

    // To check if a state has
    // been solved
    if (v[i])
        return dp[i];
    v[i] = 1;

    // Required recurrence relation
    dp[i] = max(maxSum(arr, i + 1, n),
                arr[i] + maxSum(arr, i + 2, n));

    // Returning the value
    return dp[i];
}

// Driver code
int main()
{
    int arr[] = { 12, 9, 7, 33 };

    int n = sizeof(arr) / sizeof(int);

    cout << maxSum(arr, 0, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement above approach
class GFG
{

static int maxLen = 10;

// variable to store states of dp
static int dp[] = new int[maxLen];

// variable to check if a given state
// has been solved
static boolean v[] = new boolean[maxLen];

// Function to find the maximum sum subsequence
// such that no two elements are adjacent
static int maxSum(int arr[], int i, int n)
{
    // Base case
    if (i >= n)
        return 0;

    // To check if a state has
    // been solved
    if (v[i])
        return dp[i];
    v[i] = true;

    // Required recurrence relation
    dp[i] = Math.max(maxSum(arr, i + 1, n),
                arr[i] + maxSum(arr, i + 2, n));

    // Returning the value
    return dp[i];
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 12, 9, 7, 33 };
    int n = arr.length;
    System.out.println( maxSum(arr, 0, n));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 program to implement above approach
maxLen = 10

# variable to store states of dp
dp = [0 for i in range(maxLen)]

# variable to check if a given state
# has been solved
v = [0 for i in range(maxLen)]

# Function to find the maximum sum subsequence
# such that no two elements are adjacent
def maxSum(arr, i, n):
    # Base case
    if (i >= n):
        return 0

    # To check if a state has
    # been solved
    if (v[i]):
        return dp[i]
    v[i] = 1

    # Required recurrence relation
    dp[i] = max(maxSum(arr, i + 1, n),
            arr[i] + maxSum(arr, i + 2, n))

    # Returning the value
    return dp[i]

# Driver code
if __name__ == '__main__':
    arr = [12, 9, 7, 33]

    n = len(arr)
    print(maxSum(arr, 0, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to implement above approach
using System;

class GFG
{

static int maxLen = 10;

// variable to store states of dp
static int[] dp = new int[maxLen];

// variable to check if a given state
// has been solved
static bool[] v = new bool[maxLen];

// Function to find the maximum sum subsequence
// such that no two elements are adjacent
static int maxSum(int[] arr, int i, int n)
{
    // Base case
    if (i >= n)
        return 0;

    // To check if a state has
    // been solved
    if (v[i])
        return dp[i];
    v[i] = true;

    // Required recurrence relation
    dp[i] = Math.Max(maxSum(arr, i + 1, n),
                arr[i] + maxSum(arr, i + 2, n));

    // Returning the value
    return dp[i];
}

// Driver code
public static void Main()
{
    int[] arr = { 12, 9, 7, 33 };
    int n = arr.Length;
    Console.Write( maxSum(arr, 0, n));
}
}

// This code is contributed by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement above approach

$maxLen = 10;

// variable to store states of dp
$dp = array_fill(0, $GLOBALS['maxLen'], 0);

// variable to check if a given state
// has been solved
$v = array_fill(0, $GLOBALS['maxLen'], 0);

// Function to find the maximum sum subsequence
// such that no two elements are adjacent
function maxSum($arr, $i, $n)
{
    // Base case
    if ($i >= $n)
        return 0;

    // To check if a state has
    // been solved
    if ($GLOBALS['v'][$i])
        return $GLOBALS['dp'][$i];

    $GLOBALS['v'][$i] = 1;

    // Required recurrence relation
    $GLOBALS['dp'][$i] = max(maxSum($arr, $i + 1, $n),
                $arr[$i] + maxSum($arr, $i + 2, $n));

    // Returning the value
    return $GLOBALS['dp'][$i];
}

    // Driver code
    $arr = array( 12, 9, 7, 33 );

    $n = count($arr);

    echo maxSum($arr, 0, $n);

    // This code is contributed by AnkitRai01
?>
```

## java 描述语言

```
<script>

// Javascript program to implement above approach
var maxLen = 10;

// variable to store states of dp
var dp = Array(maxLen);

// variable to check if a given state
// has been solved
var v = Array(maxLen);

// Function to find the maximum sum subsequence
// such that no two elements are adjacent
function maxSum(arr, i, n)
{
    // Base case
    if (i >= n)
        return 0;

    // To check if a state has
    // been solved
    if (v[i])
        return dp[i];
    v[i] = 1;

    // Required recurrence relation
    dp[i] = Math.max(maxSum(arr, i + 1, n),
                arr[i] + maxSum(arr, i + 2, n));

    // Returning the value
    return dp[i];
}

// Driver code
var arr = [12, 9, 7, 33 ];
var n = arr.length;
document.write( maxSum(arr, 0, n));

</script>
```

**Output:** 

```
45
```