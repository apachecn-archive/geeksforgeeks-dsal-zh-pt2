# 最大化 NxN 网格中 KxK 子网格的中值

> 原文:[https://www . geesforgeks . org/maximum-a-kxk-in-nxn-grid 子网格/](https://www.geeksforgeeks.org/maximize-median-of-a-kxk-sub-grid-in-an-nxn-grid/)

给定一个由非负整数和整数组成的大小为 **N** 的[正方形矩阵](https://www.geeksforgeeks.org/how-to-access-elements-of-a-square-matrix/)**arr【】【】【】】**，任务是找到大小为 **K** 的正方形子矩阵元素的最大[中值](https://www.geeksforgeeks.org/program-for-mean-and-median-of-an-unsorted-array/)。

**示例:**

> **输入:** arr[][] = {{1，5，12}，{6，7，11}，{8，9，10}}，N = 3，K = 2
> **输出:** 9
> **解释:**
> 所有大小为 2*2 的子方块的中位数为:
> 
> 1.  子正方形{{1，5}，{6，7}}的中值等于 5。
> 2.  子正方形{{5，12}，{7，11}}的中位数等于 7。
> 3.  子正方形{{6，7}，{8，9}}的中位数等于 7。
> 4.  子方块{{7，11}，{9，10}}的中位数等于 9。
> 
> 因此，所有可能的方阵中最大可能的中值等于 9。
> 
> **输入:** arr[][] = {{1，2，3，4}，{5，6，7，8}，{9，10，10，11}，{12，13，14，13}}，N = 4，K = 2
> **输出:** 11

**朴素方法:**解决上述给定问题的最简单方法是迭代每个大小为 **K*K** 的子矩阵，然后在所有形成的子矩阵中找到最大中值。

***时间复杂度:**O(N<sup>2</sup>* K<sup>2</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述问题可以基于以下观察进行优化:

*   如果 **M** 是正方形子矩阵的中值，那么该子矩阵中小于或等于 **M** 的数的个数必须小于 **(K <sup>2</sup> +1)/2** 。
*   想法是使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)找到给定的中值，如下所示:
    *   如果任何大小为 **K×K** 的子矩阵中小于 **M** 的个数小于 **(K <sup>2</sup> +1)/2，**则增加左边界。
    *   否则，递减右边界。
*   其思想是使用矩阵的[前缀和来计数正方形子矩阵中在恒定时间内小于特定值的元素。](https://www.geeksforgeeks.org/prefix-sum-2d-array/)

按照以下步骤解决问题:

*   初始化两个变量，说**低**为 **0** 和**高**为 [**INT_MAX**](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) 代表搜索空间的范围。
*   重复直到**低电平**小于**高电平**，并执行以下步骤:
    *   找到范围的中间值**【低，高】**，并将其存储在一个变量中，比如**中间**。
    *   初始化向量的[向量](https://www.geeksforgeeks.org/vector-of-vectors-in-c-stl-with-examples/)说**前置**将小于或等于**的元素的[计数存储在前缀子矩阵中](https://www.geeksforgeeks.org/count-smaller-equal-elements-sorted-array/)** 。
    *   使用变量 **i** 和 **j** 迭代矩阵的每个元素**arr【】【】【】**，并将 **Pre[i + 1][j + 1]** 的值更新为**Pre[I+1][j]+Pre[I][j+1]–Pre[I][j]**，然后如果 **arr[i],则将 **Pre[i + 1][j + 1]** 递增 **1****
    *   初始化一个变量，说**标记**为**假**来存储**中间**的值是否可能作为中间值。
    *   迭代**【K，N】*【K，N】**的对 **(i，j)** 的每个可能值，然后执行以下步骤:
        *   在左上角为**(I–K，j–K)**、右下角为 **(i，j)** 的正方形子矩阵中，找出小于或等于**中间**的元素个数，并将其存储在一个变量中，比如 **X** 为**Pre[I][j]–Pre[I–K][j]–Pre[I][j–K]+Pre[I–K][j–K]**。
        *   如果 **X** 小于 **(K <sup>2</sup> +1)/2** ，则标记**标志**为真，[断开回路](https://www.geeksforgeeks.org/break-statement-cc/)。
    *   如果**标志**为**真**，则将**低**的值更新为**(中间+ 1)** 。否则，将**高值**更新为**中值**。
*   完成上述步骤后，将**低的值**打印为在所有可能的大小为 **K*K** 的正方形子矩阵中获得的最大中值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to determine if a given
// value can be median
bool isMaximumMedian(vector<vector<int> >& arr,
                     int N, int K, int mid)
{
    // Stores the prefix sum array
    vector<vector<int> > Pre(
        N + 5, vector<int>(N + 5, 0));

    // Traverse the matrix arr[][]
    for (int i = 0; i < N; ++i) {
        for (int j = 0; j < N; ++j) {

            // Update Pre[i+1][j+1]
            Pre[i + 1][j + 1] = Pre[i + 1][j]
                                + Pre[i][j + 1]
                                - Pre[i][j];

            // If arr[i][j] is less
            // than or equal to mid
            if (arr[i][j] <= mid)
                Pre[i + 1][j + 1]++;
        }
    }

    // Stores the count of elements
    // should be less than mid
    int required = (K * K + 1) / 2;

    // Stores if the median mid
    // can be possible or not
    bool flag = 0;

    // Iterate over the range [K, N]
    for (int i = K; i <= N; ++i) {

        // Iterate over the range [K, N]
        for (int j = K; j <= N; ++j) {

            // Stores count of elements less
            // than or equal to the value
            // mid in submatrix with bottom
            // right vertices at (i, j)
            int X = Pre[i][j] - Pre[i - K][j]
                    - Pre[i][j - K]
                    + Pre[i - K][j - K];

            // If X is less than or
            // equal to required
            if (X < required)
                flag = 1;
        }
    }

    // Return flag
    return flag;
}

// Function to find the maximum median
// of a subsquare of the given size
int maximumMedian(vector<vector<int> >& arr,
                  int N, int K)
{
    // Stores the range of the
    // search space
    int low = 0, high = 1e9;

    // Iterate until low is less
    // than high
    while (low < high) {

        // Stores the mid value of
        // the range [low, high]
        int mid = low + (high - low) / 2;

        // If the current median can
        // be possible
        if (isMaximumMedian(arr, N, K, mid)) {

            // Update the value of low
            low = mid + 1;
        }
        else {

            // Update the value of high
            high = mid;
        }
    }

    // Return value stored in low as
    // answer
    return low;
}

// Driver Code
int main()
{
    vector<vector<int> > arr
        = { { 1, 5, 12 }, { 6, 7, 11 }, { 8, 9, 10 } };
    int N = arr.size();
    int K = 2;
    cout << maximumMedian(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG
{

// Function to determine if a given
// value can be median
static boolean isMaximumMedian(int arr[][] , int N, int K, int mid)
{

    // Stores the prefix sum array
    int [][]Pre = new int [N+5][N+5];

    // Traverse the matrix arr[][]
    for (int i = 0; i < N; ++i) {
        for (int j = 0; j < N; ++j) {

            // Update Pre[i+1][j+1]
            Pre[i + 1][j + 1] = Pre[i + 1][j]
                                + Pre[i][j + 1]
                                - Pre[i][j];

            // If arr[i][j] is less
            // than or equal to mid
            if (arr[i][j] <= mid)
                Pre[i + 1][j + 1]++;
        }
    }

    // Stores the count of elements
    // should be less than mid
    int required = (K * K + 1) / 2;

    // Stores if the median mid
    // can be possible or not
    boolean flag = false;

    // Iterate over the range [K, N]
    for (int i = K; i <= N; ++i) {

        // Iterate over the range [K, N]
        for (int j = K; j <= N; ++j) {

            // Stores count of elements less
            // than or equal to the value
            // mid in submatrix with bottom
            // right vertices at (i, j)
            int X = Pre[i][j] - Pre[i - K][j]
                    - Pre[i][j - K]
                    + Pre[i - K][j - K];

            // If X is less than or
            // equal to required
            if (X < required)
                flag = true;
        }
    }

    // Return flag
    return flag;
}

// Function to find the maximum median
// of a subsquare of the given size
static int maximumMedian(int arr[][], int N, int K)
{
    // Stores the range of the
    // search space
    int low = 0, high = (int)1e9;

    // Iterate until low is less
    // than high
    while (low < high) {

        // Stores the mid value of
        // the range [low, high]
        int mid = low + (high - low) / 2;

        // If the current median can
        // be possible
        if (isMaximumMedian(arr, N, K, mid)) {

            // Update the value of low
            low = mid + 1;
        }
        else {

            // Update the value of high
            high = mid;
        }
    }

    // Return value stored in low as
    // answer
    return low;
}

// Driver Code
public static void main(String args[])
{
   int [][] arr = { { 1, 5, 12 }, { 6, 7, 11 }, { 8, 9, 10 } };
    int N = arr.length;
    int K = 2;
    System.out.print( maximumMedian(arr, N, K));
}
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to determine if a given
# value can be median
def isMaximumMedian(arr, N, K, mid):

    # Stores the prefix sum array
    Pre = [[0 for x in range(N + 5)]
              for y in range(N + 5)]

    # Traverse the matrix arr[][]
    for i in range(N):
        for j in range(N):

            # Update Pre[i+1][j+1]
            Pre[i + 1][j + 1] = (Pre[i + 1][j] +
                                 Pre[i][j + 1] -
                                 Pre[i][j])

            # If arr[i][j] is less
            # than or equal to mid
            if (arr[i][j] <= mid):
                Pre[i + 1][j + 1] += 1

    # Stores the count of elements
    # should be less than mid
    required = (K * K + 1) // 2

    # Stores if the median mid
    # can be possible or not
    flag = 0

    # Iterate over the range [K, N]
    for i in range(K, N + 1):

        # Iterate over the range [K, N]
        for j in range(K, N + 1):

            # Stores count of elements less
            # than or equal to the value
            # mid in submatrix with bottom
            # right vertices at (i, j)
            X = (Pre[i][j] - Pre[i - K][j] -
                 Pre[i][j - K] + Pre[i - K][j - K])

            # If X is less than or
            # equal to required
            if (X < required):
                flag = 1

    # Return flag
    return flag

# Function to find the maximum median
# of a subsquare of the given size
def maximumMedian(arr, N, K):

    # Stores the range of the
    # search space
    low = 0
    high = 1000000009

    # Iterate until low is less
    # than high
    while (low < high):

        # Stores the mid value of
        # the range [low, high]
        mid = low + (high - low) // 2

        # If the current median can
        # be possible
        if (isMaximumMedian(arr, N, K, mid)):

            # Update the value of low
            low = mid + 1

        else:

            # Update the value of high
            high = mid

    # Return value stored in low as
    # answer
    return low

# Driver Code
if __name__ == "__main__":

    arr = [ [ 1, 5, 12 ],
            [ 6, 7, 11 ],
            [ 8, 9, 10 ] ]
    N = len(arr)
    K = 2

    print(maximumMedian(arr, N, K))

# This code is contributed by ukasp
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to determine if a given
// value can be median
static bool isMaximumMedian(int[,] arr, int N,
                            int K, int mid)
{

    // Stores the prefix sum array
    int [,]Pre = new int[N + 5, N + 5];

    // Traverse the matrix arr[][]
    for(int i = 0; i < N; ++i)
    {
        for(int j = 0; j < N; ++j)
        {

            // Update Pre[i+1][j+1]
            Pre[i + 1, j + 1] = Pre[i + 1, j] +
                                Pre[i, j + 1] -
                                Pre[i, j];

            // If arr[i][j] is less
            // than or equal to mid
            if (arr[i, j] <= mid)
                Pre[i + 1, j + 1]++;
        }
    }

    // Stores the count of elements
    // should be less than mid
    int required = (K * K + 1) / 2;

    // Stores if the median mid
    // can be possible or not
    bool flag = false;

    // Iterate over the range [K, N]
    for(int i = K; i <= N; ++i)
    {

        // Iterate over the range [K, N]
        for(int j = K; j <= N; ++j)
        {

            // Stores count of elements less
            // than or equal to the value
            // mid in submatrix with bottom
            // right vertices at (i, j)
            int X = Pre[i, j] - Pre[i - K, j] -
                    Pre[i, j - K] + Pre[i - K, j - K];

            // If X is less than or
            // equal to required
            if (X < required)
                flag = true;
        }
    }

    // Return flag
    return flag;
}

// Function to find the maximum median
// of a subsquare of the given size
static int maximumMedian(int[,] arr, int N, int K)
{

    // Stores the range of the
    // search space
    int low = 0, high = (int)1e9;

    // Iterate until low is less
    // than high
    while (low < high)
    {

        // Stores the mid value of
        // the range [low, high]
        int mid = low + (high - low) / 2;

        // If the current median can
        // be possible
        if (isMaximumMedian(arr, N, K, mid))
        {

            // Update the value of low
            low = mid + 1;
        }
        else
        {

            // Update the value of high
            high = mid;
        }
    }

    // Return value stored in low as
    // answer
    return low;
}

// Driver code
public static void Main(string[] args)
{
    int [,] arr = { { 1, 5, 12 },
                    { 6, 7, 11 },
                    { 8, 9, 10 } };
    int N = arr.GetLength(0);
    int K = 2;

    Console.WriteLine(maximumMedian(arr, N, K));
}
}

// This code is contributed by avijitmondal1998
```

## java 描述语言

```
<script>
       // JavaScript Program for the above approach

       // Function to determine if a given
       // value can be median
       function isMaximumMedian(arr, N, K, mid) {
           // Stores the prefix sum array
           let Pre = Array(N + 5).fill().map(() => Array(N + 5).fill(0));

           // Traverse the matrix arr[][]
           for (let i = 0; i < N; ++i) {
               for (let j = 0; j < N; ++j) {

                   // Update Pre[i+1][j+1]
                   Pre[i + 1][j + 1] = Pre[i + 1][j]
                       + Pre[i][j + 1]
                       - Pre[i][j];

                   // If arr[i][j] is less
                   // than or equal to mid
                   if (arr[i][j] <= mid)
                       Pre[i + 1][j + 1]++;
               }
           }

           // Stores the count of elements
           // should be less than mid
           let required = Math.floor((K * K + 1) / 2);

           // Stores if the median mid
           // can be possible or not
           let flag = 0;

           // Iterate over the range [K, N]
           for (let i = K; i <= N; ++i) {

               // Iterate over the range [K, N]
               for (let j = K; j <= N; ++j) {

                   // Stores count of elements less
                   // than or equal to the value
                   // mid in submatrix with bottom
                   // right vertices at (i, j)
                   let X = Pre[i][j] - Pre[i - K][j]
                       - Pre[i][j - K]
                       + Pre[i - K][j - K];

                   // If X is less than or
                   // equal to required
                   if (X < required)
                       flag = 1;
               }
           }

           // Return flag
           return flag;
       }

       // Function to find the maximum median
       // of a subsquare of the given size
       function maximumMedian(arr, N, K) {
           // Stores the range of the
           // search space
           let low = 0, high = 1e9;

           // Iterate until low is less
           // than high
           while (low < high) {

               // Stores the mid value of
               // the range [low, high]
               let mid = low + Math.floor((high - low) / 2);

               // If the current median can
               // be possible
               if (isMaximumMedian(arr, N, K, mid)) {

                   // Update the value of low
                   low = mid + 1;
               }
               else {

                   // Update the value of high
                   high = mid;
               }
           }

           // Return value stored in low as
           // answer
           return low;
       }

       // Driver Code

       let arr
           = [[1, 5, 12], [6, 7, 11], [8, 9, 10]];
       let N = arr.length;
       let K = 2;
       document.write(maximumMedian(arr, N, K));

   // This code is contributed by Potta Lokesh

   </script>
```

**Output:** 

```
9
```

***时间复杂度:**O(N<sup>2</sup>* log(10<sup>9</sup>)*
***辅助空间:** O(N <sup>2</sup> )*