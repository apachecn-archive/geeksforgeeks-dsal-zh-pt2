# 通过合并两个给定的数组

可能的最大前缀和

> 原文:[https://www . geeksforgeeks . org/最大前缀-合并两个给定数组的总和/](https://www.geeksforgeeks.org/maximum-prefix-sum-possible-by-merging-two-given-arrays/)

给定两个分别由 **N** 和 **M** 整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **A[]** 和 **B[]** ，任务是计算两个数组合并后可以得到的最大[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。

**示例:**

> **输入:** A[] = {2，-1，4，-5}，B[]={4，-3，12，4，-3}
> **输出:** 22
> **解释:**合并两个数组生成序列{2，4，-1，-3，4，12，4，-5，-3}。最大前缀和= { arr[0]，…，arr[6]}之和= 22。
> 
> **输入:** A[] = {2，1，13，5，14}，B={-1，4，-13}
> **输出:** 38
> **解释:**合并两个数组生成序列{2，1，-1，13，5，14，-13}。最大前缀和= { arr[0]，…，arr[6]}之和= 38。

**天真方法:**最简单的方法是使用[递归](https://www.geeksforgeeks.org/recursion/)，可以使用[记忆](https://www.geeksforgeeks.org/tabulation-vs-memoization/)进行优化。按照以下步骤解决问题:

*   初始化一个[地图<对< int，int >，int>](https://www.geeksforgeeks.org/map-pairs-stl/)T2【DP】进行记忆。
*   定义一个递归函数，比如**maxprobe(x，y)** 来求最大前缀和:
    *   如果 **dp[{x，y}]** 已经计算，则返回 **dp[{x，y}]。**
    *   否则，如果 **x==N || y==M，**则返回 **0** 。
    *   更新 **dp[{x，y}]** as **dp[{x，y}] = max(dp[{x，y}、a[x]+max presume(x+1，y)]、b[y]+max presume(x，y+1)]**然后返回 **dp[{x，y}]。**
*   将最大前缀和打印为**最大假定(0，0)** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>

#define int long long
using namespace std;

// Stores the dp states
map<pair<int, int>, int> dp;

// Recursive Function to calculate the maximum
// prefix sum obtained by merging two arrays
int maxPreSum(vector<int> a, vector<int> b,
              int x, int y)
{
    // If subproblem is already computed
    if (dp.find({ x, y }) != dp.end())
        return dp[{ x, y }];

    // If x >= N or y >= M
    if (x == a.size() && y == b.size())
        return 0;

    int curr = dp[{ x, y }];

    // If x < N
    if (x == a.size()) {
        curr = max(curr, b[y]
                             + maxPreSum(a, b, x, y + 1));
    }
    // If y<M
    else if (y == b.size()) {
        curr = max(curr,
                   a[x] + maxPreSum(a, b, x + 1, y));
    }

    // Otherwise
    else {
        curr = max({ curr,
                     a[x] + maxPreSum(a, b, x + 1, y),
                     b[y] + maxPreSum(a, b, x, y + 1) });
    }
    return dp[{ x, y }] = curr;
}
// Driver Code
signed main()
{
    vector<int> A = { 2, 1, 13, 5, 14 };
    vector<int> B = { -1, 4, -13 };
    cout << maxPreSum(A, B, 0, 0) << endl;
    return 0;
}
```

## C#

```
// C# implementation of above approach
using System;
using System.Collections.Generic;

class GFG{

// Stores the dp states
static Dictionary<Tuple<int,
                        int>, int> dp = new Dictionary<Tuple<int,
                                                             int>, int>();

// Recursive Function to calculate the maximum
// prefix sum obtained by merging two arrays
static int maxPreSum(int[] a, int[] b, int x, int y)
{

    // If subproblem is already computed
    if (dp.ContainsKey(new Tuple<int, int>(x, y)))
        return dp[new Tuple<int, int>(x, y)];

    // If x >= N or y >= M
    if (x == a.Length && y == b.Length)
        return 0;

    int curr = 0;
    if (dp.ContainsKey(new Tuple<int, int>(x, y)))
    {
        curr = dp[new Tuple<int, int>(x, y)];
    }

    // If x < N
    if (x == a.Length)
    {
        curr = Math.Max(curr, b[y] + maxPreSum(
            a, b, x, y + 1));
    }

    // If y<M
    else if (y == b.Length)
    {
        curr = Math.Max(curr, a[x] + maxPreSum(
            a, b, x + 1, y));
    }

    // Otherwise
    else
    {
        int max = Math.Max(a[x] + maxPreSum(a, b, x + 1, y),
                           b[y] + maxPreSum(a, b, x, y + 1));
        curr = Math.Max(curr, max);
    }
    dp[new Tuple<int,int>(x, y)] = curr;
    return dp[new Tuple<int, int>(x, y)];
}

// Driver code
static void Main()
{
    int[] A = { 2, 1, 13, 5, 14 };
    int[] B = { -1, 4, -13 };

    Console.WriteLine(maxPreSum(A, B, 0, 0));
}
}

// This code is contributed by divyesh072019
```

**Output:** 

```
38
```

***时间复杂度:**O(N * M)*
***辅助空间:** O(N*M)*

**高效方法:**上述方法可以基于[最大前缀和](https://www.geeksforgeeks.org/maximum-prefix-sum-given-range/)等于数组最大前缀和 **A[]** 和 **B[]** 之和的观察进行优化。按照以下步骤解决问题:

*   计算数组 **A[]** 的最大前缀和，并存储在一个变量中，比如 **X.**
*   计算数组 **B[]** 的最大前缀和，并存储在一个变量中，比如 **Y.**
*   打印 **X** 和**y**的和

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

int maxPresum(vector<int> a, vector<int> b)
{
    // Stores the maximum prefix
    // sum of the array A[]
    int X = max(a[0], 0);

    // Traverse the array A[]
    for (int i = 1; i < a.size(); i++) {
        a[i] += a[i - 1];
        X = max(X, a[i]);
    }

    // Stores the maximum prefix
    // sum of the array B[]
    int Y = max(b[0], 0);

    // Traverse the array B[]
    for (int i = 1; i < b.size(); i++) {
        b[i] += b[i - 1];
        Y = max(Y, b[i]);
    }
    return X + Y;
}

// Driver code
int main()
{
    vector<int> A = { 2, -1, 4, -5 };
    vector<int> B = { 4, -3, 12, 4, -3 };
    cout << maxPresum(A, B) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG {

  static int maxPresum(int [] a, int [] b)
  {

    // Stores the maximum prefix
    // sum of the array A[]
    int X = Math.max(a[0], 0);

    // Traverse the array A[]
    for (int i = 1; i < a.length; i++)
    {
      a[i] += a[i - 1];
      X = Math.max(X, a[i]);
    }

    // Stores the maximum prefix
    // sum of the array B[]
    int Y = Math.max(b[0], 0);

    // Traverse the array B[]
    for (int i = 1; i < b.length; i++) {
      b[i] += b[i - 1];
      Y = Math.max(Y, b[i]);
    }
    return X + Y;
  }

  // Driver code
  public static void main(String [] args)
  {
    int [] A = { 2, -1, 4, -5 };
    int [] B = { 4, -3, 12, 4, -3 };
    System.out.print(maxPresum(A, B));
  }
}

// This code is contributed by ukasp.
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

def maxPresum(a, b) :

    # Stores the maximum prefix
    # sum of the array A[]
    X = max(a[0], 0)

    # Traverse the array A[]
    for i in range(1, len(a)):
        a[i] += a[i - 1]
        X = max(X, a[i])

    # Stores the maximum prefix
    # sum of the array B[]
    Y = max(b[0], 0)

    # Traverse the array B[]
    for i in range(1, len(b)):
        b[i] += b[i - 1]
        Y = max(Y, b[i])

    return X + Y

# Driver code

A = [ 2, -1, 4, -5 ]
B = [ 4, -3, 12, 4, -3 ]
print(maxPresum(A, B))

# This code is contributed by code_hunt.
```

## C#

```
// C# Program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG {

  static int maxPresum(List<int> a, List<int> b)
  {

    // Stores the maximum prefix
    // sum of the array A[]
    int X = Math.Max(a[0], 0);

    // Traverse the array A[]
    for (int i = 1; i < a.Count; i++)
    {
      a[i] += a[i - 1];
      X = Math.Max(X, a[i]);
    }

    // Stores the maximum prefix
    // sum of the array B[]
    int Y = Math.Max(b[0], 0);

    // Traverse the array B[]
    for (int i = 1; i < b.Count; i++) {
      b[i] += b[i - 1];
      Y = Math.Max(Y, b[i]);
    }
    return X + Y;
  }

  // Driver code
  static void Main()
  {
    List<int> A = new List<int>(new int[]{ 2, -1, 4, -5 });
    List<int> B = new List<int>(new int[]{ 4, -3, 12, 4, -3 });
    Console.WriteLine(maxPresum(A, B));
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

    // Javascript Program to implement
    // the above approach

    function maxPresum(a, b)
    {

      // Stores the maximum prefix
      // sum of the array A[]
      let X = Math.max(a[0], 0);

      // Traverse the array A[]
      for (let i = 1; i < a.length; i++)
      {
        a[i] += a[i - 1];
        X = Math.max(X, a[i]);
      }

      // Stores the maximum prefix
      // sum of the array B[]
      let Y = Math.max(b[0], 0);

      // Traverse the array B[]
      for (let i = 1; i < b.length; i++) {
        b[i] += b[i - 1];
        Y = Math.max(Y, b[i]);
      }
      return X + Y;
    }

    let A = [ 2, -1, 4, -5 ];
    let B = [ 4, -3, 12, 4, -3 ];
    document.write(maxPresum(A, B));

</script>
```

**Output:** 

```
22
```

***时间复杂度:** O(M+N)*
***辅助空间:** O(1)*