# 通过最多两次反转任何子阵列元素的符号来最大化子阵列和

> 原文:[https://www . geesforgeks . org/maximize-subarray-sum-by-inventing-sign-of-any-subarray-至多两次/](https://www.geeksforgeeks.org/maximize-subarray-sum-by-inverting-sign-of-elements-of-any-subarray-at-most-twice/)

给定一个大小为 **n** 的数组 **A** ，最多应用两次给定操作后，求最大子阵和。在一个操作中，选择任意两个索引 **i** 和 **j** ，并将索引 **i** 到索引 **j、**的所有元素的符号反转，即 I 到 j 范围内的所有正元素变为负，所有负元素变为正。

**示例:**

> **输入:** A[] = {1，-2，-4，3，5，-6}
> **输出:** 21
> **解释:**
> 将数组从索引 1 反转到索引 2 &从索引 5 反转到索引 5(基于 0 的索引)，得到最大子数组和= 21 的{1，2，4，3，5，6}
> 
> **输入:** A[] = {2，-1，-18，3，-1，-39，5，-2 }
> T3】输出: 69

**做法:**思路是首先将所有元素合并成组。也就是说，所有连续的正元素将被求和为一个整数，并将被放置在新的数组 **arr** 中，对于连续的负元素也是如此。之后，问题简化为从该阵列中最多反相两个元素后找到[最大子阵列和](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)。

想法是使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)。现在，创建一个 **dp[n][3]** 数组，在该 dp 数组的每个索引处，维护三个数字:

*   第一个数字表示反转数组中的 no 元素后的最大子数组和。因此， **dp[i][0]** 将简单地运行卡丹算法的逻辑来获得最大子阵列和。
*   第二个数字表示将数组中的一个元素反相后的最大子数组和。因此， **dp[i][1]** 将是两个值的最大值，即 **dp[i-1][1] + arr[i]** (将一个元素反相到 I，然后将当前元素加到 I 之后的最大子阵列和)和 **dp[i][0]+ (-arr[i])** (即，将之前的未反相的最大子阵列和反相到 i-1，然后将当前元素加到 I 之后的最大子阵列和)。
*   第三个数字表示将数组中的两个元素反相后的最大子数组和。因此， **dp[i][2]** 将是两个值的最大值，即![            ](img/f7002fbb717cad93048e12827d00f7a4.png "Rendered by QuickLaTeX.com")(将一个元素反相到 i-1 后再加上当前元素后的最大子阵列和)和 ![            ](img/f7002fbb717cad93048e12827d00f7a4.png "Rendered by QuickLaTeX.com") (将两个元素反相到 i-1 后再加上当前元素后的最大子阵列和)。
*   保留一个 **maxSum** 变量，该变量将在每次索引后更新，并将等于 **maxSum** 的前一个值和所有三个当前值(即 **dp[i][0]、dp[i][1]和 dp[i][2])的最大值。**
*   返回 **maxSum** ，这就是答案。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to merge alternate elements into groups
// of positive and negative
void mergeElements(int n, vector<int>& arr, int* A)
{
    int i = 0;
    int sum = 0;
    while (i < n) {
        sum = 0;
        while (i < n && A[i] >= 0) {
            sum += A[i];
            i++;
        }
        if (sum > 0) {
            arr.push_back(sum);
        }
        sum = 0;
        while (i < n && A[i] < 0) {
            sum += A[i];
            i++;
        }
        if (sum < 0) {
            arr.push_back(sum);
        }
    }
}

// Function to return the maximum
// after inverting at most 2 elements
int findMaxSum(vector<int>& arr, int n)
{
    int maxSum = 0;
    vector<vector<int> > dp(
n,
 vector<int>(3, INT_MIN));

    dp[0][0] = max(0, arr[0]);
    dp[0][1] = -1 * arr[0];
    for (int i = 1; i < n; ++i) {

        // dp[i][0] represents sum till ith index
        // without inverting any element.
        dp[i][0] = max(arr[i],
dp[i - 1][0] + arr[i]);

        // dp[i][1] represents sum till ith index
        // after inverting one element.
        dp[i][1] = max(0, dp[i - 1][0]) - arr[i];
        if (i >= 1) {
            dp[i][1] = max(dp[i][1],
dp[i - 1][1] + arr[i]);

            // dp[i][2] represents sum till ith index
            // after inverting two elements.
            dp[i][2] = dp[i - 1][1] - arr[i];
        }

        if (i >= 2) {
            dp[i][2] = max(dp[i][2],
dp[i - 1][2] + arr[i]);
        }
        maxSum = max(maxSum, dp[i][0]);
        maxSum = max(maxSum, dp[i][1]);
        maxSum = max(maxSum, dp[i][2]);
    }
    return maxSum;
}

// Driver Code
int main()
{
    int n = 8;
    int A[8] = { 2, -1, -18, 3, -1, -39, 5, -2 };

    // vector 'arr' contains sum of consecutive
    // positive or negative elements.
    vector<int> arr;
    mergeElements(n, arr, A);

    cout << findMaxSum(arr, arr.size());
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to merge alternate elements into groups
// of positive and negative
static Vector<Integer> mergeElements(int n, Vector<Integer> arr, int[] A)
{
    int i = 0;
    int sum = 0;
    while (i < n) {
        sum = 0;
        while (i < n && A[i] >= 0) {
            sum += A[i];
            i++;
        }
        if (sum > 0) {
            arr.add(sum);
        }
        sum = 0;
        while (i < n && A[i] < 0) {
            sum += A[i];
            i++;
        }
        if (sum < 0) {
            arr.add(sum);
        }
    }
    return arr;
}

// Function to return the maximum
// after inverting at most 2 elements
static int findMaxSum(Vector<Integer> arr, int n)
{
    int maxSum = 0;
    int [][]dp = new int[n][3];

    dp[0][0] = Math.max(0, arr.get(0));
    dp[0][1] = -1 * arr.get(0);
    for (int i = 1; i < n; ++i) {

        // dp[i][0] represents sum till ith index
        // without inverting any element.
        dp[i][0] = Math.max(arr.get(i),
dp[i - 1][0] + arr.get(i));

        // dp[i][1] represents sum till ith index
        // after inverting one element.
        dp[i][1] = Math.max(0, dp[i - 1][0]) - arr.get(i);
        if (i >= 1) {
            dp[i][1] = Math.max(dp[i][1],
dp[i - 1][1] + arr.get(i));

            // dp[i][2] represents sum till ith index
            // after inverting two elements.
            dp[i][2] = dp[i - 1][1] - arr.get(i);
        }

        if (i >= 2) {
            dp[i][2] = Math.max(dp[i][2],
dp[i - 1][2] + arr.get(i));
        }
        maxSum = Math.max(maxSum, dp[i][0]);
        maxSum = Math.max(maxSum, dp[i][1]);
        maxSum = Math.max(maxSum, dp[i][2]);
    }
    return maxSum;
}

// Driver Code
public static void main(String[] args)
{
    int n = 8;
    int A[] = { 2, -1, -18, 3, -1, -39, 5, -2 };

    // vector 'arr' contains sum of consecutive
    // positive or negative elements.
    Vector<Integer> arr = new Vector<Integer>();
   arr = mergeElements(n, arr, A);

    System.out.print(findMaxSum(arr, arr.size()));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# python program for the above approach

INT_MIN = -2147483648
# Function to merge alternate elements into groups
# of positive and negative

def mergeElements(n, arr, A):

    i = 0
    sum = 0
    while (i < n):
        sum = 0
        while (i < n and A[i] >= 0):
            sum += A[i]
            i += 1

        if (sum > 0):
            arr.append(sum)

        sum = 0
        while (i < n and A[i] < 0):
            sum += A[i]
            i += 1

        if (sum < 0):
            arr.append(sum)

# Function to return the maximum
# after inverting at most 2 elements
def findMaxSum(arr, n):

    maxSum = 0
    dp = [[INT_MIN for _ in range(3)] for _ in range(n)]

    dp[0][0] = max(0, arr[0])
    dp[0][1] = -1 * arr[0]
    for i in range(1, n):

        # dp[i][0] represents sum till ith index
        # without inverting any element.
        dp[i][0] = max(arr[i], dp[i - 1][0] + arr[i])

        # dp[i][1] represents sum till ith index
        # after inverting one element.
        dp[i][1] = max(0, dp[i - 1][0]) - arr[i]
        if (i >= 1):
            dp[i][1] = max(dp[i][1], dp[i - 1][1] + arr[i])

            # dp[i][2] represents sum till ith index
            # after inverting two elements.
            dp[i][2] = dp[i - 1][1] - arr[i]

        if (i >= 2):
            dp[i][2] = max(dp[i][2], dp[i - 1][2] + arr[i])

        maxSum = max(maxSum, dp[i][0])
        maxSum = max(maxSum, dp[i][1])
        maxSum = max(maxSum, dp[i][2])

    return maxSum

# Driver Code
if __name__ == "__main__":

    n = 8
    A = [2, -1, -18, 3, -1, -39, 5, -2]

    # vector 'arr' contains sum of consecutive
    # positive or negative elements.
    arr = []
    mergeElements(n, arr, A)
    print(findMaxSum(arr, len(arr)))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to merge alternate elements into groups
    // of positive and negative
    static void mergeElements(int n, List<int> arr, int[] A)
    {
        int i = 0;
        int sum = 0;
        while (i < n) {
            sum = 0;
            while (i < n && A[i] >= 0) {
                sum += A[i];
                i++;
            }
            if (sum > 0) {
                arr.Add(sum);
            }
            sum = 0;
            while (i < n && A[i] < 0) {
                sum += A[i];
                i++;
            }
            if (sum < 0) {
                arr.Add(sum);
            }
        }
    }

    // Function to return the maximum
    // after inverting at most 2 elements
    static int findMaxSum(List<int> arr, int n)
    {
        int maxSum = 0;
        int[, ] dp = new int[n, 3];
        for (int i = 0; i < n; i++)
            for (int j = 0; j < 3; j++)
                dp[i, j] = Int32.MinValue;

        dp[0, 0] = Math.Max(0, arr[0]);
        dp[0, 1] = -1 * arr[0];
        for (int i = 1; i < n; ++i) {

            // dp[i][0] represents sum till ith index
            // without inverting any element.
            dp[i, 0]
                = Math.Max(arr[i], dp[i - 1, 0] + arr[i]);

            // dp[i][1] represents sum till ith index
            // after inverting one element.
            dp[i, 1] = Math.Max(0, dp[i - 1, 0]) - arr[i];
            if (i >= 1) {
                dp[i, 1] = Math.Max(dp[i, 1],
                                    dp[i - 1, 1] + arr[i]);

                // dp[i][2] represents sum till ith index
                // after inverting two elements.
                dp[i, 2] = dp[i - 1, 1] - arr[i];
            }

            if (i >= 2) {
                dp[i, 2] = Math.Max(dp[i, 2],
                                    dp[i - 1, 2] + arr[i]);
            }
            maxSum = Math.Max(maxSum, dp[i, 0]);
            maxSum = Math.Max(maxSum, dp[i, 1]);
            maxSum = Math.Max(maxSum, dp[i, 2]);
        }
        return maxSum;
    }

    // Driver Code
    public static void Main()
    {
        int n = 8;
        int[] A = { 2, -1, -18, 3, -1, -39, 5, -2 };

        // vector 'arr' contains sum of consecutive
        // positive or negative elements.
        List<int> arr = new List<int>();
        mergeElements(n, arr, A);

        Console.WriteLine(findMaxSum(arr, arr.Count));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to merge alternate elements into groups
        // of positive and negative
        function mergeElements(n, arr, A) {
            let i = 0;
            let sum = 0;
            while (i < n) {
                sum = 0;
                while (i < n && A[i] >= 0) {
                    sum += A[i];
                    i++;
                }
                if (sum > 0) {
                    arr.push(sum);
                }
                sum = 0;
                while (i < n && A[i] < 0) {
                    sum += A[i];
                    i++;
                }
                if (sum < 0) {
                    arr.push(sum);
                }
            }
        }

        // Function to return the maximum
        // after inverting at most 2 elements
        function findMaxSum(arr, n) {
            let maxSum = 0;

            let dp = new Array(n);

            for (let i = 0; i < dp.length; i++) {
                dp[i] = new Array(3).fill(Number.MIN_VALUE);
            }

            dp[0][0] = Math.max(0, arr[0]);
            dp[0][1] = -1 * arr[0];
            for (let i = 1; i < n; ++i) {

                // dp[i][0] represents sum till ith index
                // without inverting any element.
                dp[i][0] = Math.max(arr[i],
                    dp[i - 1][0] + arr[i]);

                // dp[i][1] represents sum till ith index
                // after inverting one element.
                dp[i][1] = Math.max(0, dp[i - 1][0]) - arr[i];
                if (i >= 1) {
                    dp[i][1] = Math.max(dp[i][1],
                        dp[i - 1][1] + arr[i]);

                    // dp[i][2] represents sum till ith index
                    // after inverting two elements.
                    dp[i][2] = dp[i - 1][1] - arr[i];
                }

                if (i >= 2) {
                    dp[i][2] = Math.max(dp[i][2],
                        dp[i - 1][2] + arr[i]);
                }
                maxSum = Math.max(maxSum, dp[i][0]);
                maxSum = Math.max(maxSum, dp[i][1]);
                maxSum = Math.max(maxSum, dp[i][2]);
            }
            return maxSum;
        }

        // Driver Code

        let n = 8;
        let A = [2, -1, -18, 3, -1, -39, 5, -2];

        // vector 'arr' contains sum of consecutive
        // positive or negative elements.
        let arr = [];
        mergeElements(n, arr, A);

        document.write(findMaxSum(arr, arr.length));

// This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
69
```

**时间复杂度**:O(N)
T3】辅助空间: O(N)