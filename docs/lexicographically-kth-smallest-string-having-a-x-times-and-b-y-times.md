# 字典上最小的字符串，具有“a”X 次和“b”Y 次

> 原文:[https://www . geeksforgeeks . org/按字典顺序-kth-最小-string-having-a-x-times-和-b-y-times/](https://www.geeksforgeeks.org/lexicographically-kth-smallest-string-having-a-x-times-and-b-y-times/)

给定三个非负整数， **X** 、 **Y** 和 **K** ，的任务是找到 **Kth** 最小的[词典字符串](https://www.geeksforgeeks.org/lexicographic-rank-of-a-string/)，该字符串具有 **X** 个字符**“a”**和 **Y** 个字符**“b”**的出现。

**示例:**

> **输入:** X = 2，Y = 3，K = 3
> **输出:** abbab
> **解释:**
> 首个词典最小字符串=“aabbb”。
> 第二个字典最小字符串=“ababb”。
> 第三个字典最小字符串=“abbab”。
> 
> **输入:** X = 4，Y = 3，K = 4
> T3】输出:aabbba

**简单方法:**最简单的方法是生成字符串 **X** 出现字符 **'a'** 和 **Y** 出现字符 **'b'** 的[所有不同排列](https://www.geeksforgeeks.org/distinct-permutations-string-set-2/)。然后首先[按照字典顺序对输出字符串数组进行排序](https://www.geeksforgeeks.org/sort-an-array-of-strings-lexicographically-based-on-prefix/)并打印 **Kth** 索引[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/)。

***时间复杂度:** O(N*N！)，其中 N 为(X + Y)*
***辅助空间:** O(N！)*

**有效方法:**该问题具有[重叠子问题属性](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和[最优子结构属性](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)。所以这个问题可以用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)来解决。像其他典型的[动态规划](https://www.geeksforgeeks.org/dynamic-programming/) (DP)问题一样，通过构造一个存储子问题结果的临时数组，可以避免相同子问题的重新计算。按照下面的步骤来解决这个问题。

*   初始化一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)、 **dp[][]** ，其中 **dp[i][j]** 表示包含 **i** 个数的 **a、**和 **j** 个数的**b**的字符串个数。
*   [使用变量 **i** : 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，X】**中迭代
    *   [使用变量 **j:** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，Y】**中迭代
        *   如果 **i** 大于 **0，**则将 **dp[i][j]** 更新为 **dp[i][j] + dp[i-1][j]** 。
        *   如果 **j** 大于 **0** ，则将 **dp[i][j]** 更新为 **dp[i][j] + dp[i][j-1]** 。
*   现在，[通过调用函数 **kthString(int X，int Y，int K)** ，递归地](https://www.geeksforgeeks.org/recursion/)找到 **Kth** 字典序最小字符串。
*   处理基本案例:
    *   如果只有**‘a’**个字符，则返回一个包含所有**‘a’**个字符的字符串。
    *   如果只有**【b】**个字符，那么返回一个包含所有**【b】**个字符的字符串。
*   如果有大于或等于 **K** 的以**‘a’**开头的字符串，则返回**“a”+kthString(X-1，Y，K)** 。
*   否则结果字符串的第一个字符是**‘b’**，返回**“b”+kthString(X，Y-1，K–DP[X-1][Y])**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

const int MAX = 30;

// Function to fill dp array
void findNumString(int X, int Y, int dp[][MAX])
{

    // Initialize all the entries with 0
    for (int i = 0; i < MAX; i++) {
        for (int j = 0; j < MAX; j++) {
            dp[i][j] = 0;
        }
    }

    // Update dp[0][0] to 1
    dp[0][0] = 1;

    // Traverse the dp array
    for (int i = 0; i <= X; ++i) {
        for (int j = 0; j <= Y; ++j) {

            // Update the value of dp[i][j]
            if (i > 0) {
                dp[i][j] += dp[i - 1][j];
            }

            if (j > 0) {
                dp[i][j] += dp[i][j - 1];
            }
        }
    }
}

// Recursive function to find the Kth
// lexicographical smallest string
string kthString(int X, int Y, int K, int dp[][MAX])
{
    // Handle the base cases
    if (X == 0) {
        return string(Y, 'b');
    }
    if (Y == 0) {
        return string(X, 'a');
    }

    // If there are more than or equal
    // to K strings which start with a,
    // then the first character is 'a'
    if (K <= dp[X - 1][Y]) {
        return string("a") + kthString(X - 1, Y, K, dp);
    }

    // Otherwise the first character
    // of the resultant string is 'b'
    else {
        return string("b")
               + kthString(X, Y - 1,
                           K - dp[X - 1][Y], dp);
    }
}

// Function to find the Kth
// lexicographical smallest string
void kthStringUtil(int X, int Y, int K)
{
    int dp[MAX][MAX];

    // Function call to fill the dp array
    findNumString(X, Y, dp);

    // Print the resultant string
    cout << kthString(X, Y, K, dp) << '\n';
}

// Driver Code
int main()
{

    // Given Input
    int X = 4;
    int Y = 3;
    int K = 4;

    // Function Call
    kthStringUtil(X, Y, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG
{

static int MAX = 30;

// Function to fill dp array
static void findNumString(int X, int Y, int dp[][])
{

    // Initialize all the entries with 0
    for (int i = 0; i < MAX; i++) {
        for (int j = 0; j < MAX; j++) {
            dp[i][j] = 0;
        }
    }

    // Update dp[0][0] to 1
    dp[0][0] = 1;

    // Traverse the dp array
    for (int i = 0; i <= X; ++i) {
        for (int j = 0; j <= Y; ++j) {

            // Update the value of dp[i][j]
            if (i > 0) {
                dp[i][j] += dp[i - 1][j];
            }

            if (j > 0) {
                dp[i][j] += dp[i][j - 1];
            }
        }
    }
}

// Recursive function to find the Kth
// lexicographical smallest string
static String kthString(int X, int Y, int K, int dp[][])
{
    // Handle the base cases
    String x1 = "";
    String y1 = "";

    for (int i=0;i<Y;i++){
        x1 += 'b';
    }
    for (int i=0;i<X;i++){
        y1 += 'a';
    }
    if (X == 0)
        return x1;
    if (Y == 0)
        return y1;

    // If there are more than or equal
    // to K strings which start with a,
    // then the first character is 'a'
    if (K <= dp[X - 1][Y]) {
        return ("a" + kthString(X - 1, Y, K, dp));
    }

    // Otherwise the first character
    // of the resultant string is 'b'
    else {
        return ("b"  + kthString(X, Y - 1, K - dp[X - 1][Y], dp));
    }
}

// Function to find the Kth
// lexicographical smallest string
static void kthStringUtil(int X, int Y, int K)
{
    int dp[][] = new int [MAX][MAX];

    // Function call to fill the dp array
    findNumString(X, Y, dp);

    // Print the resultant string
    System.out.println(kthString(X, Y, K, dp));
}

// Driver Code
public static void main(String args[])
{

    // Given Input
    int X = 4;
    int Y = 3;
    int K = 4;

    // Function Call
    kthStringUtil(X, Y, K);
    }
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python3 program for the above approach
from typing import Mapping

MAX = 30

# Function to fill dp array
def findNumString(X, Y, dp):

    # Initialize all the entries with 0
    for i in range(0, MAX):
        for j in range(0, MAX):
            dp[i][j] = 0

    # Update dp[0][0] to 1
    dp[0][0] = 1

    # Traverse the dp array
    for i in range(0, X + 1):
        for j in range(0, Y + 1):

            # Update the value of dp[i][j]
            if (i > 0):
                dp[i][j] += dp[i - 1][j]

            if (j > 0):
                dp[i][j] += dp[i][j - 1]

# Recursive function to find the Kth
# lexicographical smallest string
def kthString(X, Y, K, dp):

    # Handle the base cases
    x1 = ""
    y1 = ""

    for i in range(0, Y):
        x1 += 'b'
    for i in range(0, X):
        y1 += 'a'

    if (X == 0):
        return x1
    if (Y == 0):
        return y1

    # If there are more than or equal
    # to K strings which start with a,
    # then the first character is 'a'
    if (K <= dp[X - 1][Y]):
        return "a" + kthString(X - 1, Y, K, dp)

    # Otherwise the first character
    # of the resultant string is 'b'
    else:
        return "b" + kthString(X, Y - 1,
                           K - dp[X - 1][Y], dp)

# Function to find the Kth
# lexicographical smallest string
def kthStringUtil(X, Y, K):

    dp = [[0 for i in range(MAX)]
             for col in range(MAX)]

    # Function call to fill the dp array
    findNumString(X, Y, dp)

    # Print the resultant
    print(kthString(X, Y, K, dp))

# Driver Code

# Given Input
X = 4
Y = 3
K = 4

# Function Call
kthStringUtil(X, Y, K)

# This code is contributed by amreshkumar3
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static int MAX = 30;

// Function to fill dp array
static void findNumString(int X, int Y, int[,] dp)
{

    // Initialize all the entries with 0
    for (int i = 0; i < MAX; i++) {
        for (int j = 0; j < MAX; j++) {
            dp[i, j] = 0;
        }
    }

    // Update dp[0][0] to 1
    dp[0, 0] = 1;

    // Traverse the dp array
    for (int i = 0; i <= X; ++i) {
        for (int j = 0; j <= Y; ++j) {

            // Update the value of dp[i][j]
            if (i > 0) {
                dp[i, j] += dp[i - 1, j];
            }

            if (j > 0) {
                dp[i, j] += dp[i, j - 1];
            }
        }
    }
}

// Recursive function to find the Kth
// lexicographical smallest string
static string kthString(int X, int Y, int K, int[,] dp)
{
    // Handle the base cases
    string x1 = "";
    string y1 = "";

    for (int i=0;i<Y;i++){
        x1 += 'b';
    }
    for (int i=0;i<X;i++){
        y1 += 'a';
    }
    if (X == 0)
        return x1;
    if (Y == 0)
        return y1;

    // If there are more than or equal
    // to K strings which start with a,
    // then the first character is 'a'
    if (K <= dp[X - 1, Y]) {
        return ("a" + kthString(X - 1, Y, K, dp));
    }

    // Otherwise the first character
    // of the resultant string is 'b'
    else {
        return ("b"  + kthString(X, Y - 1, K - dp[X - 1, Y], dp));
    }
}

// Function to find the Kth
// lexicographical smallest string
static void kthStringUtil(int X, int Y, int K)
{
    int[,] dp = new int [MAX, MAX];

    // Function call to fill the dp array
    findNumString(X, Y, dp);

    // Print the resultant string
    Console.WriteLine(kthString(X, Y, K, dp));
}

// Driver code
static void Main()
{
    // Given Input
    int X = 4;
    int Y = 3;
    int K = 4;

    // Function Call
    kthStringUtil(X, Y, K);
}
}

// This code is contributed by code_hunt.
```

**Output:** 

```
aaabbba
```

***时间复杂度:**O(X * Y)*
T5】**辅助空间:** O(X*Y)

**高效方法:**通过迭代实现 **KthString** 函数，可以进一步优化上述方法。按照以下步骤解决此问题:

*   声明一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)、 **dp** ，其中**DP【I】【j】**表示包含 **i** 数的 **a、**和 **j** 数的**b**的字符串数。
*   [使用变量 **i** : 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，X】**中迭代
    *   [使用变量 **j:** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，Y】**中迭代
        *   如果 **i** 大于 **0，**则将 **dp[i][j]** 更新为 **dp[i][j] + dp[i-1][j]。**
        *   如果 **j** 大于 **0** ，则更新 **dp[i][j]** 为 **dp[i][j] + dp[i][j-1]。**
*   现在，迭代寻找第 **Kth** 个字典最小的字符串。
*   [穿越](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)而 **X** 大于**0****Y**大于 **0** :
    *   如果有大于或等于 **K** 的以**‘a’**开头的字符串，则打印**‘a’**，并以 **1** 递减 **X** 。
    *   否则，结果字符串的第一个字符是**【b】**，打印**【b】**，并以 **1** 递减 **Y** 。
*   如果只有' **a'** 字符，则打印一串所有' **a** 字符。
*   如果只有“ **b** ”字符，则打印一串所有的“ **b** ”字符。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

const int MAX = 30;

// Function to fill dp array
void findNumString(int X, int Y, int dp[][MAX])
{

    // Initialize all the entries with 0
    for (int i = 0; i < MAX; i++) {
        for (int j = 0; j < MAX; j++) {
            dp[i][j] = 0;
        }
    }

    // Update dp[0][0] to 1
    dp[0][0] = 1;

    // Traverse the dp array
    for (int i = 0; i <= X; ++i) {
        for (int j = 0; j <= Y; ++j) {

            // Update the value of dp[i][j]
            if (i > 0) {
                dp[i][j] += dp[i - 1][j];
            }

            if (j > 0) {
                dp[i][j] += dp[i][j - 1];
            }
        }
    }
}

// Iterative function to find the Kth
// lexicographical smallest string
void kthString(int X, int Y, int K, int dp[][MAX])
{

    while (X > 0 and Y > 0) {

        // If there are more than or
        // equal to K strings which start
        // with a, then print 'a'
        if (K <= dp[X - 1][Y]) {
            cout << 'a';
            X -= 1;
        }

        // Otherwise the first character
        // of the resultant string is b
        else {
            K -= dp[X - 1][Y];
            cout << 'b';
            Y -= 1;
        }
    }

    // If there are only 'a' characters
    // present then print a string of
    // all 'a' characters
    cout << string(X, 'a');

    // If there are only 'b' characters
    // present then print a string of
    // all 'b' characters
    cout << string(Y, 'b');
    cout << '\n';
}

// Function to find the Kth
// lexicographical smallest string
void kthStringUtil(int X, int Y, int K)
{
    int dp[MAX][MAX];

    // Function call to fill the dp array
    findNumString(X, Y, dp);

    // Function call to find the
    // required string
    kthString(X, Y, K, dp);
}

// Driver Code
int main()
{

    // Given Input
    int X = 4;
    int Y = 3;
    int K = 4;

    // Function Call
    kthStringUtil(X, Y, K);

    return 0;
}
```

**Output:** 

```
aaabbba
```

***时间复杂度:**O(X * Y)*
T5】**辅助空间:** O(X*Y)