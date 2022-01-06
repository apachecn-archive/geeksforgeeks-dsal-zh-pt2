# 最小化使阵列中所有相邻元素不同的成本

> 原文:[https://www . geeksforgeeks . org/最小化制造所有相邻元素的成本-阵列中的不同元素/](https://www.geeksforgeeks.org/minimize-the-cost-to-make-all-the-adjacent-elements-distinct-in-an-array/)

给定两个大小为 **N** 的整数数组**arr【】**和**cost【】**，任务是以最小的成本使所有相邻元素不同。**成本【I】**表示将 **i <sup>th</sup>** 元素增加 1 的成本。
**示例:**

> **输入:** arr[] = {2，2，3}，成本[] = {4，1，5}
> **输出:** 2
> **说明:**
> 第二要素增量成本最小。因此，第二元件的成本增加了两倍。
> 因此结果数组:{2，4，3}
> **输入:** arr[] = {1，2，3}，成本[] = {7，8，3}
> **输出:** 0

**进场:**

*   我们可以观察到，有一个元素可能需要最多增加两次。
*   这个问题可以用[动态规划来解决。](https://www.geeksforgeeks.org/dynamic-programming/)
*   创建一个[DP-表](https://www.geeksforgeeks.org/tabulation-vs-memoization/) **dp[][]** ，其中行代表元素，列代表增量。
*   **dp[i][j]** 是使用 **j** 增量将第 i <sup>个</sup>元素与其相邻元素区分开来所需的最小成本。
*   **dp[i][j]** 的值可以计算为:

> dp[i][j] = j *成本[i] +(如果两个元素不同，则为前一个元素的最小值)

以下是上述方法的实施

## C++

```
// C++ program to find the
// minimum cost required to make
// all adjacent elements distinct

#include <bits/stdc++.h>
using namespace std;

// Function that prints minimum cost required
void minimumCost(int arr[], int cost[], int N)
{

    // Dp-table
    vector<vector<int> > dp(N, vector<int>(3));

    // Base case
    // Not increasing the first element
    dp[0][0] = 0;

    // Increasing the first element by 1
    dp[0][1] = cost[0];

    // Increasing the first element by 2
    dp[0][2] = cost[0] * 2;

    for (int i = 1; i < N; i++) {
        for (int j = 0; j < 3; j++) {

            int minimum = 1e6;

            // Condition if current element
            // is not equal to previous
            // non-increased element
            if (j + arr[i] != arr[i - 1])
                minimum
                    = min(minimum,
                          dp[i - 1][0]);

            // Condition if current element
            // is not equal to previous element
            // after being increased by 1
            if (j + arr[i] != arr[i - 1] + 1)
                minimum
                    = min(minimum,
                          dp[i - 1][1]);

            // Condition if current element
            // is not equal to previous element
            // after being increased by 2
            if (j + arr[i] != arr[i - 1] + 2)
                minimum
                    = min(minimum,
                          dp[i - 1][2]);

            // Take the minimum from all cases
            dp[i][j] = j * cost[i] + minimum;
        }
    }

    int ans = 1e6;

    // Finding the minimum cost
    for (int i = 0; i < 3; i++)
        ans = min(ans, dp[N - 1][i]);

    // Printing the minimum cost
    // required to make all adjacent
    // elements distinct
    cout << ans << "\n";
}

// Driver Code
int main()
{
    int arr[] = { 1, 1, 2, 2, 3, 4 };
    int cost[] = { 3, 2, 5, 4, 2, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);

    minimumCost(arr, cost, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum
// cost required to make all
// adjacent elements distinct
import java.util.*;

class GFG{

// Function that prints minimum cost required
static void minimumCost(int arr[], int cost[],
                        int N)
{

    // Dp-table
    int [][]dp = new int[N][3];

    // Base case
    // Not increasing the first element
    dp[0][0] = 0;

    // Increasing the first element by 1
    dp[0][1] = cost[0];

    // Increasing the first element by 2
    dp[0][2] = cost[0] * 2;

    for(int i = 1; i < N; i++)
    {
       for(int j = 0; j < 3; j++)
       {
          int minimum = (int) 1e6;

          // Condition if current element
          // is not equal to previous
          // non-increased element
          if (j + arr[i] != arr[i - 1])
              minimum = Math.min(minimum, dp[i - 1][0]);

          // Condition if current element
          // is not equal to previous element
          // after being increased by 1
          if (j + arr[i] != arr[i - 1] + 1)
              minimum = Math.min(minimum, dp[i - 1][1]);

          // Condition if current element
          // is not equal to previous element
          // after being increased by 2
          if (j + arr[i] != arr[i - 1] + 2)
              minimum = Math.min(minimum, dp[i - 1][2]);

          // Take the minimum from all cases
          dp[i][j] = j * cost[i] + minimum;
       }
    }
    int ans = (int) 1e6;

    // Finding the minimum cost
    for(int i = 0; i < 3; i++)
       ans = Math.min(ans, dp[N - 1][i]);

    // Printing the minimum cost
    // required to make all adjacent
    // elements distinct
    System.out.print(ans + "\n");
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 1, 2, 2, 3, 4 };
    int cost[] = { 3, 2, 5, 4, 2, 1 };
    int N = arr.length;

    minimumCost(arr, cost, N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the
# minimum cost required to make
# all adjacent elements distinct

# Function that prints minimum cost required
def minimumCost(arr, cost, N):

    # Dp-table
    dp = [[0 for i in range(3)] for i in range(N)]

    # Base case
    # Not increasing the first element
    dp[0][0] = 0

    # Increasing the first element by 1
    dp[0][1] = cost[0]

    # Increasing the first element by 2
    dp[0][2] = cost[0] * 2

    for i in range(1, N):
        for j in range(3):

            minimum = 1e6

            # Condition if current element
            # is not equal to previous
            # non-increased element
            if (j + arr[i] != arr[i - 1]):
                minimum = min(minimum, dp[i - 1][0])

            # Condition if current element
            # is not equal to previous element
            # after being increased by 1
            if (j + arr[i] != arr[i - 1] + 1):
                minimum = min(minimum, dp[i - 1][1])

            # Condition if current element
            # is not equal to previous element
            # after being increased by 2
            if (j + arr[i] != arr[i - 1] + 2):
                minimum = min(minimum, dp[i - 1][2])

            # Take the minimum from all cases
            dp[i][j] = j * cost[i] + minimum

    ans = 1e6

    # Finding the minimum cost
    for i in range(3):
        ans = min(ans, dp[N - 1][i])

    # Printing the minimum cost
    # required to make all adjacent
    # elements distinct
    print(ans)

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 1, 2, 2, 3, 4 ]
    cost = [ 3, 2, 5, 4, 2, 1 ]
    N = len(arr)

    minimumCost(arr, cost, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find the minimum
// cost required to make all
// adjacent elements distinct
using System;

class GFG{

// Function that prints minimum cost required
static void minimumCost(int []arr, int []cost,
                        int N)
{

    // Dp-table
    int [,]dp = new int[N, 3];

    // Base case
    // Not increasing the first element
    dp[0, 0] = 0;

    // Increasing the first element by 1
    dp[0, 1] = cost[0];

    // Increasing the first element by 2
    dp[0, 2] = cost[0] * 2;

    for(int i = 1; i < N; i++)
    {
       for(int j = 0; j < 3; j++)
       {
          int minimum = (int) 1e6;

          // Condition if current element
          // is not equal to previous
          // non-increased element
          if (j + arr[i] != arr[i - 1])
              minimum = Math.Min(minimum,
                                 dp[i - 1, 0]);

          // Condition if current element
          // is not equal to previous element
          // after being increased by 1
          if (j + arr[i] != arr[i - 1] + 1)
              minimum = Math.Min(minimum,
                                 dp[i - 1, 1]);

          // Condition if current element
          // is not equal to previous element
          // after being increased by 2
          if (j + arr[i] != arr[i - 1] + 2)
              minimum = Math.Min(minimum,
                                 dp[i - 1, 2]);

          // Take the minimum from all cases
          dp[i, j] = j * cost[i] + minimum;
       }
    }
    int ans = (int) 1e6;

    // Finding the minimum cost
    for(int i = 0; i < 3; i++)
       ans = Math.Min(ans, dp[N - 1, i]);

    // Printing the minimum cost
    // required to make all adjacent
    // elements distinct
    Console.Write(ans + "\n");
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 1, 2, 2, 3, 4 };
    int []cost = { 3, 2, 5, 4, 2, 1 };
    int N = arr.Length;

    minimumCost(arr, cost, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find the minimum
// cost required to make all
// adjacent elements distinct

    // Function that prints minimum cost required
    function minimumCost(arr , cost , N) {

        // Dp-table
        var dp = Array(N).fill().map(()=>Array(3).fill(0));

        // Base case
        // Not increasing the first element
        dp[0][0] = 0;

        // Increasing the first element by 1
        dp[0][1] = cost[0];

        // Increasing the first element by 2
        dp[0][2] = cost[0] * 2;

        for (i = 1; i < N; i++) {
            for (j = 0; j < 3; j++) {
                var minimum = parseInt( 1e6);

                // Condition if current element
                // is not equal to previous
                // non-increased element
                if (j + arr[i] != arr[i - 1])
                    minimum = Math.min(minimum, dp[i - 1][0]);

                // Condition if current element
                // is not equal to previous element
                // after being increased by 1
                if (j + arr[i] != arr[i - 1] + 1)
                    minimum = Math.min(minimum, dp[i - 1][1]);

                // Condition if current element
                // is not equal to previous element
                // after being increased by 2
                if (j + arr[i] != arr[i - 1] + 2)
                    minimum = Math.min(minimum, dp[i - 1][2]);

                // Take the minimum from all cases
                dp[i][j] = j * cost[i] + minimum;
            }
        }
        var ans = parseInt( 1e6);

        // Finding the minimum cost
        for (i = 0; i < 3; i++)
            ans = Math.min(ans, dp[N - 1][i]);

        // Printing the minimum cost
        // required to make all adjacent
        // elements distinct
        document.write(ans + "\n");
    }

    // Driver Code

        var arr = [ 1, 1, 2, 2, 3, 4 ];
        var cost = [ 3, 2, 5, 4, 2, 1 ];
        var N = arr.length;

        minimumCost(arr, cost, N);

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
7
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*