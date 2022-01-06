# 最大子序列和，使得任意两个相邻元素的索引至少相差 3

> 原文:[https://www . geeksforgeeks . org/最大子序列-任意两个相邻元素的和索引-至少相差 3/](https://www.geeksforgeeks.org/maximum-sub-sequence-sum-such-that-indices-of-any-two-adjacent-elements-differs-at-least-by-3/)

给定整数数组 **arr[]** ，任务是找到数组中任何子序列的**最大和**，使得所选序列中的任何两个相邻元素在给定数组中的索引至少相差 3。
换句话说，如果你选择**arr【I】**那么你可以选择的下一个元素是**arr【I+3】**、**arr【I+4】**等等……但是你不能选择**arr【I+1】**和**arr【I+2】**。
**举例:**

> **输入:** arr[] = {1，2，-2，4，3}
> **输出:** 5
> {1，4}和{2，3}是仅有的最大和的子序列
> 。
> **输入:** arr[] = {1，2，72，4，3，9}
> **输出:** 81

**天真方法:**我们生成数组的所有可能子集，并检查当前子集是否满足条件。如果是，那么我们将它的和与我们到目前为止得到的最大和进行比较。这不是一个有效的方法，因为它需要指数级的时间。
**高效途径:**这个问题可以使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)解决。让我们决定民主党的状态。假设 **dp[i]** 是从索引 **0** 开始到索引 **i** 结束的子序列的最大可能和。现在，我们必须找到这个状态和低阶状态之间的递归关系。
在这种情况下，对于索引 **i** ，我们将有两个选择:

1.  选择当前索引:在这种情况下，关系将是**DP[I]= arr[I]+DP[I–3]**。
2.  跳过当前索引:关系将为**DP[I]= DP[I–1]**。

我们将选择最大化我们结果的道路。因此，最终的关系将是:
**DP[I]= max(DP[I–3]+arr[I]，DP[I–1])**
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum sum
// of the sub-sequence such that two
// consecutive elements have a difference of
// at least 3 in their indices
// in the given array
int max_sum(int a[], int n)
{

    int dp[n];

    // If there is a single element in the array
    if (n == 1) {

        // Either select it or don't
        dp[0] = max(0, a[0]);
    }

    // If there are two elements
    else if (n == 2) {

        // Either select the first
        // element or don't
        dp[0] = max(0, a[0]);

        // Either select the first or the second element
        // or don't select any element
        dp[1] = max(a[1], dp[0]);
    }
    else if (n >= 3) {

        // Either select the first
        // element or don't
        dp[0] = max(0, a[0]);

        // Either select the first or the second element
        // or don't select any element
        dp[1] = max(a[1], max(0, a[0]));

        // Either select first, second, third or nothing
        dp[2] = max(a[2], max(a[1], max(0, a[0])));

        int i = 3;

        // For the rest of the elements
        while (i < n) {

            // Either select the best sum till
            // previous_index or select the current
            // element + best_sum till index-3
            dp[i] = max(dp[i - 1], a[i] + dp[i - 3]);
            i++;
        }
    }

    return dp[n - 1];
}

// Driver code
int main()
{
    int arr[] = { 1, 2, -2, 4, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << max_sum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the maximum sum
// of the sub-sequence such that two
// consecutive elements have a difference of
// at least 3 in their indices
// in the given array
static int max_sum(int a[], int n)
{

    int []dp = new int[n];

    // If there is a single element in the array
    if (n == 1)
    {

        // Either select it or don't
        dp[0] = Math.max(0, a[0]);
    }

    // If there are two elements
    else if (n == 2)
    {

        // Either select the first
        // element or don't
        dp[0] = Math.max(0, a[0]);

        // Either select the first or the second element
        // or don't select any element
        dp[1] = Math.max(a[1], dp[0]);
    }
    else if (n >= 3)
    {

        // Either select the first
        // element or don't
        dp[0] = Math.max(0, a[0]);

        // Either select the first or the second element
        // or don't select any element
        dp[1] = Math.max(a[1], Math.max(0, a[0]));

        // Either select first, second, third or nothing
        dp[2] = Math.max(a[2], Math.max(a[1], Math.max(0, a[0])));

        int i = 3;

        // For the rest of the elements
        while (i < n)
        {

            // Either select the best sum till
            // previous_index or select the current
            // element + best_sum till index-3
            dp[i] = Math.max(dp[i - 1], a[i] + dp[i - 3]);
            i++;
        }
    }

    return dp[n - 1];
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, -2, 4, 3 };
    int n = arr.length;

    System.out.println(max_sum(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum sum
# of the sub-sequence such that two
# consecutive elements have a difference of
# at least 3 in their indices
# in the given array
def max_sum(a, n) :

    dp = [0]*n;

    # If there is a single element in the array
    if (n == 1) :

        # Either select it or don't
        dp[0] = max(0, a[0]);

    # If there are two elements
    elif (n == 2) :

        # Either select the first
        # element or don't
        dp[0] = max(0, a[0]);

        # Either select the first or the second element
        # or don't select any element
        dp[1] = max(a[1], dp[0]);

    elif (n >= 3) :

        # Either select the first
        # element or don't
        dp[0] = max(0, a[0]);

        # Either select the first or the second element
        # or don't select any element
        dp[1] = max(a[1], max(0, a[0]));

        # Either select first, second, third or nothing
        dp[2] = max(a[2], max(a[1], max(0, a[0])));

        i = 3;

        # For the rest of the elements
        while (i < n) :

            # Either select the best sum till
            # previous_index or select the current
            # element + best_sum till index-3
            dp[i] = max(dp[i - 1], a[i] + dp[i - 3]);
            i += 1;

    return dp[n - 1];

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, -2, 4, 3 ];
    n = len(arr);

    print(max_sum(arr, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the maximum sum
// of the sub-sequence such that two
// consecutive elements have a difference of
// at least 3 in their indices
// in the given array
static int max_sum(int []a, int n)
{

    int []dp = new int[n];

    // If there is a single element in the array
    if (n == 1)
    {

        // Either select it or don't
        dp[0] = Math.Max(0, a[0]);
    }

    // If there are two elements
    else if (n == 2)
    {

        // Either select the first
        // element or don't
        dp[0] = Math.Max(0, a[0]);

        // Either select the first or the second element
        // or don't select any element
        dp[1] = Math.Max(a[1], dp[0]);
    }
    else if (n >= 3)
    {

        // Either select the first
        // element or don't
        dp[0] = Math.Max(0, a[0]);

        // Either select the first or the second element
        // or don't select any element
        dp[1] = Math.Max(a[1], Math.Max(0, a[0]));

        // Either select first, second, third or nothing
        dp[2] = Math.Max(a[2], Math.Max(a[1], Math.Max(0, a[0])));

        int i = 3;

        // For the rest of the elements
        while (i < n)
        {

            // Either select the best sum till
            // previous_index or select the current
            // element + best_sum till index-3
            dp[i] = Math.Max(dp[i - 1], a[i] + dp[i - 3]);
            i++;
        }
    }

    return dp[n - 1];
}

// Driver code
static public void Main ()
{

    int []arr = { 1, 2, -2, 4, 3 };
    int n = arr.Length;

    Console.Write(max_sum(arr, n));
}
}

// This code is contributed by ajit..
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the maximum sum
    // of the sub-sequence such that two
    // consecutive elements have a difference of
    // at least 3 in their indices
    // in the given array
    function max_sum(a, n)
    {

        let dp = new Array(n);

        // If there is a single element in the array
        if (n == 1)
        {

            // Either select it or don't
            dp[0] = Math.max(0, a[0]);
        }

        // If there are two elements
        else if (n == 2)
        {

            // Either select the first
            // element or don't
            dp[0] = Math.max(0, a[0]);

            // Either select the first or the second element
            // or don't select any element
            dp[1] = Math.max(a[1], dp[0]);
        }
        else if (n >= 3)
        {

            // Either select the first
            // element or don't
            dp[0] = Math.max(0, a[0]);

            // Either select the first or the second element
            // or don't select any element
            dp[1] = Math.max(a[1], Math.max(0, a[0]));

            // Either select first, second, third or nothing
            dp[2] = Math.max(a[2], Math.max(a[1], Math.max(0, a[0])));

            let i = 3;

            // For the rest of the elements
            while (i < n)
            {

                // Either select the best sum till
                // previous_index or select the current
                // element + best_sum till index-3
                dp[i] = Math.max(dp[i - 1], a[i] + dp[i - 3]);
                i++;
            }
        }

        return dp[n - 1];
    }

    let arr = [ 1, 2, -2, 4, 3 ];
    let n = arr.length;

    document.write(max_sum(arr, n));

</script>
```

**Output:** 

```
5
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)