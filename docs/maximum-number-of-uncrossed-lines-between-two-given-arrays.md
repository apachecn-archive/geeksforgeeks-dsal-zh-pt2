# 两个给定数组之间未交叉的最大行数

> 原文:[https://www . geeksforgeeks . org/两个给定数组之间未交叉的最大行数/](https://www.geeksforgeeks.org/maximum-number-of-uncrossed-lines-between-two-given-arrays/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **A[]** 和 **B[]** ，任务是找出两个给定数组元素之间最大的未交叉线数。

> 只有在下列情况下，才能在两个数组元素 A[i]和 B[j]之间画一条直线:
> 
> *   A[i] = B[j]
> *   这条线不与任何其他线相交。

**示例:**

> **输入:** A[] = {3，9，2}，B[] = {3，2，9}
> **输出:** 2
> **说明:**
> A[0]至 B[0]与 A[1]至 B[2]之间的直线互不相交。
> 
> **输入:** A[] = {1，2，3，4，5}，B[] = {1，2，3，4，5 }
> T3】输出: 5

**天真法:**思路是[生成数组](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/) **A[]** 的所有子序列，并尝试在数组 **B[]** 中找到它们，这样两个子序列就可以通过连接直线连接起来。在 A[]和 B[]中发现的最长的这样的子序列将具有最大数量的非交叉行。所以打印子序列的长度。

***时间复杂度:**O(M * 2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**从上面的方法可以观察到，任务是找到两个数组中最长的公共子序列。因此，上述方法可以通过使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)在两个阵列之间找到 [**最长公共子序列**](https://www.geeksforgeeks.org/longest-common-subsequence-dp-4/) 来优化。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count maximum number
// of uncrossed lines between the
// two given arrays
int uncrossedLines(int* a, int* b,
                   int n, int m)
{
    // Stores the length of lcs
    // obtained upto every index
    int dp[n + 1][m + 1];

    // Iterate over first array
    for (int i = 0; i <= n; i++) {

        // Iterate over second array
        for (int j = 0; j <= m; j++) {

            if (i == 0 || j == 0)

                // Update value in dp table
                dp[i][j] = 0;

            // If both characters
            // are equal
            else if (a[i - 1] == b[j - 1])

                // Update the length of lcs
                dp[i][j] = 1 + dp[i - 1][j - 1];

            // If both characters
            // are not equal
            else

                // Update the table
                dp[i][j] = max(dp[i - 1][j],
                               dp[i][j - 1]);
        }
    }

    // Return the answer
    return dp[n][m];
}

// Driver Code
int main()
{
    // Given array A[] and B[]
    int A[] = { 3, 9, 2 };
    int B[] = { 3, 2, 9 };

    int N = sizeof(A) / sizeof(A[0]);
    int M = sizeof(B) / sizeof(B[0]);

    // Function Call
    cout << uncrossedLines(A, B, N, M);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to count maximum number
// of uncrossed lines between the
// two given arrays
static int uncrossedLines(int[] a, int[] b,
                          int n, int m)
{

    // Stores the length of lcs
    // obtained upto every index
    int[][] dp = new int[n + 1][m + 1];

    // Iterate over first array
    for(int i = 0; i <= n; i++)
    {

        // Iterate over second array
        for(int j = 0; j <= m; j++)
        {
            if (i == 0 || j == 0)

                // Update value in dp table
                dp[i][j] = 0;

            // If both characters
            // are equal
            else if (a[i - 1] == b[j - 1])

                // Update the length of lcs
                dp[i][j] = 1 + dp[i - 1][j - 1];

            // If both characters
            // are not equal
            else

                // Update the table
                dp[i][j] = Math.max(dp[i - 1][j],
                                    dp[i][j - 1]);
        }
    }

    // Return the answer
    return dp[n][m];
}

// Driver Code
public static void main (String[] args)
{

    // Given array A[] and B[]
    int A[] = { 3, 9, 2 };
    int B[] = { 3, 2, 9 };

    int N = A.length;
    int M = B.length;

    // Function call
    System.out.print(uncrossedLines(A, B, N, M));
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to count maximum number
# of uncrossed lines between the
# two given arrays
def uncrossedLines(a, b,
                   n, m):

    # Stores the length of lcs
    # obtained upto every index
    dp = [[0 for x in range(m + 1)]
             for y in range(n + 1)]

    # Iterate over first array
    for i in range (n + 1):

        # Iterate over second array
        for j in range (m + 1):

            if (i == 0 or j == 0):

                # Update value in dp table
                dp[i][j] = 0

            # If both characters
            # are equal
            elif (a[i - 1] == b[j - 1]):

                # Update the length of lcs
                dp[i][j] = 1 + dp[i - 1][j - 1]

            # If both characters
            # are not equal
            else:

                # Update the table
                dp[i][j] = max(dp[i - 1][j],
                               dp[i][j - 1])

    # Return the answer
    return dp[n][m]

# Driver Code
if __name__ == "__main__":

    # Given array A[] and B[]
    A = [3, 9, 2]
    B = [3, 2, 9]

    N = len(A)
    M = len(B)

    # Function Call
    print (uncrossedLines(A, B, N, M))

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count maximum number
// of uncrossed lines between the
// two given arrays
static int uncrossedLines(int[] a, int[] b,
                          int n, int m)
{

    // Stores the length of lcs
    // obtained upto every index
    int[,] dp = new int[n + 1, m + 1];

    // Iterate over first array
    for(int i = 0; i <= n; i++)
    {

        // Iterate over second array
        for(int j = 0; j <= m; j++)
        {
            if (i == 0 || j == 0)

                // Update value in dp table
                dp[i, j] = 0;

            // If both characters
            // are equal
            else if (a[i - 1] == b[j - 1])

                // Update the length of lcs
                dp[i, j] = 1 + dp[i - 1, j - 1];

            // If both characters
            // are not equal
            else

                // Update the table
                dp[i, j] = Math.Max(dp[i - 1, j],
                                    dp[i, j - 1]);
        }
    }

    // Return the answer
    return dp[n, m];
}

// Driver Code
public static void Main (String[] args)
{

    // Given array A[] and B[]
    int[] A = { 3, 9, 2 };
    int[] B = { 3, 2, 9 };

    int N = A.Length;
    int M = B.Length;

    // Function call
    Console.Write(uncrossedLines(A, B, N, M));
}
}

// This code is contributed by code_hunt
}
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count maximum number
// of uncrossed lines between the
// two given arrays
function uncrossedLines(a, b, n, m)
{

    // Stores the length of lcs
    // obtained upto every index
    let dp = new Array(n + 1);
    for(let i = 0; i< (n + 1); i++)
    {
        dp[i] = new Array(m + 1);
        for(let j = 0; j < (m + 1); j++)
        {
            dp[i][j] = 0;
        }
    }

    // Iterate over first array
    for(let i = 0; i <= n; i++)
    {

        // Iterate over second array
        for(let j = 0; j <= m; j++)
        {
            if (i == 0 || j == 0)

                // Update value in dp table
                dp[i][j] = 0;

            // If both characters
            // are equal
            else if (a[i - 1] == b[j - 1])

                // Update the length of lcs
                dp[i][j] = 1 + dp[i - 1][j - 1];

            // If both characters
            // are not equal
            else

                // Update the table
                dp[i][j] = Math.max(dp[i - 1][j],
                                    dp[i][j - 1]);
        }
    }

    // Return the answer
    return dp[n][m];
}

// Driver Code

// Given array A[] and B[]
let A = [ 3, 9, 2 ];
let B = [3, 2, 9];
let N = A.length;
let M = B.length;

// Function call
document.write(uncrossedLines(A, B, N, M));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(N*M)*