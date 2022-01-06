# 相邻数字的位“与”等于 0 的 N 位数字的计数

> 原文:[https://www . geeksforgeeks . org/n 位数计数-其相邻位数的位与等于-0/](https://www.geeksforgeeks.org/count-of-n-digit-numbers-whose-bitwise-and-of-adjacent-digits-equals-0/)

给定一个正整数 **N** ，任务是对 **N** 位数进行计数，使得相邻位数的[位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)等于 0。

**示例:**

> **输入:** N = 1
> **输出:** 10
> **说明:**从 0 到 9 的所有数字都满足给定条件，因为只有一个数字。
> 
> **输入:**N = 3
> T3】输出: 264

**天真方法:**解决给定问题的最简单方法是迭代所有可能的 N 位数字，并计算那些相邻数字的[位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)为 **0** 的数字。检查所有数字后，打印**的值并计算**作为结果。

***时间复杂度:**O(N×10<sup>N</sup>)*
***辅助空间:*** **O(1)**

**高效方法:**上述方法也可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化，因为上述问题有[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和一个[最优子结构](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)。子问题可以使用[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)存储在 **dp[][]表**中，其中**DP[数字][prev]** 存储从**数字<sup>第</sup>** 位置直到结束的答案，此时选择的前一个数字是 **prev** 。按照以下步骤解决问题:

*   通过执行以下步骤，定义一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/)，比如**数字计数(数字，前一个)**。
    *   如果**数字**的值等于 **N + 1** ，则返回 **1** 作为有效的 **N 位**数字。
    *   如果已经计算出状态**DP[数字][前一个]** 的结果，返回该状态**DP[数字][前一个]** 。
    *   如果当前**位**为 **1** ，则可以放置**【1，9】**中的任意一位。如果 **N = 1** ，那么 **0** 也可以放置。
    *   否则，遍历从 **i = 0 到 i = 9** 的所有数字，检查条件 **((i & prev) == 0)** 是否成立，并相应地将满足**“I”**的值放置在当前位置。
    *   进行有效放置后，**递归调用**数**函数进行索引**(数字+ 1)** 。**
    *   返回所有可能的有效数字位置的总和作为答案。
*   打印函数**返回的数值作为结果。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

int dp[100][10];

// Function to calculate count of 'N' digit
// numbers such that bitwise AND of adjacent
// digits is 0.
int countOfNumbers(int digit, int prev, int n)
{
    // If digit = n + 1, a valid
    // n-digit number has been formed
    if (digit == n + 1) {
        return 1;
    }

    // If the state has
    // already been computed
    int& val = dp[digit][prev];
    if (val != -1) {
        return val;
    }
    val = 0;

    // If current position is 1,
    // then any digit from [1-9] can be placed.
    // If n = 1, 0 can be also placed.
    if (digit == 1) {
        for (int i = (n == 1 ? 0 : 1); i <= 9; ++i) {
            val += countOfNumbers(digit + 1, i, n);
        }
    }

    // For remaining positions,
    // any digit from [0-9] can be placed
    // after checking the conditions.
    else {
        for (int i = 0; i <= 9; ++i) {

            // Check if bitwise AND
            // of current digit and
            // previous digit is 0.
            if ((i & prev) == 0) {
                val += countOfNumbers(digit + 1, i, n);
            }
        }
    }
    // Return answer
    return val;
}

// Driver code
int main()
{
    // Initialize dp array with -1.
    memset(dp, -1, sizeof dp);

    // Given Input
    int N = 3;

    // Function call
    cout << countOfNumbers(1, 0, N) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static int dp[][] = new int[100][10];

// Function to calculate count of 'N' digit
// numbers such that bitwise AND of adjacent
// digits is 0.
static int countOfNumbers(int digit, int prev, int n)
{

    // If digit = n + 1, a valid
    // n-digit number has been formed
    if (digit == n + 1)
    {
        return 1;
    }

    // If the state has
    // already been computed
    int val = dp[digit][prev];

    if (val != -1)
    {
        return val;
    }
    val = 0;

    // If current position is 1,
    // then any digit from [1-9] can be placed.
    // If n = 1, 0 can be also placed.
    if (digit == 1)
    {
        for(int i = (n == 1 ? 0 : 1); i <= 9; ++i)
        {
            val += countOfNumbers(digit + 1, i, n);
        }
    }

    // For remaining positions,
    // any digit from [0-9] can be placed
    // after checking the conditions.
    else
    {
        for(int i = 0; i <= 9; ++i)
        {

            // Check if bitwise AND
            // of current digit and
            // previous digit is 0.
            if ((i & prev) == 0)
            {
                val += countOfNumbers(digit + 1, i, n);
            }
        }
    }

    // Return answer
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
            dp[i][j] = -1;
        }
    }

    // Given Input
    int N = 3;

    // Function call
    System.out.println(countOfNumbers(1, 0, N));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach
dp = [[-1 for i in range(10)]
          for j in range(100)]

val = 0

# Function to calculate count of 'N' digit
# numbers such that bitwise AND of adjacent
# digits is 0.
def countOfNumbers(digit, prev, n):

    global val
    global dp

    # If digit = n + 1, a valid
    # n-digit number has been formed
    if (digit == n + 1):
        return 1

    # If the state has
    # already been computed
    val = dp[digit][prev]
    if (val != -1):
        return val

    val = 0

    # If current position is 1,
    # then any digit from [1-9] can be placed.
    # If n = 1, 0 can be also placed.
    if (digit == 1):
        i = 0 if n == 1 else 1

        while (i <= 9):
            val += countOfNumbers(digit + 1, i, n)
            i += 1

    # For remaining positions,
    # any digit from [0-9] can be placed
    # after checking the conditions.
    else:
        for i in range(10):

            # Check if bitwise AND
            # of current digit and
            # previous digit is 0.
            if ((i & prev) == 0):
                val += countOfNumbers(digit + 1, i, n)

    # Return answer
    return val

# Driver code
if __name__ == '__main__':

    # Given Input
    N = 3

    # Function call
    print(countOfNumbers(1, 0, N))

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

  static int[,] dp = new int[100, 10];

  // Function to calculate count of 'N' digit
  // numbers such that bitwise AND of adjacent
  // digits is 0.
  static int countOfNumbers(int digit, int prev, int n)
  {

    // If digit = n + 1, a valid
    // n-digit number has been formed
    if (digit == n + 1)
    {
      return 1;
    }

    // If the state has
    // already been computed
    int val = dp[digit, prev];

    if (val != -1)
    {
      return val;
    }
    val = 0;

    // If current position is 1,
    // then any digit from [1-9] can be placed.
    // If n = 1, 0 can be also placed.
    if (digit == 1)
    {
      for(int i = (n == 1 ? 0 : 1); i <= 9; ++i)
      {
        val += countOfNumbers(digit + 1, i, n);
      }
    }

    // For remaining positions,
    // any digit from [0-9] can be placed
    // after checking the conditions.
    else
    {
      for(int i = 0; i <= 9; ++i)
      {

        // Check if bitwise AND
        // of current digit and
        // previous digit is 0.
        if ((i & prev) == 0)
        {
          val += countOfNumbers(digit + 1, i, n);
        }
      }
    }

    // Return answer
    return val;
  }

  // Driver code
  public static void Main(string[] args)
  {

    // Initializing dp array with -1.
    for(int i = 0; i < 100; i++)
    {
      for(int j = 0; j < 10; j++)
      {
        dp[i, j] = -1;
      }
    }

    // Given Input
    int N = 3;

    // Function call
    Console.WriteLine(countOfNumbers(1, 0, N));
  }
}

// This code is contributed by avijitmondal1998.
```

## java 描述语言

```
<script>
        // JavaScript program for the above approach

        // Function to calculate count of 'N' digit
        // numbers such that bitwise AND of adjacent
        // digits is 0.
        function countOfNumbers(digit, prev, n)
        {

            // If digit = n + 1, a valid
            // n-digit number has been formed
            if (digit == n + 1) {
                return 1;
            }

            // If the state has
            // already been computed
            let val = dp[digit][prev];
            if (val != -1) {
                return val;
            }
            val = 0;

            // If current position is 1,
            // then any digit from [1-9] can be placed.
            // If n = 1, 0 can be also placed.
            if (digit == 1) {
                for (let i = (n == 1 ? 0 : 1); i <= 9; ++i) {
                    val += countOfNumbers(digit + 1, i, n);
                }
            }

            // For remaining positions,
            // any digit from [0-9] can be placed
            // after checking the conditions.
            else {
                for (let i = 0; i <= 9; ++i) {

                    // Check if bitwise AND
                    // of current digit and
                    // previous digit is 0.
                    if ((i & prev) == 0) {
                        val += countOfNumbers(digit + 1, i, n);
                    }
                }
            }
            // Return answer
            return val;
        }

        // Initialize dp array with -1.
        let dp = Array(100).fill().map(() =>
            Array(10).fill(-1));

        // Given Input
        let N = 3;

        // Function call
        document.write(countOfNumbers(1, 0, N) + "<br>");

    // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
264
```

***时间复杂度:**T3】O(N×10<sup>2</sup>)
*T8】辅助空间:T10】O(N×10)**