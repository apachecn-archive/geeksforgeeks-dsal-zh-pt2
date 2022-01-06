# 替换通配符“？”形成的非递减数字串的计数

> 原文:[https://www . geeksforgeeks . org/通过替换通配符形成的非递减数字字符串的计数/](https://www.geeksforgeeks.org/count-of-non-decreasing-numeric-string-formed-by-replacing-wild-card/)

给定一根由数字和 T6 组成的 **N** 大小的[弦](https://www.geeksforgeeks.org/string-data-structure/)T2 S？，任务是找到形成的字符串数量，从而替换字符**'？'**任意位数，使得字符串的位数不变。

**示例:**

> **输入:**S =“1？？？2"
> **输出:** 4
> **解释:**
> 有效替换**后的字符串'？'**是 11112，11122，11222，12222。因此，此类字符串的计数为 1。
> 
> **输入:**S =“2？？43?4 "
> T3】输出: 0

**方法:**给定的问题可以通过替换**“？”来解决**使用[递归](https://www.geeksforgeeks.org/recursion/)处理所有可能的有效数字组合，并将[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)存储在 [**dp[]** 表](https://www.geeksforgeeks.org/tabulation-vs-memoization/)中。按照以下步骤解决给定的问题:

*   初始化一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)，比如说 **dp[][]** ，这样 **dp[i][j]** 将表示长度为**I**的有效字符串的可能数量，并且在两个**端点差为 j** 的数字之间。作为包含**的不同片段？**相互独立。因此，总计数将是每个细分市场所有可用选项的乘积。
*   将 **dp[][]** 初始化为-1。
*   将三个变量 **L** 声明为 **0** 、 **R** 声明为 **9** 、 **cnt** ，这样 **L** 表示该段的左极限， **R** 表示该段的右极限， **cnt** 表示相邻的**'？'**字符。
*   让总计数存储在变量中，说 **ans** 为 **1** 。
*   定义一个函数**求解**，递归计算 **dp** 节点[的值](https://www.geeksforgeeks.org/recursion/)。求解函数将采用两个参数 **(len，gap)** ，len 将表示连续**“？”**间隙将表示该段端点之间的差异，如下所示:
    *   针对每个可能的差距进行迭代，并使用**求解(len–1，gap–I)**重新计算答案。
    *   填充节点**DP【len】【gap】**后返回求解函数得到的答案。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)中的每个字符，并执行以下步骤:
    *   如果当前字符是**“？”**然后增加变量 **cnt** 。
    *   如果当前字符不是数字，将右限即 **R** 更改为当前字符，即**R = S[I]–‘0’**。
    *   将[递归函数](https://www.geeksforgeeks.org/recursive-functions/) **计算出的答案相乘求解(cnt，R–L)**。
*   完成上述步骤后，打印**和**的值作为形成的字符串的合成计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;
#define MAXN 100005

// Define the dp table globally
int dp[MAXN][10];

// Recursive function to calculate total
// number of valid non-decreasing strings
int solve(int len, int gap)
{
    // If already calculated state
    if (dp[len][gap] != -1) {
        return dp[len][gap];
    }

    // Base Case
    if (len == 0 || gap == 0) {
        return 1;
    }
    if (gap < 0) {
        return 0;
    }

    // Stores the total count of strings
    // formed
    int ans = 0;

    for (int i = 0; i <= gap; i++) {
        ans += solve(len - 1, gap - i);
    }

    // Fill the value in dp matrix
    return dp[len][gap] = ans;
}

// Function to find the total number of
// non-decreasing string formed by
// replacing the '?'
int countValidStrings(string S)
{
    // Initialize all value of dp
    // table with -1
    memset(dp, -1, sizeof(dp));

    int N = S.length();

    // Left and Right limits
    int L = 1, R = 9;

    int cnt = 0;
    int ans = 1;

    // Iterate through all the characters
    // of the string S
    for (int i = 0; i < N; i++) {

        if (S[i] != '?') {

            // Change R to the current
            // character
            R = S[i] - '0';

            // Call the recursive function
            ans *= solve(cnt, R - L);

            // Change L to R and R to 9
            L = R;
            R = 9;

            // Reinitialize the length
            // of ? to 0
            cnt = 0;
        }
        else {

            // Increment the length of
            // the segment
            cnt++;
        }
    }

    // Update the ans
    ans *= solve(cnt, R - L);

    // Return the total count
    return ans;
}

// Driver Code
int main()
{
    string S = "1???2";
    cout << countValidStrings(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

    static final int MAXN = 100005;

    // Define the dp table globally
    static final int dp[][] = new int[MAXN][10];

    // Recursive function to calculate total
    // number of valid non-decreasing strings
    static int solve(int len, int gap)
    {
        // If already calculated state
        if (dp[len][gap] != -1) {
            return dp[len][gap];
        }

        // Base Case
        if (len == 0 || gap == 0) {
            return 1;
        }
        if (gap < 0) {
            return 0;
        }

        // Stores the total count of strings
        // formed
        int ans = 0;

        for (int i = 0; i <= gap; i++) {
            ans += solve(len - 1, gap - i);
        }

        // Fill the value in dp matrix
        return dp[len][gap] = ans;
    }

    // Function to find the total number of
    // non-decreasing string formed by
    // replacing the '?'
    static int countValidStrings(String S)
    {
        // Initialize all value of dp
        // table with -1
        for (int i = 0; i < MAXN; i++) {
            for (int j = 0; j < 10; j++) {
                dp[i][j] = -1;
            }
        }

        int N = S.length();

        // Left and Right limits
        int L = 1, R = 9;

        int cnt = 0;
        int ans = 1;

        // Iterate through all the characters
        // of the string S
        for (int i = 0; i < N; i++) {

            if (S.charAt(i) != '?') {

                // Change R to the current
                // character
                R = S.charAt(i) - '0';

                // Call the recursive function
                ans *= solve(cnt, R - L);

                // Change L to R and R to 9
                L = R;
                R = 9;

                // Reinitialize the length
                // of ? to 0
                cnt = 0;
            }
            else {

                // Increment the length of
                // the segment
                cnt++;
            }
        }

        // Update the ans
        ans *= solve(cnt, R - L);

        // Return the total count
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String S = "1???2";
        System.out.println(countValidStrings(S));
    }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

MAXN = 100005

# Define the dp table globally
dp = [[-1 for x in range(10)] for y in range(MAXN)]

# Recursive function to calculate total
# number of valid non-decreasing strings
def solve(len, gap):

    # If already calculated state
    if (dp[len][gap] != -1):
        return dp[len][gap]

    # Base Case
    if (len == 0 or gap == 0):
        return 1

    if (gap < 0):
        return 0

    # Stores the total count of strings
    # formed
    ans = 0

    for i in range(gap + 1):
        ans += solve(len - 1, gap - i)

    # Fill the value in dp matrix
    dp[len][gap] = ans
    return dp[len][gap]

# Function to find the total number of
# non-decreasing string formed by
# replacing the '?'

def countValidStrings(S):

    # Initialize all value of dp
    # table with -1
    global dp

    N = len(S)

    # Left and Right limits
    L, R = 1, 9

    cnt = 0
    ans = 1

    # Iterate through all the characters
    # of the string S
    for i in range(N):

        if (S[i] != '?'):

            # Change R to the current
            # character
            R = ord(S[i]) - ord('0')

            # Call the recursive function
            ans *= solve(cnt, R - L)

            # Change L to R and R to 9
            L = R
            R = 9

            # Reinitialize the length
            # of ? to 0
            cnt = 0

        else:

            # Increment the length of
            # the segment
            cnt += 1

    # Update the ans
    ans *= solve(cnt, R - L)

    # Return the total count
    return ans

# Driver Code
if __name__ == "__main__":

    S = "1???2"
    print(countValidStrings(S))

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG
{

static int MAXN  = 100005;

// Define the dp table globally
static int [,]dp = new int[MAXN, 10];

// Recursive function to calculate total
// number of valid non-decreasing strings
static int solve(int len, int gap)
{
    // If already calculated state
    if (dp[len,gap] != -1) {
        return dp[len,gap];
    }

    // Base Case
    if (len == 0 || gap == 0) {
        return 1;
    }
    if (gap < 0) {
        return 0;
    }

    // Stores the total count of strings
    // formed
    int ans = 0;

    for (int i = 0; i <= gap; i++) {
        ans += solve(len - 1, gap - i);
    }

    // Fill the value in dp matrix
    return dp[len,gap] = ans;
}

// Function to find the total number of
// non-decreasing string formed by
// replacing the '?'
static int countValidStrings(string S)
{

    // Initialize all value of dp
    // table with -1
    for(int i = 0; i < MAXN; i++){
        for(int j = 0; j < 10; j++){
            dp[i, j] = -1;
        }
    }

    int N = S.Length;

    // Left and Right limits
    int L = 1, R = 9;

    int cnt = 0;
    int ans = 1;

    // Iterate through all the characters
    // of the string S
    for (int i = 0; i < N; i++) {

        if (S[i] != '?') {

            // Change R to the current
            // character
            R = (int)S[i] - 48;

            // Call the recursive function
            ans *= solve(cnt, R - L);

            // Change L to R and R to 9
            L = R;
            R = 9;

            // Reinitialize the length
            // of ? to 0
            cnt = 0;
        }
        else {

            // Increment the length of
            // the segment
            cnt++;
        }
    }

    // Update the ans
    ans *= solve(cnt, R - L);

    // Return the total count
    return ans;
}

// Driver Code
public static void Main()
{
    string S = "1???2";
    Console.Write(countValidStrings(S));
}
}

// This code is contributed by SURENDR_GANGWAR.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach
        let MAXN = 100005

        // Define the dp table globally
        let dp = new Array(MAXN).fill(new Array(10));

        // Recursive function to calculate total
        // number of valid non-decreasing strings
        function solve(len, gap)
        {

            // If already calculated state
            if (dp[len][gap] != -1) {
                return dp[len][gap];
            }

            // Base Case
            if (len == 0 || gap == 0) {
                return 1;
            }
            if (gap < 0) {
                return 0;
            }

            // Stores the total count of strings
            // formed
            let ans = 0;

            for (let i = 0; i <= gap; i++) {
                ans += solve(len - 1, gap - i);
            }

            // Fill the value in dp matrix
            return dp[len][gap] = ans;
        }

        // Function to find the total number of
        // non-decreasing string formed by
        // replacing the '?'
        function countValidStrings(S)
        {

            // Initialize all value of dp
            // table with -1
            for (let i = 0; i < dp.length; i++) {
                for (let j = 0; j < dp[i].length; j++) {
                    dp[i][j] = -1;
                }
            }

            let N = S.length;

            // Left and Right limits
            let L = 1, R = 9;

            let cnt = 0;
            let ans = 1;

            // Iterate through all the characters
            // of the string S
            for (let i = 0; i < N; i++) {

                if (S[i] != '?') {

                    // Change R to the current
                    // character
                    R = S.charCodeAt(i) - '0'.charCodeAt(0);

                    // Call the recursive function
                    ans *= solve(cnt, R - L);

                    // Change L to R and R to 9
                    L = R;
                    R = 9;

                    // Reinitialize the length
                    // of ? to 0
                    cnt = 0;
                }
                else {

                    // Increment the length of
                    // the segment
                    cnt++;
                }
            }

            // Update the ans
            ans *= solve(cnt, R - L);

            // Return the total count
            return ans;
        }

        // Driver Code
        let S = "1???2";
        document.write(countValidStrings(S));

     // This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N * 10)*
T5**辅助空间:** O(N*10)