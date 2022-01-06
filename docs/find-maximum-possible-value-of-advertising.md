# 找到广告的最大可能价值

> 原文:[https://www . geesforgeks . org/find-最大可能广告价值/](https://www.geeksforgeeks.org/find-maximum-possible-value-of-advertising/)

给定 **M** 个小时的广告限制**【0，M)** 和 **N** 个广告，每个广告都有开始时间和广告价值。每个广告为 **1 分钟**长。任务是如果两个广告之间的时间差必须至少为 **K** 分钟，则找到可实现的最大可能广告值。

**示例:**

> **输入:** Arr[][] = {{0，10}，{4，10}，{5，30 } }
> N = 3
> K = 4
> M = 6
> **输出:** 40
> 要么我们从 0 和 4 开始拍广告，要么从 0 和 5 开始拍广告。
> 如果取 0 和 5 对，最大值为 40。
> 
> **输入:** Arr[][] = {{0，10}，{4，110}，{5，30 } }
> N = 3
> K = 4
> M = 6
> **输出:** 120

**进场:**

*   我们将使用动态编程，维护一个 **dp[M][2]** 其中
    *   **dp[i][0]** 表示如果在第**I**分钟开始没有广告，达到的最大广告值。
    *   **dp[i][1]** 表示如果我们选择从第 1 分钟开始的广告，所获得的最大广告价值。最终答案将是**最大 dp[M-1][0]和 dp[M-1][1]** 。
*   建立民主党州-
    *   对于 **dp[i][0]** ，由于我们没有广告在**第 I**分钟开始，因此没有 **K** 分钟的限制。因此， **dp[i][0] = max(dp[i-1][0]，dp[i-1][1])** 作为前一分钟，我们可以有两种可能的情况。
    *   对于 **dp[i][1]** ，现在我们有从 **i-th** 分钟开始的广告，这意味着在分钟**I–1，I–2，…，I –( K–1)**我们不能有任何广告。所以，我们必须看第**(I–K)分钟。因此， **dp[i][1] =值[i] + max(dp[i-K][0]，dp[i-K][1])** ，在分钟**I–K**时，我们可以再次拥有这两种场景。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

#define ll long long int

// Function to find maximum
// possible advertising value
int max_value(int array[][2], int M,
              int K, int N)
{
    // To store advertising
    // value at i-th minute
    int time[M] = { 0 };

    for (int i = 0; i < N; i++) {
        time[array[i][0]] = array[i][1];
    }

    int dp[M][2];

    // Base Case
    dp[0][0] = 0;
    dp[0][1] = time[0];

    for (int i = 1; i < M; i++) {

        // If no advertisement is
        // taken on ith minute
        dp[i][0] = max(dp[i - 1][0], dp[i - 1][1]);

        // If advertisement is taken
        // on i-th minute
        dp[i][1] = time[i];

        if (i - K >= 0) {
            dp[i][1]
                += max(dp[i - K][0], dp[i - K][1]);
        }
    }

    return max(dp[M - 1][0], dp[M - 1][1]);
}

// Driver's Code
int main()
{
    // array[][0] start time
    // array[][1] advertising value
    int array[][2] = {
        { 0, 10 },
        { 4, 110 },
        { 5, 30 }
    };

    int N = 3;
    int K = 4;
    int M = 6;

    cout << max_value(array, M, K, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;

class GFG{

// Function to find maximum
// possible advertising value
static int max_value(int array[][], int M,
                     int K, int N)
{

    // To store advertising
    // value at i-th minute
    int[] time = new int[M];

    for(int i = 0; i < N; i++)
    {
        time[array[i][0]] = array[i][1];
    }

    int[][] dp = new int[M][2];

    // Base Case
    dp[0][0] = 0;
    dp[0][1] = time[0];

    for(int i = 1; i < M; i++)
    {

        // If no advertisement is
        // taken on ith minute
        dp[i][0] = Math.max(dp[i - 1][0],
                            dp[i - 1][1]);

        // If advertisement is taken
        // on i-th minute
        dp[i][1] = time[i];

        if (i - K >= 0)
        {
            dp[i][1] += Math.max(dp[i - K][0],
                                 dp[i - K][1]);
        }
    }
    return Math.max(dp[M - 1][0], dp[M - 1][1]);
}

// Driver code
public static void main(String[] args)
{

    // array[][0] start time
    // array[][1] advertising value
    int array[][] = { { 0, 10 },
                      { 4, 110 },
                      { 5, 30 } };

    int N = 3;
    int K = 4;
    int M = 6;

    System.out.println(max_value(array, M, K, N));
}
}

// This code is contributed by offbeat
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find maximum
// possible advertising value
function max_value(array, M, K, N)
{
    // To store advertising
    // value at i-th minute
    var time = Array(M).fill(0);

    for (var i = 0; i < N; i++) {
        time[array[i][0]] = array[i][1];
    }

    var dp = Array.from(Array(M), ()=> Array(2));

    // Base Case
    dp[0][0] = 0;
    dp[0][1] = time[0];

    for (var i = 1; i < M; i++) {

        // If no advertisement is
        // taken on ith minute
        dp[i][0] = Math.max(dp[i - 1][0], dp[i - 1][1]);

        // If advertisement is taken
        // on i-th minute
        dp[i][1] = time[i];

        if (i - K >= 0) {
            dp[i][1]
                += Math.max(dp[i - K][0], dp[i - K][1]);
        }
    }

    return Math.max(dp[M - 1][0], dp[M - 1][1]);
}

// Driver's Code
// array[][0] start time
// array[][1] advertising value
var array = [
    [ 0, 10],
    [ 4, 110 ],
    [ 5, 30 ]
];
var N = 3;
var K = 4;
var M = 6;
document.write( max_value(array, M, K, N));

</script>
```

**Output:** 

```
120
```