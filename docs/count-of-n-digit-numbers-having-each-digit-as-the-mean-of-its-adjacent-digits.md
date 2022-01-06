# 以每个数字作为其相邻数字的平均值的 N 位数字的计数

> 原文:[https://www . geeksforgeeks . org/n 位数字计数-以每个数字作为其相邻数字的平均值/](https://www.geeksforgeeks.org/count-of-n-digit-numbers-having-each-digit-as-the-mean-of-its-adjacent-digits/)

给定一个正整数 **N** ，任务是计算 **N** 位数字的个数，其中数字中的每个数字是其两个相邻数字的平均值。

**示例:**

> **输入:** N = 1
> **输出:** 10
> **说明:**从 0 到 9 的所有数字都满足给定条件，因为只有一个数字。
> 
> **输入:**N = 2
> T3】输出: 90

**天真方法:**解决给定问题的最简单方法是迭代所有可能的 N 位数，并计算这些数字，其中每个数字是两个相邻数字的平均值。检查所有数字后，打印计数值作为结果。

***时间复杂度:**O(N×10<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming-subset-sum-problem/)进行优化，因为上述问题有[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和一个[最优子结构](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)。子问题可以使用[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)存储在 **dp[][][]表**中，其中**DP[数字][prev1][prev2]** 存储从**数字<sup>第</sup>** 位置直到结束的答案，当选择前一个数字时，是 **prev1** ，选择的第二个前一个数字是 **prev2** 。按照以下步骤解决问题:

*   通过执行以下步骤，定义一个递归函数，比如 **countOfNumbers(数字，prev1，prev2)** 。
    *   如果**数字**的值等于 **N + 1** ，则返回 **1** 作为有效的 **N 位**数字。
    *   如果状态**DP[数字][prev1][prev2]** 的结果已经计算出来，则返回该状态**DP[数字][prev1][prev2]。**
    *   如果当前数字为 **1** ，则可以放置来自**【1，9】**的任意数字。如果 **N = 1** ，那么 **0** 也可以放置。
    *   如果当前数字为 **2** ，则可以放置来自**【0，9】**的任意数字。
    *   否则，考虑**三个**数字 **prev1** 、 **prev2** 和**当前数字**尚未决定。这三个数字中， **prev1** 必须是**prev 2****当前**位的**均值。因此，**当前数字=(2 * prev 1)–prev 2。**如果**电流> = 0** 和**电流< = 9** 那么我们可以把它放在给定的位置。否则返回 0。**
    *   由于均值涉及整数除法，**(电流+ 1)** 如果**(电流+ 1) > = 0** 、**(电流+ 1) ≤ 9** ，也可以放在当前位置。
    *   进行有效放置后，**递归调用**数**函数进行索引**(数字+ 1)。****
    *   返回所有可能的有效数字位置的总和作为答案。
*   打印函数**返回的数值作为结果。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

int dp[100][10][10];

// Function to find number of 'N'
// digit numbers such that the element
// is mean of sum of its adjacent digits
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

    // If current position is 1,
    // then any digit from [1-9]
    // can be placed.
    // If n = 1, 0 can be also placed.
    if (digit == 1) {
        for (int i = (n == 1 ? 0 : 1); i <= 9; ++i) {
            val += countOfNumbers(
                digit + 1, i, prev1, n);
        }
    }

    // If current position is 2,
    // then any digit from [1-9]
    // can be placed.
    else if (digit == 2) {
        for (int i = 0; i <= 9; ++i) {
            val += countOfNumbers(
                digit + 1, i, prev1, n);
        }
    }
    else {

        // previous digit selected is the mean.
        int mean = prev1;

        // mean = (current + prev2) / 2
        // current = (2 * mean) - prev2
        int current = (2 * mean) - prev2;

        // Check if current and current+1
        // can be valid placements
        if (current >= 0 and current <= 9)
            val += countOfNumbers(digit + 1, current, prev1,
                                  n);

        if ((current + 1) >= 0 and (current + 1) <= 9)
            val += countOfNumbers(digit + 1, current + 1,
                                  prev1, n);
    }
    // return answer
    return val;
}

// Driver code
int main()
{
    // Initializing dp array with -1.
    memset(dp, -1, sizeof dp);

    // Given Input
    int n = 2;

    // Function call
    cout << countOfNumbers(1, 0, 0, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static int dp[][][] = new int[100][10][10];

// Function to find number of 'N'
// digit numbers such that the element
// is mean of sum of its adjacent digits
static int countOfNumbers(int digit, int prev1,
                   int prev2, int n)
{
    // If digit = n + 1, a valid
    // n-digit number has been formed
    if (digit == n + 1) {
        return 1;
    }

    // If the state has
    // already been computed
    int val = dp[digit][prev1][prev2];
    if (val != -1) {
        return val;
    }
    val = 0;

    // If current position is 1,
    // then any digit from [1-9]
    // can be placed.
    // If n = 1, 0 can be also placed.
    if (digit == 1) {
        for (int i = (n == 1 ? 0 : 1); i <= 9; ++i) {
            val += countOfNumbers(
                digit + 1, i, prev1, n);
        }
    }

    // If current position is 2,
    // then any digit from [1-9]
    // can be placed.
    else if (digit == 2) {
        for (int i = 0; i <= 9; ++i) {
            val += countOfNumbers(
                digit + 1, i, prev1, n);
        }
    }
    else {

        // previous digit selected is the mean.
        int mean = prev1;

        // mean = (current + prev2) / 2
        // current = (2 * mean) - prev2
        int current = (2 * mean) - prev2;

        // Check if current and current+1
        // can be valid placements
        if (current >= 0 && current <= 9)
            val += countOfNumbers(digit + 1, current, prev1,
                                  n);

        if ((current + 1) >= 0 && (current + 1) <= 9)
            val += countOfNumbers(digit + 1, current + 1,
                                  prev1, n);
    }
    // return answer
    return val;
}

// Driver code
public static void main(String[] args)
{

    // Initializing dp array with -1.
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

    // Given Input
    int n = 2;

    // Function call
    System.out.println(countOfNumbers(1, 0, 0, n));
}
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# python program for the above approach
dp = [[[-1 for i in range(10)] for col in range(20)] for row in range(100)]

# Function to find number of 'N'
# digit numbers such that the element
# is mean of sum of its adjacent digits
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

    # If current position is 1,
    # then any digit from [1-9]
    # can be placed.
    # If n = 1, 0 can be also placed.
    if (digit == 1):
        start = 1
        if(n == 1):
            start = 0
        for i in range(start, 10):
            val += countOfNumbers(digit + 1, i, prev1, n)

    # If current position is 2,
    # then any digit from [1-9]
    # can be placed.
    elif (digit == 2):
        for i in range(0, 10):
            val += countOfNumbers(digit + 1, i, prev1, n)
    else:

        #  previous digit selected is the mean.
        mean = prev1

        # // mean = (current + prev2) / 2
        # // current = (2 * mean) - prev2
        current = (2 * mean) - prev2

        # Check if current and current+1
        # can be valid placements
        if (current >= 0 and current <= 9):
            val += countOfNumbers(digit + 1, current, prev1, n)

        if ((current + 1) >= 0 and (current + 1) <= 9):
            val += countOfNumbers(digit + 1, current + 1, prev1, n)

    # return answer
    return val

# Driver code

# Initializing dp array with -1.
# Given Input
n = 2

# Function call
print(countOfNumbers(1, 0, 0, n))

#cThis code is contributed by amreshkumar3
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static int[,,] dp = new int[100, 10, 10];

// Function to find number of 'N'
// digit numbers such that the element
// is mean of sum of its adjacent digits
static int countOfNumbers(int digit, int prev1,
                   int prev2, int n)
{
    // If digit = n + 1, a valid
    // n-digit number has been formed
    if (digit == n + 1) {
        return 1;
    }

    // If the state has
    // already been computed
    int val = dp[digit, prev1, prev2];
    if (val != -1) {
        return val;
    }
    val = 0;

    // If current position is 1,
    // then any digit from [1-9]
    // can be placed.
    // If n = 1, 0 can be also placed.
    if (digit == 1) {
        for (int i = (n == 1 ? 0 : 1); i <= 9; ++i) {
            val += countOfNumbers(
                digit + 1, i, prev1, n);
        }
    }

    // If current position is 2,
    // then any digit from [1-9]
    // can be placed.
    else if (digit == 2) {
        for (int i = 0; i <= 9; ++i) {
            val += countOfNumbers(
                digit + 1, i, prev1, n);
        }
    }
    else {

        // previous digit selected is the mean.
        int mean = prev1;

        // mean = (current + prev2) / 2
        // current = (2 * mean) - prev2
        int current = (2 * mean) - prev2;

        // Check if current and current+1
        // can be valid placements
        if (current >= 0 && current <= 9)
            val += countOfNumbers(digit + 1, current, prev1,
                                  n);

        if ((current + 1) >= 0 && (current + 1) <= 9)
            val += countOfNumbers(digit + 1, current + 1,
                                  prev1, n);
    }
    // return answer
    return val;
}

// Driver Code
static public void Main ()
{

    // Initializing dp array with -1.
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

    // Given Input
    int n = 2;

    // Function call
    Console.Write(countOfNumbers(1, 0, 0, n));
}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>
// javascript program for the above approach

 var dp = Array(100).fill().map(() =>Array(10).fill().map(()=>Array(10).fill(-1)));

// Function to find number of 'N'
// digit numbers such that the element
// is mean of sum of its adjacent digits
function countOfNumbers(digit , prev1,
                    prev2 , n)
{
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

    // If current position is 1,
    // then any digit from [1-9]
    // can be placed.
    // If n = 1, 0 can be also placed.
    if (digit == 1) {
        for (var i = (n == 1 ? 0 : 1); i <= 9; ++i) {
            val += countOfNumbers(
                digit + 1, i, prev1, n);
        }
    }

    // If current position is 2,
    // then any digit from [1-9]
    // can be placed.
    else if (digit == 2) {
        for (var i = 0; i <= 9; ++i) {
            val += countOfNumbers(
                digit + 1, i, prev1, n);
        }
    }
    else {

        // previous digit selected is the mean.
        var mean = prev1;

        // mean = (current + prev2) / 2
        // current = (2 * mean) - prev2
        var current = (2 * mean) - prev2;

        // Check if current and current+1
        // can be valid placements
        if (current >= 0 && current <= 9)
            val += countOfNumbers(digit + 1, current, prev1,
                                  n);

        if ((current + 1) >= 0 && (current + 1) <= 9)
            val += countOfNumbers(digit + 1, current + 1,
                                  prev1, n);
    }

    // return answer
    return val;
}

// Driver code

    // Given Input
    var n = 2;

    // Function call
    document.write(countOfNumbers(1, 0, 0, n));

// This code is contributed by gauravrajput1
</script>
```

**Output**

```
90
```

***时间复杂度:**O(N×10<sup>2</sup>)*
***辅助空间:** O(N × 10 <sup>2</sup> )*