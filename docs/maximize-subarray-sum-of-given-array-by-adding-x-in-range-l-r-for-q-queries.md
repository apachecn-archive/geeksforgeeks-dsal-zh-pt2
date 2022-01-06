# 给定数组的子数组和最大化，在 Q 查询的[L，R]范围内加上 X

> 原文:[https://www . geesforgeks . org/maximize-subarray-sum-给定数组-by-add-x-in-range-l-r-for-q-query/](https://www.geeksforgeeks.org/maximize-subarray-sum-of-given-array-by-adding-x-in-range-l-r-for-q-queries/)

给定类型为 **(L，R，X)** 的 **N** 整数和 **M** 更新查询的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是在每个更新查询之后找到[最大子数组和](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)，在每个查询中，将整数 **X** 添加到数组 **arr[]** 的范围**【L，R】**中的每个元素。

**示例:**

> **输入:** arr[] = {-1，5，-2，9，3，-3，2}，查询[] = {{0，2，-10}，{4，5，2}}
> **输出:** 12 15
> **解释:**下面是解决上述例子的步骤:
> 
> *   第一次更新查询后的数组变成 arr[] = {-11，-5，-12，9，3，-3，2}。因此，最大子阵列和是子阵列 arr[3… 4]的 12。
> *   第二次更新查询后的数组变成 arr[] = {-11，-5，-12，9，5，-1，2}。因此，最大子阵列和是子阵列 arr 的 15[3…6]。
> 
> **输入:** arr[] = {-2，-5，6，-2，-3，1，5，-6，4，-1}，查询[] = {{1，4，3}，{4，5，-4}，{7，9，5}}
> **输出:** 16 10 20

**方法:**给定的问题可以使用[卡丹算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)来解决。对于每个查询，通过遍历范围**【L，R】**中的所有数组元素 **arr[]** 来更新数组元素，并向每个元素添加整数 **X** 。每次更新查询后，使用这里讨论的算法计算最大子阵列和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum subarray
// sum using Kadane's Algorithm
int maxSubarraySum(int arr[], int n)
{
    // Stores the maximum sum
    int maxSum = INT_MIN;
    int currSum = 0;

    // Loop to iterate over the array
    for (int i = 0; i <= n - 1; i++) {
        currSum += arr[i];

        // Update maxSum
        if (currSum > maxSum) {
            maxSum = currSum;
        }
        if (currSum < 0) {
            currSum = 0;
        }
    }

    // Return Answer
    return maxSum;
}

// Function to add integer X to all elements
// of the given array in range [L, R]
void updateArr(int* arr, int L, int R, int X)
{
    // Loop to iterate over the range
    for (int i = L; i <= R; i++) {
        arr[i] += X;
    }
}

// Function to find the maximum subarray sum
// after each range update query
void maxSubarraySumQuery(
    int arr[], int n,
    vector<vector<int> > query)
{
    // Loop to iterate over the queries
    for (int i = 0; i < query.size(); i++) {

        // Function call to update the array
        // according to the mentioned query
        updateArr(arr, query[i][0],
                  query[i][1],
                  query[i][2]);

        // Print the max subarray sum after
        // updating the given array
        cout << maxSubarraySum(arr, n) << " ";
    }
}

// Driver Code
int main()
{

    int arr[] = { -2, -5, 6, -2, -3,
                  1, 5, -6, 4, -1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    vector<vector<int> > query{ { 1, 4, 3 },
                                { 4, 5, -4 },
                                { 7, 9, 5 } };

    maxSubarraySumQuery(arr, N, query);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  program for the above approach
class GFG {

    // Function to find the maximum subarray
    // sum using Kadane's Algorithm
    public static int maxSubarraySum(int arr[], int n)
    {

        // Stores the maximum sum
        int maxSum = Integer.MIN_VALUE;
        int currSum = 0;

        // Loop to iterate over the array
        for (int i = 0; i <= n - 1; i++) {
            currSum += arr[i];

            // Update maxSum
            if (currSum > maxSum) {
                maxSum = currSum;
            }
            if (currSum < 0) {
                currSum = 0;
            }
        }

        // Return Answer
        return maxSum;
    }

    // Function to add integer X to all elements
    // of the given array in range [L, R]
    public static void updateArr(int[] arr, int L,
                                 int R, int X)
    {

        // Loop to iterate over the range
        for (int i = L; i <= R; i++) {
            arr[i] += X;
        }
    }

    // Function to find the maximum subarray sum
    // after each range update query
    public static void maxSubarraySumQuery(int arr[], int n, int[][] query)
    {

        // Loop to iterate over the queries
        for (int i = 0; i < query.length; i++)
        {

            // Function call to update the array
            // according to the mentioned query
            updateArr(arr, query[i][0],
                    query[i][1],
                    query[i][2]);

            // Print the max subarray sum after
            // updating the given array
            System.out.print(maxSubarraySum(arr, n) + " ");
        }
    }

    // Driver Code
    public static void main(String args[])
    {
        int arr[] = { -2, -5, 6, -2, -3,
                1, 5, -6, 4, -1 };
        int N = arr.length;
        int[][] query = { { 1, 4, 3 }, { 4, 5, -4 }, { 7, 9, 5 } };
        maxSubarraySumQuery(arr, N, query);
    }
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to find the maximum subarray
# sum using Kadane's Algorithm
def maxSubarraySum(arr, n):

    # Stores the maximum sum
    maxSum = 10 ** -9
    currSum = 0

    # Loop to iterate over the array
    for i in range(n):
        currSum += arr[i]

        # Update maxSum
        if (currSum > maxSum):
            maxSum = currSum
        if (currSum < 0):
            currSum = 0
    # Return Answer
    return maxSum

# Function to add integer X to all elements
# of the given array in range[L, R]
def updateArr(arr, L, R, X):
    # Loop to iterate over the range
    for i in range(L, R + 1):
        arr[i] += X

# Function to find the maximum subarray sum
# after each range update query
def maxSubarraySumQuery(arr, n, query):

    # Loop to iterate over the queries
    for i in range(len(query)):

        # Function call to update the array
        # according to the mentioned query
        updateArr(arr, query[i][0],
                  query[i][1],
                  query[i][2])

        # Print the max subarray sum after
        # updating the given array
        print(maxSubarraySum(arr, n), end=" ")

# Driver Code
arr = [-2, -5, 6, -2, -3, 1, 5, -6, 4, -1]
N = len(arr)
query = [[1, 4, 3],[4, 5, -4],[7, 9, 5]]

maxSubarraySumQuery(arr, N, query)

# This code is contributed by gfgking
```

## C#

```
// C#  program for the above approach
using System;
class GFG
{

    // Function to find the maximum subarray
    // sum using Kadane's Algorithm
    public static int maxSubarraySum(int[] arr, int n)
    {

        // Stores the maximum sum
        int maxSum = int.MinValue;
        int currSum = 0;

        // Loop to iterate over the array
        for (int i = 0; i <= n - 1; i++)
        {
            currSum += arr[i];

            // Update maxSum
            if (currSum > maxSum)
            {
                maxSum = currSum;
            }
            if (currSum < 0)
            {
                currSum = 0;
            }
        }

        // Return Answer
        return maxSum;
    }

    // Function to add integer X to all elements
    // of the given array in range [L, R]
    public static void updateArr(int[] arr, int L,
                                 int R, int X)
    {

        // Loop to iterate over the range
        for (int i = L; i <= R; i++)
        {
            arr[i] += X;
        }
    }

    // Function to find the maximum subarray sum
    // after each range update query
    public static void maxSubarraySumQuery(int[] arr, int n, int[,] query)
    {

        // Loop to iterate over the queries
        for (int i = 0; i < query.Length; i++)
        {

            // Function call to update the array
            // according to the mentioned query
            updateArr(arr, query[i, 0],
                    query[i, 1],
                    query[i, 2]);

            // Print the max subarray sum after
            // updating the given array
            Console.Write(maxSubarraySum(arr, n) + " ");
        }
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { -2, -5, 6, -2, -3, 1, 5, -6, 4, -1 };
        int N = arr.Length;
        int[,] query = { { 1, 4, 3 }, { 4, 5, -4 }, { 7, 9, 5 } };
        maxSubarraySumQuery(arr, N, query);
    }
}

// This code is contributed by _saurabh_jaiswal.
```

## java 描述语言

```
<script>
    // JavaScript Program to implement
    // the above approach

    // Function to find the maximum subarray
    // sum using Kadane's Algorithm
    function maxSubarraySum(arr, n)
    {

        // Stores the maximum sum
        let maxSum = Number.MIN_VALUE;
        let currSum = 0;

        // Loop to iterate over the array
        for (let i = 0; i <= n - 1; i++) {
            currSum += arr[i];

            // Update maxSum
            if (currSum > maxSum) {
                maxSum = currSum;
            }
            if (currSum < 0) {
                currSum = 0;
            }
        }

        // Return Answer
        return maxSum;
    }

    // Function to add integer X to all elements
    // of the given array in range [L, R]
    function updateArr(arr, L, R, X) {
        // Loop to iterate over the range
        for (let i = L; i <= R; i++) {
            arr[i] += X;
        }
    }

    // Function to find the maximum subarray sum
    // after each range update query
    function maxSubarraySumQuery(
        arr, n,
        query) {
        // Loop to iterate over the queries
        for (let i = 0; i < query.length; i++) {

            // Function call to update the array
            // according to the mentioned query
            updateArr(arr, query[i][0],
                query[i][1],
                query[i][2]);

            // Print the max subarray sum after
            // updating the given array
            document.write(maxSubarraySum(arr, n) + " ");
        }
    }

    // Driver Code
    let arr = [-2, -5, 6, -2, -3,
        1, 5, -6, 4, -1];
    let N = arr.length;
    let query = [[1, 4, 3],
    [4, 5, -4],
    [7, 9, 5]];

    maxSubarraySumQuery(arr, N, query);

// This code is contributed by Potta Lokesh
</script>
```

**Output**

```
16 10 20 
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(1)*