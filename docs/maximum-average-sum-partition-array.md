# 一个数组的最大平均和划分

> 原文:[https://www . geesforgeks . org/maximum-average-sum-partition-array/](https://www.geeksforgeeks.org/maximum-average-sum-partition-array/)

给定一个数组，我们将一行数字 A 划分为最多 K 个相邻(非空)的组，那么得分就是每组的平均值之和。能得的最高分是多少？
**例:**

> 输入:A = { 9，1，2，3，9 }
> K = 3
> 输出:20
> 说明:我们可以将 A 划分为[9]，[1，2，3]，[9]。答案是 9 + (1 + 2 + 3) / 3 + 9 = 20。
> 我们也可以将 A 划分为[9，1]，[2]，[3，9]。这种划分会导致 5 + 2 + 6 = 13 的分数，这更糟糕。
> 输入:A[] = { 1，2，3，4，5，6，7 }
> K = 4
> 输出:20.5
> 说明:我们可以将 A 划分为[1，2，3，4]，[5]，[6]，[7]。答案是 2.5 + 5 + 6 + 7 = 20.5。

一个简单的解决方法是使用递归。一个有效的解决办法是记忆，我们保持最大的分数到 k，即 1，2，3…到 k；
让备忘录[i][k]成为最佳分数分配 A[i..n-1]最多分成 K 个部分。在第一组中，我们将 A[i..n-1]变成 A[i..j-1]和 A[j..n-1]，那么我们的候选分区有 score average(i，j) + score(j，k-1))，其中 average(i，j)=(A[I]+A[I+1]+…+A[j-1])/(j–I)。我们取其中最高分。
总的来说，我们在一般情况下的递归是:
memo[n][k] = max(memo[n][k]，分数(memo，I，A，k-1) +平均值(I，j))
为从 n-1 到 1 的所有 I。

## C++

```
// CPP program for maximum average sum partition
#include <bits/stdc++.h>
using namespace std;

#define MAX 1000

double memo[MAX][MAX];

// bottom up approach to calculate score
double score(int n, vector<int>& A, int k)
{
    if (memo[n][k] > 0)
        return memo[n][k];
    double sum = 0;
    for (int i = n - 1; i > 0; i--) {
        sum += A[i];
        memo[n][k] = max(memo[n][k], score(i, A, k - 1) +
                                          sum / (n - i));
    }
    return memo[n][k];
}

double largestSumOfAverages(vector<int>& A, int K)
{
    int n = A.size();
    double sum = 0;
    memset(memo, 0.0, sizeof(memo));
    for (int i = 0; i < n; i++) {
        sum += A[i];

        // storing averages from starting to each i ;
        memo[i + 1][1] = sum / (i + 1);
    }
    return score(n, A, K);
}

int main()
{
    vector<int> A = { 9, 1, 2, 3, 9 };
    int K = 3; // atmost partitioning size
    cout << largestSumOfAverages(A, K) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for maximum average sum partition
import java.util.Arrays;
import java.util.Vector;

class GFG
{

    static int MAX = 1000;
    static double[][] memo = new double[MAX][MAX];

    // bottom up approach to calculate score
    public static double score(int n, Vector<Integer> A, int k)
    {
        if (memo[n][k] > 0)
            return memo[n][k];

        double sum = 0;
        for (int i = n - 1; i > 0; i--)
        {
            sum += A.elementAt(i);

            memo[n][k] = Math.max(memo[n][k],
                                  score(i, A, k - 1) +
                                  sum / (n - i));
        }
        return memo[n][k];
    }

    public static double largestSumOfAverages(Vector<Integer> A, int K)
    {
        int n = A.size();
        double sum = 0;

        for (int i = 0; i < memo.length; i++)
        {
            for (int j = 0; j < memo[i].length; j++)
                memo[i][j] = 0.0;
        }

        for (int i = 0; i < n; i++)
        {
            sum += A.elementAt(i);

            // storing averages from starting to each i ;
            memo[i + 1][1] = sum / (i + 1);
        }

        return score(n, A, K);
    }

    // Driver code
    public static void main(String[] args)
    {
        Vector<Integer> A = new Vector<>(Arrays.asList(9, 1, 2, 3, 9));
        int K = 3;
        System.out.println(largestSumOfAverages(A, K));

    }
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 program for maximum average sum partition
MAX = 1000

memo = [[0.0 for i in range(MAX)]
             for i in range(MAX)]

# bottom up approach to calculate score
def score(n, A, k):
    if (memo[n][k] > 0):
        return memo[n][k]
    sum = 0
    i = n - 1
    while(i > 0):
        sum += A[i]
        memo[n][k] = max(memo[n][k], score(i, A, k - 1) +
                                       int(sum / (n - i)))

        i -= 1

    return memo[n][k]

def largestSumOfAverages(A, K):
    n = len(A)
    sum = 0
    for i in range(n):
        sum += A[i]

        # storing averages from starting to each i ;
        memo[i + 1][1] = int(sum / (i + 1))

    return score(n, A, K)

# Driver Code
if __name__ == '__main__':
    A = [9, 1, 2, 3, 9]
    K = 3 # atmost partitioning size
    print(largestSumOfAverages(A, K))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program for maximum average sum partition
using System;
using System.Collections.Generic;

class GFG
{
    static int MAX = 1000;
    static double[,] memo = new double[MAX, MAX];

    // bottom up approach to calculate score
    public static double score(int n,
                               List<int> A, int k)
    {
        if (memo[n, k] > 0)
            return memo[n, k];

        double sum = 0;
        for (int i = n - 1; i > 0; i--)
        {
            sum += A[i];

            memo[n, k] = Math.Max(memo[n, k],
                                  score(i, A, k - 1) +
                                  sum / (n - i));
        }
        return memo[n, k];
    }

    public static double largestSumOfAverages(List<int> A,
                                                   int K)
    {
        int n = A.Count;
        double sum = 0;

        for (int i = 0;
                 i < memo.GetLength(0); i++)
        {
            for (int j = 0;
                     j < memo.GetLength(1); j++)
                memo[i, j] = 0.0;
        }

        for (int i = 0; i < n; i++)
        {
            sum += A[i];

            // storing averages from
            // starting to each i;
            memo[i + 1, 1] = sum / (i + 1);
        }

        return score(n, A, K);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int [] arr = {9, 1, 2, 3, 9};
        List<int> A = new List<int>(arr);
        int K = 3;
        Console.WriteLine(largestSumOfAverages(A, K));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program for maximum average sum partition

let MAX = 1000;

let memo = new Array(MAX).fill(0).map(() => new Array(MAX).fill(0));

// bottom up approach to calculate score
function score(n, A, k) {
    if (memo[n][k] > 0)
        return memo[n][k];
    let sum = 0;
    for (let i = n - 1; i > 0; i--) {
        sum += A[i];
        memo[n][k] = Math.max(memo[n][k], score(i, A, k - 1) +
            sum / (n - i));
    }
    return memo[n][k];
}

function largestSumOfAverages(A, K) {
    let n = A.length;
    let sum = 0;

    for (let i = 0; i < n; i++) {
        sum += A[i];

        // storing averages from starting to each i ;
        memo[i + 1][1] = sum / (i + 1);
    }
    return score(n, A, K);
}

let A = [9, 1, 2, 3, 9];
let K = 3; // atmost partitioning size
document.write(largestSumOfAverages(A, K) + "<br>");

</script>
```

**Output:** 

```
20
```

上述问题现在可以很容易地理解为动态规划。
设 dp(i，K)为将 A[i:j]划分为最多 K 个部分的最佳得分。如果我们将 A[i:j]划分成的第一组在 j 之前结束，那么我们的候选划分具有得分平均值(I，j) + dp(j，k-1))。一般情况下的递归是 dp(i，k) = max(average(i，N)，(average(i，j) + dp(j，k-1))。我们可以预先计算前缀和，以便快速执行代码。

## C++

```
// CPP program for maximum average sum partition
#include <bits/stdc++.h>
using namespace std;

double largestSumOfAverages(vector<int>& A, int K)
{
    int n = A.size();

    // storing prefix sums
    double pre_sum[n+1];
    pre_sum[0] = 0;
    for (int i = 0; i < n; i++)
        pre_sum[i + 1] = pre_sum[i] + A[i];

    // for each i to n storing averages
    double dp[n] = {0};
    double sum = 0;
    for (int i = 0; i < n; i++)
        dp[i] = (pre_sum[n] - pre_sum[i]) / (n - i);

    for (int k = 0; k < K - 1; k++)
        for (int i = 0; i < n; i++)
            for (int j = i + 1; j < n; j++)
                dp[i] = max(dp[i], (pre_sum[j] -
                         pre_sum[i]) / (j - i) + dp[j]);

    return dp[0];
}

// Driver code
int main()
{
    vector<int> A = { 9, 1, 2, 3, 9 };
    int K = 3; // atmost partitioning size
    cout << largestSumOfAverages(A, K) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for maximum average sum partition
import java.util.*;

class GFG
{

static double largestSumOfAverages(int[] A, int K)
{
    int n = A.length;

    // storing prefix sums
    double []pre_sum = new double[n + 1];
    pre_sum[0] = 0;
    for (int i = 0; i < n; i++)
        pre_sum[i + 1] = pre_sum[i] + A[i];

    // for each i to n storing averages
    double []dp = new double[n];
    double sum = 0;
    for (int i = 0; i < n; i++)
        dp[i] = (pre_sum[n] - pre_sum[i]) / (n - i);

    for (int k = 0; k < K - 1; k++)
        for (int i = 0; i < n; i++)
            for (int j = i + 1; j < n; j++)
                dp[i] = Math.max(dp[i], (pre_sum[j] -
                        pre_sum[i]) / (j - i) + dp[j]);

    return dp[0];
}

// Driver code
public static void main(String[] args)
{
    int []A = { 9, 1, 2, 3, 9 };
    int K = 3; // atmost partitioning size
    System.out.println(largestSumOfAverages(A, K));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program for maximum average
# sum partition
def largestSumOfAverages(A, K):

    n = len(A);

    # storing prefix sums
    pre_sum = [0] * (n + 1);
    pre_sum[0] = 0;
    for i in range(n):
        pre_sum[i + 1] = pre_sum[i] + A[i];

    # for each i to n storing averages
    dp = [0] * n;
    sum = 0;
    for i in range(n):
        dp[i] = (pre_sum[n] -
                 pre_sum[i]) / (n - i);

    for k in range(K - 1):
        for i in range(n):
            for j in range(i + 1, n):
                dp[i] = max(dp[i], (pre_sum[j] -
                                    pre_sum[i]) /
                                    (j - i) + dp[j]);

    return int(dp[0]);

# Driver code
A = [ 9, 1, 2, 3, 9 ];
K = 3; # atmost partitioning size
print(largestSumOfAverages(A, K));

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program for maximum average sum partition
using System;
using System.Collections.Generic;

class GFG
{
static double largestSumOfAverages(int[] A,
                                   int K)
{
    int n = A.Length;

    // storing prefix sums
    double []pre_sum = new double[n + 1];
    pre_sum[0] = 0;
    for (int i = 0; i < n; i++)
        pre_sum[i + 1] = pre_sum[i] + A[i];

    // for each i to n storing averages
    double []dp = new double[n];
    for (int i = 0; i < n; i++)
        dp[i] = (pre_sum[n] - pre_sum[i]) / (n - i);

    for (int k = 0; k < K - 1; k++)
        for (int i = 0; i < n; i++)
            for (int j = i + 1; j < n; j++)
                dp[i] = Math.Max(dp[i], (pre_sum[j] -
                        pre_sum[i]) / (j - i) + dp[j]);

    return dp[0];
}

// Driver code
public static void Main(String[] args)
{
    int []A = { 9, 1, 2, 3, 9 };
    int K = 3; // atmost partitioning size
    Console.WriteLine(largestSumOfAverages(A, K));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// javascript program for maximum average sum partition

    function largestSumOfAverages(A , K) {
        var n = A.length;

        // storing prefix sums
        var pre_sum = Array(n + 1).fill(-1);
        pre_sum[0] = 0;
        for (var i = 0; i < n; i++)
            pre_sum[i + 1] = pre_sum[i] + A[i];

        // for each i to n storing averages
        var dp = Array(n).fill(-1);
        var sum = 0;
        for (var i = 0; i < n; i++)
            dp[i] = (pre_sum[n] - pre_sum[i]) / (n - i);

        for (k = 0; k < K - 1; k++)
            for (i = 0; i < n; i++)
                for (j = i + 1; j < n; j++)
                    dp[i] = Math.max(dp[i], (pre_sum[j] - pre_sum[i]) / (j - i) + dp[j]);

        return dp[0];
    }

    // Driver code
        var A = [ 9, 1, 2, 3, 9 ];
        var K = 3; // atmost partitioning size
        document.write(largestSumOfAverages(A, K));

// This code is contributed by umadevi9616
</script>
```

**Output:** 

```
20
```