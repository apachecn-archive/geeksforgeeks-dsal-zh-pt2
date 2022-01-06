# 任何数组元素的最大频率，精确 K 个增量

> 原文:[https://www . geeksforgeeks . org/任何数组元素的最大频率-精确 k 增量/](https://www.geeksforgeeks.org/maximum-frequency-of-any-array-element-possible-by-exactly-k-increments/)

给定一个由 **N** 个正整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是在精确执行**个 K** 个增量后，找到任意数组元素的最高[个频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)

**示例:**

> **输入:** arr[] = {1，3，2，2}，K = 2
> **输出:** 3
> **解释:**
> 下面是执行的操作:
> 
> 1.  向索引 2(= 2)处的元素添加 1，然后数组修改为{1，3，3，2}。
> 2.  向索引 3(= 2)处的元素添加 1，然后数组修改为{1，3，3，3}。
> 
> 经过以上步骤，一个数组元素的最大频率为 3。
> 
> **输入:** arr[] = {4，3，4}，K = 5
> T3】输出: 2

**方法:**使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)和[排序](https://www.geeksforgeeks.org/sorting-algorithms/)可以解决给定的问题。按照以下步骤解决此问题:

*   初始化变量说**开始**、**结束**、**求和**为 **0** 、 **mostFreq** 为 [INT_MIN。](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/)
*   [按递增顺序排列数组**arr[]**](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   [使用变量**结束**迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**，并执行以下步骤:
    *   将**和**的值增加 **arr【结束】**的值。
    *   当 **(sum + K)** 的值小于**(arr[end]*(end–start+1))**的值时，将 **sum** 的值减**arr【start】**，将 **start** 的值增 **1** 。
    *   将**最大频率**的值更新为**最大频率**和**(结束–开始+ 1)** 的最大值。
*   初始化一个变量，说 **reqSum** 作为**(arr[N-1]* N–sum)**的值，将结果和存储到[使所有数组元素相等](https://www.geeksforgeeks.org/minimum-increment-decrement-to-make-array-elements-equal/)。
*   如果 **mostFreq** 的值为 **N** ， **K** 的值大于 **reqSum** ，则 **K** 的值递减 **reqSum** 。
*   如果 **K** 的值是 **N** 的倍数，则打印 **N** 。否则，打印**(N–1)**的值。
*   完成以上步骤后，打印 **mostFreq** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the highest frequency
// of any array element possible by
// exactly K increment operations
void findMostFrequent(int arr[], int N,
                      int K)
{
    int start = 0, end = 0;

    // Sort the given array
    sort(arr, arr + N);

    // Stores the maximum frequency
    // and the sum of sliding window
    int mostFreq = INT_MIN, sum = 0;

    // Traverse the array arr[]
    for (end = 0; end < N; end++) {

        // Add the current element
        // to the window
        sum = sum + arr[end];

        // Decreasing the window size
        while (sum + K < arr[end] * (end - start + 1)) {

            // Update the value of sum
            // by subtracting arr[start]
            sum = sum - arr[start];

            // Increment the value
            // of the start
            start++;
        }

        // Update maximum window size
        mostFreq = max(mostFreq,
                       end - start + 1);
    }

    // Stores the required sum to
    // make all elements of arr[] equal
    int reqSum = arr[N - 1] * N - sum;

    // If result from at most K increments
    // is N and K is greater than reqSum
    if (mostFreq == N && reqSum < K) {

        // Decrement the value of K
        // by reqSum
        K = K - reqSum;

        // If K is mutilpe of N then
        // increment K/N times to
        // every element
        if (K % N == 0) {
            cout << N << endl;
        }

        // Otherwise first make every
        // element equal then increment
        // remaining K to one element
        else {
            cout << N - 1 << endl;
        }

        return;
    }

    // Print the answer
    cout << mostFreq << endl;
}

// Driver Code
int main()
{
    int arr[] = { 4, 3, 4 };
    int K = 5;
    int N = sizeof(arr) / sizeof(arr[0]);
    findMostFrequent(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG {

// Function to find the highest frequency
// of any array element possible by
// exactly K increment operations
static void findMostFrequent(int arr[], int N,
                      int K)
{
    int start = 0, end = 0;

    // Sort the given array
    Arrays.sort(arr);

    // Stores the maximum frequency
    // and the sum of sliding window
    int mostFreq = Integer.MIN_VALUE, sum = 0;

    // Traverse the array arr[]
    for (end = 0; end < N; end++) {

        // Add the current element
        // to the window
        sum = sum + arr[end];

        // Decreasing the window size
        while (sum + K < arr[end] * (end - start + 1)) {

            // Update the value of sum
            // by subtracting arr[start]
            sum = sum - arr[start];

            // Increment the value
            // of the start
            start++;
        }

        // Update maximum window size
        mostFreq = Math.max(mostFreq,
                       end - start + 1);
    }

    // Stores the required sum to
    // make all elements of arr[] equal
    int reqSum = arr[N - 1] * N - sum;

    // If result from at most K increments
    // is N and K is greater than reqSum
    if (mostFreq == N && reqSum < K) {

        // Decrement the value of K
        // by reqSum
        K = K - reqSum;

        // If K is mutilpe of N then
        // increment K/N times to
        // every element
        if (K % N == 0) {
            System.out.println(N);
        }

        // Otherwise first make every
        // element equal then increment
        // remaining K to one element
        else {
            System.out.println(N - 1);
        }

        return;
    }

    // Print the answer
    System.out.println( mostFreq);
}

    // Driver Code
    public static void main(String[] args)
    {
    int arr[] = { 4, 3, 4 };
    int K = 5;
    int N = arr.length;
    findMostFrequent(arr, N, K);
    }
}

// This code is contributed by target_2.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the highest frequency
# of any array element possible by
# exactly K increment operations
def findMostFrequent( arr,  N, K):
    start = 0
    end = 0

    # Sort the given array
    arr.sort()

    # Stores the maximum frequency
    # and the sum of sliding window
    mostFreq = -2**31
    sum = 0

    # Traverse the array arr[]
    for end in range(N):

        # Add the current element
        # to the window
        sum = sum + arr[end]

        # Decreasing the window size
        while (sum + K < arr[end] * (end - start + 1)):

            # Update the value of sum
            # by subtracting arr[start]
            sum = sum - arr[start]

            # Increment the value
            # of the start
            start += 1

        # Update maximum window size
        mostFreq = max(mostFreq, end - start + 1)

    # Stores the required sum to
    # make all elements of arr[] equal
    reqSum = arr[N - 1] * N - sum

    # If result from at most K increments
    # is N and K is greater than reqSum
    if (mostFreq == N and reqSum < K):

        # Decrement the value of K
        # by reqSum
        K = K - reqSum

        # If K is mutilpe of N then
        # increment K/N times to
        # every element
        if (K % N == 0):
            print(N)

        # Otherwise first make every
        # element equal then increment
        # remaining K to one element
        else:
            print(N - 1)
        return
    # Print the answer
    print(mostFreq)

# Driver Code
arr = [4, 3, 4]
K = 5
N = len(arr)
findMostFrequent(arr, N, K)

# This code is contributed by shubhamsingh10
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the highest frequency
// of any array element possible by
// exactly K increment operations
static void findMostFrequent(int []arr, int N,
                             int K)
{
    int start = 0, end = 0;

    // Sort the given array
    Array.Sort(arr);

    // Stores the maximum frequency
    // and the sum of sliding window
    int mostFreq = Int32.MinValue, sum = 0;

    // Traverse the array arr[]
    for(end = 0; end < N; end++)
    {

        // Add the current element
        // to the window
        sum = sum + arr[end];

        // Decreasing the window size
        while (sum + K < arr[end] * (end - start + 1))
        {

            // Update the value of sum
            // by subtracting arr[start]
            sum = sum - arr[start];

            // Increment the value
            // of the start
            start++;
        }

        // Update maximum window size
        mostFreq = Math.Max(mostFreq,
                            end - start + 1);
    }

    // Stores the required sum to
    // make all elements of arr[] equal
    int reqSum = arr[N - 1] * N - sum;

    // If result from at most K increments
    // is N and K is greater than reqSum
    if (mostFreq == N && reqSum < K)
    {

        // Decrement the value of K
        // by reqSum
        K = K - reqSum;

        // If K is mutilpe of N then
        // increment K/N times to
        // every element
        if (K % N == 0)
        {
            Console.Write(N);
        }

        // Otherwise first make every
        // element equal then increment
        // remaining K to one element
        else
        {
            Console.Write(N - 1);
        }
        return;
    }

    // Print the answer
    Console.Write( mostFreq);
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 4, 3, 4 };
    int K = 5;
    int N = arr.Length;

    findMostFrequent(arr, N, K);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the highest frequency
// of any array element possible by
// exactly K increment operations
function findMostFrequent(arr, N, K) {
    let start = 0, end = 0;

    // Sort the given array
    arr.sort((a, b) => a - b);

    // Stores the maximum frequency
    // and the sum of sliding window
    let mostFreq = Number.MIN_SAFE_INTEGER, sum = 0;

    // Traverse the array arr[]
    for (end = 0; end < N; end++) {

        // Add the current element
        // to the window
        sum = sum + arr[end];

        // Decreasing the window size
        while (sum + K < arr[end] * (end - start + 1)) {

            // Update the value of sum
            // by subtracting arr[start]
            sum = sum - arr[start];

            // Increment the value
            // of the start
            start++;
        }

        // Update maximum window size
        mostFreq = Math.max(mostFreq,
            end - start + 1);
    }

    // Stores the required sum to
    // make all elements of arr[] equal
    let reqSum = arr[N - 1] * N - sum;

    // If result from at most K increments
    // is N and K is greater than reqSum
    if (mostFreq == N && reqSum < K) {

        // Decrement the value of K
        // by reqSum
        K = K - reqSum;

        // If K is mutilpe of N then
        // increment K/N times to
        // every element
        if (K % N == 0) {
            document.write(N + "<br>");
        }

        // Otherwise first make every
        // element equal then increment
        // remaining K to one element
        else {
            document.write(N - 1 + "<br>");
        }

        return;
    }

    // Print the answer
    document.write(mostFreq + "<br>");
}

// Driver Code
let arr = [4, 3, 4];
let K = 5;
let N = arr.length
findMostFrequent(arr, N, K);

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(1)*