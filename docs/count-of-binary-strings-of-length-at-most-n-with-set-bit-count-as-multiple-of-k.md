# 长度最多为 N 的二进制字符串的计数，设置的位数为 K 的倍数

> 原文:[https://www . geeksforgeeks . org/最多 n 个二进制长度字符串的计数，设置为 k 的倍数位计数/](https://www.geeksforgeeks.org/count-of-binary-strings-of-length-at-most-n-with-set-bit-count-as-multiple-of-k/)

给定两个整数 **N** 和 **K** ，任务是找到长度至多为 **N** 的二进制字符串的计数，该计数可以形成为使得连续的 **1** 的计数总是 **K** 的倍数。

**示例:**

> **输入:** N = 3，K = 2
> **输出:** 6
> **解释:**包含连续 1 作为 K 的倍数的 N 长度的二进制字符串如下:
> 
> 1.  长度 1:“0”，包含 0 个连续的 1。
> 2.  长度 2:“00”、“11”，分别包含 0 和 2 个连续的 1。
> 3.  长度 3:“000”、“011”、“110”分别包含 0 和 2 个连续 1 的两种不同组合。
> 
> 所以，可以形成的字符串总数是 6。
> 
> **输入:** N = 5，K = 4
> T3】输出: 8

**方法:**利用[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)借助[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)可以解决给定的问题。按照以下步骤解决给定的问题:

*   创建一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/) **cntStrings(N，K)** ，该函数返回长度为 **N** 的字符串数，其连续 1 为 **K** 的倍数。这可以通过从当前索引向下一个 **K** 连续索引赋值 1，并递归调用剩余字符串，或者向当前索引赋值 0，并递归调用剩余字符串来实现。
*   创建一个[数组](https://www.geeksforgeeks.org/array-data-structure/) **dp[]** ，该数组存储上述递归函数的[记忆值](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)。
*   为范围**【1，N】**内 **i** 的所有可能值调用函数 **cntStrings(i，K)** ，并将它们的总和存储在变量 **cnt** 中。
*   存储在 **cnt** 中的值是要求的答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

int dp[1001];

// Recursive function to find the count
// of valid binary strings of length n
int cntString(int n, int k)
{
    // Base Case
    if (n == 0) {
        return 1;
    }

    // If current value is already calculated
    if (dp[n] != -1) {
        return dp[n];
    }

    // Stores the current answer
    int ans = 0;

    // Case for element at next k indices as 1
    if (n >= k) {
        ans += cntString(n - k, k);
    }

    // Case for element at current index as 0
    ans += cntString(n - 1, k);

    // Return ans with storing it in dp[]
    return dp[n] = ans;
}

// Function to find the count of valid
// binary strings of atmost N length
int cntStringAll(int N, int K)
{
    // Initializing all elements with -1
    memset(dp, -1, sizeof(dp));

    // Stores the final answer
    int cnt = 0;

    // Iterate and calculate the total
    // possible binary strings of each
    // length in the range [1, N]
    for (int i = 1; i <= N; i++) {
        cnt += cntString(i, K);
    }

    // Return Answer
    return cnt;
}

// Driver Code
int main()
{
    int N = 5;
    int K = 4;

    cout << cntStringAll(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG {

    static int dp[] = new int[1001];

    // Recursive function to find the count
    // of valid binary strings of length n
    static int cntString(int n, int k)
    {
        // Base Case
        if (n == 0) {
            return 1;
        }

        // If current value is already calculated
        if (dp[n] != -1) {
            return dp[n];
        }

        // Stores the current answer
        int ans = 0;

        // Case for element at next k indices as 1
        if (n >= k) {
            ans += cntString(n - k, k);
        }

        // Case for element at current index as 0
        ans += cntString(n - 1, k);

        // Return ans with storing it in dp[]
        return dp[n] = ans;
    }

    // Function to find the count of valid
    // binary strings of atmost N length
    static int cntStringAll(int N, int K)
    {
        // Initializing all elements with -1
        for (int i = 0; i < 1001; i++)
            dp[i] = -1;

        // Stores the final answer
        int cnt = 0;

        // Iterate and calculate the total
        // possible binary strings of each
        // length in the range [1, N]
        for (int i = 1; i <= N; i++) {
            cnt += cntString(i, K);
        }

        // Return Answer
        return cnt;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 5;
        int K = 4;

        System.out.println(cntStringAll(N, K));
    }
}

// This code is contributed by dwivediyash
```

## 蟒蛇 3

```
# python program for the above approach
dp = [-1 for _ in range(1001)]

# Recursive function to find the count
# of valid binary strings of length n
def cntString(n, k):

        # Base Case
    if (n == 0):
        return 1

        # If current value is already calculated
    if (dp[n] != -1):
        return dp[n]

        # Stores the current answer
    ans = 0

    # Case for element at next k indices as 1
    if (n >= k):
        ans += cntString(n - k, k)

        # Case for element at current index as 0
    ans += cntString(n - 1, k)

    # Return ans with storing it in dp[]
    dp[n] = ans

    return dp[n]

# Function to find the count of valid
# binary strings of atmost N length
def cntStringAll(N, K):

        # Stores the final answer
    cnt = 0

    # Iterate and calculate the total
    # possible binary strings of each
    # length in the range [1, N]
    for i in range(1, N + 1):
        cnt += cntString(i, K)

    # Return Answer
    return cnt

# Driver Code
if __name__ == "__main__":

    N = 5
    K = 4

    print(cntStringAll(N, K))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

    static int []dp = new int[1001];

    // Recursive function to find the count
    // of valid binary strings of length n
    static int cntString(int n, int k)
    {

        // Base Case
        if (n == 0) {
            return 1;
        }

        // If current value is already calculated
        if (dp[n] != -1) {
            return dp[n];
        }

        // Stores the current answer
        int ans = 0;

        // Case for element at next k indices as 1
        if (n >= k) {
            ans += cntString(n - k, k);
        }

        // Case for element at current index as 0
        ans += cntString(n - 1, k);

        // Return ans with storing it in dp[]
        return dp[n] = ans;
    }

    // Function to find the count of valid
    // binary strings of atmost N length
    static int cntStringAll(int N, int K)
    {

        // Initializing all elements with -1
        for (int i = 0; i < 1001; i++)
            dp[i] = -1;

        // Stores the final answer
        int cnt = 0;

        // Iterate and calculate the total
        // possible binary strings of each
        // length in the range [1, N]
        for (int i = 1; i <= N; i++) {
            cnt += cntString(i, K);
        }

        // Return Answer
        return cnt;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int N = 5;
        int K = 4;

        Console.WriteLine(cntStringAll(N, K));
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
    // JavaScript program for the above approach

    let dp = new Array(1001).fill(-1);

    // Recursive function to find the count
    // of valid binary strings of length n
    const cntString = (n, k) => {
        // Base Case
        if (n == 0) {
            return 1;
        }

        // If current value is already calculated
        if (dp[n] != -1) {
            return dp[n];
        }

        // Stores the current answer
        let ans = 0;

        // Case for element at next k indices as 1
        if (n >= k) {
            ans += cntString(n - k, k);
        }

        // Case for element at current index as 0
        ans += cntString(n - 1, k);

        // Return ans with storing it in dp[]
        return dp[n] = ans;
    }

    // Function to find the count of valid
    // binary strings of atmost N length
    const cntStringAll = (N, K) => {

        // Stores the final answer
        let cnt = 0;

        // Iterate and calculate the total
        // possible binary strings of each
        // length in the range [1, N]
        for (let i = 1; i <= N; i++) {
            cnt += cntString(i, K);
        }

        // Return Answer
        return cnt;
    }

    // Driver Code
    let N = 5;
    let K = 4;

    document.write(cntStringAll(N, K));

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
8
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)