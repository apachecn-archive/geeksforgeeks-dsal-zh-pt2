# 通过重复减 3 或除 5

将减少 N 到 2 的操作减到最少

> 原文:[https://www . geesforgeks . org/minimum-operations-to-reduce-n-to-2-by-reducing-by-3-or-division-by-5/](https://www.geeksforgeeks.org/minimize-operations-to-reduce-n-to-2-by-repeatedly-reducing-by-3-or-dividing-by-5/)

给定一个正整数 **N** ，任务是找到将 **N** 转换为 **2** 所需的最小操作数，方法是将 **N** 减 **3** 或者如果 **N** 可被 **5** 整除，则将 **N** 除以 **5** 。如果无法将 **N** 降为 **2** ，则打印**-1”**。

**示例:**

> **输入:** N =10
> **输出:** 1
> **说明:**
> 以下是将 N 减少到 2 的操作:
> 
> 1.  将 N 除以 5，将 N 减少到 10/5 = 2。
> 
> 经过以上操作，N 减为 2。因此，所需的最小操作数为 1。
> 
> **输入:**N = 25
> T3】输出: 2

**方法:**给定的问题可以通过使用 [**动态规划**](https://www.geeksforgeeks.org/dynamic-programming/) 来解决，思路是从 **2** 开始迭代，两个操作反向执行，即不做减法，做 **3** 的加法，不做除法，在每个状态下做与 **5** 的乘法，将 **N** 的每个可能值的最小操作数存储在数组 **dp[]** 中

如果达到 **N** 的值，则打印**DP【N】**的值作为最小操作次数。否则，打印 **-1** 。按照以下步骤解决问题:

*   初始化一个辅助数组，说出 **(N + 1)** 大小的 **dp[]** ，用 [**INT_MAX**](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) 初始化所有数组元素。
*   将**DP【2】**的值设置为等于 **0** 。
*   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，将**DP【I】**的值更新为:
    *   dp[i * 5] = min（dp[i * 5]， dp[i] + 1）.
    *   dp[i + 3] = min（dp[i + 3]， dp[i] + 1）.
*   如果**DP【N】**的值为 **INT_MAX** ，则打印 **-1** 。否则，打印**DP【N】**作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of operations to reduce N to 2 by
// dividing N by 5 or decrementing by 3
int minimumOperations(int N)
{
    // Initialize the dp array
    int dp[N + 1];
    int i;

    // Initialize the array dp[]
    for (int i = 0; i <= N; i++) {
        dp[i] = 1e9;
    }

    // For N = 2 number of operations
    // needed is zero
    dp[2] = 0;

    // Iterating over the range [1, N]
    for (i = 2; i <= N; i++) {

        // If it's not possible to
        // create current N
        if (dp[i] == 1e9)
            continue;

        // Multiply with 5
        if (i * 5 <= N) {
            dp[i * 5] = min(dp[i * 5],
                            dp[i] + 1);
        }

        // Adding the value 3
        if (i + 3 <= N) {
            dp[i + 3] = min(dp[i + 3],
                            dp[i] + 1);
        }
    }

    // Checking if not possible to
    // make the number as 2
    if (dp[N] == 1e9)
        return -1;

    // Return the minimum number
    // of operations
    return dp[N];
}

// Driver Code
int main()
{
    int N = 25;
    cout << minimumOperations(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG {

    // Function to find the minimum number
    // of operations to reduce N to 2 by
    // dividing N by 5 or decrementing by 3
    static int minimumOperations(int N)
    {

        // Initialize the dp array
        int[] dp = new int[N + 1];
        int i;

        // Initialize the array dp[]
        for (i = 0; i <= N; i++) {
            dp[i] = (int)1e9;
        }

        // For N = 2 number of operations
        // needed is zero
        dp[2] = 0;

        // Iterating over the range [1, N]
        for (i = 2; i <= N; i++) {

            // If it's not possible to
            // create current N
            if (dp[i] == (int)1e9)
                continue;

            // Multiply with 5
            if (i * 5 <= N) {
                dp[i * 5] = Math.min(dp[i * 5], dp[i] + 1);
            }

            // Adding the value 3
            if (i + 3 <= N) {
                dp[i + 3] = Math.min(dp[i + 3], dp[i] + 1);
            }
        }

        // Checking if not possible to
        // make the number as 2
        if (dp[N] == 1e9)
            return -1;

        // Return the minimum number
        // of operations
        return dp[N];
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 25;

        System.out.println(minimumOperations(N));
    }
}

// This code is contributed by Potta Lokesh
```

## C#

```
// C# program for above approach
using System;

class GFG{

    // Function to find the minimum number
    // of operations to reduce N to 2 by
    // dividing N by 5 or decrementing by 3
    static int minimumOperations(int N)
    {

        // Initialize the dp array
        int[] dp = new int[N + 1];
        int i;

        // Initialize the array dp[]
        for (i = 0; i <= N; i++) {
            dp[i] = (int)1e9;
        }

        // For N = 2 number of operations
        // needed is zero
        dp[2] = 0;

        // Iterating over the range [1, N]
        for (i = 2; i <= N; i++) {

            // If it's not possible to
            // create current N
            if (dp[i] == (int)1e9)
                continue;

            // Multiply with 5
            if (i * 5 <= N) {
                dp[i * 5] = Math.Min(dp[i * 5], dp[i] + 1);
            }

            // Adding the value 3
            if (i + 3 <= N) {
                dp[i + 3] = Math.Min(dp[i + 3], dp[i] + 1);
            }
        }

        // Checking if not possible to
        // make the number as 2
        if (dp[N] == 1e9)
            return -1;

        // Return the minimum number
        // of operations
        return dp[N];
    }

// Driver Code
public static void Main(String[] args)
{
    int N = 25;

    Console.Write(minimumOperations(N));
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>
    // JavaScript Program for the above approach

    // Function to find the minimum number
    // of operations to reduce N to 2 by
    // dividing N by 5 or decrementing by 3
    function minimumOperations(N)
    {

        // Initialize the dp array
        let dp = new Array(N + 1);
        let i;

        // Initialize the array dp[]
        for (i = 0; i <= N; i++) {
            dp[i] = 1e9;
        }

        // For N = 2 number of operations
        // needed is zero
        dp[2] = 0;

        // Iterating over the range [1, N]
        for (i = 2; i <= N; i++) {

            // If it's not possible to
            // create current N
            if (dp[i] == 1e9)
                continue;

            // Multiply with 5
            if (i * 5 <= N) {
                dp[i * 5] = Math.min(dp[i * 5], dp[i] + 1);
            }

            // Adding the value 3
            if (i + 3 <= N) {
                dp[i + 3] = Math.min(dp[i + 3], dp[i] + 1);
            }
        }

        // Checking if not possible to
        // make the number as 2
        if (dp[N] == 1e9)
            return -1;

        // Return the minimum number
        // of operations
        return dp[N];
    }

    // Driver Code

    let N = 25;

    document.write(minimumOperations(N));

// This code is contributed by sanjoy_62.
</script>
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the minimum number
# of operations to reduce N to 2 by
# dividing N by 5 or decrementing by 3
def minimumOperations(N):
    # Initialize the dp array
    dp = [0 for i in range(N + 1)]

    # Initialize the array dp[]
    for i in range(N+1):
        dp[i] = 1000000000

    # For N = 2 number of operations
    # needed is zero
    dp[2] = 0

    # Iterating over the range [1, N]
    for i in range(2,N+1,1):
        # If it's not possible to
        # create current N
        if (dp[i] == 1000000000):
            continue

        # Multiply with 5
        if (i * 5 <= N):
            dp[i * 5] = min(dp[i * 5], dp[i] + 1)

        # Adding the value 3
        if (i + 3 <= N):
            dp[i + 3] = min(dp[i + 3], dp[i] + 1)

    # Checking if not possible to
    # make the number as 2
    if (dp[N] == 1000000000):
        return -1

    # Return the minimum number
    # of operations
    return dp[N]

# Driver Code
if __name__ == '__main__':
    N = 25
    print(minimumOperations(N))
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)