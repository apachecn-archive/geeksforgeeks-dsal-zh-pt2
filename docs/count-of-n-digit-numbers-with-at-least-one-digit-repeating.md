# 至少有一个数字重复的 N 位数计数

> 原文:[https://www . geeksforgeeks . org/n 位数重复数/](https://www.geeksforgeeks.org/count-of-n-digit-numbers-with-at-least-one-digit-repeating/)

给定一个正整数 **N** ，任务是找到 **N** 位数字的[号，使得该数字中至少有一位数字出现不止一次。](https://www.geeksforgeeks.org/print-all-n-digit-strictly-increasing-numbers/)

**示例:**

> **输入:** N = 2
> **输出:** 9
> **解释:**
> 所有至少 1 位出现一次以上的 2 位数都是{11，22，33，44，55，66，77，88，99}。因此，总数为 9。
> 
> **输入:**N = 5
> T3】输出: 62784

**天真方法:**解决给定问题的最简单方法是生成所有可能的 **N** 位数字，并对那些至少有一个数字出现多次的数字进行计数。检查所有数字后，打印**计数的值**作为数字的总计数。

***时间复杂度:**O(N * 10<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化，因为上述问题有[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和一个[最优子结构](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)。子问题可以存储在 **dp[][][]** 表[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)中，其中**DP[数字][掩码][重复的]** 存储从**数字<sup>第</sup>** 位置直到结束的答案，其中**掩码**存储到目前为止包含在数字中的所有数字，重复的**表示任何数字是否出现过一次以上。按照以下步骤解决问题:**

*   初始化一个全局[多维数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)**DP【50】【1024】【2】**，所有值为 **-1** ，存储每次递归调用的结果。
*   通过执行以下步骤定义一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/)，比如**数字(数字，掩码，重复，N)** 。
    *   如果一个**数字的值**等于 **(N + 1)** ，那么如果**重复**等于**真**，则返回 **1** 作为有效的 **N-** 数字。否则，返回 **0** 。
    *   如果**重复**等于**真**，则返回**幂(10，N-数字+ 1)** 。
    *   如果状态**DP[数字][掩码][重复]** 的结果已经计算出来，则返回该值**DP[数字][掩码][重复]** 。
    *   如果当前**数字**为 **1** ，则可以放置来自**【1，9】**的任意数字，如果 **N = 1** ，则也可以放置 **0** 。
    *   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)T2【N = = 1？0 : 1，9] 使用变量 **i** 并执行以下步骤:
        *   如果设置了**掩码**的 [i <sup>第</sup>位](https://www.geeksforgeeks.org/check-whether-k-th-bit-set-not/)，则添加 **countOfNumbers 的值(数字+ 1，掩码|(1 < < i)，1，N)** 。
        *   否则，添加 **countOfNumbers 的值(数字+ 1，掩码|(1 < < i)，0，N)** 。
    *   否则，[使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，9】**，并执行以下步骤:
        *   如果设置了**掩码**的 [i <sup>第</sup>位](https://www.geeksforgeeks.org/check-whether-k-th-bit-set-not/)，则添加 **countOfNumbers 的值(数字+ 1，掩码|(1 < < i)，1，N)** 。
        *   否则，添加 **countOfNumbers 的值(数字+ 1，掩码|(1 < < i)，0，N)** 。
    *   作为当前递归调用的结果，返回所有可能的有效数字位置**值**的总和。
*   打印[函数](https://www.geeksforgeeks.org/functions-in-c/) **返回的数值(1，0，0，N)** 作为满足给定标准的 N 位数的结果计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

int dp[50][1 << 10][2];

// Function to find the number of N
// digit numbers such that at least
// one digit occurs more than once
int countOfNumbers(int digit, int mask,
                   bool repeated, int n)
{
    // Base Case
    if (digit == n + 1) {
        if (repeated == true) {
            return 1;
        }
        return 0;
    }

    // If repeated is true, then for
    // remaining positions any digit
    // can be placed
    if (repeated == true) {
        return pow(10, n - digit + 1);
    }

    // If the current state has already
    // been computed, then return it
    int& val = dp[digit][mask][repeated];
    if (val != -1) {
        return val;
    }

    // Stores the count of number for
    // the current recursive calls
    val = 0;

    // If current position is 1, then
    // any digit can be placed.

    // If n = 1, 0 can be also placed
    if (digit == 1) {

        for (int i = (n == 1 ? 0 : 1);
             i <= 9; ++i) {

            // If a digit has occurred
            // for the second time, then
            // set repeated to 1
            if (mask & (1 << i)) {
                val += countOfNumbers(
                    digit + 1, mask | (1 << i), 1, n);
            }

            // Otherwise
            else {
                val += countOfNumbers(
                    digit + 1, mask | (1 << i), 0, n);
            }
        }
    }

    // For remaining positions any
    // digit can be placed
    else {
        for (int i = 0; i <= 9; ++i) {

            // If a digit has occurred
            // for the second time, then
            // set repeated to 1
            if (mask & (1 << i)) {
                val += countOfNumbers(
                    digit + 1, mask | (1 << i), 1, n);
            }
            else {
                val += countOfNumbers(
                    digit + 1, mask | (1 << i), 0, n);
            }
        }
    }

    // Return the resultant count for
    // the current recursive call
    return val;
}

// Function to count all the N-digit
// numbers having at least one digit's
// occurrence more than once
void countNDigitNumber(int N)
{
    // Initialize dp array with -1
    memset(dp, -1, sizeof dp);

    // Function to count all possible
    // number satisfying the given
    // criteria
    cout << countOfNumbers(1, 0, 0, N);
}

// Driver Code
int main()
{
    int N = 2;
    countNDigitNumber(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Arrays;

// Java program for the above approach

class GFG {

    public static int[][][] dp = new int[50][1 << 10][2];

    // Function to find the number of N
    // digit numbers such that at least
    // one digit occurs more than once
    public static int countOfNumbers(int digit, int mask,
                                     int repeated, int n)
    {

        // Base Case
        if (digit == n + 1) {
            if (repeated == 1) {
                return 1;
            }
            return 0;
        }

        // If repeated is true, then for
        // remaining positions any digit
        // can be placed
        if (repeated == 1) {
            return (int) Math.pow(10, n - digit + 1);
        }

        // If the current state has already
        // been computed, then return it
        int val = dp[digit][mask][repeated];
        if (val != -1) {
            return val;
        }

        // Stores the count of number for
        // the current recursive calls
        val = 0;

        // If current position is 1, then
        // any digit can be placed.

        // If n = 1, 0 can be also placed
        if (digit == 1) {

            for (int i = (n == 1 ? 0 : 1); i <= 9; ++i) {

                // If a digit has occurred
                // for the second time, then
                // set repeated to 1
                if ((mask & (1 << i)) > 0) {
                    val += countOfNumbers(digit + 1, mask | (1 << i), 1, n);
                }

                // Otherwise
                else {
                    val += countOfNumbers(digit + 1, mask | (1 << i), 0, n);
                }
            }
        }

        // For remaining positions any
        // digit can be placed
        else {
            for (int i = 0; i <= 9; ++i) {

                // If a digit has occurred
                // for the second time, then
                // set repeated to 1
                if ((mask & (1 << i)) > 0) {
                    val += countOfNumbers(digit + 1, mask | (1 << i), 1, n);
                } else {
                    val += countOfNumbers(digit + 1, mask | (1 << i), 0, n);
                }
            }
        }

        // Return the resultant count for
        // the current recursive call
        return val;
    }

    // Function to count all the N-digit
    // numbers having at least one digit's
    // occurrence more than once
    public static void countNDigitNumber(int N)
    {

        // Initialize dp array with -1
        for (int i = 0; i < 50; i++) {
            for (int j = 0; j < 1 << 10; j++) {
                for (int k = 0; k < 2; k++) {
                    dp[i][j][k] = -1;
                }
            }
        }

        // Function to count all possible
        // number satisfying the given
        // criteria
        System.out.println(countOfNumbers(1, 0, 0, N));
    }

    // Driver Code
    public static void main(String args[])
    {
        int N = 2;
        countNDigitNumber(N);

    }
}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# Python program for the above approach

dp = [[[-1 for i in range(2)] for i in range(1 << 10)] for i in range(50)]

# Function to find the number of N
# digit numbers such that at least
# one digit occurs more than once
def countOfNumbers(digit, mask, repeated, n):
    global dp
    # Base Case
    if (digit == n + 1):
        if (repeated == True):
            return 1
        return 0

    # If repeated is true, then for
    # remaining positions any digit
    # can be placed
    if (repeated == True):
        return pow(10, n - digit + 1)

    # If the current state has already
    # been computed, then return it
    val = dp[digit][mask][repeated]
    if (val != -1):
        return val

    # Stores the count of number for
    # the current recursive calls
    val = 4

    # If current position is 1, then
    # any digit can be placed.

    # If n = 1, 0 can be also placed
    if (digit == 1):

        for i in range((0 if (n==1) else 1),10):
            # If a digit has occurred
            # for the second time, then
            # set repeated to 1
            if (mask & (1 << i)):
                val += countOfNumbers(digit + 1, mask | (1 << i), 1, n)
            # Otherwise
        else:
                val += countOfNumbers(digit + 1, mask | (1 << i), 0, n)

    # For remaining positions any
    # digit can be placed
    else:
        for i in range(10):
            # If a digit has occurred
            # for the second time, then
            # set repeated to 1
            if (mask & (1 << i)):
                val += countOfNumbers(digit + 1, mask | (1 << i), 1, n)
        else:
                val += countOfNumbers(digit + 1, mask | (1 << i), 0, n)

    # Return the resultant count for
    # the current recursive call
    dp[digit][mask][repeated] = val
    return dp[digit][mask][repeated]

# Function to count all the N-digit
# numbers having at least one digit's
# occurrence more than once
def countNDigitNumber(N):

    # Function to count all possible
    # number satisfying the given
    # criteria
    print  (countOfNumbers(1, 0, 0, N))

# Driver Code
if __name__ == '__main__':
    N = 2
    countNDigitNumber(N)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

public static int[,,] dp = new int[50, 1 << 10, 2];

// Function to find the number of N
// digit numbers such that at least
// one digit occurs more than once
public static int countOfNumbers(int digit, int mask,
                                 int repeated, int n)
{

    // Base Case
    if (digit == n + 1)
    {
        if (repeated == 1)
        {
            return 1;
        }
        return 0;
    }

    // If repeated is true, then for
    // remaining positions any digit
    // can be placed
    if (repeated == 1)
    {
        return(int)Math.Pow(10, n - digit + 1);
    }

    // If the current state has already
    // been computed, then return it
    int val = dp[digit, mask, repeated];
    if (val != -1)
    {
        return val;
    }

    // Stores the count of number for
    // the current recursive calls
    val = 0;

    // If current position is 1, then
    // any digit can be placed.

    // If n = 1, 0 can be also placed
    if (digit == 1)
    {
        for(int i = (n == 1 ? 0 : 1); i <= 9; ++i)
        {

            // If a digit has occurred
            // for the second time, then
            // set repeated to 1
            if ((mask & (1 << i)) > 0)
            {
                val += countOfNumbers(
                    digit + 1, mask | (1 << i), 1, n);
            }

            // Otherwise
            else
            {
                val += countOfNumbers(
                    digit + 1, mask | (1 << i), 0, n);
            }
        }
    }

    // For remaining positions any
    // digit can be placed
    else
    {
        for(int i = 0; i <= 9; ++i)
        {

            // If a digit has occurred
            // for the second time, then
            // set repeated to 1
            if ((mask & (1 << i)) > 0)
            {
                val += countOfNumbers(
                    digit + 1, mask | (1 << i), 1, n);
            }
            else
            {
                val += countOfNumbers(
                    digit + 1, mask | (1 << i), 0, n);
            }
        }
    }

    // Return the resultant count for
    // the current recursive call
    return val;
}

// Function to count all the N-digit
// numbers having at least one digit's
// occurrence more than once
public static void countNDigitNumber(int N)
{

    // Initialize dp array with -1
    for(int i = 0; i < 50; i++)
    {
        for(int j = 0; j < 1 << 10; j++)
        {
            for(int k = 0; k < 2; k++)
            {
                dp[i, j, k] = -1;
            }
        }
    }

    // Function to count all possible
    // number satisfying the given
    // criteria
    Console.Write(countOfNumbers(1, 0, 0, N));
}

// Driver Code
public static void Main()
{
    int N = 2;

    countNDigitNumber(N);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

let dp = new Array(50).fill(0)
    .map(() => new Array(1 << 10).fill(0)
        .map(() => new Array(2).fill(-1)));

// Function to find the number of N
// digit numbers such that at least
// one digit occurs more than once
function countOfNumbers(digit, mask, repeated, n) {
    // Base Case
    if (digit == n + 1) {
        if (repeated == true) {
            return 1;
        }
        return 0;
    }

    // If repeated is true, then for
    // remaining positions any digit
    // can be placed
    if (repeated == true) {
        return Math.pow(10, n - digit + 1);
    }

    // If the current state has already
    // been computed, then return it
    let val = dp[digit][mask][repeated];
    if (val != -1) {
        return val;
    }

    // Stores the count of number for
    // the current recursive calls
    val = 0;

    // If current position is 1, then
    // any digit can be placed.

    // If n = 1, 0 can be also placed
    if (digit == 1) {

        for (let i = (n == 1 ? 0 : 1);
            i <= 9; ++i) {

            // If a digit has occurred
            // for the second time, then
            // set repeated to 1
            if (mask & (1 << i)) {
                val += countOfNumbers(
                    digit + 1, mask | (1 << i), 1, n);
            }

            // Otherwise
            else {
                val += countOfNumbers(
                    digit + 1, mask | (1 << i), 0, n);
            }
        }
    }

    // For remaining positions any
    // digit can be placed
    else {
        for (let i = 0; i <= 9; ++i) {

            // If a digit has occurred
            // for the second time, then
            // set repeated to 1
            if (mask & (1 << i)) {
                val += countOfNumbers(
                    digit + 1, mask | (1 << i), 1, n);
            }
            else {
                val += countOfNumbers(
                    digit + 1, mask | (1 << i), 0, n);
            }
        }
    }

    // Return the resultant count for
    // the current recursive call
    return val;
}

// Function to count all the N-digit
// numbers having at least one digit's
// occurrence more than once
function countNDigitNumber(N) {
    // Initialize dp array with -1

    // Function to count all possible
    // number satisfying the given
    // criteria
    document.write(countOfNumbers(1, 0, 0, N));
}

// Driver Code

let N = 2;
countNDigitNumber(N);

</script>
```

**Output:** 

```
9
```

***时间复杂度:**O(10 * N * 2<sup>10</sup>* 2<sup>)</sup>*
***辅助空间:** O(N * 2 <sup>10</sup> * 2)*