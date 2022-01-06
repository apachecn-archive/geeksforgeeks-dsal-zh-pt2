# 具有总和值 K 的最长递增子序列

> 原文:[https://www . geeksforgeeks . org/最长递增子序列-具有和值-atmat-k/](https://www.geeksforgeeks.org/longest-increasing-subsequence-having-sum-value-atmost-k/)

给定一个大小为 **N** 的整数数组 **arr[]** 和一个整数 **K** 。任务是找出和小于等于 **K** 的最长子序列的长度。

**示例:**

> **输入:** arr[] = {0，8，4，12，2，10，6，14，1，9，5，13，3，11，7，15} K = 40
> **输出:** 5
> **解释:**
> 如果我们选择子序列{0，1，3，7，15}，那么总和将是 **26** ，小于 **40** 。因此，最长增加的可能子序列长度是 **5** 。
> 
> **输入:** arr[] = {5，8，3，7，9，1 } K = 4
> T3】输出: 1

**进场:**

1.  上述问题可以用递归来解决。
    *   如果总和小于 **K** ，则选择该位置的元素，并探索其余项目。
    *   把元素留在那个位置，探索剩下的。

递归关系将被给出为:

> ***递推关系:***
> T(N) = max(求解(arr，N，arr[i]，i+1，K-arr[i])+1，求解(arr，N，prevele，i+1，K))；
> ***基础条件:***
> 如果(i > = N || K < = 0)
> 返回 0

下面是上述方法的实现:

## C++

```
// C++ program to find the Longest
// Increasing Subsequence having sum
// value atmost K
#include <bits/stdc++.h>
using namespace std;

int solve(int arr[], int N,
          int prevele, int i, int K)
{
    // check for base cases
    if (i >= N || K <= 0)
        return 0;

    // check if it is possible to take
    // current elements
    if (arr[i] <= prevele
        || (K - arr[i] < 0)) {

        return solve(arr, N, prevele,
                     i + 1, K);
    }

    // if current element is ignored
    else {
        int ans = max(
            solve(arr, N, arr[i],
                  i + 1, K - arr[i])
                + 1,
            solve(arr, N, prevele,
                  i + 1, K));
        return ans;
    }
}

// Driver Code
int main()
{
    int N = 16;
    int arr[N]
        = { 0, 8, 4, 12,
            2, 10, 6, 14,
            1, 9, 5, 13,
            3, 11, 7, 15 };
    int K = 40;

    cout << solve(arr, N,
                  INT_MIN, 0, K)
         << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the Longest
// Increasing Subsequence having sum
// value atmost K
import java.io.*;

class GFG{

static int solve(int arr[], int N,
                 int prevele, int i, int K)
{

    // Check for base cases
    if (i >= N || K <= 0)
        return 0;

    // Check if it is possible to take
    // current elements
    if (arr[i] <= prevele ||
       (K - arr[i] < 0))
    {
        return solve(arr, N, prevele,
                     i + 1, K);
    }

    // If current element is ignored
    else
    {
        int ans = Math.max(solve(arr, N, arr[i],
                              i + 1, K - arr[i]) + 1,
                           solve(arr, N, prevele,
                                 i + 1, K));

        return ans;
    }
}

// Driver code
public static void main (String[] args)
{
    int N = 16;
    int arr[] = new int[]{ 0, 8, 4, 12,
                           2, 10, 6, 14,
                           1, 9, 5, 13,
                           3, 11, 7, 15 };
    int K = 40;

    System.out.print(solve(arr, N,
          Integer.MIN_VALUE, 0, K));
}
}

// This code is contributed by Pratima Pandey
```

## 蟒蛇 3

```
# Python3 program to find the Longest
# Increasing Subsequence having sum
# value atmost K
import sys

def solve(arr, N, prevele, i, K):

    # Check for base cases
    if (i >= N or K <= 0):
        return 0;

    # Check if it is possible to take
    # current elements
    if (arr[i] <= prevele or
       (K - arr[i] < 0)):
        return solve(arr, N, prevele,
                     i + 1, K);

    # If current element is ignored
    else:
        ans = max(solve(arr, N, arr[i],
                     i + 1, K - arr[i]) + 1,
                  solve(arr, N, prevele,
                        i + 1, K));

        return ans;

# Driver code
if __name__ == '__main__':

    N = 16;
    arr = [ 0, 8, 4, 12,
            2, 10, 6, 14,
            1, 9, 5, 13,
            3, 11, 7, 15 ];
    K = 40;

    print(solve(arr, N, -sys.maxsize, 0, K));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to find the Longest
// Increasing Subsequence having sum
// value atmost K
using System;

class GFG{

static int solve(int[] arr, int N,
                 int prevele, int i, int K)
{

    // Check for base cases
    if (i >= N || K <= 0)
        return 0;

    // Check if it is possible to take
    // current elements
    if (arr[i] <= prevele ||
       (K - arr[i] < 0))
    {
        return solve(arr, N, prevele,
                     i + 1, K);
    }

    // If current element is ignored
    else
    {
        int ans = Math.Max(solve(arr, N, arr[i],
                                 i + 1, K - arr[i]) + 1,
                           solve(arr, N, prevele,
                                 i + 1, K));

        return ans;
    }
}

// Driver code
public static void Main ()
{
    int N = 16;
    int[] arr = new int[]{ 0, 8, 4, 12,
                           2, 10, 6, 14,
                           1, 9, 5, 13,
                           3, 11, 7, 15 };
    int K = 40;

    Console.Write(solve(arr, N,
        Int32.MinValue, 0, K));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program to find the Longest
// Increasing Subsequence having sum
// value atmost K

function solve(arr, N, prevele, i, K)
{
    // check for base cases
    if (i >= N || K <= 0)
        return 0;

    // check if it is possible to take
    // current elements
    if (arr[i] <= prevele
        || (K - arr[i] < 0)) {

        return solve(arr, N, prevele,
                     i + 1, K);
    }

    // if current element is ignored
    else {
        var ans = Math.max(
            solve(arr, N, arr[i],
                  i + 1, K - arr[i])
                + 1,
            solve(arr, N, prevele,
                  i + 1, K));
        return ans;
    }
}

// Driver Code
var N = 16;
var arr
    = [0, 8, 4, 12,
        2, 10, 6, 14,
        1, 9, 5, 13,
        3, 11, 7, 15];
var K = 40;
document.write( solve(arr, N,
              -1000000000, 0, K));

</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O (1)*