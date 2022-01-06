# 二进制串中最长的非递增子序列

> 原文:[https://www . geesforgeks . org/最长非递增二进制字符串中的子序列/](https://www.geeksforgeeks.org/longest-non-increasing-subsequence-in-a-binary-string/)

给定一个大小为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是找到给定字符串 **S** 中最长非递增子序列[的长度。](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/)

**示例:**

> **输入:**S = " 010111011010100001011 "
> **输出:** 12
> **说明:**最长的不递增子序列为“1111111100000”，长度等于 12。
> 
> **输入:**S = 10101
> T3】输出: 3

**方法:**给定的问题可以通过观察字符串 **S** 是一个二进制字符串来解决，所以一个非递增的子序列总是由 **0** 和更多连续的 **1s** 或 **1** 和更多连续的 **0s** 组成。按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)，比如**pre【】**，存储 **1s** 的数量，直到 **i** 的每个索引 **i** 都在**【0，N–1】**的范围内。
*   初始化一个[数组](https://www.geeksforgeeks.org/suffix-array-set-1-introduction/)，比如**post【】**，存储 **0s** 的数量，直到在**【0，N–1】**范围内的 **i** 到字符串末尾的每个索引 **i** 。
*   初始化一个变量，比如说**和**，它存储给定字符串 **S** 中最长非递增子序列的[长度。](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/)
*   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**并将 **ans** 的值更新为 **ans** 和**的最大值(pre[i] + post[i])** 。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the length of the
// longest non-increasing subsequence
int findLength(string str, int n)
{
    // Stores the prefix and suffix
    // count of 1s and 0s respectively
    int pre[n], post[n];

    // Initialize the array
    memset(pre, 0, sizeof(pre));
    memset(post, 0, sizeof(post));

    // Store the number of '1's
    // up to current index i in pre
    for (int i = 0; i < n; i++) {

        // Find the prefix sum
        if (i != 0) {
            pre[i] += pre[i - 1];
        }

        // If the current element
        // is '1', update the pre[i]
        if (str[i] == '1') {
            pre[i] += 1;
        }
    }

    // Store the number of '0's over
    // the range [i, N - 1]
    for (int i = n - 1; i >= 0; i--) {

        // Find the suffix sum
        if (i != n - 1)
            post[i] += post[i + 1];

        // If the current element
        // is '0', update post[i]
        if (str[i] == '0')
            post[i] += 1;
    }

    // Stores the maximum length
    int ans = 0;

    // Find the maximum value of
    // pre[i] + post[i]
    for (int i = 0; i < n; i++) {
        ans = max(ans, pre[i] + post[i]);
    }

    // Return the answer
    return ans;
}

// Driver Code
int main()
{
    string S = "0101110110100001011";
    cout << findLength(S, S.length());

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the length of the
// longest non-increasing subsequence
static int findLength(String str, int n)
{

    // Stores the prefix and suffix
    // count of 1s and 0s respectively
    int pre[] = new int[n];
    int post[] = new int[n];

    // Initialize the array
    for(int i = 0; i < n; i++)
    {
        pre[i] = 0;
        post[i] = 0;
    }

    // Store the number of '1's
    // up to current index i in pre
    for(int i = 0; i < n; i++)
    {

        // Find the prefix sum
        if (i != 0)
        {
            pre[i] += pre[i - 1];
        }

        // If the current element
        // is '1', update the pre[i]
        if (str.charAt(i) == '1')
        {
            pre[i] += 1;
        }
    }

    // Store the number of '0's over
    // the range [i, N - 1]
    for(int i = n - 1; i >= 0; i--)
    {

        // Find the suffix sum
        if (i != n - 1)
            post[i] += post[i + 1];

        // If the current element
        // is '0', update post[i]
        if (str.charAt(i) == '0')
            post[i] += 1;
    }

    // Stores the maximum length
    int ans = 0;

    // Find the maximum value of
    // pre[i] + post[i]
    for(int i = 0; i < n; i++)
    {
        ans = Math.max(ans, pre[i] + post[i]);
    }

    // Return the answer
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    String S = "0101110110100001011";
    System.out.println(findLength(S, S.length()));
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the length of the
# longest non-increasing subsequence
def findLength(str, n):

    # Stores the prefix and suffix
    # count of 1s and 0s respectively
    pre = [0] * n
    post  = [0] * n

    # Store the number of '1's
    # up to current index i in pre
    for i in range(n):

        # Find the prefix sum
        if (i != 0):
            pre[i] += pre[i - 1]

        # If the current element
        # is '1', update the pre[i]
        if (str[i] == '1'):
            pre[i] += 1

    # Store the number of '0's over
    # the range [i, N - 1]
    for i in range(n - 1, -1, -1):

        # Find the suffix sum
        if (i != (n - 1)):
            post[i] += post[i + 1]

        # If the current element
        # is '0', update post[i]
        if (str[i] == '0'):
            post[i] += 1

    # Stores the maximum length
    ans = 0

    # Find the maximum value of
    # pre[i] + post[i]
    for i in range(n):
        ans = max(ans, pre[i] + post[i])

    # Return the answer
    return ans

# Driver Code
S = "0101110110100001011"
n = len(S)

print(findLength(S, n))

# This code is contributed by susmitakundugoaldanga
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the length of the
// longest non-increasing subsequence
static int findLength(String str, int n)
{

    // Stores the prefix and suffix
    // count of 1s and 0s respectively
    int []pre = new int[n];
    int []post = new int[n];

    // Initialize the array
    for(int i = 0; i < n; i++)
    {
        pre[i] = 0;
        post[i] = 0;
    }

    // Store the number of '1's
    // up to current index i in pre
    for(int i = 0; i < n; i++)
    {

        // Find the prefix sum
        if (i != 0)
        {
            pre[i] += pre[i - 1];
        }

        // If the current element
        // is '1', update the pre[i]
        if (str[i] == '1')
        {
            pre[i] += 1;
        }
    }

    // Store the number of '0's over
    // the range [i, N - 1]
    for(int i = n - 1; i >= 0; i--)
    {

        // Find the suffix sum
        if (i != n - 1)
            post[i] += post[i + 1];

        // If the current element
        // is '0', update post[i]
        if (str[i] == '0')
            post[i] += 1;
    }

    // Stores the maximum length
    int ans = 0;

    // Find the maximum value of
    // pre[i] + post[i]
    for(int i = 0; i < n; i++)
    {
        ans = Math.Max(ans, pre[i] + post[i]);
    }

    // Return the answer
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    String S = "0101110110100001011";
    Console.WriteLine(findLength(S, S.Length));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the length of the
// longest non-increasing subsequence
function findLength(str, n)
{

    // Stores the prefix and suffix
    // count of 1s and 0s respectively
    let pre = Array.from({length: n}, (_, i) => 0);
    let post = Array.from({length: n}, (_, i) => 0);

    // Initialize the array
    for(let i = 0; i < n; i++)
    {
        pre[i] = 0;
        post[i] = 0;
    }

    // Store the number of '1's
    // up to current index i in pre
    for(let i = 0; i < n; i++)
    {

        // Find the prefix sum
        if (i != 0)
        {
            pre[i] += pre[i - 1];
        }

        // If the current element
        // is '1', update the pre[i]
        if (str[i] == '1')
        {
            pre[i] += 1;
        }
    }

    // Store the number of '0's over
    // the range [i, N - 1]
    for(let i = n - 1; i >= 0; i--)
    {

        // Find the suffix sum
        if (i != n - 1)
            post[i] += post[i + 1];

        // If the current element
        // is '0', update post[i]
        if (str[i] == '0')
            post[i] += 1;
    }

    // Stores the maximum length
    let ans = 0;

    // Find the maximum value of
    // pre[i] + post[i]
    for(let i = 0; i < n; i++)
    {
        ans = Math.max(ans, pre[i] + post[i]);
    }

    // Return the answer
    return ans;
}

// Driver Code

    let S = "0101110110100001011";
    document.write(findLength(S, S.length));

</script>
```

**Output:** 

```
12
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)