# 来自前 N 个自然数的所有可能的 K 大小子集的最小值的平均值

> 原文:[https://www . geeksforgeeks . org/从第一个 n 个自然数开始的最小 k 大小子集平均值/](https://www.geeksforgeeks.org/mean-of-minimum-of-all-possible-k-size-subsets-from-first-n-natural-numbers/)

给定两个正整数 **N** 和 **K** ，任务是[从第一个**N**T10】自然数](https://www.geeksforgeeks.org/mean/)中找出**大小 K** 的所有可能子集的最小值的平均值。

**示例:**

> **输入:** N = 3，K = 2
> **输出:** 1.33333
> **说明:**
> 大小 K 的所有可能子集为{1，2}、{1，3}、{2，3}。所有子集的最小值分别是 1、1 和 2。所有最小值的平均值为(1 + 1 + 2)/3 = 1.3333。
> 
> **输入:** N = 3，K = 1
> T3】输出: 2.00000

**天真方法:**解决给定问题最简单的方法是[找到由元素**【1，N】**](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)构成的所有子集，并找到大小为 **K** 的子集的所有[最小元素的](https://www.geeksforgeeks.org/minimum-difference-max-min-k-size-subsets/)[均值](https://www.geeksforgeeks.org/mathematics-mean-variance-and-standard-deviation/)。

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效法:**通过观察**大小 K** 形成的子集总数由**给出<sup>N</sup>C<sub>K</sub>T9】每个元素表示 **i** 出现**T13】(N–I)C<sub>(K–1)</sub>**次数作为最小元素，也可以优化上述方法。**

因此，思路是求**(<sup>N–I</sup>C<sub>K–1)</sub>)* I**对 **i** 所有可能值的和，除以形成的子集总数，即 **<sup>N</sup> C <sub>K</sub>** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the value of nCr
int nCr(int n, int r, int f[])
{
    // Base Case
    if (n < r) {
        return 0;
    }

    // Find nCr recursively
    return f[n] / (f[r] * f[n - r]);
}

// Function to find the expected minimum
// values of all the subsets of size K
int findMean(int N, int X)
{
    // Find the factorials that will
    // be used later
    int f[N + 1];
    f[0] = 1;

    // Find the factorials
    for (int i = 1; i <= N; i++) {
        f[i] = f[i - 1] * i;
    }

    // Total number of subsets
    int total = nCr(N, X, f);

    // Stores the sum of minimum over
    // all possible subsets
    int count = 0;

    // Iterate over all possible minimum
    for (int i = 1; i <= N; i++) {
        count += nCr(N - i, X - 1, f) * i;
    }

    // Find the mean over all subsets
    double E_X = double(count) / double(total);

    cout << setprecision(10) << E_X;

    return 0;
}

// Driver Code
int main()
{
    int N = 3, X = 2;
    findMean(N, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG {

    // Function to find the value of nCr
    static int nCr(int n, int r, int f[]) {
        // Base Case
        if (n < r) {
            return 0;
        }

        // Find nCr recursively
        return f[n] / (f[r] * f[n - r]);
    }

    // Function to find the expected minimum
    // values of all the subsets of size K
    static int findMean(int N, int X) {
        // Find the factorials that will
        // be used later
        int[] f = new int[N + 1];
        f[0] = 1;

        // Find the factorials
        for (int i = 1; i <= N; i++) {
            f[i] = f[i - 1] * i;
        }

        // Total number of subsets
        int total = nCr(N, X, f);

        // Stores the sum of minimum over
        // all possible subsets
        int count = 0;

        // Iterate over all possible minimum
        for (int i = 1; i <= N; i++) {
            count += nCr(N - i, X - 1, f) * i;
        }

        // Find the mean over all subsets
        double E_X = (double) (count) / (double) (total);

        System.out.print(String.format("%.6f", E_X));

        return 0;
    }

    // Driver Code
    public static void main(String[] args) {
        int N = 3, X = 2;
        findMean(N, X);

    }
}

// This code contributed by Princi Singh
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the value of nCr
def nCr(n, r, f):

    # Base Case
    if (n < r):
        return 0

    # Find nCr recursively
    return f[n] / (f[r] * f[n - r])

# Function to find the expected minimum
# values of all the subsets of size K
def findMean(N, X):

    # Find the factorials that will
    # be used later
    f = [0 for i in range(N + 1)]
    f[0] = 1

    # Find the factorials
    for i in range(1,N+1,1):
        f[i] = f[i - 1] * i

    # Total number of subsets
    total = nCr(N, X, f)

    # Stores the sum of minimum over
    # all possible subsets
    count = 0

    # Iterate over all possible minimum
    for i in range(1,N+1,1):
        count += nCr(N - i, X - 1, f) * i

    # Find the mean over all subsets
    E_X = (count) / (total)

    print("{0:.9f}".format(E_X))

    return 0

# Driver Code
if __name__ == '__main__':
    N = 3
    X = 2
    findMean(N, X)

# This code is contributed by ipg201607.
```

## C#

```
// C# code for the above approach
using System;

public class GFG
{

// Function to find the value of nCr
    static int nCr(int n, int r, int[] f)
    {

        // Base Case
        if (n < r) {
            return 0;
        }

        // Find nCr recursively
        return f[n] / (f[r] * f[n - r]);
    }

    // Function to find the expected minimum
    // values of all the subsets of size K
    static int findMean(int N, int X)
    {

        // Find the factorials that will
        // be used later
        int[] f = new int[N + 1];
        f[0] = 1;

        // Find the factorials
        for (int i = 1; i <= N; i++) {
            f[i] = f[i - 1] * i;
        }

        // Total number of subsets
        int total = nCr(N, X, f);

        // Stores the sum of minimum over
        // all possible subsets
        int count = 0;

        // Iterate over all possible minimum
        for (int i = 1; i <= N; i++) {
            count += nCr(N - i, X - 1, f) * i;
        }

        // Find the mean over all subsets
        double E_X = (double) (count) / (double) (total);

        Console.Write("{0:F9}", E_X);

        return 0;
    }

    // Driver Code
    static public void Main (){

        // Code
       int N = 3, X = 2;
        findMean(N, X);
    }
}

// This code is contributed by Potta Lokesh
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the value of nCr
function nCr(n, r, f) {
  // Base Case
  if (n < r) {
    return 0;
  }

  // Find nCr recursively
  return f[n] / (f[r] * f[n - r]);
}

// Function to find the expected minimum
// values of all the subsets of size K
function findMean(N, X) {
  // Find the factorials that will
  // be used later
  let f = new Array(N + 1).fill(0);
  f[0] = 1;

  // Find the factorials
  for (let i = 1; i <= N; i++) {
    f[i] = f[i - 1] * i;
  }

  // Total number of subsets
  let total = nCr(N, X, f);

  // Stores the sum of minimum over
  // all possible subsets
  let count = 0;

  // Iterate over all possible minimum
  for (let i = 1; i <= N; i++) {
    count += nCr(N - i, X - 1, f) * i;
  }

  // Find the mean over all subsets
  let E_X = count / total;

  document.write(parseFloat(E_X).toFixed(9));

  return 0;
}

// Driver Code

let N = 3,
  X = 2;
findMean(N, X);

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
1.333333333
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)