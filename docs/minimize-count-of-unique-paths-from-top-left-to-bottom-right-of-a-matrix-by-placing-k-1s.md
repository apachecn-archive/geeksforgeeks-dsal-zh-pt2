# 通过放置 K ^ 1s

来最小化从矩阵左上角到右下角的唯一路径的数量

> 原文:[https://www . geesforgeks . org/通过放置 k-1s 来最小化从矩阵的左上角到右下角的唯一路径数/](https://www.geeksforgeeks.org/minimize-count-of-unique-paths-from-top-left-to-bottom-right-of-a-matrix-by-placing-k-1s/)

给定两个整数 **N** 和 **M** ，其中 **M** 和 **N** 表示仅由 **0** 组成的尺寸矩阵 **N * M** 。任务是仅通过在矩阵中精确放置 **K** 1s，最小化从矩阵左上角 **(0，0)** 到右下角**(N–1，M–1)**的唯一路径数。

**注意:**右下角和左上角单元格都不能修改为 0。

**示例:**

> **输入:** N = 3，M = 3，K = 1
> **输出:** 2
> **解释:**
> 在矩阵中放置 K(= 1) 1s 生成矩阵[[0，0，0]，[0，1，0]，[0，0，0]]只留下从左上角到右下角单元格的两条可能路径。
> 路径为[(0，0) → (0，1) → (0，2) → (1，2) → (2，2)]和[(0，0) → (1，0) → (2，0) → (2，1) → (2，2)]
> 
> **输入:** N = 3，M = 3，K = 3
> **输出** : 0
> **解释:**
> 放置 K(= 3) 1s 生成矩阵[[0，1，1]，[1，0，0]，[0，0，0]]从左上角到右下角没有可能的路径。

**方法:**可以通过考虑以下可能的情况来解决问题。

1.  **如果 K ≥ 2:** 通过在矩阵的(0，1)和(1，0)单元中放置两个 1，可以将可能路径的数量减少到 **0** 。
2.  **如果 K = 0:** 计数保持 **C(N+M-2，N-1)。**
3.  **如果 K = 1:** 在矩阵中心放置 1， **((N-1)/2，(M-1)/2)** 以最小化路径数。因此，这种情况下可能的路径数如下:

> 结果=从左上方到达右下方的总路径数–(从左上方到达中点的路径数*从中点到达端点的路径数)
> 其中
> 
> *   从左上方到达右下方的途径总数= C<sub>(N+M–2，N–1)</sub>
> *   从左上角到中点的路径数= C<sub>((N–1)/2+(M–1)/2，(N–1)/2)</sub>
> *   从中点= C<sub>(((N–1)–(N–1)/2)+((M–1)–(M–1)/2)、((N–1)–(N–1)/2))</sub>到达终点的途径数

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the value of
// Binomial Coefficient C(n, k)
int ncr(int n, int k)
{
    int res = 1;

    // Since C(n, k) = C(n, n-k)
    if (k > n - k)
        k = n - k;

    // Calculate the value of
    // [n * (n-1) *---* (n-k+1)] /
    // [k * (k-1) *----* 1]
    for (int i = 0; i < k; ++i) {
        res *= (n - i);
        res /= (i + 1);
    }

    return res;
}

// Function to find the minimum
// count of paths from top
// left to bottom right by
// placing K 1s in the matrix
int countPath(int N, int M, int K)
{
    int answer;
    if (K >= 2)
        answer = 0;
    else if (K == 0)
        answer = ncr(N + M - 2, N - 1);
    else {

        // Count of ways without 1s
        answer = ncr(N + M - 2, N - 1);

        // Count of paths from starting
        // point to mid point
        int X = (N - 1) / 2 + (M - 1) / 2;
        int Y = (N - 1) / 2;
        int midCount = ncr(X, Y);

        // Count of paths from mid
        // point to end point
        X = ((N - 1) - (N - 1) / 2)
            + ((M - 1) - (M - 1) / 2);

        Y = ((N - 1) - (N - 1) / 2);
        midCount *= ncr(X, Y);
        answer -= midCount;
    }
    return answer;
}

// Driver Code
int main()
{
    int N = 3;
    int M = 3;
    int K = 1;

    cout << countPath(N, M, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG{

// Function to return the value of
// Binomial Coefficient C(n, k)
static int ncr(int n, int k)
{
    int res = 1;

    // Since C(n, k) = C(n, n-k)
    if (k > n - k)
        k = n - k;

    // Calculate the value of
    // [n * (n-1) *---* (n-k+1)] /
    // [k * (k-1) *----* 1]
    for (int i = 0; i < k; ++i)
    {
        res *= (n - i);
        res /= (i + 1);
    }
    return res;
}

// Function to find the minimum
// count of paths from top
// left to bottom right by
// placing K 1s in the matrix
static int countPath(int N, int M, int K)
{
    int answer;
    if (K >= 2)
        answer = 0;
    else if (K == 0)
        answer = ncr(N + M - 2, N - 1);
    else
    {
        // Count of ways without 1s
        answer = ncr(N + M - 2, N - 1);

        // Count of paths from starting
        // point to mid point
        int X = (N - 1) / 2 + (M - 1) / 2;
        int Y = (N - 1) / 2;
        int midCount = ncr(X, Y);

        // Count of paths from mid
        // point to end point
        X = ((N - 1) - (N - 1) / 2) +
            ((M - 1) - (M - 1) / 2);
        Y = ((N - 1) - (N - 1) / 2);
        midCount *= ncr(X, Y);
        answer -= midCount;
    }
    return answer;
}

// Driver Code
public static void main(String[] args)
{
    int N = 3;
    int M = 3;
    int K = 1;
    System.out.print(countPath(N, M, K));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
#Python3 Program to implement
#the above approach
#Function to return the value of
#Binomial Coefficient C(n, k)
def ncr(n, k):
    res = 1

    #Since C(n, k) = C(n, n-k)
    if (k > n - k):
        k = n - k

    #Calculate the value of
    #[n * (n-1) *---* (n-k+1)] /
    #[k * (k-1) *----* 1]
    for i in range(k):
        res *= (n - i)
        res //= (i + 1)

    return res

#Function to find the minimum
#count of paths from top
#left to bottom right by
#placing K 1s in the matrix
def countPath(N, M, K):
    answer = 0
    if (K >= 2):
        answer = 0
    elif (K == 0):
        answer = ncr(N + M - 2, N - 1)
    else:

        #Count of ways without 1s
        answer = ncr(N + M - 2, N - 1)

        #Count of paths from starting
        #poto mid point
        X = (N - 1) // 2 + (M - 1) // 2
        Y = (N - 1) // 2
        midCount = ncr(X, Y)

        #Count of paths from mid
        #poto end point
        X = ((N - 1) - (N - 1) // 2)+
            ((M - 1) - (M - 1) // 2)

        Y = ((N - 1) - (N - 1) // 2)
        midCount *= ncr(X, Y)
        answer -= midCount

    return answer

#Driver Code
if __name__ == '__main__':
    N = 3
    M = 3
    K = 1
    print(countPath(N, M, K))

# This code is contributed by Mohit Kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to return the value of
// Binomial Coefficient C(n, k)
static int ncr(int n, int k)
{
    int res = 1;

    // Since C(n, k) = C(n, n-k)
    if (k > n - k)
        k = n - k;

    // Calculate the value of
    // [n * (n-1) *---* (n-k+1)] /
    // [k * (k-1) *----* 1]
    for(int i = 0; i < k; ++i)
    {
        res *= (n - i);
        res /= (i + 1);
    }
    return res;
}

// Function to find the minimum
// count of paths from top
// left to bottom right by
// placing K 1s in the matrix
static int countPath(int N, int M, int K)
{
    int answer;

    if (K >= 2)
        answer = 0;
    else if (K == 0)
        answer = ncr(N + M - 2, N - 1);
    else
    {

        // Count of ways without 1s
        answer = ncr(N + M - 2, N - 1);

        // Count of paths from starting
        // point to mid point
        int X = (N - 1) / 2 + (M - 1) / 2;
        int Y = (N - 1) / 2;
        int midCount = ncr(X, Y);

        // Count of paths from mid
        // point to end point
        X = ((N - 1) - (N - 1) / 2) +
            ((M - 1) - (M - 1) / 2);
        Y = ((N - 1) - (N - 1) / 2);

        midCount *= ncr(X, Y);
        answer -= midCount;
    }
    return answer;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 3;
    int M = 3;
    int K = 1;

    Console.Write(countPath(N, M, K));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

// Function to return the value of
// Binomial Coefficient C(n, k)
function ncr(n, k)
{
    var res = 1;

    // Since C(n, k) = C(n, n-k)
    if (k > n - k)
        k = n - k;

    // Calculate the value of
    // [n * (n-1) *---* (n-k+1)] /
    // [k * (k-1) *----* 1]
    for (var i = 0; i < k; ++i) {
        res *= (n - i);
        res /= (i + 1);
    }

    return res;
}

// Function to find the minimum
// count of paths from top
// left to bottom right by
// placing K 1s in the matrix
function countPath(N, M, K)
{
    var answer;
    if (K >= 2)
        answer = 0;
    else if (K == 0)
        answer = ncr(N + M - 2, N - 1);
    else {

        // Count of ways without 1s
        answer = ncr(N + M - 2, N - 1);

        // Count of paths from starting
        // point to mid point
        var X = (N - 1) / 2 + (M - 1) / 2;
        var Y = (N - 1) / 2;
        var midCount = ncr(X, Y);

        // Count of paths from mid
        // point to end point
        X = ((N - 1) - (N - 1) / 2)
            + ((M - 1) - (M - 1) / 2);

        Y = ((N - 1) - (N - 1) / 2);
        midCount *= ncr(X, Y);
        answer -= midCount;
    }
    return answer;
}

// Driver Code
var N = 3;
var M = 3;
var K = 1;
document.write( countPath(N, M, K));

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N+M)*
***辅助空间:** O(1)*