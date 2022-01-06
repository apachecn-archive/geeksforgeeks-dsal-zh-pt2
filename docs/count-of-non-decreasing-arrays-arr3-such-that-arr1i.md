# 非递减数组 arr3[]的计数，使得 arr 1[I]<= arr 3[I]<= arr 2[I]

> 原文:[https://www . geeksforgeeks . org/非递减数组计数-arr 3-so-arr 1i/](https://www.geeksforgeeks.org/count-of-non-decreasing-arrays-arr3-such-that-arr1i/)

给定两个具有非递减顺序的 **N** 整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr1[]** 和 **arr2[]** ，任务是为范围内 **i** 的所有值找到长度为 **N** 的非递减数组 **arr3[]** 的计数，使得**arr 1[I]<= arr 3[I]<= arr 2[I]**

**示例**:

> **输入** : arr1[] = {1，1}，arr2[] = {2，3}
> **输出** : 5
> **说明:**符合要求条件的 5 个可能数组为{1，1}、{1，2}、{1，3}、{2，2}、{2，3}
> 
> **输入**:范围[]= {-12，15}、{3，9}、{-5，-2}、{20，25}、{16，20}}
> 输出 : 247

**方法:**给定的问题可以使用[动态规划](http://www.geeksforgeeks.org/dynamic-programming/)来解决。考虑一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **dp[][]** ，使得 **dp[i][j]** 代表长度为 **i** 的数组的计数，使得 **i <sup>第</sup>** 元素为 **j** 。将 dp 数组的所有元素初始化为 **0** 和 **dp[0][0]为 1** 。经观察，上述问题的动力定位关系可以表述如下:

> **DP[I][j]=**T2]

因此，使用上述关系，计算范围**【0，N】**中的每个 **i** 和范围**【0，M】**中的每个 **j** 的 **dp[i][j]** 的值，其中 **M** 表示给定数组**arr 1【】**和**arr 2【】**中的最大整数。因此，存储在 **dp[N][M]** 中的值是必需的答案。

下面是上述方法的实现:

## C++

```
// C++ Program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the count of
// valid sorted arrays
int arrCount(int arr1[], int arr2[], int N)
{

    // Maximum possible value
    // of arr1 and arr2
    int M = 1000;

    // Stores the dp states
    vector<vector<int> > dp(
        N + 1,
        vector<int>(M + 1, 0));

    // Initial condition
    dp[0][0] = 1;

    // Loop to iterate over range [0, N]
    for (int i = 0; i <= N; i++) {

        // Loop to iterate over
        // the range [0, M]
        for (int j = 0; j < M; j++) {
            dp[i][j + 1] += dp[i][j];
        }

        // If current index is not
        // the final index
        if (i != N) {

            // Loop to iterate in the
            // range [arr1[i], arr2[i]]
            for (int j = arr1[i]; j <= arr2[i]; j++)
                dp[i + 1][j] += dp[i][j];
        }
    }

    // Return Answer
    return dp[N][M];
}

// Driver Code
int main()
{
    int arr1[] = { 1, 1 };
    int arr2[] = { 2, 3 };
    int N = sizeof(arr1) / sizeof(int);

    cout << arrCount(arr1, arr2, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program of the above approach
import java.util.*;

public class GFG{

// Function to find the count of
// valid sorted arrays
static int arrCount(int[] arr1, int[] arr2, int N)
{

    // Maximum possible value
    // of arr1 and arr2
    int M = 1000;

    // Stores the dp states
    int[][] dp = new int[N + 1][M + 1];

    // Initial condition
    dp[0][0] = 1;

    // Loop to iterate over range [0, N]
    for(int i = 0; i <= N; i++)
    {

        // Loop to iterate over
        // the range [0, M]
        for(int j = 0; j < M; j++)
        {
            dp[i][j + 1] += dp[i][j];
        }

        // If current index is not
        // the final index
        if (i != N)
        {

            // Loop to iterate in the
            // range [arr1[i], arr2[i]]
            for(int j = arr1[i]; j <= arr2[i]; j++)
                dp[i + 1][j] += dp[i][j];
        }
    }

    // Return Answer
    return dp[N][M];
}

// Driver Code
public static void main(String args[])
{
    int[] arr1 = { 1, 1 };
    int[] arr2 = { 2, 3 };
    int N = arr1.length;

    System.out.println(arrCount(arr1, arr2, N));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to find the count of
# valid sorted arrays
def arrCount(arr1, arr2, N):

    # Maximum possible value
    # of arr1 and arr2
    M = 1000

    # Stores the dp states
    dp = [0] * (N + 1)
    for i in range(len(dp)):
        dp[i] = [0] * (M + 1)

    # Initial condition
    dp[0][0] = 1

    # Loop to iterate over range [0, N]
    for i in range(N + 1):

        # Loop to iterate over
        # the range [0, M]
        for j in range(M):
            dp[i][j + 1] += dp[i][j]

        # If current index is not
        # the final index
        if (i != N):

            # Loop to iterate in the
            # range [arr1[i], arr2[i]]
            for j in range(arr1[i], arr2[i] + 1):
                dp[i + 1][j] += dp[i][j]

    # Return Answer
    return dp[N][M]

# Driver Code
arr1 = [1, 1]
arr2 = [2, 3]
N = len(arr1)

print(arrCount(arr1, arr2, N))

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# Program of the above approach
using System;

class GFG{

// Function to find the count of
// valid sorted arrays
static int arrCount(int[] arr1, int[] arr2, int N)
{

    // Maximum possible value
    // of arr1 and arr2
    int M = 1000;

    // Stores the dp states
    int[,] dp = new int[N + 1, M + 1];

    // Initial condition
    dp[0, 0] = 1;

    // Loop to iterate over range [0, N]
    for(int i = 0; i <= N; i++)
    {

        // Loop to iterate over
        // the range [0, M]
        for(int j = 0; j < M; j++)
        {
            dp[i, j + 1] += dp[i, j];
        }

        // If current index is not
        // the final index
        if (i != N)
        {

            // Loop to iterate in the
            // range [arr1[i], arr2[i]]
            for(int j = arr1[i]; j <= arr2[i]; j++)
                dp[i + 1, j] += dp[i, j];
        }
    }

    // Return Answer
    return dp[N, M];
}

// Driver Code
public static void Main()
{
    int[] arr1 = { 1, 1 };
    int[] arr2 = { 2, 3 };
    int N = arr1.Length;

    Console.WriteLine(arrCount(arr1, arr2, N));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
    // JavaScript Program to implement
    // the above approach

    // Function to find the count of
    // valid sorted arrays
    function arrCount(arr1, arr2, N) {

        // Maximum possible value
        // of arr1 and arr2
        let M = 1000;

        // Stores the dp states
        let dp = new Array(N + 1);
        for (let i = 0; i < dp.length; i++) {
            dp[i] = new Array(M + 1).fill(0);
        }

        // Initial condition
        dp[0][0] = 1;

        // Loop to iterate over range [0, N]
        for (let i = 0; i <= N; i++) {

            // Loop to iterate over
            // the range [0, M]
            for (let j = 0; j < M; j++) {
                dp[i][j + 1] += dp[i][j];
            }

            // If current index is not
            // the final index
            if (i != N) {

                // Loop to iterate in the
                // range [arr1[i], arr2[i]]
                for (let j = arr1[i]; j <= arr2[i]; j++)
                    dp[i + 1][j] += dp[i][j];
            }
        }

        // Return Answer
        return dp[N][M];
    }

    // Driver Code

    let arr1 = [1, 1];
    let arr2 = [2, 3];
    let N = arr1.length;

    document.write(arrCount(arr1, arr2, N));

// This code is contributed by Potta Lokesh
</script>
```

**Output**

```
5
```

***时间** **复杂度:** O(N * M)，其中 M 代表数组 arr1[]和 arr2[]中整数的最大值。*
***辅助空间:** O(N * M)*