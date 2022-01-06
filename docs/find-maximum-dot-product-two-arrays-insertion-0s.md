# 求插入 0 的两个数组的最大点积

> 原文:[https://www . geesforgeks . org/find-maximum-dot-product-two-array-insert-0s/](https://www.geeksforgeeks.org/find-maximum-dot-product-two-arrays-insertion-0s/)

给定两个大小为 m 和 n 的正整数数组，其中 m > n。我们需要通过在第二个数组中插入零来最大化点积，但我们不能打乱元素的顺序。

**示例:**

```
Input : A[] = {2, 3 , 1, 7, 8} 
        B[] = {3, 6, 7}        
Output : 107
Explanation : We get maximum dot product after
inserting 0 at first and third positions in 
second array.
Maximum Dot Product : = A[i] * B[j] 
2*0 + 3*3 + 1*0 + 7*6 + 8*7 = 107

Input : A[] = {1, 2, 3, 6, 1, 4}
        B[] = {4, 5, 1}
Output : 46
```

问于:[定向面试](https://www.geeksforgeeks.org/directi-interview-experience-set-17-campus/)

看待这个问题的另一种方式是，对于每对元素元素 A[i]和 B[j]，其中 j >= i，我们有两个选择:

1.  我们把 A[i]和 B[j]相乘，然后加到乘积上(我们包括 A[i])。
2.  我们将 A[i]从产品中排除(换句话说，我们在 B[]的当前位置插入 0)

思路是用[动态编程](https://www.geeksforgeeks.org/dynamic-programming-set-2-optimal-substructure-property/)。

```
1) Given Array A[] of size 'm' and B[] of size 'n'

2) Create 2D matrix 'DP[n + 1][m + 1]' initialize it
with '0'

3) Run loop outer loop for i = 1 to n
     Inner loop j = i to m

       // Two cases arise
       // 1) Include A[j]
       // 2) Exclude A[j] (insert 0 in B[])      
       dp[i][j]  = max(dp[i-1][j-1] + A[j-1] * B[i -1],
                       dp[i][j-1]) 

    // Last return maximum dot product that is 
    return dp[n][m]
```

以下是上述想法的实现。

## C++

```
// C++ program to find maximum dot product of two array
#include<bits/stdc++.h>
using namespace std;

// Function compute Maximum Dot Product and
// return it
long long int MaxDotProduct(int A[], int B[],
                            int m, int n)
{
    // Create 2D Matrix that stores dot product
    // dp[i+1][j+1] stores product considering B[0..i]
    // and A[0...j]. Note that since all m > n, we fill
    // values in upper diagonal of dp[][]
    long long int dp[n+1][m+1];
    memset(dp, 0, sizeof(dp));

    // Traverse through all elements of B[]
    for (int i=1; i<=n; i++)

        // Consider all values of A[] with indexes greater
        // than or equal to i and compute dp[i][j]
        for (int j=i; j<=m; j++)

            // Two cases arise
            // 1) Include A[j]
            // 2) Exclude A[j] (insert 0 in B[])
            dp[i][j] = max((dp[i-1][j-1] + (A[j-1]*B[i-1])) ,
                            dp[i][j-1]);

    // return Maximum Dot Product
    return dp[n][m] ;
}

// Driver program to test above function
int main()
{
    int A[] = { 2, 3 , 1, 7, 8 } ;
    int B[] = { 3, 6, 7 } ;
    int m = sizeof(A)/sizeof(A[0]);
    int n = sizeof(B)/sizeof(B[0]);
    cout << MaxDotProduct(A, B, m, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum
// dot product of two array
import java.util.*;

class GFG
{
// Function to compute Maximum
// Dot Product and return it
static int MaxDotProduct(int A[], int B[], int m, int n)
{
    // Create 2D Matrix that stores dot product
    // dp[i+1][j+1] stores product considering B[0..i]
    // and A[0...j]. Note that since all m > n, we fill
    // values in upper diagonal of dp[][]
    int dp[][] = new int[n + 1][m + 1];
    for (int[] row : dp)
    Arrays.fill(row, 0);

    // Traverse through all elements of B[]
    for (int i = 1; i <= n; i++)

    // Consider all values of A[] with indexes greater
    // than or equal to i and compute dp[i][j]
    for (int j = i; j <= m; j++)

        // Two cases arise
        // 1) Include A[j]
        // 2) Exclude A[j] (insert 0 in B[])
        dp[i][j] =
            Math.max((dp[i - 1][j - 1] +
                    (A[j - 1] * B[i - 1])), dp[i][j - 1]);

    // return Maximum Dot Product
    return dp[n][m];
}

// Driver code
public static void main(String[] args) {
    int A[] = {2, 3, 1, 7, 8};
    int B[] = {3, 6, 7};
    int m = A.length;
    int n = B.length;
    System.out.print(MaxDotProduct(A, B, m, n));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python 3 program to find maximum dot
# product of two array

# Function compute Maximum Dot Product
# and return it
def MaxDotProduct(A, B, m, n):

    # Create 2D Matrix that stores dot product
    # dp[i+1][j+1] stores product considering
    # B[0..i] and A[0...j]. Note that since
    # all m > n, we fill values in upper
    # diagonal of dp[][]
    dp = [[0 for i in range(m + 1)]
             for j in range(n + 1)]

    # Traverse through all elements of B[]
    for i in range(1, n + 1, 1):

        # Consider all values of A[] with indexes
        # greater than or equal to i and compute
        # dp[i][j]
        for j in range(i, m + 1, 1):

            # Two cases arise
            # 1) Include A[j]
            # 2) Exclude A[j] (insert 0 in B[])
            dp[i][j] = max((dp[i - 1][j - 1] +
                            (A[j - 1] * B[i - 1])) ,
                            dp[i][j - 1])

    # return Maximum Dot Product
    return dp[n][m]

# Driver Code
if __name__ == '__main__':
    A = [2, 3 , 1, 7, 8]
    B = [3, 6, 7]
    m = len(A)
    n = len(B)
    print(MaxDotProduct(A, B, m, n))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to find maximum
// dot product of two array
using System;

public class GFG{

    // Function to compute Maximum
    // Dot Product and return it
    static int MaxDotProduct(int []A, int []B, int m, int n)
    {
        // Create 2D Matrix that stores dot product
        // dp[i+1][j+1] stores product considering B[0..i]
        // and A[0...j]. Note that since all m > n, we fill
        // values in upper diagonal of dp[][]
        int [,]dp = new int[n + 1,m + 1];

        // Traverse through all elements of B[]
        for (int i = 1; i <= n; i++)

        // Consider all values of A[] with indexes greater
        // than or equal to i and compute dp[i][j]
        for (int j = i; j <= m; j++)

            // Two cases arise
            // 1) Include A[j]
            // 2) Exclude A[j] (insert 0 in B[])
            dp[i,j] =
                Math.Max((dp[i - 1,j - 1] +
                        (A[j - 1] * B[i - 1])), dp[i,j - 1]);

        // return Maximum Dot Product
        return dp[n,m];
    }

    // Driver code
    public static void Main() {
        int []A = {2, 3, 1, 7, 8};
        int []B = {3, 6, 7};
        int m = A.Length;
        int n = B.Length;
        Console.Write(MaxDotProduct(A, B, m, n));
    }
}

/*This code is contributed by 29AjayKumar*/
```

## java 描述语言

```
<script>
// Javascript program to find maximum
// dot product of two array

// Function to compute Maximum
// Dot Product and return it
function MaxDotProduct(A, B, m, n)
{
    // Create 2D Matrix that stores dot product
    // dp[i+1][j+1] stores product considering B[0..i]
    // and A[0...j]. Note that since all m > n, we fill
    // values in upper diagonal of dp[][]
    let dp = new Array(n + 1);
    for(let i = 0; i < (n + 1); i++)
    {
        dp[i] = new Array(m+1);
        for(let j = 0; j < m + 1; j++)
        {
            dp[i][j] = 0;
        }
    }

    // Traverse through all elements of B[]
    for (let i = 1; i <= n; i++)

    // Consider all values of A[] with indexes greater
    // than or equal to i and compute dp[i][j]
    for (let j = i; j <= m; j++)

        // Two cases arise
        // 1) Include A[j]
        // 2) Exclude A[j] (insert 0 in B[])
        dp[i][j] =
            Math.max((dp[i - 1][j - 1] +
                    (A[j - 1] * B[i - 1])), dp[i][j - 1]);

    // return Maximum Dot Product
    return dp[n][m];
}

// Driver code
let A = [2, 3, 1, 7, 8];
let B = [3, 6, 7];
let m = A.length;
let n = B.length;
document.write(MaxDotProduct(A, B, m, n));

// This code is contributed by rag2127
</script>
```

**输出:**

```
107
```

**时间复杂度:** O(nm)

本文由 [**尼尚·辛格**](https://practice.geeksforgeeks.org/user-profile.php?user=_code) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。