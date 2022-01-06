# 严格递增的 N 位数计数

> 原文:[https://www . geeksforgeeks . org/严格递增的 n 位数计数/](https://www.geeksforgeeks.org/count-of-strictly-increasing-n-digit-numbers/)

给定一个正整数 **N** ，任务是找到 **N 位数字**的个数，使得每个数字都小于其相邻的数字。

**示例:**

> **输入:** N = 1
> **输出:** 10
> **说明:**从【0–9】开始的所有数字都满足条件，因为只有一个数字。
> 
> **输入:**N = 3
> T3】输出: 525

**天真方法:**解决给定问题的最简单方法是迭代所有可能的 **N** 位数字，对于每个这样的数字，检查其所有数字是否满足给定标准。如果发现是真的，那么数一数这些数字。检查所有数字后，打印获得的总计数。

***时间复杂度:**O(10<sup>N</sup>* N)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化，因为它有[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和[最优子结构。](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)子问题可以使用[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)存储在 **dp[][][]表**中，其中 **dp[i][prev][sign]** 存储从 **i <sup>th</sup>** 位置直到结束的结果，当选择前一个数字时， **prev** 和变量**符号**用于指示当前数字是否必须小于或大于前一个数字按照以下步骤解决问题:

*   定义一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/)，比如说**数(数字，前一个，符号)**有三个参数:数字，符号和前一个。
    *   检查[基本情况](https://www.geeksforgeeks.org/recursive-functions/)，即如果 **i** 的值等于 **N** ，则返回 **1** 作为有效的 **N** 位数。
    *   初始化一个变量，比如说 **val = 0** ，来存储所有可能的 N 位数计数。
    *   如果 **i** 为 **0** ，则可以放置来自**【1–9】**的任意数字，如果 **N = 1** ，则也可以放置 **0** 。
    *   如果 **i** 是 **1** ，那么可以放置来自**【0–9】**的任意数字，使得当前数字是**而不是**等于前一个数字。
    *   如果**符号**的值为 **1** ，则放置**当前的**数字，使其比之前的**数字少**，并将符号更改为 **0** 进行下一次递归调用。
    *   如果**符号**的值为 **0** ，则放置**当前的**数字，使其比前一个**数字多**，并将符号更改为 **1** 进行下一次递归调用。****
    *   ****进行有效放置后，**递归调用**数**函数进行索引**(数字+ 1)** 。******
    *   **返回作为每次当前[递归调用](https://www.geeksforgeeks.org/recursion/)的结果的所有可能的有效数字位置的总和。**
*   **完成上述步骤后，打印函数**返回的数值作为结果计数。****

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Declaration of dp table
int dp[100][10][2];

// Function to find the count of all N
// digit numbers such that all the digit
// is less than its adjacent digits
int solve(int i, int n, int prev, bool sign)
{
    // Base Case:
    // If i = n, then return 1 as valid
    // number has been formed
    if (i == n) {
        return 1;
    }

    int& val = dp[i][prev][sign];

    // If the state has already been
    // computed, then return it
    if (val != -1)
        return val;

    // Stores the total count of ways
    // for the current recursive call
    val = 0;

    // If i = 0, any digit from [1-9]
    // can  be placed and also if N = 1
    //, then 0 can also be placed
    if (i == 0) {
        for (int digit = (n == 1 ? 0 : 1);
             digit <= 9;
             ++digit) {
            val += solve(i + 1, n,
                         digit, sign);
        }
    }

    // If i = 1, any digit from [0-9]
    // can be placed such that digit
    // is not equal to previous digit
    else if (i == 1) {
        for (int digit = 0; digit <= 9;
             ++digit) {

            // If the current digit is
            // not same as the prev
            if (digit != prev) {
                val += solve(i + 1, n, digit,
                             (digit > prev));
            }
        }
    }

    else {

        // Place the current digit such
        // that it is less than the
        // previous digit
        if (sign == 1) {
            for (int digit = prev - 1;
                 digit >= 0;
                 --digit) {

                val += solve(i + 1, n,
                             digit, 0);
            }
        }

        // Place current digit such
        // that it is more than the
        // previous digit
        else {
            for (int digit = prev + 1;
                 digit <= 9;
                 ++digit) {

                val += solve(i + 1, n,
                             digit, 1);
            }
        }
    }

    // Return the resultant total count
    return val;
}

// Function to find all N-digit numbers
// satisfying the given criteria
void countNdigitNumber(int N)
{

    // Initialize an array dp[] with
    // all elements as -1
    memset(dp, -1, sizeof dp);

    // Function call to count all
    // possible ways
    cout << solve(0, N, 0, 0);
}

// Driver Code
int main()
{
    int N = 3;
    countNdigitNumber(N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;
public class MyClass
{

// Declaration of dp table
static int[][][] dp = new int[100][10][2];

// Function to find the count of all N
// digit numbers such that all the digit
// is less than its adjacent digits
static int solve(int i, int n, int prev, int sign)
{

    // Base Case:
    // If i = n, then return 1 as valid
    // number has been formed
    if (i == n) {
        return 1;
    }

    int val = dp[i][prev][sign];

    // If the state has already been
    // computed, then return it
    if (val != -1)
        return val;

    // Stores the total count of ways
    // for the current recursive call
    val = 0;

    // If i = 0, any digit from [1-9]
    // can  be placed and also if N = 1
    //, then 0 can also be placed
    if (i == 0) {
        for (int digit = (n == 1 ? 0 : 1);
             digit <= 9;
             ++digit) {
            val += solve(i + 1, n,
                         digit, sign);
        }
    }

    // If i = 1, any digit from [0-9]
    // can be placed such that digit
    // is not equal to previous digit
    else if (i == 1) {
        for (int digit = 0; digit <= 9;
             ++digit) {

            // If the current digit is
            // not same as the prev
            if (digit != prev) {
                val += solve(i + 1, n, digit,((digit > prev)?1:0));
            }
        }
    }

    else {

        // Place the current digit such
        // that it is less than the
        // previous digit
        if (sign == 1) {
            for (int digit = prev - 1;
                 digit >= 0;
                 --digit) {

                val += solve(i + 1, n,
                             digit, 0);
            }
        }

        // Place current digit such
        // that it is more than the
        // previous digit
        else {
            for (int digit = prev + 1;
                 digit <= 9;
                 ++digit) {

                val += solve(i + 1, n,
                             digit, 1);
            }
        }
    }

    // Return the resultant total count
    return val;
}

// Function to find all N-digit numbers
// satisfying the given criteria
static void countNdigitNumber(int N)
{

    // Initialize an array dp[] with
    // all elements as -1
    for (int[][] row : dp)
    {
        for (int[] rowColumn : row)
        {
            Arrays.fill(rowColumn, -1);
        }
    }
    // Function call to count all
    // possible ways
     System.out.println(solve(0, N, 0, 0));
}

// Driver Code
 public static void main(String args[])
{
    int N = 3;
    countNdigitNumber(N);
}
}

// This code is contributed by SoumikMondal
```

## **蟒蛇 3**

```
# python 3 program for the above approach

# Declaration of dp table
dp = [[[-1 for x in range(2)] for y in range(10)] for z in range(100)]

# Function to find the count of all N
# digit numbers such that all the digit
# is less than its adjacent digits
def solve(i,  n,  prev,  sign):

    # Base Case:
    # If i = n, then return 1 as valid
    # number has been formed
    if (i == n):
        return 1

    val = dp[i][prev][sign]

    # If the state has already been
    # computed, then return it
    if (val != -1):
        return val

    # Stores the total count of ways
    # for the current recursive call
    val = 0

    # If i = 0, any digit from [1-9]
    # can  be placed and also if N = 1
    # , then 0 can also be placed
    if (i == 0):
        if (n == 1):
            digit = 0
        else:
            digit = 1
        while digit <= 9:

            val += solve(i + 1, n,
                         digit, sign)
            digit += 1

    # If i = 1, any digit from [0-9]
    # can be placed such that digit
    # is not equal to previous digit
    elif (i == 1):
        for digit in range(10):

            # If the current digit is
            # not same as the prev
            if (digit != prev):
                val += solve(i + 1, n, digit,
                             (digit > prev))

    else:

        # Place the current digit such
        # that it is less than the
        # previous digit
        if (sign == 1):
            for digit in range(prev - 1,
                               -1, -1):

                val += solve(i + 1, n,
                             digit, 0)

        # Place current digit such
        # that it is more than the
        # previous digit
        else:
            for digit in range(prev + 1, 10):

                val += solve(i + 1, n,
                             digit, 1)

    # Return the resultant total count
    return val

# Function to find all N-digit numbers
# satisfying the given criteria
def countNdigitNumber(N):

    # Initialize an array dp[] with
    # all elements as -1

    # Function call to count all
    # possible ways
    print(solve(0, N, 0, 0))

# Driver Code
if __name__ == "__main__":

    N = 3
    countNdigitNumber(N)

    # This code is contributed by ukasp.
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class MyClass
{

// Declaration of dp table
static int[,,] dp = new int[100,10,2];

// Function to find the count of all N
// digit numbers such that all the digit
// is less than its adjacent digits
static int solve(int i, int n, int prev, int sign)
{

    // Base Case:
    // If i = n, then return 1 as valid
    // number has been formed
    if (i == n) {
        return 1;
    }

    int val = dp[i,prev,sign];

    // If the state has already been
    // computed, then return it
    if (val != -1)
        return val;

    // Stores the total count of ways
    // for the current recursive call
    val = 0;

    // If i = 0, any digit from [1-9]
    // can  be placed and also if N = 1
    //, then 0 can also be placed
    if (i == 0) {
        for (int digit = (n == 1 ? 0 : 1);
             digit <= 9;
             ++digit) {
            val += solve(i + 1, n,
                         digit, sign);
        }
    }

    // If i = 1, any digit from [0-9]
    // can be placed such that digit
    // is not equal to previous digit
    else if (i == 1) {
        for (int digit = 0; digit <= 9;
             ++digit) {

            // If the current digit is
            // not same as the prev
            if (digit != prev) {
                val += solve(i + 1, n, digit,((digit > prev)?1:0));
            }
        }
    }

    else {

        // Place the current digit such
        // that it is less than the
        // previous digit
        if (sign == 1) {
            for (int digit = prev - 1;
                 digit >= 0;
                 --digit) {

                val += solve(i + 1, n,
                             digit, 0);
            }
        }

        // Place current digit such
        // that it is more than the
        // previous digit
        else {
            for (int digit = prev + 1;
                 digit <= 9;
                 ++digit) {

                val += solve(i + 1, n,
                             digit, 1);
            }
        }
    }

    // Return the resultant total count
    return val;
}

// Function to find all N-digit numbers
// satisfying the given criteria
static void countNdigitNumber(int N)
{

    // Initialize an array []dp with
    // all elements as -1
    for(int i = 0;i<100;i++)
{
    for (int j = 0; j < 10; j++) {
        for (int k = 0; k < 2; k++)
            dp[i,j,k] = -1;
    }
}
    // Function call to count all
    // possible ways
     Console.WriteLine(solve(0, N, 0, 0));
}

// Driver Code
 public static void Main(String []args)
{
    int N = 3;
    countNdigitNumber(N);
}
}

// This code is contributed by 29AjayKumar
```

## **java 描述语言**

```
<script>
// javascript program for the above approach

    // Declaration of dp table
     var dp = Array(100).fill().map(()=>Array(10).fill().map(()=>Array(2).fill(-1)));

    // Function to find the count of all N
    // digit numbers such that all the digit
    // is less than its adjacent digits
    function solve(i , n , prev , sign) {

        // Base Case:
        // If i = n, then return 1 as valid
        // number has been formed
        if (i == n) {
            return 1;
        }

        var val = dp[i][prev][sign];

        // If the state has already been
        // computed, then return it
        if (val != -1)
            return val;

        // Stores the total count of ways
        // for the current recursive call
        val = 0;

        // If i = 0, any digit from [1-9]
        // can be placed and also if N = 1
        // , then 0 can also be placed
        if (i == 0) {
            for (var digit = (n == 1 ? 0 : 1); digit <= 9; ++digit) {
                val += solve(i + 1, n, digit, sign);
            }
        }

        // If i = 1, any digit from [0-9]
        // can be placed such that digit
        // is not equal to previous digit
        else if (i == 1) {
            for (var digit = 0; digit <= 9; ++digit) {

                // If the current digit is
                // not same as the prev
                if (digit != prev) {
                    val += solve(i + 1, n, digit, ((digit > prev) ? 1 : 0));
                }
            }
        }

        else {

            // Place the current digit such
            // that it is less than the
            // previous digit
            if (sign == 1) {
                for (var digit = prev - 1; digit >= 0; --digit) {

                    val += solve(i + 1, n, digit, 0);
                }
            }

            // Place current digit such
            // that it is more than the
            // previous digit
            else {
                for (var digit = prev + 1; digit <= 9; ++digit) {

                    val += solve(i + 1, n, digit, 1);
                }
            }
        }

        // Return the resultant total count
        return val;
    }

    // Function to find all N-digit numbers
    // satisfying the given criteria
    function countNdigitNumber(N) {

        // Function call to count all
        // possible ways
        document.write(solve(0, N, 0, 0));
    }

    // Driver Code

        var N = 3;
        countNdigitNumber(N);

// This code is contributed by gauravrajput1
</script>
```

****Output:** 

```
525
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(N)**