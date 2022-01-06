# 计算从起点石到达终点的方式，每一步最多跳 K 次

> 原文:[https://www . geesforgeks . org/count-way-to-end-start-stone-with-顶多-k-jump-at-at-step/](https://www.geeksforgeeks.org/count-ways-to-reach-end-from-start-stone-with-at-most-k-jumps-at-each-step/)

从左到右连续给定 **N** 颗石头。从每块石头中，最多可以跳到 **K** 块石头。任务是找到从**某物**石头到达**第 n 个**石头的途径总数。
**举例:**

> **输入:** N = 5，s = 2，K = 2
> **输出:**总途径= 3
> **解释:**
> 假设 s1、s2、s3、s4、s5 是石头。从第二块石头到第五块石头的可能路径:
> S2->S3->S4->S5
> S2->S4->S5
> S2->S3->S5
> 因此总路数= 3
> **输入:** N = 8，s = 1，K = 3
> **输出:**总路数= 44

**进场:**

1.  假设 **dp[i]** 是用石头到达**的路数。**
2.  既然有大气 **K 跳**，那么之前所有 **K** 的石头都可以到达带有石头的**。**
3.  迭代所有可能的 **K 跳跃**，并继续将这个可能的组合添加到[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **dp[]** 中。
4.  那么从**石到达**第 N 个**节点的可能途径总数将是**DP【N-1】**。**
5.  例如:

> 假设 N = 5，s = 2，K = 2，那么我们必须从某块石头到达第 N 块石头。
> 让 dp[N+1]是存储从 sth stone 到达第 N 个 Node 的路径数的数组。
> 最初，dp[] = { 0，0，0，0，0，0 }和 dp[s] = 1，然后
> dp[] = { 0，0，1，0，0，0 }
> 到达第三个，
> 只有 1 条路，最多 2 跳，即从石头 2 开始(跳= 1)。更新 dp[3] = dp[2]
> dp[] = { 0，0，1，1，0，0 }
> 到达第 4 个石，
> 最多跳 2 次的两种方式，即从石 2(跳= 2)和石 3(跳= 1)。更新 dp[4] = dp[3] + dp[2]
> dp[] = { 0，0，1，1，2，0 }
> 到达第 5 石，
> 最多跳 2 次的两种方式，即从石 3(跳= 2)和石 4(跳= 1)。更新 dp[5] = dp[4] + dp[3]
> dp[] = { 0，0，1，1，2，3 }
> 现在 dp[N] = 3 是从某个石头到达第 N 个石头的途径数。

以下是上述方法的实现:

## C++

```
// C++ program to find total no.of ways
// to reach nth step
#include "bits/stdc++.h"
using namespace std;

// Function which returns total no.of ways
// to reach nth step from sth steps
int TotalWays(int n, int s, int k)
{
    // Initialize dp array with 0s.
    vector<int> dp(n,0);

    // Initialize (s-1)th index to 1
    dp[s - 1] = 1;

    // Iterate a loop from s to n
    for (int i = s; i < n; i++) {

        // starting range for counting ranges
        int idx = max(s - 1, i - k);

        // Calculate Maximum moves to
        // Reach ith step
        for (int j = idx; j < i; j++) {
            dp[i] += dp[j];
        }
    }

    // For nth step return dp[n-1]
    return dp[n - 1];
}

// Driver Code
int main()
{
    // no of steps
    int n = 5;

    // Atmost steps allowed
    int k = 2;

    // starting range
    int s = 2;
    cout << "Total Ways = "
         << TotalWays(n, s, k);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find total no.of ways
// to reach nth step
class GFG{

// Function which returns total no.of ways
// to reach nth step from sth steps
static int TotalWays(int n, int s, int k)
{
    // Initialize dp array
    int []dp = new int[n];

    // Initialize (s-1)th index to 1
    dp[s - 1] = 1;

    // Iterate a loop from s to n
    for (int i = s; i < n; i++) {

        // starting range for counting ranges
        int idx = Math.max(s - 1, i - k);

        // Calculate Maximum moves to
        // Reach ith step
        for (int j = idx; j < i; j++) {
            dp[i] += dp[j];
        }
    }

    // For nth step return dp[n-1]
    return dp[n - 1];
}

// Driver Code
public static void main(String[] args)
{
    // no of steps
    int n = 5;

    // Atmost steps allowed
    int k = 2;

    // starting range
    int s = 2;
    System.out.print("Total Ways = "
         + TotalWays(n, s, k));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python 3 program to find total no.of ways
# to reach nth step

# Function which returns total no.of ways
# to reach nth step from sth steps
def TotalWays(n, s, k):

    # Initialize dp array
    dp = [0]*n

    # Initialize (s-1)th index to 1
    dp[s - 1] = 1

    # Iterate a loop from s to n
    for i in range(s, n):

        # starting range for counting ranges
        idx = max(s - 1, i - k)

        # Calculate Maximum moves to
        # Reach ith step
        for j in range( idx, i) :
            dp[i] += dp[j]

    # For nth step return dp[n-1]
    return dp[n - 1]

# Driver Code
if __name__ == "__main__":
    # no of steps
    n = 5

    # Atmost steps allowed
    k = 2

    # starting range
    s = 2
    print("Total Ways = ", TotalWays(n, s, k))

# This code is contributed by chitranayal
```

## C#

```
// C# program to find total no.of ways
// to reach nth step
using System;

class GFG{

    // Function which returns total no.of ways
    // to reach nth step from sth steps
    static int TotalWays(int n, int s, int k)
    {
        // Initialize dp array
        int []dp = new int[n];

        // Initialize (s-1)th index to 1
        dp[s - 1] = 1;

        // Iterate a loop from s to n
        for (int i = s; i < n; i++) {

            // starting range for counting ranges
            int idx = Math.Max(s - 1, i - k);

            // Calculate Maximum moves to
            // Reach ith step
            for (int j = idx; j < i; j++) {
                dp[i] += dp[j];
            }
        }

        // For nth step return dp[n-1]
        return dp[n - 1];
    }

    // Driver Code
    public static void Main(string[] args)
    {
        // no of steps
        int n = 5;

        // Atmost steps allowed
        int k = 2;

        // starting range
        int s = 2;
        Console.Write("Total Ways = "+ TotalWays(n, s, k));
    }
}

// This code is contributed by Yash_R
```

## java 描述语言

```
<script>
// Javascript program to find total no.of ways
// to reach nth step

// Function which returns total no.of ways
// to reach nth step from sth steps
function TotalWays(n, s, k)
{
    // Initialize dp array
    let dp = new Array(n);

    // filling all the elements with 0
    dp.fill(0);

    // Initialize (s-1)th index to 1
    dp[s - 1] = 1;

    // Iterate a loop from s to n
    for (let i = s; i < n; i++) {

        // starting range for counting ranges
        let idx = Math.max(s - 1, i - k);

        // Calculate Maximum moves to
        // Reach ith step
        for (let j = idx; j < i; j++) {
            dp[i] += dp[j];
        }
    }

    // For nth step return dp[n-1]
    return dp[n - 1];
}

// Driver Code

    // no of steps
    let n = 5;

    // Atmost steps allowed
    let k = 2;

    // starting range
    let s = 2;
    document.write("Total Ways = " + TotalWays(n, s, k));

    // This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
Total Ways = 3
```

**时间复杂度:** O(N <sup>2</sup> ，其中 N 为石子数。
**辅助空间:** O(N)