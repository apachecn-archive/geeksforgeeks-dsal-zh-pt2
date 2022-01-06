# 不同奇数和偶数计数相等的 N 位数计数

> 原文:[https://www . geeksforgeeks . org/n 位数字计数-具有相等计数的不同奇数和偶数数字/](https://www.geeksforgeeks.org/count-of-n-digit-numbers-having-equal-count-of-distinct-odd-and-even-digits/)

给定一个正整数 **N** ，任务是对 **N** 位数进行计数，使得该数中不同奇数和偶数位数的计数相同。

**示例:**

> **输入:** N = 2
> **输出:** 45
> **说明:**
> 对于 2 位数，为了满足条件，第一位可以是偶数，第二位可以是奇数，或者第二位可以是奇数，第一位是偶数。第一种情况有(4×5)= 20 种可能性，第二种情况有(5×5)= 25 种可能性。因此答案是 45。
> 
> **输入:**N = 3
> T3】输出: 135

**天真方法:**解决给定问题的最简单方法是[生成所有可能的 **N** 位数](https://www.geeksforgeeks.org/print-all-n-digit-strictly-increasing-numbers/)并计算那些不同的奇数和偶数位数相同的数字。检查所有数字后，打印**计数的值**作为数字的总计数。

***时间复杂度:**O(N * 10<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化，因为上述问题有[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和一个[最优子结构](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)。子问题可以存储在 **dp[][][]表** [记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)中，其中**DP[index][even mask][odd mask]**存储从 **i <sup>th</sup>** 索引位置到结束的答案，其中 **evenMask** 用于确定数字中不同的偶数位数，而 **oddMask** 用于使用确定数字中不同的奇数位数按照以下步骤解决问题:

*   初始化一个全局[多维数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)**DP【100】【1】<T5【5】【1】<<5】**，所有值为-1，存储每次递归调用的结果。
*   定义一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/)，通过执行以下步骤说出**个数(索引，偶数掩码，奇数掩码，N)**
    *   如果一个**指数**的值等于**(N+1)**
        *   计算**偶数掩码**和**奇数掩码**中的设置位数。
        *   如果它们具有相同的计数，那么不同的偶数和奇数的数目是相同的，因此返回 **1** ，因为已经形成了有效的 N 位数。
        *   否则返回 **0** 。
    *   如果状态**的结果 DP[索引][evenMask][oddMask]** 已经计算出来，则返回该值**DP[索引][evenMask][oddMask]** 。
    *   如果当前**索引**为 **1** ，则可以放置来自**【1-9】**的任意数字，如果 **N = 1** ，则也可以放置 **0** 。
    *   对于所有其他索引，可以放置从**【0-9】**开始的任意数字。
    *   对于任何放置的数字，根据数字的奇偶校验，将**偶数掩码**或**奇数掩码**的**(数字/2)<sup>第</sup>**位设置为 **1** 。它表示数字中存在特定的数字。由于我们是用 **2** 来划分数字的，所以大小为 **(1 < < 5)** 的位掩码对于每个 **oddMask** 和 **evenMask** 就足够了。
    *   进行有效放置后，**递归调用**(索引+ 1)** 的**计数**函数。**
    *   返回所有可能的有效数字位置的总和作为答案。
*   完成以上步骤后，将函数 **countOfNumbers(1，0，0，N** )返回的值打印为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Stores the dp-states
int dp[100][1 << 5][1 << 5];

// Recursive Function to find number
// of N-digit numbers which has equal
// count of distinct odd & even digits
int countOfNumbers(int index, int evenMask,
                   int oddMask, int N)
{
    // If index is N + 1
    if (index == N + 1) {

        // Find the count of set bits
        // in the evenMask
        int countOfEvenDigits
            = __builtin_popcount(evenMask);

        // Find the count of set bits
        // in the oddMask
        int countOfOddDigits
            = __builtin_popcount(oddMask);

        // If the count of set bits in both
        // masks are equal then return 1
        // as they have equal number of
        // distinct odd and even digits
        if (countOfOddDigits
            == countOfEvenDigits) {
            return 1;
        }
        return 0;
    }

    int& val = dp[index][evenMask][oddMask];

    // If the state has already
    // been computed
    if (val != -1)
        return val;

    val = 0;

    // If current position is 1, then
    // any digit from [1-9] can be
    // placed

    // If N = 1, 0 can be also placed
    if (index == 1) {

        for (int digit = (N == 1 ? 0 : 1);
             digit <= 9; ++digit) {

            // If digit is odd
            if (digit & 1) {

                // Set the (digit/2)th bit
                // of the oddMask
                val += countOfNumbers(
                    index + 1, evenMask,
                    oddMask | (1 << (digit / 2)), N);
            }

            // Set the (digit/2)th bit
            // of the number evenMask
            else {

                val += countOfNumbers(
                    index + 1,
                    evenMask | (1 << (digit / 2)),
                    oddMask, N);
            }
        }
    }

    // For remaining positions, any
    // digit from [0-9] can be placed
    else {
        for (int digit = 0;
             digit <= 9; ++digit) {

            // If digit is odd
            if (digit & 1) {

                // Set the (digit/2)th
                // bit of oddMask
                val += countOfNumbers(
                    index + 1, evenMask,
                    oddMask | (1 << (digit / 2)), N);
            }

            else {

                // Set the (digit/2)th
                // bit of evenMask
                val += countOfNumbers(
                    index + 1,
                    evenMask | (1 << (digit / 2)),
                    oddMask, N);
            }
        }
    }

    // Return the answer
    return val;
}

// Function to find number of N-digit
// numbers which has equal count of
// distinct odd and even digits
void countNDigitNumber(int N)
{

    // Initialize dp array with -1
    memset(dp, -1, sizeof dp);

    // Function Call
    cout << countOfNumbers(1, 0, 0, N);
}

// Driver Code
int main()
{
    int N = 3;
    countNDigitNumber(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Stores the dp-states
static int[][][] dp = new int[100][1 << 5][1 << 5];

// Returns number of set bits in a number
static int __builtin_popcount(int n)
{
    int d, t = 0;

    while(n > 0)
    {
        d = n % 2;
        n = n / 2;

        if (d == 1)
            t++;
    }
    return t;
}

// Recursive Function to find number
// of N-digit numbers which has equal
// count of distinct odd & even digits
static int countOfNumbers(int index, int evenMask,
                          int oddMask, int N)
{

    // If index is N + 1
    if (index == N + 1)
    {

        // Find the count of set bits
        // in the evenMask
        int countOfEvenDigits = __builtin_popcount(evenMask);

        // Find the count of set bits
        // in the oddMask
        int countOfOddDigits = __builtin_popcount(oddMask);

        // If the count of set bits in both
        // masks are equal then return 1
        // as they have equal number of
        // distinct odd and even digits
        if (countOfOddDigits == countOfEvenDigits)
        {
            return 1;
        }
        return 0;
    }

    int val = dp[index][evenMask][oddMask];

    // If the state has already
    // been computed
    if (val != -1)
        return val;

    val = 0;

    // If current position is 1, then
    // any digit from [1-9] can be
    // placed

    // If N = 1, 0 can be also placed
    if (index == 1)
    {
        for(int digit = (N == 1 ? 0 : 1);
                digit <= 9; ++digit)
        {

            // If digit is odd
            if ((digit & 1) != 0)
            {

                // Set the (digit/2)th bit
                // of the oddMask
                val += countOfNumbers(
                    index + 1, evenMask,
                    oddMask | (1 << (digit / 2)), N);
            }

            // Set the (digit/2)th bit
            // of the number evenMask
            else
            {
                val += countOfNumbers(
                    index + 1,
                    evenMask | (1 << (digit / 2)),
                    oddMask, N);
            }
        }
    }

    // For remaining positions, any
    // digit from [0-9] can be placed
    else
    {
        for(int digit = 0; digit <= 9; ++digit)
        {

            // If digit is odd
            if ((digit & 1) != 0)
            {

                // Set the (digit/2)th
                // bit of oddMask
                val += countOfNumbers(
                    index + 1, evenMask,
                    oddMask | (1 << (digit / 2)), N);
            }
            else
            {

                // Set the (digit/2)th
                // bit of evenMask
                val += countOfNumbers(
                    index + 1,
                    evenMask | (1 << (digit / 2)),
                    oddMask, N);
            }
        }
    }

    // Return the answer
    return val;
}

// Function to find number of N-digit
// numbers which has equal count of
// distinct odd and even digits
static void countNDigitNumber(int N)
{

    // Initialize dp array with -1
    for(int i = 0; i < 100; i++)
    {
        for(int j = 0; j < (1 << 5); j++)
        {
            for(int k = 0; k < (1 << 5); k++)
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
    countNDigitNumber(N);
}
}

// This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Stores the dp-states
static int[,,] dp = new int[100, 1 << 5, 1 << 5];

// Returns number of set bits in a number
static int __builtin_popcount(int n)
{
    int d, t = 0;

    while(n > 0)
    {
        d = n % 2;
        n = n / 2;

        if (d == 1)
            t++;
    }
    return t;
}

// Recursive Function to find number
// of N-digit numbers which has equal
// count of distinct odd & even digits
static int countOfNumbers(int index, int evenMask,
                          int oddMask, int N)
{

    // If index is N + 1
    if (index == N + 1)
    {

        // Find the count of set bits
        // in the evenMask
        int countOfEvenDigits = __builtin_popcount(evenMask);

        // Find the count of set bits
        // in the oddMask
        int countOfOddDigits = __builtin_popcount(oddMask);

        // If the count of set bits in both
        // masks are equal then return 1
        // as they have equal number of
        // distinct odd and even digits
        if (countOfOddDigits == countOfEvenDigits)
        {
            return 1;
        }
        return 0;
    }

    int val = dp[index, evenMask, oddMask];

    // If the state has already
    // been computed
    if (val != -1)
        return val;

    val = 0;

    // If current position is 1, then
    // any digit from [1-9] can be
    // placed

    // If N = 1, 0 can be also placed
    if (index == 1)
    {
        for(int digit = (N == 1 ? 0 : 1);
                digit <= 9; ++digit)
        {

            // If digit is odd
            if ((digit & 1) != 0)
            {

                // Set the (digit/2)th bit
                // of the oddMask
                val += countOfNumbers(
                    index + 1, evenMask,
                    oddMask | (1 << (digit / 2)), N);
            }

            // Set the (digit/2)th bit
            // of the number evenMask
            else
            {
                val += countOfNumbers(
                    index + 1,
                    evenMask | (1 << (digit / 2)),
                    oddMask, N);
            }
        }
    }

    // For remaining positions, any
    // digit from [0-9] can be placed
    else
    {
        for(int digit = 0; digit <= 9; ++digit)
        {

            // If digit is odd
            if ((digit & 1) != 0)
            {

                // Set the (digit/2)th
                // bit of oddMask
                val += countOfNumbers(
                    index + 1, evenMask,
                    oddMask | (1 << (digit / 2)), N);
            }
            else
            {

                // Set the (digit/2)th
                // bit of evenMask
                val += countOfNumbers(
                    index + 1,
                    evenMask | (1 << (digit / 2)),
                    oddMask, N);
            }
        }
    }

    // Return the answer
    return val;
}

// Function to find number of N-digit
// numbers which has equal count of
// distinct odd and even digits
static void countNDigitNumber(int N)
{

    // Initialize dp array with -1
    for(int i = 0; i < 100; i++)
    {
        for(int j = 0; j < (1 << 5); j++)
        {
            for(int k = 0; k < (1 << 5); k++)
            {
                dp[i, j, k] = -1;
            }
        }
    }

    // Function Call
    Console.Write(countOfNumbers(1, 0, 0, N));
}

// Driver Code
public static void Main()
{
    int N = 3;
    countNDigitNumber(N);
}
}

// This code is contributed by target_2.
```

## java 描述语言

```
<script>
// javascript program for the above approach   
// Stores the dp-states
     var dp = Array(100).fill().map(()=>Array(1 << 5).fill().map(()=>Array(1 << 5).fill(0)));

    // Returns number of set bits in a number
    function __builtin_popcount(n) {
        var d, t = 0;

        while (n > 0) {
            d = n % 2;
            n = parseInt(n / 2);

            if (d == 1)
                t++;
        }
        return t;
    }

    // Recursive Function to find number
    // of N-digit numbers which has equal
    // count of distinct odd & even digits
    function countOfNumbers(index , evenMask , oddMask , N) {

        // If index is N + 1
        if (index == N + 1) {

            // Find the count of set bits
            // in the evenMask
            var countOfEvenDigits = __builtin_popcount(evenMask);

            // Find the count of set bits
            // in the oddMask
            var countOfOddDigits = __builtin_popcount(oddMask);

            // If the count of set bits in both
            // masks are equal then return 1
            // as they have equal number of
            // distinct odd and even digits
            if (countOfOddDigits == countOfEvenDigits) {
                return 1;
            }
            return 0;
        }

        var val = dp[index][evenMask][oddMask];

        // If the state has already
        // been computed
        if (val != -1)
            return val;

        val = 0;

        // If current position is 1, then
        // any digit from [1-9] can be
        // placed

        // If N = 1, 0 can be also placed
        if (index == 1) {
            for (digit = (N == 1 ? 0 : 1); digit <= 9; ++digit) {

                // If digit is odd
                if ((digit & 1) != 0) {

                    // Set the (digit/2)th bit
                    // of the oddMask
                    val += countOfNumbers(index + 1, evenMask, oddMask | (1 << (digit / 2)), N);
                }

                // Set the (digit/2)th bit
                // of the number evenMask
                else {
                    val += countOfNumbers(index + 1, evenMask | (1 << (digit / 2)), oddMask, N);
                }
            }
        }

        // For remaining positions, any
        // digit from [0-9] can be placed
        else {
            for (var digit = 0; digit <= 9; ++digit) {

                // If digit is odd
                if ((digit & 1) != 0) {

                    // Set the (digit/2)th
                    // bit of oddMask
                    val += countOfNumbers(index + 1, evenMask, oddMask | (1 << (digit / 2)), N);
                } else {

                    // Set the (digit/2)th
                    // bit of evenMask
                    val += countOfNumbers(index + 1, evenMask | (1 << (digit / 2)), oddMask, N);
                }
            }
        }

        // Return the answer
        return val;
    }

    // Function to find number of N-digit
    // numbers which has equal count of
    // distinct odd and even digits
    function countNDigitNumber(N) {

        // Initialize dp array with -1
        for (var i = 0; i < 100; i++) {
            for (var j = 0; j < (1 << 5); j++) {
                for (var k = 0; k < (1 << 5); k++) {
                    dp[i][j][k] = -1;
                }
            }
        }

        // Function Call
        document.write(countOfNumbers(1, 0, 0, N));
    }

    // Driver code
        var N = 3;
        countNDigitNumber(N);

// This code is contributed by gauravrajput1
</script>
```

**Output:** 

```
135
```

***时间复杂度:**O(N * 10 * 2<sup>5</sup>* 2<sup>5</sup>)*
***辅助空间:**O(N * 2<sup>5</sup>* 2<sup>5</sup>)*