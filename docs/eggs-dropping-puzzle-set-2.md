# 鸡蛋掉落拼图|第二集

> 原文:[https://www.geeksforgeeks.org/eggs-dropping-puzzle-set-2/](https://www.geeksforgeeks.org/eggs-dropping-puzzle-set-2/)

给定 **N** 鸡蛋和 **K** 楼层，任务是找到所需的最小试验次数，在最坏的情况下，找到所有楼层都安全的楼层。如果从地板上掉下一个鸡蛋不会打破鸡蛋，那么地板是安全的。详情请参考 [n 蛋 k 层](https://www.geeksforgeeks.org/egg-dropping-puzzle-dp-11/)。

**示例:**

> **输入:** N = 2，K = 10
> **输出:** 4
> **说明:**
> 第一次试训是在 4<sup>楼。此后出现了两种情况:</sup>
> 
> 1.  如果鸡蛋破了，我们还剩一个鸡蛋，所以我们还需要三次试验。
> 2.  如果鸡蛋没有破，下一次尝试是从 7 楼开始。同样，出现了两种情况。
> 
> **输入:** N = 2，K = 100
> T3】输出: 14

**先决条件:** [落蛋谜题](https://www.geeksforgeeks.org/egg-dropping-puzzle-dp-11/)
T5】进场:换个方式考虑这个问题:
让**DP【x】【n】**是给定 **n** 个鸡蛋和 **x** 个招式可以检查的最大楼层数。
则方程为:

1.  如果鸡蛋碎了，那么我们可以检查**DP[x–1][n–1]**楼层。
2.  如果鸡蛋没有碎，那么我们可以检查**DP[x–1][n]+1**层。

由于我们需要覆盖 **k** 层，**DP【x】【n】>= k .**
**DP【x】【n】**与组合数量相似，并呈指数级增长至 **k**
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum number
// of trials needed in the worst case
// with n eggs and k floors
int eggDrop(int n, int k)
{
    vector<vector<int> > dp(k + 1, vector<int>(n + 1, 0));

    int x = 0;

    // Fill all the entries in table using
    // optimal substructure property
    while (dp[x][n] < k) {

        x++;
        for (int i = 1; i <= n; i++)
            dp[x][i] = dp[x - 1][i - 1] + dp[x - 1][i] + 1;
    }

    // Return the minimum number of moves
    return x;
}

// Driver code
int main()
{
    int n = 2, k = 36;

    cout << eggDrop(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the minimum number
// of trials needed in the worst case
// with n eggs and k floors
static int eggDrop(int n, int k)
{
    int dp[][] = new int [k + 1][n + 1];

    int x = 0;

    // Fill all the entries in table using
    // optimal substructure property
    while (dp[x][n] < k)
    {

        x++;
        for (int i = 1; i <= n; i++)
            dp[x][i] = dp[x - 1][i - 1] +
                       dp[x - 1][i] + 1;
    }

    // Return the minimum number of moves
    return x;
}

// Driver code
public static void main(String args[])
{
    int n = 2, k = 36;

    System.out.println( eggDrop(n, k));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function to return the minimum number
# of trials needed in the worst case
# with n eggs and k floors
def eggDrop(n, k):
    dp = [[0 for i in range(n + 1)] for
           j in range(k + 1)]

    x = 0;

    # Fill all the entries in table using
    # optimal substructure property
    while (dp[x][n] < k):

        x += 1;
        for i in range(1, n + 1):
            dp[x][i] = dp[x - 1][i - 1] + \
                        dp[x - 1][i] + 1;

    # Return the minimum number of moves
    return x;

# Driver code
if __name__ == '__main__':
    n = 2; k = 36;

    print(eggDrop(n, k));

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the minimum number
// of trials needed in the worst case
// with n eggs and k floors
static int eggDrop(int n, int k)
{
    int [,]dp = new int [k + 1, n + 1];

    int x = 0;

    // Fill all the entries in table using
    // optimal substructure property
    while (dp[x, n] < k)
    {

        x++;
        for (int i = 1; i <= n; i++)
            dp[x, i] = dp[x - 1, i - 1] +
                    dp[x - 1, i] + 1;
    }

    // Return the minimum number of moves
    return x;
}

// Driver code
public static void Main(String []args)
{
    int n = 2, k = 36;

    Console.WriteLine(eggDrop(n, k));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the minimum number
// of trials needed in the worst case
// with n eggs and k floors
function eggDrop(n, k)
{
    let dp = new Array();

    for(let i = 0; i < k + 1; i++){
        dp.push(new Array(n + 1).fill(0))
    }

    let x = 0;

    // Fill all the entries in table using
    // optimal substructure property
    while (dp[x][n] < k) {

        x++;
        for (let i = 1; i <= n; i++)
            dp[x][i] = dp[x - 1][i - 1] + dp[x - 1][i] + 1;
    }

    // Return the minimum number of moves
    return x;
}

// Driver code
let n = 2, k = 36;
document.write(eggDrop(n, k));
</script>
```

**Output:** 

```
8
```

**时间复杂度:**O(NlogK)
T3】空间复杂度: O(N * K)