# 尽量减少要添加或删除的字符数，使同一子串的字符串重复

> 原文:[https://www . geesforgeks . org/最小化要添加或删除的字符数，以使相同子字符串的字符串重复/](https://www.geeksforgeeks.org/minimize-the-count-of-characters-to-be-added-or-removed-to-make-string-repetition-of-same-substring/)

给定由 **N** 字符组成的[字符串](https://www.geeksforgeeks.org/string-class-in-java/) **S** ，任务是通过执行最少数量的以下操作来修改字符串 **S** ，使得修改后的字符串 **S** 是其一半的串联。

*   在字符串的任何索引处插入任何新字符。
*   从字符串 **S** 中删除任何字符。
*   用字符串 **S** 中的任何其他字符替换任何字符。

**示例:**

> **输入:**S =“aabbaabb”
> T3】输出: 0
> **解释:**
> 给定字符串 S =“aabbaabb”的形式为 A = B + B，其中 B =“AABB”。因此，所需的最小操作数为 0。
> 
> **输入:**S = " ABA "
> T3】输出: 1

**方法:**给定的问题可以通过[遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)来解决，并在每个可能的索引处执行给定的操作[递归](https://www.geeksforgeeks.org/recursion/)，然后在遍历字符串后找到所需的最小操作。按照以下步骤解决给定的问题:

*   初始化一个变量，说 **minSteps** 为 [**INT_MAX**](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) ，存储所需的最小操作数。
*   [使用变量 **i** 遍历给定的字符串 **S**](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) ，并执行以下步骤:
    *   找到子字符串 **S1** 作为**S【0，I】**和 **S2** 作为**S【I，N】**。
    *   现在找到将 **S1** 转换为 **S2** 所需的最小步骤数，并使用本文[和](https://www.geeksforgeeks.org/edit-distance-dp-5/)中讨论的方法将其存储在变量**计数**中，因为操作与本文[和](https://www.geeksforgeeks.org/edit-distance-dp-5/)相似。
    *   将**分步骤**的值更新为**分步骤**和**计数**的最小值。
*   完成上述步骤后，打印**分步骤**的值作为最小操作结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum of
// the three numbers
int getMin(int x, int y, int z)
{
    return min(min(x, y), z);
}

// Function to find the minimum number
// operations required to convert string
// str1 to str2 using the operations
int editDistance(string str1, string str2,
                 int m, int n)
{
    // Stores the results of subproblems
    int dp[m + 1][n + 1];

    // Fill dp[][] in bottom up manner
    for (int i = 0; i <= m; i++) {
        for (int j = 0; j <= n; j++) {

            // If str1 is empty, then
            // insert all characters
            // of string str2
            if (i == 0)

                // Minimum operations
                // is j
                dp[i][j] = j;

            // If str2 is empty, then
            // remove all characters
            // of string str2
            else if (j == 0)

                // Minimum operations
                // is i
                dp[i][j] = i;

            // If the last characters
            // are same, then ignore
            // last character
            else if (str1[i - 1] == str2[j - 1])
                dp[i][j] = dp[i - 1][j - 1];

            // If the last character
            // is different, then
            // find the minimum
            else {

                // Perform one of the
                // insert, remove and
                // the replace
                dp[i][j] = 1
                           + getMin(
                                 dp[i][j - 1],
                                 dp[i - 1][j],
                                 dp[i - 1][j - 1]);
            }
        }
    }

    // Return the minimum number of
    // steps required
    return dp[m][n];
}

// Function to find the minimum number
// of steps to modify the string such
// that first half and second half
// becomes the same
void minimumSteps(string& S, int N)
{
    // Stores the minimum number of
    // operations required
    int ans = INT_MAX;

    // Traverse the given string S
    for (int i = 1; i < N; i++) {

        string S1 = S.substr(0, i);
        string S2 = S.substr(i);

        // Find the minimum operations
        int count = editDistance(
            S1, S2, S1.length(),
            S2.length());

        // Update the ans
        ans = min(ans, count);
    }

    // Print the result
    cout << ans << '\n';
}

// Driver Code
int main()
{
    string S = "aabb";
    int N = S.length();
    minimumSteps(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

// Function to find the minimum of
// the three numbers
static int getMin(int x, int y, int z)
{
    return Math.min(Math.min(x, y), z);
}

// Function to find the minimum number
// operations required to convert String
// str1 to str2 using the operations
static int editDistance(String str1, String str2,
                 int m, int n)
{

    // Stores the results of subproblems
    int [][]dp = new int[m + 1][n + 1];

    // Fill dp[][] in bottom up manner
    for (int i = 0; i <= m; i++)
    {
        for (int j = 0; j <= n; j++)
        {

            // If str1 is empty, then
            // insert all characters
            // of String str2
            if (i == 0)

                // Minimum operations
                // is j
                dp[i][j] = j;

            // If str2 is empty, then
            // remove all characters
            // of String str2
            else if (j == 0)

                // Minimum operations
                // is i
                dp[i][j] = i;

            // If the last characters
            // are same, then ignore
            // last character
            else if (str1.charAt(i - 1) == str2.charAt(j - 1))
                dp[i][j] = dp[i - 1][j - 1];

            // If the last character
            // is different, then
            // find the minimum
            else {

                // Perform one of the
                // insert, remove and
                // the replace
                dp[i][j] = 1
                           + getMin(
                                 dp[i][j - 1],
                                 dp[i - 1][j],
                                 dp[i - 1][j - 1]);
            }
        }
    }

    // Return the minimum number of
    // steps required
    return dp[m][n];
}

// Function to find the minimum number
// of steps to modify the String such
// that first half and second half
// becomes the same
static void minimumSteps(String S, int N)
{

    // Stores the minimum number of
    // operations required
    int ans = Integer.MAX_VALUE;

    // Traverse the given String S
    for (int i = 1; i < N; i++) {

        String S1 = S.substring(0, i);
        String S2 = S.substring(i);

        // Find the minimum operations
        int count = editDistance(
            S1, S2, S1.length(),
            S2.length());

        // Update the ans
        ans = Math.min(ans, count);
    }

    // Print the result
    System.out.print(ans);
}

// Driver Code
public static void main(String[] args)
{
    String S = "aabb";
    int N = S.length();
    minimumSteps(S, N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program for the above approach;

# Function to find the minimum of
# the three numbers
def getMin(x, y, z):
    return min(min(x, y), z)

# Function to find the minimum number
# operations required to convert string
# str1 to str2 using the operations
def editDistance(str1, str2, m, n):

    # Stores the results of subproblems
    dp = [[0 for i in range(n + 1)] for j in range(m + 1)]

    # Fill dp[][] in bottom up manner
    for i in range(0, m + 1):
        for j in range(0, n + 1):

            # If str1 is empty, then
            # insert all characters
            # of string str2
            if (i == 0):

                # Minimum operations
                # is j
                dp[i][j] = j

            # If str2 is empty, then
            # remove all characters
            # of string str2
            elif (j == 0):

                # Minimum operations
                # is i
                dp[i][j] = i

            # If the last characters
            # are same, then ignore
            # last character
            elif (str1[i - 1] == str2[j - 1]):
                dp[i][j] = dp[i - 1][j - 1]

            # If the last character
            # is different, then
            # find the minimum
            else:

                # Perform one of the
                # insert, remove and
                # the replace
                dp[i][j] = 1 + getMin( dp[i][j - 1], dp[i - 1][j], dp[i - 1][j - 1])

    # Return the minimum number of
    # steps required
    return dp[m][n]

# Function to find the minimum number
# of steps to modify the string such
# that first half and second half
# becomes the same
def minimumSteps(S, N):
    # Stores the minimum number of
    # operations required
    ans = 10**10

    # Traverse the given string S
    for i in range(1, N):
        S1 = S[:i]
        S2 = S[i:]

        # Find the minimum operations
        count = editDistance(S1, S2, len(S1), len(S2))

        # Update the ans
        ans = min(ans, count)

    # Print the result
    print(ans)

# Driver Code
S = "aabb"
N = len(S)
minimumSteps(S, N)

# This code is contributed by gfgking
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

// Function to find the minimum of
// the three numbers
static int getMin(int x, int y, int z)
{
    return Math.Min(Math.Min(x, y), z);
}

// Function to find the minimum number
// operations required to convert String
// str1 to str2 using the operations
static int editDistance(string str1, string str2,
                 int m, int n)
{

    // Stores the results of subproblems
    int [,]dp = new int[m + 1,n + 1];

    // Fill dp[,] in bottom up manner
    for (int i = 0; i <= m; i++)
    {
        for (int j = 0; j <= n; j++)
        {

            // If str1 is empty, then
            // insert all characters
            // of String str2
            if (i == 0)

                // Minimum operations
                // is j
                dp[i,j] = j;

            // If str2 is empty, then
            // remove all characters
            // of String str2
            else if (j == 0)

                // Minimum operations
                // is i
                dp[i,j] = i;

            // If the last characters
            // are same, then ignore
            // last character
            else if (str1[i - 1] == str2[j - 1])
                dp[i,j] = dp[i - 1,j - 1];

            // If the last character
            // is different, then
            // find the minimum
            else {

                // Perform one of the
                // insert, remove and
                // the replace
                dp[i,j] = 1
                           + getMin(
                                 dp[i,j - 1],
                                 dp[i - 1,j],
                                 dp[i - 1,j - 1]);
            }
        }
    }

    // Return the minimum number of
    // steps required
    return dp[m,n];
}

// Function to find the minimum number
// of steps to modify the String such
// that first half and second half
// becomes the same
static void minimumSteps(string S, int N)
{

    // Stores the minimum number of
    // operations required
    int ans = int.MaxValue;

    // Traverse the given String S
    for (int i = 1; i < N; i++) {

        string S1 = S.Substring(0, i);
        string S2 = S.Substring(i);

        // Find the minimum operations
        int count = editDistance(
            S1, S2, S1.Length,
            S2.Length);

        // Update the ans
        ans = Math.Min(ans, count);
    }

    // Print the result
    Console.Write(ans);
}

// Driver Code
public static void Main(string[] args)
{
    string S = "aabb";
    int N = S.Length;
    minimumSteps(S, N);
}
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach;

        // Function to find the minimum of
        // the three numbers
        function getMin(x, y, z) {
            return Math.min(Math.min(x, y), z);
        }

        // Function to find the minimum number
        // operations required to convert string
        // str1 to str2 using the operations
        function editDistance(str1, str2, m, n)
        {

            // Stores the results of subproblems
            let dp = new Array(m + 1).fill(new Array(n + 1));

            // Fill dp[][] in bottom up manner
            for (let i = 0; i <= m; i++) {
                for (let j = 0; j <= n; j++) {

                    // If str1 is empty, then
                    // insert all characters
                    // of string str2
                    if (i == 0)

                        // Minimum operations
                        // is j
                        dp[i][j] = j;

                    // If str2 is empty, then
                    // remove all characters
                    // of string str2
                    else if (j == 0)

                        // Minimum operations
                        // is i
                        dp[i][j] = i;

                    // If the last characters
                    // are same, then ignore
                    // last character
                    else if (str1[i - 1] == str2[j - 1])
                        dp[i][j] = dp[i - 1][j - 1];

                    // If the last character
                    // is different, then
                    // find the minimum
                    else {

                        // Perform one of the
                        // insert, remove and
                        // the replace
                        dp[i][j] = 1
                            + getMin(
                                dp[i][j - 1],
                                dp[i - 1][j],
                                dp[i - 1][j - 1]);
                    }
                }
            }

            // Return the minimum number of
            // steps required
            return dp[m][n];
        }

        // Function to find the minimum number
        // of steps to modify the string such
        // that first half and second half
        // becomes the same
        function minimumSteps(S, N) {
            // Stores the minimum number of
            // operations required
            let ans = Number.MAX_VALUE;

            // Traverse the given string S
            for (let i = 1; i < N; i++) {

                let S1 = S.substring(0, i);
                let S2 = S.substring(i);

                // Find the minimum operations
                let count = editDistance(
                    S1, S2, S1.length,
                    S2.length);

                // Update the ans
                ans = Math.min(ans, count);
            }

            // Print the result
            document.write(ans - 1);
        }

        // Driver Code
        let S = "aabb";
        let N = S.length;
        minimumSteps(S, N);

   // This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N <sup>2</sup> )*