# 满足给定条件的最长子序列

> 原文:[https://www . geesforgeks . org/满足给定条件的最长子序列/](https://www.geeksforgeeks.org/longest-sub-sequence-that-satisfies-the-given-conditions/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是找到给定数组中最长的子序列，使得对于子序列 **(arr[i]，arr[j])** 中的所有对 **i！= j** 或者 **arr[i]除 arr[j]** 或者反之。如果不存在这样的子序列，则打印-1。
**举例:**

> **输入:** arr[] = {2，4，6，1，3，11}
> **输出:** 3
> 最长有效子序列为{1，2，6}和{1，3，6}。
> **输入:** arr[] = {21，22，6，4，13，7，332}
> **输出:** 2

**方法:**这个问题是[最长递增子序列](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/)问题的简单变异。改变的是基本条件和通过给定数组排序来减少计算次数的技巧。

*   首先对给定的数组进行排序，这样我们只需要检查 **i > j** 的**arr【I】>arr【j】**处的值。
*   然后我们使用两个循环向前移动，外环从 **1** 运行到 **N** ，内环从 **0** 运行到 **i** 。
*   现在，在内部循环中，我们必须找到**arr【j】**的编号，其中 **j** 是从 **0** 到**I–1**的编号，它将元素**arr【I】**分开。
*   递推关系为 **dp[i] = max(dp[i]，1 + dp[j])** 。
*   我们将更新名为 **res** 的变量中的最大**DP【I】**值，这将是最终答案。

以下是上述方法的实现:

## C++

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the length of the
// longest required sub-sequence
int find(int n, int a[])
{
    // Sort the array
    sort(a, a + n);

    // To store the resultant length
    int res = 1;
    int dp[n];

    // If array contains only one element
    // then it divides itself
    dp[0] = 1;

    for (int i = 1; i < n; i++) {

        // Every element divides itself
        dp[i] = 1;

        // Count for all numbers which
        // are lesser than a[i]
        for (int j = 0; j < i; j++) {

            if (a[i] % a[j] == 0) {

                // If a[i] % a[j] then update the maximum
                // subsequence length,
                // dp[i] = max(dp[i], 1 + dp[j])
                // where j is in the range [0, i-1]
                dp[i] = std::max(dp[i], 1 + dp[j]);
            }
        }

        res = std::max(res, dp[i]);
    }

    // If array contains only one element
    // then i = j which doesn't satisfy the condition
    return (res == 1) ? -1 : res;
}

// Driver code
int main()
{
    int a[] = { 2, 4, 6, 1, 3, 11 };
    int n = sizeof(a) / sizeof(int);

    cout << find(n, a);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;
import java.io.*;

class GFG
{

// Function to return the length of the
// longest required sub-sequence
static int find(int n, int a[])
{
    // Sort the array
    Arrays.sort(a);

    // To store the resultant length
    int res = 1;
    int dp[] = new int[n];

    // If array contains only one element
    // then it divides itself
    dp[0] = 1;

    for (int i = 1; i < n; i++)
    {

        // Every element divides itself
        dp[i] = 1;

        // Count for all numbers which
        // are lesser than a[i]
        for (int j = 0; j < i; j++)
        {

            if (a[i] % a[j] == 0)
            {

                // If a[i] % a[j] then update the maximum
                // subsequence length,
                // dp[i] = Math.max(dp[i], 1 + dp[j])
                // where j is in the range [0, i-1]
                dp[i] = Math.max(dp[i], 1 + dp[j]);
            }
        }

        res = Math.max(res, dp[i]);
    }

    // If array contains only one element
    // then i = j which doesn't satisfy the condition
    return (res == 1) ? -1 : res;
}

// Driver code
public static void main (String[] args)
{
    int a[] = { 2, 4, 6, 1, 3, 11 };
    int n = a.length;

    System.out.println (find(n, a));
}
}

// This code is contributed by jit_t
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the length of the
# longest required sub-sequence
def find(n, a) :

    # Sort the array
    a.sort();

    # To store the resultant length
    res = 1;
    dp = [0]*n;

    # If array contains only one element
    # then it divides itself
    dp[0] = 1;

    for i in range(1, n) :

        # Every element divides itself
        dp[i] = 1;

        # Count for all numbers which
        # are lesser than a[i]
        for j in range(i) :

            if (a[i] % a[j] == 0) :

                # If a[i] % a[j] then update the maximum
                # subsequence length,
                # dp[i] = max(dp[i], 1 + dp[j])
                # where j is in the range [0, i-1]
                dp[i] = max(dp[i], 1 + dp[j]);

        res = max(res, dp[i]);

    # If array contains only one element
    # then i = j which doesn't satisfy the condition
    if (res == 1):
        return -1
    else :
        return res;

# Driver code
if __name__ == "__main__" :

    a = [ 2, 4, 6, 1, 3, 11 ];
    n = len(a);

    print(find(n, a));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the length of the
// longest required sub-sequence
static int find(int n, int []a)
{
    // Sort the array
    Array.Sort(a);

    // To store the resultant length
    int res = 1;
    int []dp = new int[n];

    // If array contains only one element
    // then it divides itself
    dp[0] = 1;

    for (int i = 1; i < n; i++)
    {

        // Every element divides itself
        dp[i] = 1;

        // Count for all numbers which
        // are lesser than a[i]
        for (int j = 0; j < i; j++)
        {

            if (a[i] % a[j] == 0)
            {

                // If a[i] % a[j] then update the maximum
                // subsequence length,
                // dp[i] = Math.max(dp[i], 1 + dp[j])
                // where j is in the range [0, i-1]
                dp[i] = Math.Max(dp[i], 1 + dp[j]);
            }
        }

        res = Math.Max(res, dp[i]);
    }

    // If array contains only one element
    // then i = j which doesn't satisfy the condition
    return (res == 1) ? -1 : res;
}

// Driver code
public static void Main ()
{
    int []a = { 2, 4, 6, 1, 3, 11 };
    int n = a.Length;

    Console.WriteLine(find(n, a));
}
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>
// javascript implementation of the approach

// Function to return the length of the
// longest required sub-sequence
function find(n , a)
{
    // Sort the array
    a.sort();

    // To store the resultant length
    var res = 1;
    var dp = Array.from({length: n}, (_, i) => 0);

    // If array contains only one element
    // then it divides itself
    dp[0] = 1;

    for (var i = 1; i < n; i++)
    {

        // Every element divides itself
        dp[i] = 1;

        // Count for all numbers which
        // are lesser than a[i]
        for (var j = 0; j < i; j++)
        {

            if (a[i] % a[j] == 0)
            {

                // If a[i] % a[j] then update the maximum
                // subsequence length,
                // dp[i] = Math.max(dp[i], 1 + dp[j])
                // where j is in the range [0, i-1]
                dp[i] = Math.max(dp[i], 1 + dp[j]);
            }
        }

        res = Math.max(res, dp[i]);
    }

    // If array contains only one element
    // then i = j which doesn't satisfy the condition
    return (res == 1) ? -1 : res;
}

// Driver code
    var a = [ 2, 4, 6, 1, 3, 11 ];
    var n = a.length;

    document.write(find(n, a));

// This code is contributed by jit_t

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
3
```