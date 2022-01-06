# 相邻数字的绝对差不增加的 N 位数的计数

> 原文:[https://www . geeksforgeeks . org/n 位数计数-其相邻位数之间的绝对差值不增加/](https://www.geeksforgeeks.org/count-of-n-digit-numbers-whose-absolute-difference-between-adjacent-digits-is-non-increasing/)

给定一个正整数 **N** ，任务是按非递增顺序计算连续数字之间有绝对差的 **N** 位数。

**示例:**

> **输入:** N = 1
> **输出:** 10
> **说明:**
> 从 0 到 9 的所有数字都满足给定条件，因为只有一个数字。
> 
> **输入:**N = 3
> T3】输出: 495

**天真方法:**解决给定问题最简单的方法是迭代[所有可能的 N 位数](https://www.geeksforgeeks.org/count-of-n-digit-numbers-whose-sum-of-digits-equals-to-given-sum/)并计算那些位数不递增的数字。检查所有数字后，打印**的数值并计算**作为结果。

***时间复杂度:**O(N * 10<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化，因为上述问题有[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和[最优子结构](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)。子问题可以使用[记忆](https://www.geeksforgeeks.org/tabulation-vs-memoization/)存储在 **dp[][][]表**中，其中**DP[数字][prev1][prev2]** 存储从**数字<sup>第</sup>** 位置直到结束的答案，当选择前一个数字时，是 **prev1** ，选择的第二个前一个数字是 **prev2** 。按照以下步骤解决问题:

*   通过执行以下步骤，定义一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/)，比如**数字计数(数字，prev1，prev2)** 。
    *   如果**位数**的值等于 **N + 1** ，则返回 **1** 作为有效的 **N 位数**形成。
    *   如果状态**DP[数字][prev1][prev2]** 的结果已经计算出来，则返回该状态**DP[数字][prev1][prev2]** 。
    *   如果当前**位**为 **1** ，则可以放置**【1，9】**中的任意一位。如果 **N = 1** ，那么 **0** 也可以放置。
    *   如果当前**位**为 **2** ，则可以放置**【0，9】**中的任意一位。
    *   否则，遍历从 **i = 0 到 i = 9 的所有数字**，检查条件**(ABS(prev 1–I)<= ABS(prev 1–prev 2))**是否有效，并相应地将满足**‘I’**的值放置在当前位置。
    *   进行有效放置后，**递归调用**数**函数进行索引**(数字+ 1)** 。**
    *   返回所有可能的有效数字位置的总和作为答案。
*   打印函数**返回的数值作为结果。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

int dp[100][10][10];

// Function to count N-digit numbers
// having absolute difference between
// adjacent digits in non-increasing order
int countOfNumbers(int digit, int prev1,
                   int prev2, int n)
{
    // If digit = n + 1, a valid
    // n-digit number has been formed
    if (digit == n + 1) {
        return 1;
    }

    // If the state has
    // already been computed
    int& val = dp[digit][prev1][prev2];

    if (val != -1) {
        return val;
    }
    val = 0;

    // If the current digit is 1,
    // then any digit from [1-9]
    // can be placed
    if (digit == 1) {

        for (int i = (n == 1 ? 0 : 1);
             i <= 9; ++i) {
            val += countOfNumbers(
                digit + 1, i, prev1, n);
        }
    }

    // If the current digit is 2, any
    // digit from [0-9] can be placed
    else if (digit == 2) {

        for (int i = 0; i <= 9; ++i) {

            val += countOfNumbers(
                digit + 1, i, prev1, n);
        }
    }

    // For other digits, any digit i
    // can be placed which satisfies
    // abs(prev1 - i) <= abs(prev1 - prev2)
    else {
        int diff = abs(prev2 - prev1);

        for (int i = 0; i <= 9; ++i) {

            // If absolute difference is
            // less than or equal to diff
            if (abs(prev1 - i) <= diff) {

                val += countOfNumbers(
                    digit + 1, i,
                    prev1, n);
            }
        }
    }
    return val;
}

// Function to count N-digit numbers with
// absolute difference between adjacent
// digits in non increasing order
int countNumbersUtil(int N)
{
    // Initialize dp table with -1
    memset(dp, -1, sizeof dp);

    // Function Call
    cout << countOfNumbers(1, 0, 0, N);
}

// Driver code
int main()
{
    int N = 3;
    countNumbersUtil(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

static int dp[][][] = new int[100][10][10];

// Function to count N-digit numbers
// having absolute difference between
// adjacent digits in non-increasing order
static int countOfNumbers(int digit, int prev1,
                          int prev2, int n)
{

    // If digit = n + 1, a valid
    // n-digit number has been formed
    if (digit == n + 1)
    {
        return 1;
    }

    // If the state has
    // already been computed
    int val = dp[digit][prev1][prev2];

    if (val != -1)
    {
        return val;
    }
    val = 0;

    // If the current digit is 1,
    // then any digit from [1-9]
    // can be placed
    if (digit == 1)
    {
        for(int i = (n == 1 ? 0 : 1);
                i <= 9; ++i)
        {
            val += countOfNumbers(
                digit + 1, i, prev1, n);
        }
    }

    // If the current digit is 2, any
    // digit from [0-9] can be placed
    else if (digit == 2)
    {
        for(int i = 0; i <= 9; ++i)
        {
            val += countOfNumbers(
                digit + 1, i, prev1, n);
        }
    }

    // For other digits, any digit i
    // can be placed which satisfies
    // abs(prev1 - i) <= abs(prev1 - prev2)
    else
    {
        int diff = Math.abs(prev2 - prev1);

        for(int i = 0; i <= 9; ++i)
        {

            // If absolute difference is
            // less than or equal to diff
            if (Math.abs(prev1 - i) <= diff)
            {
                val += countOfNumbers(
                    digit + 1, i,
                    prev1, n);
            }
        }
    }
    return val;
}

// Function to count N-digit numbers with
// absolute difference between adjacent
// digits in non increasing order
static void countNumbersUtil(int N)
{

    // Initialize dp table with -1
    for(int i = 0; i < 100; i++)
    {
        for(int j = 0; j < 10; j++)
        {
            for(int k = 0; k < 10; k++)
            {
                dp[i][j][k] = -1;
            }
        }
    }

    // Function Call
    System.out.println(countOfNumbers(1, 0, 0, N));
}

// Driver code
public static void main(String[] args)
{
    int N = 3;

    countNumbersUtil(N);
}
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python3 program for the above approach
dp = [[[0 for i in range(10)]
          for col in range(10)]
          for row in range(100)]

# Function to count N-digit numbers
# having absolute difference between
# adjacent digits in non-increasing order
def countOfNumbers(digit, prev1, prev2, n):

    # If digit = n + 1, a valid
    # n-digit number has been formed
    if (digit == n + 1):
        return 1

    # If the state has
    # already been computed
    val = dp[digit][prev1][prev2]

    if (val != -1):
        return val

    val = 0

    # If the current digit is 1,
    # then any digit from [1-9]
    # can be placed
    if (digit == 1):
        i = 1
        if n == 1:
            i = 0

        for j in range(i, 10):
            val += countOfNumbers(digit + 1, j, prev1, n)

    # If the current digit is 2, any
    # digit from [0-9] can be placed
    elif (digit == 2):
        for i in range(0, 10):
            val += countOfNumbers(digit + 1, i, prev1, n)

    # For other digits, any digit i
    # can be placed which satisfies
    # abs(prev1 - i) <= abs(prev1 - prev2)
    else:
        diff = abs(prev2 - prev1)
        for i in range(0, 10):

            # If absolute difference is
            # less than or equal to diff
            if (abs(prev1 - i) <= diff):
                val += countOfNumbers(digit + 1, i, prev1, n)
    return val

# Function to count N-digit numbers with
# absolute difference between adjacent
# digits in non increasing order
def countNumbersUtil(N):

    # Initialize dp table with -1
    for i in range(0, 100):
        for j in range(0, 10):
            for k in range(0, 10):
                dp[i][j][k] = -1

    # Function Call
    print(countOfNumbers(1, 0, 0, N))

# Driver code
N = 3

countNumbersUtil(N)

# This code is contributed by amreshkumar3
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static int[,,] dp = new int[100, 10, 10];

// Function to count N-digit numbers
// having absolute difference between
// adjacent digits in non-increasing order
static int countOfNumbers(int digit, int prev1,
                          int prev2, int n)
{

    // If digit = n + 1, a valid
    // n-digit number has been formed
    if (digit == n + 1)
    {
        return 1;
    }

    // If the state has
    // already been computed
    int val = dp[digit, prev1, prev2];

    if (val != -1)
    {
        return val;
    }
    val = 0;

    // If the current digit is 1,
    // then any digit from [1-9]
    // can be placed
    if (digit == 1)
    {
        for(int i = (n == 1 ? 0 : 1);
                i <= 9; ++i)
        {
            val += countOfNumbers(
                digit + 1, i, prev1, n);
        }
    }

    // If the current digit is 2, any
    // digit from [0-9] can be placed
    else if (digit == 2)
    {
        for(int i = 0; i <= 9; ++i)
        {
            val += countOfNumbers(
                digit + 1, i, prev1, n);
        }
    }

    // For other digits, any digit i
    // can be placed which satisfies
    // abs(prev1 - i) <= abs(prev1 - prev2)
    else
    {
        int diff = Math.Abs(prev2 - prev1);

        for(int i = 0; i <= 9; ++i)
        {

            // If absolute difference is
            // less than or equal to diff
            if (Math.Abs(prev1 - i) <= diff)
            {
                val += countOfNumbers(
                    digit + 1, i,
                    prev1, n);
            }
        }
    }
    return val;
}

// Function to count N-digit numbers with
// absolute difference between adjacent
// digits in non increasing order
static void countNumbersUtil(int N)
{

    // Initialize dp table with -1
    for(int i = 0; i < 100; i++)
    {
        for(int j = 0; j < 10; j++)
        {
            for(int k = 0; k < 10; k++)
            {
                dp[i, j, k] = -1;
            }
        }
    }

    // Function Call
    Console.WriteLine(countOfNumbers(1, 0, 0, N));
}

// Driver code
static public void Main()
{
    int N = 3;

    countNumbersUtil(N);
}
}

// This code is contributed by splevel62
```

## java 描述语言

```
<script>
// javascript program for the above approach

     var dp = Array(100).fill().map(() => Array(10).fill(0).map(()=>Array(10).fill(0)));

    // Function to count N-digit numbers
    // having absolute difference between
    // adjacent digits in non-increasing order
    function countOfNumbers(digit , prev1 , prev2 , n) {

        // If digit = n + 1, a valid
        // n-digit number has been formed
        if (digit == n + 1) {
            return 1;
        }

        // If the state has
        // already been computed
        var val = dp[digit][prev1][prev2];

        if (val != -1) {
            return val;
        }
        val = 0;

        // If the current digit is 1,
        // then any digit from [1-9]
        // can be placed
        if (digit == 1) {
            for (var i = (n == 1 ? 0 : 1); i <= 9; ++i) {
                val += countOfNumbers(digit + 1, i, prev1, n);
            }
        }

        // If the current digit is 2, any
        // digit from [0-9] can be placed
        else if (digit == 2) {
            for (var i = 0; i <= 9; ++i) {
                val += countOfNumbers(digit + 1, i, prev1, n);
            }
        }

        // For other digits, any digit i
        // can be placed which satisfies
        // abs(prev1 - i) <= abs(prev1 - prev2)
        else {
            var diff = Math.abs(prev2 - prev1);

            for (var i = 0; i <= 9; ++i) {

                // If absolute difference is
                // less than or equal to diff
                if (Math.abs(prev1 - i) <= diff) {
                    val += countOfNumbers(digit + 1, i, prev1, n);
                }
            }
        }
        return val;
    }

    // Function to count N-digit numbers with
    // absolute difference between adjacent
    // digits in non increasing order
    function countNumbersUtil(N) {

        // Initialize dp table with -1
        for (var i = 0; i < 100; i++) {
            for (var j = 0; j < 10; j++) {
                for (var k = 0; k < 10; k++) {
                    dp[i][j][k] = -1;
                }
            }
        }

        // Function Call
        document.write(countOfNumbers(1, 0, 0, N));
    }

    // Driver code
        var N = 3;
        countNumbersUtil(N);

// This code is contributed by gauravrajput1
</script>
```

**Output**

```
495
```

***时间复杂度:**O(N * 10<sup>3</sup>)*
***辅助空间:** O(N * 10 <sup>2</sup> )*