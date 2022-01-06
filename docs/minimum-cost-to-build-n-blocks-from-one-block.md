# 从一个区块建造 N 个区块的最小成本

> 原文:[https://www . geesforgeks . org/从一个块构建 n 个块的最低成本/](https://www.geeksforgeeks.org/minimum-cost-to-build-n-blocks-from-one-block/)

给定数字 N，任务是通过执行以下操作从 1 个块构建 N 个块:

1.  容器内存在的块数翻倍，该操作的成本为`X`。
2.  将容器内存在的块数增加 1，该操作的成本为`Y`。
3.  将容器内存在的块数减少一个，该操作的成本为`Z`。

**示例:**

> **输入:** N = 5，X = 2，Y = 1，Z = 3
> **输出:** 4
> **说明:**
> 在第一次操作中只需将块数增加 1，成本= 1，块数= 2
> 在第二次操作中将块数增加一倍，成本= 3，块数= 4
> 在第三次操作中再次将 _ 块数增加 1，成本= 4，块数= 5
> 所以最小成本= 4
> 
> **输入:** N = 7，X = 1，Y = 7，Z = 2
> T3】输出: 5

**进场:**

*   让`f(i)`表示构建`i`块的最小成本。所以 **`f(i)` = `min(f(2*i)+X, f(i-1)+Y, f(i+1)+Z)`**
    这里电流值取决于它的下一个值以及它的前一个值，但是你知道在动态编程中电流值只取决于它的前一个值。所以试着把它的下一个值转换成它的前一个值。我们可以将`f(2*i)`写成`f(i/2)`，因为当我们已经构建了 i/2 块时，我们可以将当前块的数量增加一倍，或者将块的数量增加 1，或者将块的数量减少 1。这里不需要计算`f(2*i)`。
    现在

    ```
    f(i) = min(f(i/2)+X, f(i-1)+Y, f(i+1)+Z)
    ```

*   如果`i`是偶数，那么`(i+1)`一定是奇数。我们只能通过执行增量操作和双重操作来构建`(i)`块，那么为什么不需要执行减量操作呢？
    这是因为`(i+1)`是奇数。因此，如果您通过执行增量操作来构建`(i+1)`区块，则确认我们已经构建了`i`区块，这意味着我们构建`i`区块的成本最低。如果我们执行任何其他操作，它必须增加你的最佳成本，这是无关紧要的。所以当 I 为偶数时的递推关系:

    ```
    f(i)=min(f(i/2)+X, f(i-1)+Y)
    ```

*   If `i` is odd then `(i+1)` must be even. We can build `(i+1)` blocks only by performing double operation or decrement operation why not increment operation?
    This is because if you have already built `i` blocks then no need to build `(i+1)` blocks because it will add more cost. So we can calculate `f(i+1)=f((i+1)/2)+ X.` So recurrence relation when i is odd:

    ```
    f(i)=min(f(i-1)+Y, f( (i+1)/2)+X+Z)
    ```

    以下是上述方法的实现:

    ## 卡片打印处理机（Card Print Processor 的缩写）

    ```
    // C++ program to Minimum cost
    // to build N blocks from one block

    #include <bits/stdc++.h>
    using namespace std;

    // Function to calculate
    // min cost to build N blocks
    int minCost(int n, int x, int y, int z)
    {
        int dp[n + 1] = { 0 };

        // Initialize base case
        dp[0] = dp[1] = 0;

        for (int i = 2; i <= n; i++) {
            // Recurence when
            // i is odd
            if (i % 2 == 1) {
                dp[i] = min(
                    dp[(i + 1) / 2] + x + z,
                    dp[i - 1] + y);
            }
            // Recurence when
            // i is even
            else {
                dp[i] = min(dp[i / 2] + x,
                            dp[i - 1] + y);
            }
        }

        return dp[n];
    }

    // Driver code
    int main()
    {
        int n = 5, x = 2, y = 1, z = 3;
        cout << minCost(n, x, y, z) << endl;

        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // Java program to Minimum cost
    // to build N blocks from one block
    class GFG
    {

    // Function to calculate
    // min cost to build N blocks
    static int minCost(int n, int x, int y, int z)
    {
        int dp[] = new int[n + 1];

        // Initialize base case
        dp[0] = dp[1] = 0;

        for (int i = 2; i <= n; i++)
        {
            // Recurence when
            // i is odd
            if (i % 2 == 1)
            {
                dp[i] = Math.min(
                    dp[(i + 1) / 2] + x + z,
                    dp[i - 1] + y);
            }
            // Recurence when
            // i is even
            else 
            {
                dp[i] = Math.min(dp[i / 2] + x,
                            dp[i - 1] + y);
            }
        }

        return dp[n];
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 5, x = 2, y = 1, z = 3;
        System.out.print(minCost(n, x, y, z) +"\n");

    }
    }

    // This code is contributed by Rajput-Ji
    ```

    ## 计算机编程语言

    ```
    # python3 program to Minimum cost
    # to build N blocks from one block

    # Function to calculate
    # min cost to build N blocks
    def minCost(n, x, y, z):
        dp = [0] * (n + 1)

        # Initialize base case
        dp[0] = dp[1] = 0

        for i in range(2, n + 1):

            # Recurence when
            # i is odd
            if (i % 2 == 1):
                dp[i] = min(dp[(i + 1) // 2] + x + z, dp[i - 1] + y)

            # Recurence when
            # i is even
            else:
                dp[i] = min(dp[i // 2] + x, dp[i - 1] + y)

        return dp[n]

    # Driver code
    n = 5
    x = 2
    y = 1
    z = 3
    print(minCost(n, x, y, z))

    # This code is contributed by mohit kumar 29
    ```

    ## C#

    ```
    // C# program to Minimum cost
    // to build N blocks from one block
    using System;

    class GFG
    {

    // Function to calculate
    // min cost to build N blocks
    static int minCost(int n, int x, int y, int z)
    {
        int []dp = new int[n + 1];

        // Initialize base case
        dp[0] = dp[1] = 0;

        for (int i = 2; i <= n; i++)
        {
            // Recurence when
            // i is odd
            if (i % 2 == 1)
            {
                dp[i] = Math.Min(
                    dp[(i + 1) / 2] + x + z,
                    dp[i - 1] + y);
            }

            // Recurence when
            // i is even
            else
            {
                dp[i] = Math.Min(dp[i / 2] + x,
                            dp[i - 1] + y);
            }
        }
        return dp[n];
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 5, x = 2, y = 1, z = 3;
        Console.Write(minCost(n, x, y, z) +"\n");
    }
    }

    // This code is contributed by PrinciRaj1992
    ```

    **Output:**

    ```
    4

    ```