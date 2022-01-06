# 最大化第 k 个索引处的值，创建相邻差为 1 且总和小于 M 的 N 大小数组

> 原文:[https://www . geeksforgeeks . org/最大化-价值-at-kth-index-to-create-n-size-array-with-near-difference-1-and-sum-小于-m/](https://www.geeksforgeeks.org/maximize-value-at-kth-index-to-create-n-size-array-with-adjacent-difference-1-and-sum-less-than-m/)

给定三个数字 **N** 、 **K** 和 **M** ，任务是如果正值被分配给所有 **N** 指数，使得值的总和小于 **M** ，并且相邻位置的值之差为 atmost 1，则找到可以分配给 **Kth** 指数的最大值。

**示例:**

> **输入** : N=3，M=10，K=2
> **输出** : 4
> **说明**:赋值的最佳方式是{3，4，3}。总和= 3+4+3 = 10≤m。
> 注意:{3，4，2}不是有效的分布，因为 4-2=2 > 1
> 
> **输入** : N=7，M=100，K=6
> 输出 : 16

**方法:**以下观察有助于解决问题:

1.  如果 **X** 被分配在 **Kth** 指数，那么，最优分配如下:
    1.  如果 **X** 小于 **K-1** ，则左边的最佳分布为 **(X-1)、(X-2)、……(X-K+1)、(1)、(1)……**
    2.  否则就是 **(X-1)、(X-2)、……(X-K+1)**。
    3.  如果 **X** 小于 **N-K** ，则左边的最佳分布为 **(X-1)、(X-2)、……(X-N+K)、1、1……**
    4.  否则就是 **(X-1)、(X-2)、……(X-N+K)**。
2.  [使用 AP 系列](https://www.geeksforgeeks.org/program-sum-arithmetic-series/)，**(X-1)+(X-2)+(X-3)+……+(X-Y)**之和为**Y *(X-1+X-Y)/2 = Y *(2X-Y-1)/2**

**X** 的最大值可以用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)的概念来计算。按照以下步骤解决问题:

1.  初始化一个变量 **ans** 到 **-1** ，存储答案。
2.  初始化两个变量**低**到 **0** 和**高**到 **M** ，用于二进制搜索。
3.  [循环，同时](https://www.geeksforgeeks.org/loops-in-c-and-cpp/) **低**不大于**高**，并执行以下操作:
    1.  计算**中间**作为**高**和**低**的平均值。
    2.  将变量**值**初始化为 **0** ，以存储当前的分配总和。
    3.  将 **L** (在 **K** 左边的索引数)初始化为 **K-1** 、 **R** (在 **K** 右边的索引数)初始化为 **N-K** 。
    4.  将**中间**的值加到**值**上。
    5.  如上所述，在 **K** 的左侧和右侧分配数字，并将它们的值添加到**值**中。
    6.  如果 val 小于 **M** ，更新 ans 为 **ans** 和**中间**的最大值。将**低**更新为**中+1** 。
    7.  否则，将**高**更新为**中 1** 。
4.  返回〔t0〕年〔t1〕年。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
// Function to calculate maximum value that can be placed at
// the Kth index in a distribution in which difference of
// adjacent elements is less than 1 and total sum of
// distribution is M.
int calculateMax(int N, int M, int K)
{
    // variable to store final answer
    int ans = -1;
    // variables for binary search
    int low = 0, high = M;
    // Binary search
    while (low <= high) {
        // variable for binary search
        int mid = (low + high) / 2;
        // variable to store total sum of array
        int val = 0;
        // number of indices on the left excluding the Kth
        // index
        int L = K - 1;
        // number of indices on the left excluding the Kth
        // index
        int R = N - K;
        // add mid to final sum
        val += mid;
        // distribution on left side is possible
        if (mid >= L) {
            // sum of distribution on the left side
            val += (L) * (2 * mid - L - 1) / 2;
        }
        else {
            // sum of distribution on the left side with
            // (L-mid) 1s
            val += mid * (mid - 1) / 2 + (L - mid);
        }
        // distribution on right side is possible
        if (mid >= R) {
            // sum of distribution on the right side
            val += (R) * (2 * mid - R - 1) / 2;
        }
        else {
            // sum of distribution on the left side with
            // (R-mid) 1s
            val += mid * (mid - 1) / 2 + (R - mid);
        }
        // Distribution is valid
        if (val <= M) {
            ans = max(ans, mid);
            low = mid + 1;
        }
        else
            high = mid - 1;
    }
    // return answer
    return ans;
}
// Driver code
int main()
{
    // Input
    int N = 7, M = 100, K = 6;

    // Function call
    cout << calculateMax(N, M, K) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

  // Function to calculate maximum value that can be
  // placed at
  // the Kth index in a distribution in which difference
  // of adjacent elements is less than 1 and total sum of
  // distribution is M.
  public static int calculateMax(int N, int M, int K)
  {

    // variable to store final answer
    int ans = -1;

    // variables for binary search
    int low = 0, high = M;

    // Binary search
    while (low <= high)
    {

      // variable for binary search
      int mid = (low + high) / 2;

      // variable to store total sum of array
      int val = 0;

      // number of indices on the left excluding the
      // Kth index
      int L = K - 1;

      // number of indices on the left excluding the
      // Kth index
      int R = N - K;

      // add mid to final sum
      val += mid;

      // distribution on left side is possible
      if (mid >= L)
      {

        // sum of distribution on the left side
        val += (L) * (2 * mid - L - 1) / 2;
      }
      else
      {

        // sum of distribution on the left side with
        // (L-mid) 1s
        val += mid * (mid - 1) / 2 + (L - mid);
      }

      // distribution on right side is possible
      if (mid >= R)
      {

        // sum of distribution on the right side
        val += (R) * (2 * mid - R - 1) / 2;
      }
      else
      {

        // sum of distribution on the left side with
        // (R-mid) 1s
        val += mid * (mid - 1) / 2 + (R - mid);
      }

      // Distribution is valid
      if (val <= M) {
        ans = Math.max(ans, mid);
        low = mid + 1;
      }
      else
        high = mid - 1;
    }

    // return answer
    return ans;
  }

  // Driver code
  public static void main(String[] args)
  {
    // Input
    int N = 7, M = 100, K = 6;

    // Function call
    System.out.println(calculateMax(N, M, K));
  }
}

// This code is contributed by lokeshpotta20.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate maximum value
# that can be placed at the Kth index
# in a distribution in which difference
# of adjacent elements is less than 1
# and total sum of distribution is M.
def calculateMax(N, M, K):

    # Variable to store final answer
    ans = -1

    # Variables for binary search
    low = 0
    high = M

    # Binary search
    while (low <= high):

        # Variable for binary search
        mid = (low + high) / 2

        # Variable to store total sum of array
        val = 0

        # Number of indices on the left excluding
        # the Kth index
        L = K - 1

        # Number of indices on the left excluding
        # the Kth index
        R = N - K

        # Add mid to final sum
        val += mid

        # Distribution on left side is possible
        if (mid >= L):

            # Sum of distribution on the left side
            val += (L) * (2 * mid - L - 1) / 2

        else:

            # Sum of distribution on the left side
            # with (L-mid) 1s
            val += mid * (mid - 1) / 2 + (L - mid)

        # Distribution on right side is possible
        if (mid >= R):

            # Sum of distribution on the right side
            val += (R) * (2 * mid - R - 1) / 2

        else:

            # Sum of distribution on the left side with
            # (R-mid) 1s
            val += mid * (mid - 1) / 2 + (R - mid)

        # Distribution is valid
        if (val <= M):
            ans = max(ans, mid)
            low = mid + 1
        else:
            high = mid - 1

    # Return answer
    return int(ans)

# Driver code

# Input
N = 7
M = 100
K = 6

# Function call
print(calculateMax(N, M, K));

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to calculate maximum value that can be
  // placed at
  // the Kth index in a distribution in which difference
  // of adjacent elements is less than 1 and total sum of
  // distribution is M.
  public static int calculateMax(int N, int M, int K)
  {

    // variable to store final answer
    int ans = -1;

    // variables for binary search
    int low = 0, high = M;

    // Binary search
    while (low <= high)
    {

      // variable for binary search
      int mid = (low + high) / 2;

      // variable to store total sum of array
      int val = 0;

      // number of indices on the left excluding the
      // Kth index
      int L = K - 1;

      // number of indices on the left excluding the
      // Kth index
      int R = N - K;

      // add mid to final sum
      val += mid;

      // distribution on left side is possible
      if (mid >= L)
      {

        // sum of distribution on the left side
        val += (L) * (2 * mid - L - 1) / 2;
      }
      else
      {

        // sum of distribution on the left side with
        // (L-mid) 1s
        val += mid * (mid - 1) / 2 + (L - mid);
      }

      // distribution on right side is possible
      if (mid >= R)
      {

        // sum of distribution on the right side
        val += (R) * (2 * mid - R - 1) / 2;
      }
      else
      {

        // sum of distribution on the left side with
        // (R-mid) 1s
        val += mid * (mid - 1) / 2 + (R - mid);
      }

      // Distribution is valid
      if (val <= M) {
        ans = Math.Max(ans, mid);
        low = mid + 1;
      }
      else
        high = mid - 1;
    }

    // return answer
    return ans;
  }

// Driver code
static void Main()
{

    // Input
    int N = 7, M = 100, K = 6;

    // Function call
    Console.Write(calculateMax(N, M, K));

}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>
        // JavaScript program for the above approach

        // Function to calculate maximum value that can be placed at
        // the Kth index in a distribution in which difference of
        // adjacent elements is less than 1 and total sum of
        // distribution is M.
        function calculateMax(N, M, K)
        {

            // variable to store final answer
            var ans = -1;

            // variables for binary search
            var low = 0, high = M;

            // Binary search
            while (low <= high)
            {

                // variable for binary search
                var mid = parseInt((low + high) / 2);

                // variable to store total sum of array
                var val = 0;

                // number of indices on the left excluding the Kth
                // index
                var L = K - 1;

                // number of indices on the left excluding the Kth
                // index
                var R = N - K;

                // add mid to final sum
                val += mid;

                // distribution on left side is possible
                if (mid >= L)
                {

                    // sum of distribution on the left side
                    val += (L) * ((2 * mid - L - 1) / 2);
                }
                else
                {

                    // sum of distribution on the left side with
                    // (L-mid) 1s
                    val += mid * parseInt((mid - 1) / 2) + (L - mid);
                }

                // distribution on right side is possible
                if (mid >= R)
                {

                    // sum of distribution on the right side
                    val += (R) * (2 * mid - R - 1) / 2;
                }
                else
                {

                    // sum of distribution on the left side with
                    // (R-mid) 1s
                    val += mid * parseInt((mid - 1) / 2) + (R - mid);
                }

                // Distribution is valid
                if (val <= M)
                {
                    ans = Math.max(ans, mid);
                    low = mid + 1;
                }
                else
                    high = mid - 1;
            }

            // return answer
            return ans;
        }

        // Driver code

        // Input
        let N = 7, M = 100, K = 6;

        // Function call
        document.write(calculateMax(N, M, K));

// This code is contributed by lokeshpotta20.
    </script>
```

**Output**

```
16
```

***时间复杂度:** O(LogM)*
***辅助空间:** O(1)*