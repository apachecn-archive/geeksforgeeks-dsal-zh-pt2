# 余数至少为 K 的前 N 个自然数对的计数

> 原文:[https://www . geeksforgeeks . org/从第一个 n 个自然数开始的配对计数，余数至少为-k/](https://www.geeksforgeeks.org/count-of-pairs-from-first-n-natural-numbers-with-remainder-at-least-k/)

给定两个正整数 **N** 和 **K** ，任务是找出范围**【1，N】**内的配对数量 **(a，b)** ，使得 **a%b** 至少为**K**。

**示例:**

> **输入:** N = 5，K = 2
> **输出:** 7
> **说明:**
> 以下是满足给定标准的所有可能对:
> 
> 1.  (2，3):2% 3 的值= 2(>= K)。
> 2.  (5，3):5% 3 的值= 2(>= K)。
> 3.  (2，4):2% 4 的值= 2(>= K)。
> 4.  (3，4):3% 4 的值= 3(>= K)。
> 5.  (2，5):2% 5 的值= 2(>= K)。
> 6.  (3，5):3% 5 的值= 3(>= K)。
> 7.  (4，5):4% 5 的值= 4(>= K)。
> 
> 因此，对的总数是 7。
> 
> **输入:** N = 6，K = 0
> T3】输出: 36

**天真法:**解决给定问题最简单的方法是在**【1，N】**范围内生成所有可能的对 **(a，b)** ，如果 **a%b** 的值至少为**K**，那么就统计这个对。检查所有配对后，打印获得的全部配对。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以通过迭代范围**【1，N】**并固定对中的第二个数，即 **b** 进行优化。对于每个固定的 **b** 将有一个 **N/b** 的周期，每个周期可以与**(b–K)**元素组合。所以总共会有**(N/b)*(b–K)**元素。现在对于剩余的元素 **N%b** 将有**最大值(0，N % b–k+1)**对。按照以下步骤解决问题:

*   如果 **K** 的值为 **0** ，则打印 **N <sup>2</sup>** 作为有效对的合成数。
*   初始化变量，比如说**和**为 **0** ，存储结果对的计数。
*   [使用变量 **b** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【K+1，N】**，并执行以下步骤:
    *   将**(不适用)*(b–K)**的值添加到变量**和**中。
    *   将**(N % b–K+1)**或 **0** 的最大值加到变量**和**上。
*   执行上述步骤后，打印**和**的值作为结果对计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the number of pairs
// (a, b) such that a%b is at least K
int countTotalPairs(int N, int K)
{
    // Base Case
    if (K == 0) {
        return N * N;
    }

    // Stores resultant count of pairs
    int ans = 0;

    // Iterate over the range [K + 1, N]
    for (int b = K + 1; b <= N; b++) {

        // Find the cycled elements
        ans += (N / b) * (b - K);

        // Find the remaining elements
        ans += max(N % b - K + 1, 0);
    }

    // Return the resultant possible
    // count of pairs
    return ans;
}

// Driver Code
int main()
{
    int N = 5, K = 2;
    cout << countTotalPairs(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.io.*;

class GFG {

  // Function to count the number of pairs
  // (a, b) such that a%b is at least K
  public static int countTotalPairs(int N, int K)
  {

    // Base case
    if (K == 0) {
      return N * N;
    }

    // Stores resultant count of pairs
    int ans = 0;

    // Iterate over the range [K + 1, N]
    for (int i = K + 1; i <= N; i++)
    {

      // Find the cycled element
      ans += (N / i) * (i - K);
      if ((N % i) - K + 1 > 0)
      {

        // Find the remaining element
        ans += (N % i) - K + 1;
      }
    }

    // Return the resultant possible
    // count of pairs
    return ans;
  }

  // Driver code
  public static void main(String[] args)
  {
    int N = 5, K = 2;
    System.out.println(countTotalPairs(N, K));
  }
}

// This code is contributed by maddler.
```

## 蟒蛇 3

```
# Python program for the above approach;

# Function to count the number of pairs
# (a, b) such that a%b is at least K
def countTotalPairs(N, K):
    # Base Case
    if (K == 0) :
        return N * N

    # Stores resultant count of pairs
    ans = 0

    # Iterate over the range [K + 1, N]
    for b in range(K + 1, N + 1) :

        # Find the cycled elements
        ans += (N // b) * (b - K)

        # Find the remaining elements
        ans += max(N % b - K + 1, 0)

    # Return the resultant possible
    # count of pairs
    return ans

# Driver Code

N = 5
K = 2
print(countTotalPairs(N, K))

# This code is contributed by _saurabh_jaiswal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count the number of pairs
// (a, b) such that a%b is at least K
static int countTotalPairs(int N, int K)
{
    // Base Case
    if (K == 0) {
        return N * N;
    }

    // Stores resultant count of pairs
    int ans = 0;

    // Iterate over the range [K + 1, N]
    for (int b = K + 1; b <= N; b++) {

        // Find the cycled elements
        ans += (N / b) * (b - K);

        // Find the remaining elements
        ans += Math.Max(N % b - K + 1, 0);
    }

    // Return the resultant possible
    // count of pairs
    return ans;
}

// Driver Code
public static void Main()
{
    int N = 5, K = 2;
    Console.Write(countTotalPairs(N, K));
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach;

        // Function to count the number of pairs
        // (a, b) such that a%b is at least K
        function countTotalPairs(N, K) {
            // Base Case
            if (K == 0) {
                return N * N;
            }

            // Stores resultant count of pairs
            let ans = 0;

            // Iterate over the range [K + 1, N]
            for (let b = K + 1; b <= N; b++) {

                // Find the cycled elements
                ans += Math.floor((N / b) * (b - K));

                // Find the remaining elements
                ans += Math.max(N % b - K + 1, 0);
            }

            // Return the resultant possible
            // count of pairs
            return ans;
        }

        // Driver Code

        let N = 5, K = 2;
        document.write(countTotalPairs(N, K));

   // This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
7
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)