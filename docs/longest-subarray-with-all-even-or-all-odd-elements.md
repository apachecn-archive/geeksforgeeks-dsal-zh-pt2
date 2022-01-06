# 具有所有偶数或所有奇数元素的最长子阵列

> 原文:[https://www . geesforgeks . org/全偶或全奇元素的最长子阵列/](https://www.geeksforgeeks.org/longest-subarray-with-all-even-or-all-odd-elements/)

给定一个非负整数的[数组](https://www.geeksforgeeks.org/array-data-structure/)**A[]****N**，任务是找到最长的[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的长度，使得该[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)中的所有元素都是奇数或偶数。

**示例:**

> **输入:** A[] = {2，5，7，2，4，6，8，3}
> **输出:** 4
> **解释:**长度为 4 的子数组{2，4，6，8}具有所有偶数元素
> 
> **输入:** A[] = {2，3，2，5，7，3}
> **输出:** 3
> **说明:**长度为 3 的子阵{5，7，3}具有所有奇数元素

**天真方法:**解决这个问题的天真方法是考虑所有连续的子阵列，对于每个子阵列，检查所有元素是偶数还是奇数。其中最长的将是答案。
***时间复杂度:** O(N^2)*
***辅助空间:** O(1)*

**高效方法:**解决这个问题的主要思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)(它同时具有–[最优子结构](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)和[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/))这样，如果有一些连续的奇数元素，那么下一个奇数元素将把那个连续数组的长度增加 1。即使是元素也是如此。按照以下步骤解决问题:

*   [初始化一个数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/) **dp[ ]** ，其中 **dp[i]** 存储结束于 **A[i]** 的[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的长度。
*   用 **1** 初始化**DP【0】**。
*   将变量**和**初始化为 **1** 来存储答案。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**，并执行以下步骤:
    *   如果 **A[i]%2** 等于 **A[i-1]%2，**则将 **dp[i]** 的值设置为 **dp[i-1]+1。**
    *   否则，将 **dp[i]** 的值设置为 **1。**
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下步骤:
    *   将 **ans** 的值设置为 **ans** 或**DP【I】的最大值。**
*   执行上述步骤后，打印**和**的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate longest substring
// with odd or even elements
int LongestOddEvenSubarray(int A[], int N)
{
    // Initializing dp[]
    int dp[N];

    // Initializing dp[0] with 1
    dp[0] = 1;

    // ans will store the final answer
    int ans = 1;

    // Traversing the array from index 1 to N - 1
    for (int i = 1; i < N; i++) {

        // Checking both current and previous element
        // is even or odd
        if ((A[i] % 2 == 0 && A[i - 1] % 2 == 0)
            || (A[i] % 2 != 0 && A[i - 1] % 2 != 0)) {

            // Updating dp[i] with dp[i-1] + 1
            dp[i] = dp[i - 1] + 1;
        }
        else
            dp[i] = 1;
    }

    for (int i = 0; i < N; i++)
        // Storing max element to ans
        ans = max(ans, dp[i]);

    // Returning the final answer
    return ans;
}

// Driver Code
int main()
{
    // Input
    int A[] = { 2, 5, 7, 2, 4, 6, 8, 3 };
    int N = sizeof(A) / sizeof(A[0]);

    // Function call
    cout << LongestOddEvenSubarray(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

    // Function to calculate longest substring
    // with odd or even elements
    static int LongestOddEvenSubarray(int A[], int N)
    {

        // Initializing dp[]
        int dp[] = new int[N];

        // Initializing dp[0] with 1
        dp[0] = 1;

        // ans will store the final answer
        int ans = 1;

        // Traversing the array from index 1 to N - 1
        for (int i = 1; i < N; i++) {

            // Checking both current and previous element
            // is even or odd
            if ((A[i] % 2 == 0 && A[i - 1] % 2 == 0)
                || (A[i] % 2 != 0 && A[i - 1] % 2 != 0)) {

                // Updating dp[i] with dp[i-1] + 1
                dp[i] = dp[i - 1] + 1;
            }
            else
                dp[i] = 1;
        }

        for (int i = 0; i < N; i++)
            // Storing max element to ans
            ans = Math.max(ans, dp[i]);

        // Returning the final answer
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Input
        int A[] = { 2, 5, 7, 2, 4, 6, 8, 3 };
        int N = A.length;

        // Function call
        System.out.println(LongestOddEvenSubarray(A, N));
    }
}

// This code is contributed by Potta Lokesh
```

## C#

```
// C# program for the above approach
using System;

class GFG{

    // Function to calculate longest substring
    // with odd or even elements
    static int LongestOddEvenSubarray(int[] A, int N)
    {

        // Initializing dp[]
        int[] dp = new int[N];

        // Initializing dp[0] with 1
        dp[0] = 1;

        // ans will store the final answer
        int ans = 1;

        // Traversing the array from index 1 to N - 1
        for (int i = 1; i < N; i++) {

            // Checking both current and previous element
            // is even or odd
            if ((A[i] % 2 == 0 && A[i - 1] % 2 == 0)
                || (A[i] % 2 != 0 && A[i - 1] % 2 != 0)) {

                // Updating dp[i] with dp[i-1] + 1
                dp[i] = dp[i - 1] + 1;
            }
            else
                dp[i] = 1;
        }

        for (int i = 0; i < N; i++)

            // Storing max element to ans
            ans = Math.Max(ans, dp[i]);

        // Returning the final answer
        return ans;
    }

// Driver Code
public static void Main()
{
    // Input
        int[] A = { 2, 5, 7, 2, 4, 6, 8, 3 };
        int N = A.Length;

        // Function call
        Console.Write(LongestOddEvenSubarray(A, N));
}
}

// This code is contributed by target_2.
```

## 蟒蛇 3

```
# Python 3 implementation for the above approach

# Function to calculate longest substring
# with odd or even elements
def LongestOddEvenSubarray(A, N):
    # Initializing dp[]
    dp = [0 for i in range(N)]

    # Initializing dp[0] with 1
    dp[0] = 1

    # ans will store the final answer
    ans = 1

    # Traversing the array from index 1 to N - 1
    for i in range(1, N, 1):

        # Checking both current and previous element
        # is even or odd
        if ((A[i] % 2 == 0 and A[i - 1] % 2 == 0) or (A[i] % 2 != 0 and A[i - 1] % 2 != 0)):

            # Updating dp[i] with dp[i-1] + 1
            dp[i] = dp[i - 1] + 1
        else:
            dp[i] = 1

    for i in range(N):
        # Storing max element to ans
        ans = max(ans, dp[i])

    # Returning the final answer
    return ans

# Driver Code
if __name__ == '__main__':
    # Input
    A = [2, 5, 7, 2, 4, 6, 8, 3]
    N = len(A)

    # Function call
    print(LongestOddEvenSubarray(A, N))

    # This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// JavaScript implementation for the above approach

// Function to calculate longest substring
// with odd or even elements
function LongestOddEvenSubarray(A, N)
{

  // Initializing dp[]
  let dp = new Array(N);

  // Initializing dp[0] with 1
  dp[0] = 1;

  // ans will store the final answer
  let ans = 1;

  // Traversing the array from index 1 to N - 1
  for (let i = 1; i < N; i++)
  {

    // Checking both current and previous element
    // is even or odd
    if (
      (A[i] % 2 == 0 && A[i - 1] % 2 == 0) ||
      (A[i] % 2 != 0 && A[i - 1] % 2 != 0)
    ) {
      // Updating dp[i] with dp[i-1] + 1
      dp[i] = dp[i - 1] + 1;
    } else dp[i] = 1;
  }

  for (let i = 0; i < N; i++)

    // Storing max element to ans
    ans = Math.max(ans, dp[i]);

  // Returning the final answer
  return ans;
}

// Driver Code
// Input
let A = [2, 5, 7, 2, 4, 6, 8, 3];
let N = A.length;

// Function call
document.write(LongestOddEvenSubarray(A, N));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output**

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

**空间优化:**通过观察可以进一步优化上述方法的空间复杂度，对于计算 **dp[i]** ，只有 **dp[i-1]** 的值是相关的。因此，将 **dp[i-1]** 存储在一个变量中，并在每次迭代中更新该变量。此外，在每次迭代中更新答案。按照以下步骤解决问题:

*   将变量 **dp** 初始化为 **1** 存储[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的长度，直到 **i-1** 和 **ans** 为 **1** 存储答案。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**，并执行以下步骤:
    *   如果 **A[i]%2** 等于 **A[i-1]%2，**则将 **dp** 的值设置为 **dp+1** ，将 **ans** 的值设置为 **ans** 或 **dp 的最大值。**
    *   否则，将 **dp** 的值设置为 **1。**
*   执行上述步骤后，打印**和**的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate longest substring
// with odd or even elements
int LongestOddEvenSubarray(int A[], int N)
{
    // Initializing dp
    int dp;

    // Initializing dp with 1
    dp = 1;

    // ans will store the final answer
    int ans = 1;

    // Traversing the array from index 1 to N - 1
    for (int i = 1; i < N; i++) {

        // Checking both current and previous element
        // is even or odd
        if ((A[i] % 2 == 0 && A[i - 1] % 2 == 0)
            || (A[i] % 2 != 0 && A[i - 1] % 2 != 0)) {

            // Updating dp with (previous dp value) + 1
            dp = dp + 1;

            // Storing max element so far to ans
            ans = max(ans, dp);
        }
        else
            dp = 1;
    }

    // Returning the final answer
    return ans;
}

// Driver code
int main()
{
    // Input
    int A[] = { 2, 5, 7, 2, 4, 6, 8, 3 };
    int N = sizeof(A) / sizeof(A[0]);

    // Function call
    cout << LongestOddEvenSubarray(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.util.*;
class GFG
{

// Function to calculate longest subString
// with odd or even elements
static int LongestOddEvenSubarray(int A[], int N)
{

    // Initializing dp
    int dp;

    // Initializing dp with 1
    dp = 1;

    // ans will store the final answer
    int ans = 1;

    // Traversing the array from index 1 to N - 1
    for (int i = 1; i < N; i++) {

        // Checking both current and previous element
        // is even or odd
        if ((A[i] % 2 == 0 && A[i - 1] % 2 == 0)
            || (A[i] % 2 != 0 && A[i - 1] % 2 != 0)) {

            // Updating dp with (previous dp value) + 1
            dp = dp + 1;

            // Storing max element so far to ans
            ans = Math.max(ans, dp);
        }
        else
            dp = 1;
    }

    // Returning the final answer
    return ans;
}

// Driver code
public static void main(String[] args)
{

    // Input
    int A[] = { 2, 5, 7, 2, 4, 6, 8, 3 };
    int N = A.length;

    // Function call
    System.out.print(LongestOddEvenSubarray(A, N));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python implementation for the above approach

# Function to calculate longest substring
# with odd or even elements
def LongestOddEvenSubarray(A, N):

    # Initializing dp
    # Initializing dp with 1
    dp = 1

    # ans will store the final answer
    ans = 1

    # Traversing the array from index 1 to N - 1
    for i in range(1, N):

        # Checking both current and previous element
        # is even or odd
        if ((A[i] % 2 == 0 and A[i - 1] % 2 == 0) or (A[i] % 2 != 0 and A[i - 1] % 2 != 0)):

            # Updating dp with (previous dp value) + 1
            dp = dp + 1

            # Storing max element so far to ans
            ans = max(ans, dp)
        else:
            dp = 1

    # Returning the final answer
    return ans

# Driver code

# Input
A =  [2, 5, 7, 2, 4, 6, 8, 3 ]
N = len(A)

# Function call
print(LongestOddEvenSubarray(A, N))

# This code is contributed by shivani
```

## C#

```
// C# implementation for the above approach
using System;

public class GFG
{

// Function to calculate longest subString
// with odd or even elements
static int longestOddEvenSubarray(int []A, int N)
{

    // Initializing dp
    int dp;

    // Initializing dp with 1
    dp = 1;

    // ans will store the readonly answer
    int ans = 1;

    // Traversing the array from index 1 to N - 1
    for (int i = 1; i < N; i++) {

        // Checking both current and previous element
        // is even or odd
        if ((A[i] % 2 == 0 && A[i - 1] % 2 == 0)
            || (A[i] % 2 != 0 && A[i - 1] % 2 != 0)) {

            // Updating dp with (previous dp value) + 1
            dp = dp + 1;

            // Storing max element so far to ans
            ans = Math.Max(ans, dp);
        }
        else
            dp = 1;
    }

    // Returning the readonly answer
    return ans;
}

// Driver code
public static void Main(String[] args)
{

    // Input
    int []A = { 2, 5, 7, 2, 4, 6, 8, 3 };
    int N = A.Length;

    // Function call
    Console.Write(longestOddEvenSubarray(A, N));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript implementation for the above approach

// Function to calculate longest substring
// with odd or even elements
function LongestOddEvenSubarray(A, N) {
  // Initializing dp
  let dp;

  // Initializing dp with 1
  dp = 1;

  // ans will store the final answer
  let ans = 1;

  // Traversing the array from index 1 to N - 1
  for (let i = 1; i < N; i++) {
    // Checking both current and previous element
    // is even or odd
    if (
      (A[i] % 2 == 0 && A[i - 1] % 2 == 0) ||
      (A[i] % 2 != 0 && A[i - 1] % 2 != 0)
    ) {
      // Updating dp with (previous dp value) + 1
      dp = dp + 1;

      // Storing max element so far to ans
      ans = Math.max(ans, dp);
    } else dp = 1;
  }

  // Returning the final answer
  return ans;
}

// Driver code
// Input
let A = [2, 5, 7, 2, 4, 6, 8, 3];
let N = A.length;

// Function call
document.write(LongestOddEvenSubarray(A, N));

</script>
```

**Output**

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)