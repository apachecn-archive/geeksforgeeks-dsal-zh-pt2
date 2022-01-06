# 相邻元素之间绝对差最多为 1 的 N 尺寸阵列的计数

> 原文:[https://www . geeksforgeeks . org/大小为 n 的数组计数相邻元素之间的绝对差值最多为 1/](https://www.geeksforgeeks.org/count-of-arrays-of-size-n-having-absolute-difference-between-adjacent-elements-at-most-1/)

给定一个正整数 **M** 和一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**以及表示为 **-1** 的数组中缺少的几个整数，任务是在用范围**【1，M】**内的元素替换所有 **-1** 后，找出不同数组的计数，使得任意一对相邻元素之间的绝对差值最多为 **1** 。

**示例:**

> **输入:** arr[] = {2，-1，2}，M = 5
> **输出:** 3
> **解释:**
> 符合给定条件的数组是{2，1，2}、{2，2，2}和{2，3，2}。
> 
> **输入:** arr[] = {4，-1，2，1，-1，-1}，M = 10
> T3】输出: 5

**方法:**给定的问题可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)基于以下观察来解决:

*   考虑一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)，比如说 **dp[][]** ，其中 **dp[i][j]** 表示长度为 **i+1** 的有效数组的计数，它们的最后一个元素为 **j** 。
*   由于任意相邻元素之间的绝对差值最多只能是 **1** ，所以对于任意整数 **j** ，有效的相邻整数可以是 **j-1** 、 **j** 、 **j+1** 。因此，任何状态 **dp[i][j]** 可以使用以下关系式计算:

> **DP[I][j]= DP[I-1][j]+DP[I-1][j-1]+DP[I-1][j+1]**T3]

*   在 **arr[i] = -1** 的情况下，对于 **j** 在**【1，M】**范围内的所有值，计算*T3【DP[I][j]=(DP[I-1][j]+DP[I-1][j-1]+DP[I-1][j+1])*。
*   在**逮捕【I】的情况下！= -1** ，计算*T3】DP[I][j]=(DP[I-1][j]+DP[I-1][j-1]+DP[I-1][j+1])T5】为 **j = arr[i]** 。*
*   请注意，在 **arr[0] = -1** 的情况下，范围**【1，M】**中的所有值都可以作为 1 <sup>st</sup> 数组元素到达，因此为范围**【1，M】**中的所有 **j** 初始化**DP[0][arr[0]]= 1**。
*   所需答案将是范围**【1，M】**内所有 **j** 的**DP【N–1】【j】**的所有值之和。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the count of possible
// arrays such that the absolute difference
// between any adjacent elements is atmost 1
int countArray(int arr[], int N, int M)
{
    // Stores the dp states where dp[i][j]
    // represents count of arrays of length
    // i+1 having their last element as j
    int dp[N][M + 2];
    memset(dp, 0, sizeof dp);

    // Case where 1st array element is missing
    if (arr[0] == -1) {
        // All integers in range [1, M]
        // are reachable
        for (int j = 1; j <= M; j++) {
            dp[0][j] = 1;
        }
    }
    else {
        // Only reachable integer is arr[0]
        dp[0][arr[0]] = 1;
    }

    // Iterate through all values of i
    for (int i = 1; i < N; i++) {

        // If arr[i] is not missing
        if (arr[i] != -1) {

            // Only valid value of j is arr[i]
            int j = arr[i];
            dp[i][j] += dp[i - 1][j - 1] + dp[i - 1][j]
                        + dp[i - 1][j + 1];
        }

        // If arr[i] is missing
        if (arr[i] == -1) {

            // Iterate through all possible
            // values of j in range [1, M]
            for (int j = 1; j <= M; j++) {
                dp[i][j] += dp[i - 1][j - 1] + dp[i - 1][j]
                            + dp[i - 1][j + 1];
            }
        }
    }

    // Stores the count of valid arrays
    int arrCount = 0;

    // Calculate the total count of
    // valid arrays
    for (int j = 1; j <= M; j++) {
        arrCount += dp[N - 1][j];
    }

    // Return answer
    return arrCount;
}

// Driver Code
int main()
{
    int arr[] = { 4, -1, 2, 1, -1, -1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int M = 10;

    // Function Call
    cout << countArray(arr, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
class GFG
{

    // Function to find the count of possible
    // arrays such that the absolute difference
    // between any adjacent elements is atmost 1
    public static int countArray(int arr[], int N, int M)
    {

        // Stores the dp states where dp[i][j]
        // represents count of arrays of length
        // i+1 having their last element as j
        int[][] dp = new int[N][M + 2];
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M + 2; j++) {
                dp[i][j] = 0;
            }
        }

        // Case where 1st array element is missing
        if (arr[0] == -1)
        {

            // All integers in range [1, M]
            // are reachable
            for (int j = 1; j <= M; j++) {
                dp[0][j] = 1;
            }
        } else {
            // Only reachable integer is arr[0]
            dp[0][arr[0]] = 1;
        }

        // Iterate through all values of i
        for (int i = 1; i < N; i++) {

            // If arr[i] is not missing
            if (arr[i] != -1) {

                // Only valid value of j is arr[i]
                int j = arr[i];
                dp[i][j] += dp[i - 1][j - 1] + dp[i - 1][j] + dp[i - 1][j + 1];
            }

            // If arr[i] is missing
            if (arr[i] == -1) {

                // Iterate through all possible
                // values of j in range [1, M]
                for (int j = 1; j <= M; j++) {
                    dp[i][j] += dp[i - 1][j - 1] + dp[i - 1][j] + dp[i - 1][j + 1];
                }
            }
        }

        // Stores the count of valid arrays
        int arrCount = 0;

        // Calculate the total count of
        // valid arrays
        for (int j = 1; j <= M; j++) {
            arrCount += dp[N - 1][j];
        }

        // Return answer
        return arrCount;
    }

    // Driver Code
    public static void main(String args[]) {
        int arr[] = { 4, -1, 2, 1, -1, -1 };
        int N = arr.length;
        int M = 10;

        // Function Call
        System.out.println(countArray(arr, N, M));

    }
}

// This code is contributed by _saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python 3 program of the above approach

# Function to find the count of possible
# arrays such that the absolute difference
# between any adjacent elements is atmost 1
def countArray(arr, N, M):

    # Stores the dp states where dp[i][j]
    # represents count of arrays of length
    # i+1 having their last element as j
    dp = [[0 for i in range(M+2)] for j in range(N)]

    # Case where 1st array element is missing
    if (arr[0] == -1):

        # All integers in range [1, M]
        # are reachable
        for j in range(1,M+1,1):
            dp[0][j] = 1

    else:
        # Only reachable integer is arr[0]
        dp[0][arr[0]] = 1

    # Iterate through all values of i
    for i in range(1, N, 1):

        # If arr[i] is not missing
        if(arr[i] != -1):

            # Only valid value of j is arr[i]
            j = arr[i]
            dp[i][j] += dp[i - 1][j - 1] + dp[i - 1][j] + dp[i - 1][j + 1]

        # If arr[i] is missing
        if (arr[i] == -1):

            # Iterate through all possible
            # values of j in range [1, M]
            for j in range(1,M+1,1):
                dp[i][j] += dp[i - 1][j - 1] + dp[i - 1][j] + dp[i - 1][j + 1]

    # Stores the count of valid arrays
    arrCount = 0

    # Calculate the total count of
    # valid arrays
    for j in range(1,M+1,1):
        arrCount += dp[N - 1][j]

    # Return answer
    return arrCount

# Driver Code
if __name__ == '__main__':
    arr = [4, -1, 2, 1, -1, -1]
    N = len(arr)
    M = 10

    # Function Call
    print(countArray(arr, N, M))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program of the above approach
using System;
public class GFG
{

    // Function to find the count of possible
    // arrays such that the absolute difference
    // between any adjacent elements is atmost 1
    public static int countArray(int []arr, int N, int M)
    {

        // Stores the dp states where dp[i][j]
        // represents count of arrays of length
        // i+1 having their last element as j
        int[,] dp = new int[N, M + 2];
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M + 2; j++) {
                dp[i, j] = 0;
            }
        }

        // Case where 1st array element is missing
        if (arr[0] == -1)
        {

            // All integers in range [1, M]
            // are reachable
            for (int j = 1; j <= M; j++) {
                dp[0, j] = 1;
            }
        } else {
            // Only reachable integer is arr[0]
            dp[0, arr[0]] = 1;
        }

        // Iterate through all values of i
        for (int i = 1; i < N; i++) {

            // If arr[i] is not missing
            if (arr[i] != -1) {

                // Only valid value of j is arr[i]
                int j = arr[i];
                dp[i, j] += dp[i - 1, j - 1] + dp[i - 1, j] + dp[i - 1, j + 1];
            }

            // If arr[i] is missing
            if (arr[i] == -1) {

                // Iterate through all possible
                // values of j in range [1, M]
                for (int j = 1; j <= M; j++) {
                    dp[i, j] += dp[i - 1, j - 1] + dp[i - 1, j] + dp[i - 1, j + 1];
                }
            }
        }

        // Stores the count of valid arrays
        int arrCount = 0;

        // Calculate the total count of
        // valid arrays
        for (int j = 1; j <= M; j++) {
            arrCount += dp[N - 1, j];
        }

        // Return answer
        return arrCount;
    }

    // Driver Code
    public static void Main(String[] args) {
        int []arr = { 4, -1, 2, 1, -1, -1 };
        int N = arr.Length;
        int M = 10;

        // Function Call
        Console.WriteLine(countArray(arr, N, M));
    }
}

// This code is contributed by AnkThon.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the count of possible
        // arrays such that the absolute difference
        // between any adjacent elements is atmost 1
        function countArray(arr, N, M) {
            // Stores the dp states where dp[i][j]
            // represents count of arrays of length
            // i+1 having their last element as j
            let dp = new Array(N);

            // Loop to create 2D array using 1D array
            for (let i = 0; i < dp.length; i++) {
                dp[i] = new Array(M + 2).fill(0);
            }

            // Case where 1st array element is missing
            if (arr[0] == -1) {
                // All integers in range [1, M]
                // are reachable
                for (let j = 1; j <= M; j++) {
                    dp[0][j] = 1;
                }
            }
            else {
                // Only reachable integer is arr[0]
                dp[0][arr[0]] = 1;
            }

            // Iterate through all values of i
            for (let i = 1; i < N; i++) {

                // If arr[i] is not missing
                if (arr[i] != -1) {

                    // Only valid value of j is arr[i]
                    let j = arr[i];
                    dp[i][j] += dp[i - 1][j - 1] + dp[i - 1][j]
                        + dp[i - 1][j + 1];
                }

                // If arr[i] is missing
                if (arr[i] == -1) {

                    // Iterate through all possible
                    // values of j in range [1, M]
                    for (let j = 1; j <= M; j++) {
                        dp[i][j] += dp[i - 1][j - 1] + dp[i - 1][j]
                            + dp[i - 1][j + 1];
                    }
                }
            }

            // Stores the count of valid arrays
            let arrCount = 0;

            // Calculate the total count of
            // valid arrays
            for (let j = 1; j <= M; j++) {
                arrCount += dp[N - 1][j];
            }

            // Return answer
            return arrCount;
        }

        // Driver Code

        let arr = [4, -1, 2, 1, -1, -1];
        let N = arr.length;
        let M = 10;

        // Function Call
        document.write(countArray(arr, N, M));

     // This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
5
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(N*M)*