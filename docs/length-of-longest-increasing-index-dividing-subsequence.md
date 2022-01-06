# 最长递增指数划分子序列的长度

> 原文:[https://www . geeksforgeeks . org/最长递增索引分割子序列的长度/](https://www.geeksforgeeks.org/length-of-longest-increasing-index-dividing-subsequence/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是找到最长的递增子序列，这样任何元素的索引都可以被前一个元素(LIIDS)的索引整除。以下是 LIIDS 的必要条件:
如果 I，j 是给定数组中的两个索引。然后:

*   i < j
*   j % i = 0
*   arr[i] < arr[j]

**例:**

> **输入:** arr[] = {1，2，3，7，9，10}
> **输出:** 3
> **解释:**
> 子序列= {1，2，7}
> 子序列元素的索引= {1，2，4}
> 索引条件:
> 2 可被 1 整除
> 4 可被 2 整除
> 或
> 另一个可能的子序列= {1，3，14 6}
> 索引条件:
> 3 可被 1 整除
> 6 可被 3 整除
> **输入:** arr[] = {7，1，3，4，6}
> **输出:** 2
> **解释:**
> 子序列的元素的索引= {1，4}
> 子序列的元素的索引= {2，4}
> 索引条件:
> 4 可被 2 整除

**方法:**思路是用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)的概念来解决这个问题。

*   首先创建一个 dp[]数组，并用 1 初始化该数组。这是因为，分割子序列的最小长度是 1。
*   现在，对于数组中的每个索引“I”，以其倍数递增索引处的值的计数。
*   最后，当对所有值执行上述步骤时，数组中存在的最大值就是所需的答案。

以下是上述方法的实现:

## C++

```
// C++ program to find the length of
// the longest increasing sub-sequence
// such that the index of the element is
// divisible by index of previous element

#include <bits/stdc++.h>
using namespace std;

// Function to find the length of
// the longest increasing sub-sequence
// such that the index of the element is
// divisible by index of previous element
int LIIDS(int arr[], int N)
{
    // Initialize the dp[] array with 1 as a
    // single element will be of 1 length
    int dp[N + 1];

    int ans = 0;
    for (int i = 1; i <= N; i++) {
        dp[i] = 1;
    }

    // Traverse the given array
    for (int i = 1; i <= N; i++) {

        // If the index is divisible by
        // the previous index
        for (int j = i + i; j <= N; j += i) {

            // if increasing
            // subsequence identified
            if (arr[j] > arr[i]) {
                dp[j] = max(dp[j], dp[i] + 1);
            }
        }

        // Longest length is stored
        ans = max(ans, dp[i]);
    }
    return ans;
}

// Driver code
int main()
{

    int arr[] = { 1, 2, 3, 7, 9, 10 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << LIIDS(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the length of
// the longest increasing sub-sequence
// such that the index of the element is
// divisible by index of previous element
import java.util.*;

class GFG{

// Function to find the length of
// the longest increasing sub-sequence
// such that the index of the element is
// divisible by index of previous element
static int LIIDS(int arr[], int N)
{

    // Initialize the dp[] array with 1 as a
    // single element will be of 1 length
    int[] dp = new int[N + 1];
    int ans = 0;

    for(int i = 1; i <= N; i++)
    {
       dp[i] = 1;
    }

    // Traverse the given array
    for(int i = 1; i <= N; i++)
    {

       // If the index is divisible by
       // the previous index
       for(int j = i + i; j <= N; j += i)
       {

          // If increasing
          // subsequence identified
          if (j < arr.length && arr[j] > arr[i])
          {
              dp[j] = Math.max(dp[j], dp[i] + 1);
          }
       }

       // Longest length is stored
       ans = Math.max(ans, dp[i]);
    }
    return ans;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 1, 2, 3, 7, 9, 10 };
    int N = arr.length;

    System.out.println(LIIDS(arr, N));
}
}

// This code is contributed by AbhiThakur
```

## 蟒蛇 3

```
# Python3 program to find the length of
# the longest increasing sub-sequence
# such that the index of the element is
# divisible by index of previous element

# Function to find the length of
# the longest increasing sub-sequence
# such that the index of the element is
# divisible by index of previous element
def LIIDS(arr, N):

    # Initialize the dp[] array with 1 as a
    # single element will be of 1 length
    dp = []
    for i in range(1, N + 1):
        dp.append(1)

    ans = 0

    # Traverse the given array
    for i in range(1, N + 1):

        # If the index is divisible by
        # the previous index
        j = i + i
        while j <= N:

            # If increasing
            # subsequence identified
            if j < N and i < N and arr[j] > arr[i]:
                dp[j] = max(dp[j], dp[i] + 1)

            j += i

        # Longest length is stored
        if i < N:
            ans = max(ans, dp[i])

    return ans

# Driver code
arr = [ 1, 2, 3, 7, 9, 10 ]

N = len(arr)

print(LIIDS(arr, N))

# This code is contributed by ishayadav181
```

## C#

```
// C# program to find the length of
// the longest increasing sub-sequence
// such that the index of the element is
// divisible by index of previous element
using System;

class GFG{

// Function to find the length of
// the longest increasing sub-sequence
// such that the index of the element is
// divisible by index of previous element
static int LIIDS(int[] arr, int N)
{

    // Initialize the dp[] array with 1 as a
    // single element will be of 1 length
    int[] dp = new int[N + 1];
    int ans = 0;

    for(int i = 1; i <= N; i++)
    {
        dp[i] = 1;
    }

    // Traverse the given array
    for(int i = 1; i <= N; i++)
    {

        // If the index is divisible by
        // the previous index
        for(int j = i + i; j <= N; j += i)
        {

            // If increasing
            // subsequence identified
            if (j < arr.Length && arr[j] > arr[i])
            {
                dp[j] = Math.Max(dp[j], dp[i] + 1);
            }
        }

        // Longest length is stored
        ans = Math.Max(ans, dp[i]);
    }
    return ans;
}

// Driver code
public static void Main()
{
    int[] arr = new int[] { 1, 2, 3, 7, 9, 10 };
    int N = arr.Length;

    Console.WriteLine(LIIDS(arr, N));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program to find the length of
// the longest increasing sub-sequence
// such that the index of the element is
// divisible by index of previous element

// Function to find the length of
// the longest increasing sub-sequence
// such that the index of the element is
// divisible by index of previous element
function LIIDS(arr, N)
{

    // Initialize the dp[] array with 1 as a
    // single element will be of 1 length
    let dp = [];
    let ans = 0;

    for(let i = 1; i <= N; i++)
    {
       dp[i] = 1;
    }

    // Traverse the given array
    for(let i = 1; i <= N; i++)
    {

       // If the index is divisible by
       // the previous index
       for(let j = i + i; j <= N; j += i)
       {

          // If increasing
          // subsequence identified
          if (j < arr.length && arr[j] > arr[i])
          {
              dp[j] = Math.max(dp[j], dp[i] + 1);
          }
       }

       // Longest length is stored
       ans = Math.max(ans, dp[i]);
    }
    return ans;
}

// Driver code

    let arr = [ 1, 2, 3, 7, 9, 10 ];
    let N = arr.length;

    document.write(LIIDS(arr, N));

// This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
3
```

**时间复杂度:** *O(N log(N))* ，其中 N 为数组长度。