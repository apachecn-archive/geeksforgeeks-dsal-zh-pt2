# 计算将数组分成两个子集的方法，这两个子集的和之差等于 K

> 原文:[https://www . geesforgeks . org/count-way-将数组拆分为两个子集-它们的和等于 k 之差/](https://www.geeksforgeeks.org/count-ways-to-split-array-into-two-subsets-having-difference-between-their-sum-equal-to-k/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**A【】**和一个整数 **diff** ，任务是计算将数组拆分为两个[子集](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/) ( *非空子集是可能的*)的方法数量，使得它们的和之差等于 **diff** 。

**示例:**

> **输入:** A[] = {1，1，2，3}，diff = 1
> **输出:** 3
> **说明:**所有可能的组合如下:
> 
> *   {1，1，2}和{3}
> *   {1，3}和{1，2}
> *   {1，2}和{1，3}
> 
> 所有分区的和之差都等于 1。因此，路的数量是 3。
> 
> **输入:** A[] = {1，6，11，5}，diff = 1
> T3】输出: 2

**天真方法:**解决问题的最简单方法基于以下观察:

> 让分区子集 **S1** 和 **S2** 中的元素之和分别为 **sum1** 和 **sum2** 。
> 让[数组](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/) **A[]** 之和为 **X** 。
> 给定，**sum 1–sum 2 = diff**–(1)
> 此外，**sum 1+sum 2 = X**–(2)
> 
> 从等式(1)和(2)可知，
> **sum1 = (X + diff)/2**

因此，任务简化为[寻找给定和的子集数量](https://www.geeksforgeeks.org/count-of-subsets-with-sum-equal-to-x/)。
因此，解决这个问题最简单的方法是通过[生成所有可能的子集](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)并检查该子集是否有所需的和。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(N)*

**高效途径:**优化上述途径，思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。初始化一个大小为 **N*X** 的 **dp[][]** 表，其中 **dp[i][C]** 存储子阵列 **A[i…N-1]** 的子集数，使得它们的和等于 **C** 。因此，递归非常简单，因为只有两个选择，即要么考虑子集中的 **i <sup>th</sup>** 元素，要么不考虑。所以循环关系将是:

> **dp[i][C] = dp[i – 1][C – A[i]] + dp[i-1][C]**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of ways to divide
// the array into two subsets and such that the
// difference between their sums is equal to diff
int countSubset(int arr[], int n, int diff)
{
    // Store the sum of the set S1
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];
    sum += diff;
    sum = sum / 2;

    // Initializing the matrix
    int t[n + 1][sum + 1];

    // Number of ways to get sum
    // using 0 elements is 0
    for (int j = 0; j <= sum; j++)
        t[0][j] = 0;

    // Number of ways to get sum 0
    // using i elements is 1
    for (int i = 0; i <= n; i++)
        t[i][0] = 1;

    // Traverse the 2D array
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= sum; j++) {

            // If the value is greater
            // than the sum store the
            // value of previous state
            if (arr[i - 1] > j)
                t[i][j] = t[i - 1][j];

            else {
                t[i][j] = t[i - 1][j]
                          + t[i - 1][j - arr[i - 1]];
            }
        }
    }

    // Return the result
    return t[n][sum];
}

// Driver Code
int main()
{
    // Given Input
    int diff = 1, n = 4;
    int arr[] = { 1, 1, 2, 3 };

    // Function Call
    cout << countSubset(arr, n, diff);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
public class GFG
{

    // Function to count the number of ways to divide
    // the array into two subsets and such that the
    // difference between their sums is equal to diff
    static int countSubset(int []arr, int n, int diff)
    {

        // Store the sum of the set S1
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += arr[i];
        sum += diff;
        sum = sum / 2;

        // Initializing the matrix
        int t[][] = new int[n + 1][sum + 1];

        // Number of ways to get sum
        // using 0 elements is 0
        for (int j = 0; j <= sum; j++)
            t[0][j] = 0;

        // Number of ways to get sum 0
        // using i elements is 1
        for (int i = 0; i <= n; i++)
            t[i][0] = 1;

        // Traverse the 2D array
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= sum; j++) {

                // If the value is greater
                // than the sum store the
                // value of previous state
                if (arr[i - 1] > j)
                    t[i][j] = t[i - 1][j];

                else {
                    t[i][j] = t[i - 1][j]
                              + t[i - 1][j - arr[i - 1]];
                }
            }
        }

        // Return the result
        return t[n][sum];
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given Input
        int diff = 1, n = 4;
        int arr[] = { 1, 1, 2, 3 };

        // Function Call
        System.out.print(countSubset(arr, n, diff));
    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of ways to divide
# the array into two subsets and such that the
# difference between their sums is equal to diff
def countSubset(arr, n, diff):

    # Store the sum of the set S1
    sum = 0
    for i in range(n):
        sum += arr[i]

    sum += diff
    sum = sum // 2

    # Initializing the matrix
    t = [[0 for i in range(sum + 1)]
            for i in range(n + 1)]

    # Number of ways to get sum
    # using 0 elements is 0
    for j in range(sum + 1):
        t[0][j] = 0

    # Number of ways to get sum 0
    # using i elements is 1
    for i in range(n + 1):
        t[i][0] = 1

    # Traverse the 2D array
    for i in range(1, n + 1):
        for j in range(1, sum + 1):

            # If the value is greater
            # than the sum store the
            # value of previous state
            if (arr[i - 1] > j):
                t[i][j] = t[i - 1][j]
            else:
                t[i][j] = t[i - 1][j] + t[i - 1][j - arr[i - 1]]

    # Return the result
    return t[n][sum]

# Driver Code
if __name__ == '__main__':

    # Given Input
    diff, n = 1, 4
    arr = [ 1, 1, 2, 3 ]

    # Function Call
    print (countSubset(arr, n, diff))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach

using System;

public class GFG
{

    // Function to count the number of ways to divide
    // the array into two subsets and such that the
    // difference between their sums is equal to diff
    static int countSubset(int []arr, int n, int diff)
    {

        // Store the sum of the set S1
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += arr[i];
        sum += diff;
        sum = sum / 2;

        // Initializing the matrix
        int [,]t = new int[n + 1, sum + 1];

        // Number of ways to get sum
        // using 0 elements is 0
        for (int j = 0; j <= sum; j++)
            t[0,j] = 0;

        // Number of ways to get sum 0
        // using i elements is 1
        for (int i = 0; i <= n; i++)
            t[i,0] = 1;

        // Traverse the 2D array
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= sum; j++) {

                // If the value is greater
                // than the sum store the
                // value of previous state
                if (arr[i - 1] > j)
                    t[i,j] = t[i - 1,j];

                else {
                    t[i,j] = t[i - 1,j]
                              + t[i - 1,j - arr[i - 1]];
                }
            }
        }

        // Return the result
        return t[n,sum];
    }

    // Driver Code
    public static void Main(string[] args)
    {

        // Given Input
        int diff = 1, n = 4;
        int []arr = { 1, 1, 2, 3 };

        // Function Call
        Console.Write(countSubset(arr, n, diff));
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count the number of ways to divide
// the array into two subsets and such that the
// difference between their sums is equal to diff
function countSubset(arr, n, diff)
{
    // Store the sum of the set S1
    var sum = 0;
    for (var i = 0; i < n; i++){
        sum += arr[i];
    }
    sum += diff;
    sum = sum / 2;

    // Initializing the matrix
    //int t[n + 1][sum + 1];
    var t = new Array(n + 1);

    // Loop to create 2D array using 1D array
    for (var i = 0; i < t.length; i++) {
        t[i] = new Array(sum + 1);
    }

    // Loop to initialize 2D array elements.
    for (var i = 0; i < t.length; i++) {
        for (var j = 0; j < t[i].length; j++) {
            t[i][j] = 0;
        }
    }

    // Number of ways to get sum
    // using 0 elements is 0
    for (var j = 0; j <= sum; j++)
        t[0][j] = 0;

    // Number of ways to get sum 0
    // using i elements is 1
    for (var i = 0; i <= n; i++)
        t[i][0] = 1;

    // Traverse the 2D array
    for (var i = 1; i <= n; i++) {
        for (var j = 1; j <= sum; j++) {

            // If the value is greater
            // than the sum store the
            // value of previous state
            if (arr[i - 1] > j)
                t[i][j] = t[i - 1][j];

            else {
                t[i][j] = t[i - 1][j]
                          + t[i - 1][j - arr[i - 1]];
            }
        }
    }

    // Return the result
    return t[n][sum];
}

// Driver Code

// Given Input
var diff = 1;
var n = 4;
var arr = [ 1, 1, 2, 3 ];

// Function Call
document.write(countSubset(arr, n, diff));

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(S*N)，其中 S =* [*阵元之和*](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)*+K/2*
***辅助空间:** O(S*N)*