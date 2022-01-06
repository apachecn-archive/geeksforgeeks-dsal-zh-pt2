# 对数组进行排序所需的最小增量或减量操作

> 原文:[https://www . geeksforgeeks . org/最小-递增-或-递减-操作-需要进行数组排序/](https://www.geeksforgeeks.org/minimum-increment-or-decrement-operations-required-to-make-the-array-sorted/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是通过执行最少数量的运算以非递减顺序对数组进行排序。在一次操作中，数组的一个元素可以增加或减少 **1** 。打印所需的最小操作数。
**举例:**

> **输入:** arr[] = {1，2，1，4，3}
> **输出:** 2
> 第三个元素(1)加 1，第四个元素(4)减 1
> 得到{1，2，2，3，3}
> **输入:** arr[] = {1，2，2，100}
> **输出:** 0
> 给定数组已经排序。

**观察:**由于我们希望最小化对数组进行排序所需的操作数量，因此以下内容应该成立:

*   数字永远不会减少到小于初始数组最小值的值。
*   数字永远不会增加到大于初始数组的最大值。
*   将一个数字从 X 更改为 Y 所需的操作数是绝对数量(X–Y)。

**逼近:**基于以上观察，这个问题可以用动态规划来解决。

1.  让 **DP(i，j)** 表示当 **i <sup>th</sup>** 元素等于 **j** 时，使数组的 **1 <sup>st</sup> i** 元素按非递减顺序排序所需的最小操作。
2.  现在 **DP(N，j)** 需要计算 **j** 的所有可能值，其中 **N** 是数组的大小。根据观察， **j ≥初始数组的最小元素**， **j ≤初始数组的最大元素**。
3.  **DP(i，j)** 中的基本情况，其中 **i = 1** 可以很容易地回答。将 **1 <sup>st</sup>** 元素按非递减顺序排序，使 **1 <sup>st</sup>** 元素等于 **j** 所需的最小操作是什么？。 **DP(1，j) = abs(数组[1]–j)**。
4.  现在考虑 **i > 1** 的 **DP(i，j)** 。如果将 **i <sup>th</sup>** 元素设置为 **j** ，则需要对**1<sup>ST</sup>**T14】I–1 元素进行排序，并且**(I–1)<sup>th</sup>**元素必须为 **≤ j** 即 **DP(i，j)=(DP(I–1，k)中的最小值)**
5.  利用上述递推关系和基本情况，结果很容易计算出来。

以下是上述 aprecht 的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum number
// of given operations required
// to sort the array
int getMinimumOps(vector<int> ar)
{
    // Number of elements in the array
    int n = ar.size();

    // Smallest element in the array
    int small = *min_element(ar.begin(), ar.end());

    // Largest element in the array
    int large = *max_element(ar.begin(), ar.end());

    /*
        dp(i, j) represents the minimum number
        of operations needed to make the
        array[0 .. i] sorted in non-decreasing
        order given that ith element is j
    */
    int dp[n][large + 1];

    // Fill the dp[]][ array for base cases
    for (int j = small; j <= large; j++) {
        dp[0][j] = abs(ar[0] - j);
    }

    /*
        Using results for the first (i - 1)
        elements, calculate the result
        for the ith element
    */
    for (int i = 1; i < n; i++) {
        int minimum = INT_MAX;
        for (int j = small; j <= large; j++) {

            /*
            If the ith element is j then we can have
            any value from small to j for the i-1 th
            element
            We choose the one that requires the
            minimum operations
        */
            minimum = min(minimum, dp[i - 1][j]);
            dp[i][j] = minimum + abs(ar[i] - j);
        }
    }

    /*
        If we made the (n - 1)th element equal to j
        we required dp(n-1, j) operations
        We choose the minimum among all possible
        dp(n-1, j) where j goes from small to large
    */
    int ans = INT_MAX;
    for (int j = small; j <= large; j++) {
        ans = min(ans, dp[n - 1][j]);
    }

    return ans;
}

// Driver code
int main()
{
    vector<int> ar = { 1, 2, 1, 4, 3 };

    cout << getMinimumOps(ar);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the minimum number
// of given operations required
// to sort the array
static int getMinimumOps(Vector<Integer> ar)
{
    // Number of elements in the array
    int n = ar.size();

    // Smallest element in the array
    int small = Collections.min(ar);

    // Largest element in the array
    int large = Collections.max(ar);

    /*
        dp(i, j) represents the minimum number
        of operations needed to make the
        array[0 .. i] sorted in non-decreasing
        order given that ith element is j
    */
    int [][]dp = new int[n][large + 1];

    // Fill the dp[]][ array for base cases
    for (int j = small; j <= large; j++)
    {
        dp[0][j] = Math.abs(ar.get(0) - j);
    }

    /*
        Using results for the first (i - 1)
        elements, calculate the result
        for the ith element
    */
    for (int i = 1; i < n; i++)
    {
        int minimum = Integer.MAX_VALUE;
        for (int j = small; j <= large; j++)
        {

            /*
            If the ith element is j then we can have
            any value from small to j for the i-1 th
            element
            We choose the one that requires the
            minimum operations
            */
            minimum = Math.min(minimum, dp[i - 1][j]);
            dp[i][j] = minimum + Math.abs(ar.get(i) - j);
        }
    }

    /*
        If we made the (n - 1)th element equal to j
        we required dp(n-1, j) operations
        We choose the minimum among all possible
        dp(n-1, j) where j goes from small to large
    */
    int ans = Integer.MAX_VALUE;
    for (int j = small; j <= large; j++)
    {
        ans = Math.min(ans, dp[n - 1][j]);
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    Integer []arr = { 1, 2, 1, 4, 3 };
    Vector<Integer> ar = new Vector<>(Arrays.asList(arr));

    System.out.println(getMinimumOps(ar));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum number
# of given operations required
# to sort the array
def getMinimumOps(ar):

    # Number of elements in the array
    n = len(ar)

    # Smallest element in the array
    small = min(ar)

    # Largest element in the array
    large = max(ar)

    """
        dp(i, j) represents the minimum number
        of operations needed to make the
        array[0 .. i] sorted in non-decreasing
        order given that ith element is j
    """
    dp = [[ 0 for i in range(large + 1)]
              for i in range(n)]

    # Fill the dp[]][ array for base cases
    for j in range(small, large + 1):
        dp[0][j] = abs(ar[0] - j)
    """
    /*
        Using results for the first (i - 1)
        elements, calculate the result
        for the ith element
    */
    """
    for i in range(1, n):
        minimum = 10**9
        for j in range(small, large + 1):

        # """
        #     /*
        #     If the ith element is j then we can have
        #     any value from small to j for the i-1 th
        #     element
        #     We choose the one that requires the
        #     minimum operations
        # """
            minimum = min(minimum, dp[i - 1][j])
            dp[i][j] = minimum + abs(ar[i] - j)
    """
    /*
        If we made the (n - 1)th element equal to j
        we required dp(n-1, j) operations
        We choose the minimum among all possible
        dp(n-1, j) where j goes from small to large
    */
    """
    ans = 10**9
    for j in range(small, large + 1):
        ans = min(ans, dp[n - 1][j])

    return ans

# Driver code
ar = [1, 2, 1, 4, 3]

print(getMinimumOps(ar))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Linq;
using System.Collections.Generic;            

class GFG
{

// Function to return the minimum number
// of given operations required
// to sort the array
static int getMinimumOps(List<int> ar)
{
    // Number of elements in the array
    int n = ar.Count;

    // Smallest element in the array
    int small = ar.Min();

    // Largest element in the array
    int large = ar.Max();

    /*
        dp(i, j) represents the minimum number
        of operations needed to make the
        array[0 .. i] sorted in non-decreasing
        order given that ith element is j
    */
    int [,]dp = new int[n, large + 1];

    // Fill the dp[], array for base cases
    for (int j = small; j <= large; j++)
    {
        dp[0, j] = Math.Abs(ar[0] - j);
    }

    /*
        Using results for the first (i - 1)
        elements, calculate the result
        for the ith element
    */
    for (int i = 1; i < n; i++)
    {
        int minimum = int.MaxValue;
        for (int j = small; j <= large; j++)
        {

            /*
            If the ith element is j then we can have
            any value from small to j for the i-1 th
            element
            We choose the one that requires the
            minimum operations
            */
            minimum = Math.Min(minimum, dp[i - 1, j]);
            dp[i, j] = minimum + Math.Abs(ar[i] - j);
        }
    }

    /*
        If we made the (n - 1)th element equal to j
        we required dp(n-1, j) operations
        We choose the minimum among all possible
        dp(n-1, j) where j goes from small to large
    */
    int ans = int.MaxValue;
    for (int j = small; j <= large; j++)
    {
        ans = Math.Min(ans, dp[n - 1, j]);
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 1, 4, 3 };
    List<int> ar = new List<int>(arr);

    Console.WriteLine(getMinimumOps(ar));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the minimum number
// of given operations required
// to sort the array
function getMinimumOps(ar)
{
    // Number of elements in the array
    var n = ar.length;

    // Smallest element in the array
    var small = Math.min.apply(Math,ar);

    // Largest element in the array
    var large = Math.max.apply(Math,ar);

    /*
        dp(i, j) represents the minimum number
        of operations needed to make the
        array[0 .. i] sorted in non-decreasing
        order given that ith element is j
    */
    var dp = new Array(n);
    var i,j;
    for(i=0;i<dp.length;i++)
        dp[i] = new Array(large+1);

    // Fill the dp[]][ array for base cases
    for (j = small; j <= large; j++) {
        dp[0][j] = Math.abs(ar[0] - j);
    }

    /*
        Using results for the first (i - 1)
        elements, calculate the result
        for the ith element
    */
    for (i = 1; i < n; i++) {
        var minimum = 2147483647;
        for (j = small; j <= large; j++) {

            /*
            If the ith element is j then we can have
            any value from small to j for the i-1 th
            element
            We choose the one that requires the
            minimum operations
        */
            minimum = Math.min(minimum, dp[i - 1][j]);
            dp[i][j] = minimum + Math.abs(ar[i] - j);
        }
    }

    /*
        If we made the (n - 1)th element equal to j
        we required dp(n-1, j) operations
        We choose the minimum among all possible
        dp(n-1, j) where j goes from small to large
    */
    var ans = 2147483647;
    for (j = small; j <= large; j++) {
        ans = Math.min(ans, dp[n - 1][j]);
    }

    return ans;
}

// Driver code
    var ar = [1, 2, 1, 4, 3];

    document.write(getMinimumOps(ar));

</script>
```

**Output:** 

```
2
```

**复杂度分析:**
**时间复杂度:** O(N*R)，上述方法的时间复杂度为 O(N*R)，其中 N 为数组中的元素个数，R =数组中最大–最小的元素+ 1。
**辅助空间:** O(N *大)