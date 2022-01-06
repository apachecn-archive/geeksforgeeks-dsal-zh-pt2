# 通过在每一步增加 1 或加倍来最小化从 0 到 K 的步数

> 原文:[https://www . geeksforgeeks . org/通过每一步增加 1 或增加一倍来最小化从 0 到 k 的步骤/](https://www.geeksforgeeks.org/minimize-steps-to-reach-k-from-0-by-adding-1-or-doubling-at-each-step/)

给定一个正整数 **K** ，任务是找到以下两种类型的最小运算次数，要求将 0 改为 K:

*   给操作数加一
*   将操作数乘以 2。

**例:**

> **输入:** K = 1
> **输出:** 1
> **解释:**
> 步骤 1: 0 + 1 = 1 = K
> **输入:** K = 4
> **输出:** 3
> **解释:**
> 步骤 1: 0 + 1 = 1，
> 步骤 2: 1 * 2 = 2，
> 步骤 3:2 * 2 = 4 = 4

**进场:**

*   如果 **K** 是奇数，最后一步一定是加 1。
*   如果 **K** 是偶数，最后一步是乘以 2，以最小化步数。
*   创建一个 dp[]表，在每个 **dp[i]** 中存储到达 **i** 所需的最少步骤。

> ![dp[i] =\begin{cases} dp[i - 1] + 1 & \text{; if i is odd} \\ dp[\frac{i}{2}] + 1 & \text{; if i is even} \end{cases}  ](img/e38b284a382385082b40ec086af72cb9.png "Rendered by QuickLaTeX.com")

以下是上述方法的实现:

## C++

```
// C++ program to implement the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum operations
int minOperation(int k)
{
    // vector dp is initialised
    // to store the steps
    vector<int> dp(k + 1, 0);

    for (int i = 1; i <= k; i++) {

        dp[i] = dp[i - 1] + 1;

        // For all even numbers
        if (i % 2 == 0) {
            dp[i]
                = min(dp[i],
                      dp[i / 2] + 1);
        }
    }
    return dp[k];
}

// Driver Code
int main()
{
    int K = 12;
    cout << minOperation(k);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the above approach
class GFG{

// Function to find minimum operations
static int minOperation(int k)
{

    // dp is initialised
    // to store the steps
    int dp[] = new int[k + 1];

    for(int i = 1; i <= k; i++)
    {
       dp[i] = dp[i - 1] + 1;

       // For all even numbers
       if (i % 2 == 0)
       {
           dp[i] = Math.min(dp[i], dp[i / 2] + 1);
       }
    }
    return dp[k];
}

// Driver Code
public static void main (String []args)
{
    int K = 12;
    System.out.print( minOperation(K));
}
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 program to implement the above approach

# Function to find minimum operations
def minOperation(k):

    # dp is initialised
    # to store the steps
    dp = [0] * (k + 1)

    for i in range(1, k + 1):
        dp[i] = dp[i - 1] + 1

        # For all even numbers
        if (i % 2 == 0):
            dp[i]= min(dp[i], dp[i // 2] + 1)

    return dp[k]

# Driver Code
if __name__ == '__main__':

    k = 12

    print(minOperation(k))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement the above approach
using System;
class GFG{

// Function to find minimum operations
static int minOperation(int k)
{

    // dp is initialised
    // to store the steps
    int []dp = new int[k + 1];

    for(int i = 1; i <= k; i++)
    {
        dp[i] = dp[i - 1] + 1;

        // For all even numbers
        if (i % 2 == 0)
        {
            dp[i] = Math.Min(dp[i], dp[i / 2] + 1);
        }
    }
    return dp[k];
}

// Driver Code
public static void Main()
{
    int K = 12;
    Console.Write(minOperation(K));
}
}

// This code is contributed by Nidhi_Biet
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

// Function to find minimum operations
function minOperation(k)
{

    // dp is initialised
    // to store the steps
    let dp = Array.from({length: k+1}, (_, i) => 0);

    for(let i = 1; i <= k; i++)
    {
       dp[i] = dp[i - 1] + 1;

       // For all even numbers
       if (i % 2 == 0)
       {
           dp[i] = Math.min(dp[i], dp[i / 2] + 1);
       }
    }
    return dp[k];
}

  // Driver Code   
    let K = 12;
    document.write( minOperation(K));

 // This code is contributed by target_2.
</script>
```

**Output:** 

```
5
```