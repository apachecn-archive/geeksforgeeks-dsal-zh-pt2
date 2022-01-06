# 计算使用指定尺寸的瓷砖铺设 N 长板材的方法

> 原文:[https://www . geesforgeks . org/count-way-to-tile-an-n-length-board-using-tiles-of-specified-dimensions/](https://www.geeksforgeeks.org/count-ways-to-tile-an-n-length-board-using-tiles-of-specified-dimensions/)

给定一个整数 **N** ，任务是平铺一块尺寸为 **N * 1** 的板，任务是统计使用尺寸为 **1 * 1** 和 **2 * 1** 的板进行平铺的方式数。

**示例:**

> **输入:** N = 2
> **输出:** 5
> **解释:**
> 将 1×1 块瓷砖水平放置，另 1×1 块瓷砖垂直放置，平铺 2×1 大小的木板。
> 垂直铺 1×1 瓷砖，水平铺 1×1 瓷砖，铺 2×1 尺寸的木板。
> 以水平方式放置 1×1 瓷砖，以水平方式放置另一个 1×1 瓷砖，从而平铺尺寸为 2×1 的板。
> 垂直放置 1×1 块瓷砖，再垂直放置 1×1 块瓷砖，贴上 2×1 的木板。
> 水平放置 2×1 瓷砖，平铺 2×1 尺寸的板材。
> 因此，要求输出为 5。
> 
> **输入:**N = 1
> T3】输出: 2

**方法:**使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)可以解决问题。想法是将**N×1**板分成更小的板，然后计算平铺更小的板的方法。最后，打印平铺**N×1**板的方式总数。按照以下步骤解决问题:

*   以下是放置第一个图块的三种方法:
    *   将 **1 x 1** 瓷砖垂直放置。
    *   水平放置**1×1**瓷砖。
    *   水平放置**2×1**瓷砖。
*   因此，解决问题的递推关系如下:

> 碳纳米管(N) = 2 *碳纳米管(N–1)+碳纳米管(N–2)

*   初始化一个数组，比如说， **dp[]** ，其中 **dp[i]** 存储平铺 **i x 1** 板的方式数。
*   迭代范围**【2，N】**并使用[制表方法](https://www.geeksforgeeks.org/tabulation-vs-memoization/)填充数组 **dp[]** 。
*   最后，打印**DP【N】**的值。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the ways to tile N * 1
// board using 1 * 1 and 2 * 1 tiles
long countWaysToTileBoard(long N)
{

    // dp[i]: Stores count of ways to tile
    // i * 1 board using given tiles
    long dp[N + 1];

    // Base Case
    dp[0] = 1;
    dp[1] = 2;

    // Iterate over the range [2, N]
    for (int i = 2; i <= N; i++) {

        // Fill dp[i] using
        // the recurrence relation
        dp[i] = (2 * dp[i - 1]
                    + dp[i - 2] );
    }

    cout << dp[N];
}

// Driver Code
int main()
{
    // Given N
    long N = 2;

    // Function Call
    countWaysToTileBoard(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to count the ways to tile N * 1
// board using 1 * 1 and 2 * 1 tiles
static void countWaysToTileBoard(int N)
{

    // dp[i]: Stores count of ways to tile
    // i * 1 board using given tiles
    int dp[] = new int[N + 1];

    // Base Case
    dp[0] = 1;
    dp[1] = 2;

    // Iterate over the range [2, N]
    for(int i = 2; i <= N; i++)
    {

        // Fill dp[i] using
        // the recurrence relation
        dp[i] = (2 * dp[i - 1] +
                     dp[i - 2]);
    }
    System.out.print(dp[N]);
}

// Driver Code
public static void main (String[] args)
{

    // Given N
    int N = 2;

    // Function Call
    countWaysToTileBoard(N);
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count the ways to tile N * 1
# board using 1 * 1 and 2 * 1 tiles
def countWaysToTileBoard( N) :

    # dp[i]: Stores count of ways to tile
    # i * 1 board using given tiles
    dp = [0]*(N + 1)

    # Base Case
    dp[0] = 1
    dp[1] = 2

    # Iterate over the range [2, N]
    for i in range(2, N + 1) :

        # Fill dp[i] using
        # the recurrence relation
        dp[i] = (2 * dp[i - 1] + dp[i - 2] )

    print(dp[N])

# Driver Code
if __name__ == "__main__" :

    # Given N
    N = 2

    # Function Call
    countWaysToTileBoard(N)

  # This code is contributed by jana_sayantan 
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to count the ways to tile N * 1
// board using 1 * 1 and 2 * 1 tiles
static void countWaysToTileBoard(int N)
{

    // dp[i]: Stores count of ways to tile
    // i * 1 board using given tiles
    int []dp = new int[N + 1];

    // Base Case
    dp[0] = 1;
    dp[1] = 2;

    // Iterate over the range [2, N]
    for(int i = 2; i <= N; i++)
    {

        // Fill dp[i] using
        // the recurrence relation
        dp[i] = (2 * dp[i - 1] +
                     dp[i - 2]);
    }
    Console.Write(dp[N]);
}

// Driver Code
public static void Main(String[] args)
{

    // Given N
    int N = 2;

    // Function Call
    countWaysToTileBoard(N);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript program for above approach

// Function to count the ways to tile N * 1
// board using 1 * 1 and 2 * 1 tiles
function countWaysToTileBoard(N)
{

    // dp[i]: Stores count of ways to tile
    // i * 1 board using given tiles
    let dp = [];

    // Base Case
    dp[0] = 1;
    dp[1] = 2;

    // Iterate over the range [2, N]
    for(let i = 2; i <= N; i++)
    {

        // Fill dp[i] using
        // the recurrence relation
        dp[i] = (2 * dp[i - 1] +
                     dp[i - 2]);
    }
    document.write(dp[N]);
}

// Driver Code

     // Given N
    let N = 2;

    // Function Call
    countWaysToTileBoard(N);

</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)