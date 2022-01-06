# 给定大小的两个不重叠子阵列的最大和

> 原文:[https://www . geeksforgeeks . org/给定大小的两个不重叠子阵列的最大和/](https://www.geeksforgeeks.org/maximum-sum-two-non-overlapping-subarrays-of-given-size/)

给定一个阵列，我们需要找到两个具有特定长度 K 的子阵列，使得这些子阵列的和在所有可能的子阵列选择中是最大的。
**例:**

```
Input : arr[] = [2, 5, 1, 2, 7, 3, 0]
        K = 2
Output : 2 5
         7 3
We can choose two arrays of maximum sum
as [2, 5] and [7, 3], the sum of these two 
subarrays is maximum among all possible 
choices of subarrays of length 2.

Input : arr[] = {10, 1, 3, 15, 30, 40, 4, 50, 2, 1}
        K = 3
Output : 3 15 30 
         40 4 50 
```

我们可以用类似于两个指针的方法来解决这个问题。首先，我们将前缀和存储在一个单独的数组中，这样就可以在恒定时间内计算任何子数组和。之后，我们将从(N–2K)和(N–K)索引初始化我们的两个子阵列，其中 N 是阵列的长度，K 是所需的子阵列长度。然后我们将从(N–2K)索引向 0 移动，每次我们将检查当前索引处的子阵列和(当前索引+ K)处的子阵列和是否大于先前选择的子阵列(如果是)，然后更新总和。我们可以在这里看到，由于我们需要最大化我们的总和，我们可以独立地对待两个子阵列。在每个索引处，我们将检查当前索引处的子阵和以及 K 距离处的子阵和，我们将独立选择最大和，并将最终答案更新为这两个数组的和。在下面的代码中，索引也是以一对的形式和，以实际打印子阵列。解决方案的总时间复杂度将是线性的。
为了更好的理解，请看下面的代码。

## C++

```
// C++ program to get maximum sum two non-overlapping
// subarrays of same specified length
#include <bits/stdc++.h>
using namespace std;

// Utility method to get sum of subarray
// from index i to j
int getSubarraySum(int sum[], int i, int j)
{
    if (i == 0)
        return sum[j];
    else
        return (sum[j] - sum[i - 1]);
}

// Method prints two non-overlapping subarrays of
// length K whose sum is maximum
void maximumSumTwoNonOverlappingSubarray(int arr[],
                                      int N, int K)
{
    int sum[N];

    // filling prefix sum array
    sum[0] = arr[0];
    for (int i = 1; i < N; i++)
        sum[i] = sum[i - 1] + arr[i];

    //    initializing subarrays from (N-2K) and (N-K) indices
    pair<int, int> resIndex = make_pair(N - 2 * K, N - K);

    //    initializing result sum from above subarray sums
    int maxSum2Subarray = getSubarraySum(sum, N - 2 * K, N - K - 1) +
                          getSubarraySum(sum, N - K, N - 1);

    //    storing second subarray maximum and its starting index
    pair<int, int> secondSubarrayMax = make_pair(N - K,
                          getSubarraySum(sum, N - K, N - 1));

    //    looping from N-2K-1 towards 0
    for (int i = N - 2 * K - 1; i >= 0; i--)
    {
        //    get subarray sum from (current index + K)
        int cur = getSubarraySum(sum, i + K, i + 2  * K - 1);

        // if (current index + K) sum is more  then update
        // secondSubarrayMax
        if (cur >= secondSubarrayMax.second)
            secondSubarrayMax = make_pair(i + K, cur);

        //    now getting complete sum (sum of both subarrays)
        cur = getSubarraySum(sum, i, i + K - 1) +
              secondSubarrayMax.second;

        //    if it is more then update main result
        if (cur >= maxSum2Subarray)
        {
            maxSum2Subarray = cur;
            resIndex = make_pair(i, secondSubarrayMax.first);
        }
    }

    //    printing actual subarrays
    for (int i = resIndex.first; i < resIndex.first + K; i++)
        cout << arr[i] << " ";
    cout << endl;

    for (int i = resIndex.second; i < resIndex.second + K; i++)
        cout << arr[i] << " ";
    cout << endl;
}

//    Driver code to test above methods
int main()
{
    int arr[] = {2, 5, 1, 2, 7, 3, 0};
    int N = sizeof(arr) / sizeof(int);

    //    K will be given such that (N >= 2K)
    int K = 2;

    maximumSumTwoNonOverlappingSubarray(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to get maximum sum two non-overlapping
// subarrays of same specified length
class GFG
{

static class pair
{
    int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Utility method to get sum of subarray
// from index i to j
static int getSubarraySum(int sum[],
                          int i, int j)
{
    if (i == 0)
        return sum[j];
    else
        return (sum[j] - sum[i - 1]);
}

// Method prints two non-overlapping subarrays of
// length K whose sum is maximum
static void maximumSumTwoNonOverlappingSubarray(int arr[],
                                                int N, int K)
{
    int []sum = new int[N];

    // filling prefix sum array
    sum[0] = arr[0];
    for (int i = 1; i < N; i++)
        sum[i] = sum[i - 1] + arr[i];

    // initializing subarrays from
    // (N-2K) and (N-K) indices
    pair resIndex = new pair(N - 2 * K, N - K);

    // initializing result sum from above subarray sums
    int maxSum2Subarray = getSubarraySum(sum, N - 2 * K,
                                              N - K - 1) +
                          getSubarraySum(sum, N - K, N - 1);

    // storing second subarray maximum and
    // its starting index
    pair secondSubarrayMax = new pair(N - K,
                       getSubarraySum(sum, N - K, N - 1));

    // looping from N-2K-1 towards 0
    for (int i = N - 2 * K - 1; i >= 0; i--)
    {
        // get subarray sum from (current index + K)
        int cur = getSubarraySum(sum, i + K, i + 2 * K - 1);

        // if (current index + K) sum is more
        // then update secondSubarrayMax
        if (cur >= secondSubarrayMax.second)
            secondSubarrayMax = new pair(i + K, cur);

        // now getting complete sum (sum of both subarrays)
        cur = getSubarraySum(sum, i, i + K - 1) +
            secondSubarrayMax.second;

        // if it is more then update main result
        if (cur >= maxSum2Subarray)
        {
            maxSum2Subarray = cur;
            resIndex = new pair(i, secondSubarrayMax.first);
        }
    }

    // printing actual subarrays
    for (int i = resIndex.first;
             i < resIndex.first + K; i++)
        System.out.print(arr[i] + " ");
    System.out.println();

    for (int i = resIndex.second;
             i < resIndex.second + K; i++)
        System.out.print(arr[i] + " ");
    System.out.println();
}

// Driver code to test above methods
public static void main(String[] args)
{
    int arr[] = {2, 5, 1, 2, 7, 3, 0};
    int N = arr.length;

    // K will be given such that (N >= 2K)
    int K = 2;

    maximumSumTwoNonOverlappingSubarray(arr, N, K);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to get maximum Sum two
# non-overlapping subarrays of same specified length

# Utility method to get Sum of
# subarray from index i to j
def getSubarraySum(Sum, i, j):

    if i == 0:
        return Sum[j]
    else:
        return Sum[j] - Sum[i - 1]

# Method prints two non-overlapping subarrays
# of length K whose Sum is maximum
def maximumSumTwoNonOverlappingSubarray(arr, N, K):

    Sum = [None] * N

    # filling prefix Sum array
    Sum[0] = arr[0]
    for i in range(1, N):
        Sum[i] = Sum[i - 1] + arr[i]

    # Initializing subarrays from
    # (N-2K) and (N-K) indices
    resIndex = (N - 2 * K, N - K)

    # initializing result Sum from above subarray Sums
    maxSum2Subarray = (getSubarraySum(Sum, N - 2 * K, N - K - 1) +
                       getSubarraySum(Sum, N - K, N - 1))

    # storing second subarray maximum and its starting index
    secondSubarrayMax = (N - K, getSubarraySum(Sum, N - K, N - 1))

    # looping from N-2K-1 towards 0
    for i in range(N - 2 * K - 1, -1, -1):

        # get subarray Sum from (current index + K)
        cur = getSubarraySum(Sum, i + K, i + 2 * K - 1)

        # if (current index + K) Sum is more
        # than update secondSubarrayMax
        if cur >= secondSubarrayMax[1]:
            secondSubarrayMax = (i + K, cur)

        # now getting complete Sum (Sum of both subarrays)
        cur = (getSubarraySum(Sum, i, i + K - 1) +
                           secondSubarrayMax[1])

        # If it is more then update main result
        if cur >= maxSum2Subarray:

            maxSum2Subarray = cur
            resIndex = (i, secondSubarrayMax[0])

    # printing actual subarrays
    for i in range(resIndex[0], resIndex[0] + K):
        print(arr[i], end = " ")
    print()

    for i in range(resIndex[1], resIndex[1] + K):
        print(arr[i], end = " ")
    print()

# Driver Code
if __name__ == "__main__":

    arr = [2, 5, 1, 2, 7, 3, 0]
    N = len(arr)

    # K will be given such that (N >= 2K)
    K = 2

    maximumSumTwoNonOverlappingSubarray(arr, N, K)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to get maximum sum two non-overlapping
// subarrays of same specified length
using System;

class GFG
{

class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Utility method to get sum of subarray
// from index i to j
static int getSubarraySum(int []sum,
                        int i, int j)
{
    if (i == 0)
        return sum[j];
    else
        return (sum[j] - sum[i - 1]);
}

// Method prints two non-overlapping subarrays of
// length K whose sum is maximum
static void maximumSumTwoNonOverlappingSubarray(int []arr,
                                                int N, int K)
{
    int []sum = new int[N];

    // filling prefix sum array
    sum[0] = arr[0];
    for (int i = 1; i < N; i++)
        sum[i] = sum[i - 1] + arr[i];

    // initializing subarrays from
    // (N-2K) and (N-K) indices
    pair resIndex = new pair(N - 2 * K, N - K);

    // initializing result sum from above subarray sums
    int maxSum2Subarray = getSubarraySum(sum, N - 2 * K,
                                            N - K - 1) +
                        getSubarraySum(sum, N - K, N - 1);

    // storing second subarray maximum and
    // its starting index
    pair secondSubarrayMax = new pair(N - K,
                    getSubarraySum(sum, N - K, N - 1));

    // looping from N-2K-1 towards 0
    for (int i = N - 2 * K - 1; i >= 0; i--)
    {
        // get subarray sum from (current index + K)
        int cur = getSubarraySum(sum, i + K, i + 2 * K - 1);

        // if (current index + K) sum is more
        // then update secondSubarrayMax
        if (cur >= secondSubarrayMax.second)
            secondSubarrayMax = new pair(i + K, cur);

        // now getting complete sum (sum of both subarrays)
        cur = getSubarraySum(sum, i, i + K - 1) +
            secondSubarrayMax.second;

        // if it is more then update main result
        if (cur >= maxSum2Subarray)
        {
            maxSum2Subarray = cur;
            resIndex = new pair(i, secondSubarrayMax.first);
        }
    }

    // printing actual subarrays
    for (int i = resIndex.first;
            i < resIndex.first + K; i++)
        Console.Write(arr[i] + " ");
    Console.WriteLine();

    for (int i = resIndex.second;
            i < resIndex.second + K; i++)
        Console.Write(arr[i] + " ");
    Console.WriteLine();
}

// Driver code
public static void Main(String[] args)
{
    int []arr = {2, 5, 1, 2, 7, 3, 0};
    int N = arr.Length;

    // K will be given such that (N >= 2K)
    int K = 2;

    maximumSumTwoNonOverlappingSubarray(arr, N, K);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to get maximum sum two non-overlapping
// subarrays of same specified length

// Utility method to get sum of subarray
// from index i to j
function getSubarraySum(sum, i, j) {
    if (i == 0)
        return sum[j];
    else
        return (sum[j] - sum[i - 1]);
}

// Method prints two non-overlapping subarrays of
// length K whose sum is maximum
function maximumSumTwoNonOverlappingSubarray(arr, N, K) {
    let sum = new Array(N);

    // filling prefix sum array
    sum[0] = arr[0];
    for (let i = 1; i < N; i++)
        sum[i] = sum[i - 1] + arr[i];

    // initializing subarrays from (N-2K) and (N-K) indices
    let resIndex = [N - 2 * K, N - K];

    // initializing result sum from above subarray sums
    let maxSum2Subarray = getSubarraySum(sum, N - 2 * K, N - K - 1) +
        getSubarraySum(sum, N - K, N - 1);

    // storing second subarray maximum and its starting index
    let secondSubarrayMax = [N - K,
    getSubarraySum(sum, N - K, N - 1)];

    // looping from N-2K-1 towards 0
    for (let i = N - 2 * K - 1; i >= 0; i--) {
        // get subarray sum from (current index + K)
        let cur = getSubarraySum(sum, i + K, i + 2 * K - 1);

        // if (current index + K) sum is more then update
        // secondSubarrayMax
        if (cur >= secondSubarrayMax[1])
            secondSubarrayMax = [i + K, cur];

        // now getting complete sum (sum of both subarrays)
        cur = getSubarraySum(sum, i, i + K - 1) +
            secondSubarrayMax[1];

        // if it is more then update main result
        if (cur >= maxSum2Subarray) {
            maxSum2Subarray = cur;
            resIndex = [i, secondSubarrayMax[0]];
        }
    }

    // printing actual subarrays
    for (let i = resIndex[0]; i < resIndex[0] + K; i++)
        document.write(arr[i] + " ");
    document.write("<br>");

    for (let i = resIndex[1]; i < resIndex[1] + K; i++)
        document.write(arr[i] + " ");
    document.write("<br>");
}

// Driver code to test above methods

let arr = [2, 5, 1, 2, 7, 3, 0];
let N = arr.length;

// K will be given such that (N >= 2K)
let K = 2;

maximumSumTwoNonOverlappingSubarray(arr, N, K);

</script>
```

**输出:**

```
2 5
7 3
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。