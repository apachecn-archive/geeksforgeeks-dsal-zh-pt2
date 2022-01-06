# 在给定条件下将一个阵列分成 K 个子阵列

> 原文:[https://www . geeksforgeeks . org/用给定条件将数组分成 k 个子数组/](https://www.geeksforgeeks.org/divide-an-array-into-k-subarray-with-the-given-condition/)

给定一个数组 **arr[]** 和一个整数 **K** 。任务是将阵列分成 **K** 个部分(子阵列)，使得所有子阵列的值之和最小。
每个子阵列的值定义为:

*   从那个子阵列中取最大值。
*   用最大值减去子阵列的每个元素。
*   取减法后所有值的总和。

任务是将数组划分为 **K** 个部分后，将数值之和最小化。
**例:**

> **输入:** arr[] = { 2，9，5，4，8，3，6 }，K = 2
> **输出:** 19
> **说明:**
> 两组分别是:{ 2 } max = 2 和{9，5，4，8，3，6 } max = 9，
> 第一组差之和= 2–2 = 0，
> 第二组差之和=(9-9)+(9-5)+(9-4)+(9-8)+(9-3)+(9-6)= 19
> **输入:** arr[] = { 12，20，30，14，25}，K = 3
> **输出:** 19

**方法:**
蛮力的解决方法是尝试所有可能的分区，取最小的整体。虽然这个解决方案在时间上是指数级的。在递归解决方案中，有许多重叠的子问题可以使用动态规划进行优化。
因此，我们可以形成一个基本的递归公式，计算每个可能的解，并找到最佳可能的解。我们可以看到递归解有许多重叠的子问题，我们可以使用动态规划来降低复杂性。
递归公式:
**F(i，K) = {所有值的最小值，使得 j < i【最大值(Arr[i..j])*(I–j+1)–Sum(A[I…j]]}+F(j，K-1)**
自下而上的方法可以先计算子问题的值，然后存储。
这里 **dp[i][j]** 定义了如果数组是从索引 **i** 开始，并且有 **j** 分区，可以得到的最小值。
那么问题的答案就是 **dp[0][K]** ，数组从 **0** 开始，有 **K** 分区。
以下是上述方法的实施:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to divide an array into k
// parts such that the sum of difference
// of every element with the maximum element
// of that part is minimum
int divideArray(int arr[], int n, int k)
{
    // Dp to store the values
    int dp[500][500] = { 0 };

    k -= 1;

    // Fill up the dp table
    for (int i = n - 1; i >= 0; i--) {
        for (int j = 0; j <= k; j++) {
            // Intitilize maximum value
            dp[i][j] = INT_MAX;

            // Max element and the sum
            int max_ = -1, sum = 0;

            // Run a loop from i to n
            for (int l = i; l < n; l++) {
                // Find the maximum number
                // from i to l and the sum
                // from i to l
                max_ = max(max_, arr[l]);
                sum += arr[l];

                // Find the sum of difference
                // of every element with the
                // maximum element
                int diff = (l - i + 1) * max_ - sum;

                // If the array can be divided
                if (j > 0)
                    dp[i][j]
                        = min(dp[i][j],
                              diff + dp[l + 1][j - 1]);
                else
                    dp[i][j] = diff;
            }
        }
    }

    // Returns the minimum sum
    // in K parts
    return dp[0][k];
}

// Driver code
int main()
{
    int arr[] = { 2, 9, 5, 4, 8, 3, 6 };
    int n = sizeof(arr) / sizeof(int);
    int k = 2;

    cout << divideArray(arr, n, k) << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    // Function to divide an array into k
    // parts such that the sum of difference
    // of every element with the maximum element
    // of that part is minimum
    static int divideArray(int arr[], int n, int k)
    {
        // Dp to store the values
        int dp[][] = new int[500][500];

        int i, j;

        for(i = 0; i < 500; i++)
            for(j = 0; j < 500; j++)
                dp[i][j] = 0;

        k -= 1;

        // Fill up the dp table
        for (i = n - 1; i >= 0; i--)
        {
            for (j = 0; j <= k; j++)
            {

                // Intitilize maximum value
                dp[i][j] = Integer.MAX_VALUE;

                // Max element and the sum
                int max_ = -1, sum = 0;

                // Run a loop from i to n
                for (int l = i; l < n; l++)
                {
                    // Find the maximum number
                    // from i to l and the sum
                    // from i to l
                    max_ = Math.max(max_, arr[l]);
                    sum += arr[l];

                    // Find the sum of difference
                    // of every element with the
                    // maximum element
                    int diff = (l - i + 1) * max_ - sum;

                    // If the array can be divided
                    if (j > 0)
                        dp[i][j] = Math.min(dp[i][j], diff +
                                            dp[l + 1][j - 1]);
                    else
                        dp[i][j] = diff;
                }
            }
        }

        // Returns the minimum sum
        // in K parts
        return dp[0][k];
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 2, 9, 5, 4, 8, 3, 6 };
        int n = arr.length;
        int k = 2;

        System.out.println(divideArray(arr, n, k));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to divide an array into k
# parts such that the summ of difference
# of every element with the maximum element
# of that part is minimum
def divideArray(arr, n, k):

    # Dp to store the values
    dp = [[0 for i in range(500)]
             for i in range(500)]

    k -= 1

    # Fill up the dp table
    for i in range(n - 1, -1, -1):
        for j in range(0, k + 1):

            # Intitilize maximum value
            dp[i][j] = 10**9

            # Max element and the summ
            max_ = -1
            summ = 0

            # Run a loop from i to n
            for l in range(i, n):

                # Find the maximum number
                # from i to l and the summ
                # from i to l
                max_ = max(max_, arr[l])
                summ += arr[l]

                # Find the summ of difference
                # of every element with the
                # maximum element
                diff = (l - i + 1) * max_ - summ

                # If the array can be divided
                if (j > 0):
                    dp[i][j]= min(dp[i][j], diff +
                                  dp[l + 1][j - 1])
                else:
                    dp[i][j] = diff

    # Returns the minimum summ
    # in K parts
    return dp[0][k]

# Driver code
arr = [2, 9, 5, 4, 8, 3, 6]
n = len(arr)
k = 2

print(divideArray(arr, n, k))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

    // Function to divide an array into k
    // parts such that the sum of difference
    // of every element with the maximum element
    // of that part is minimum
    static int divideArray(int []arr, int n, int k)
    {
        // Dp to store the values
        int [,]dp = new int[500, 500];

        int i, j;

        for(i = 0; i < 500; i++)
            for(j = 0; j < 500; j++)
                dp[i, j] = 0;

        k -= 1;

        // Fill up the dp table
        for (i = n - 1; i >= 0; i--)
        {
            for (j = 0; j <= k; j++)
            {

                // Intitilize maximum value
                dp[i, j] = int.MaxValue;

                // Max element and the sum
                int max_ = -1, sum = 0;

                // Run a loop from i to n
                for (int l = i; l < n; l++)
                {
                    // Find the maximum number
                    // from i to l and the sum
                    // from i to l
                    max_ = Math.Max(max_, arr[l]);
                    sum += arr[l];

                    // Find the sum of difference
                    // of every element with the
                    // maximum element
                    int diff = (l - i + 1) * max_ - sum;

                    // If the array can be divided
                    if (j > 0)
                        dp[i, j] = Math.Min(dp[i, j], diff +
                                            dp[l + 1, j - 1]);
                    else
                        dp[i, j] = diff;
                }
            }
        }

        // Returns the minimum sum
        // in K parts
        return dp[0, k];
    }

    // Driver code
    public static void Main (String[] args)
    {
        int []arr = { 2, 9, 5, 4, 8, 3, 6 };
        int n = arr.Length;
        int k = 2;

        Console.WriteLine(divideArray(arr, n, k));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to divide an array into k
// parts such that the sum of difference
// of every element with the maximum element
// of that part is minimum
function divideArray(arr, n, k)
{
    // Dp to store the values
    var dp = Array.from(Array(500), ()=> Array(500).fill(0));

    k -= 1;

    // Fill up the dp table
    for (var i = n - 1; i >= 0; i--) {
        for (var j = 0; j <= k; j++) {
            // Intitilize maximum value
            dp[i][j] = 1000000000;

            // Max element and the sum
            var max_ = -1, sum = 0;

            // Run a loop from i to n
            for (var l = i; l < n; l++) {
                // Find the maximum number
                // from i to l and the sum
                // from i to l
                max_ = Math.max(max_, arr[l]);
                sum += arr[l];

                // Find the sum of difference
                // of every element with the
                // maximum element
                var diff = (l - i + 1) * max_ - sum;

                // If the array can be divided
                if (j > 0)
                    dp[i][j]
                        = Math.min(dp[i][j],
                              diff + dp[l + 1][j - 1]);
                else
                    dp[i][j] = diff;
            }
        }
    }

    // Returns the minimum sum
    // in K parts
    return dp[0][k];
}

// Driver code
var arr = [2, 9, 5, 4, 8, 3, 6 ];
var n = arr.length;
var k = 2;
document.write( divideArray(arr, n, k) + "<br>");

</script>
```

**Output:** 

```
19
```