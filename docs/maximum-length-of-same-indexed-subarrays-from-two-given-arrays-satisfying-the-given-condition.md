# 满足给定条件的两个给定阵列的相同索引子阵列的最大长度

> 原文:[https://www . geeksforgeeks . org/满足给定条件的两个给定数组中相同索引子数组的最大长度/](https://www.geeksforgeeks.org/maximum-length-of-same-indexed-subarrays-from-two-given-arrays-satisfying-the-given-condition/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和**brr【】**以及一个整数 **C** ，任务是找到相同索引子阵的最大可能长度，比如 **K** ，使得 **K** 长度子阵中的最大元素之和与**brr【】**中的 **K** 和 **K** 之和之间的乘积

**示例:**

> **输入:** arr[] = {2，1，3，4，5}，brr[] = {3，6，1，3，4}，C = 25
> **输出:** 3
> **说明:**考虑子阵 arr[] = {2，1，3} (Sum = 6)和 brr[] = {3，6，1}(最大元素= 6)，最大元素+ sum * K = 6 + 6 * 3 = 24，小于 C(= 25)。
> 
> **输入:** arr[] ={1，2，1，6，5，5，6，1}，brr[] = {14，8，15，15，9，10，7，12}，C = 40
> T3】输出: 3
> **解释:**考虑子阵 arr[] ={1，2，1} (Sum = 4)和 brr[] = {14，8，15}(最大元素= 6)，最大元素+ sum * K

**天真方法:**最简单的方法是[生成两个给定阵列的所有可能的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，并考虑两个阵列中所有相似索引的子阵列，并检查给定条件。打印满足给定条件的子阵列的最大长度。

***时间复杂度:**O(K * N<sup>2</sup>)*
***辅助空间:** O(1)*

**基于二进制搜索的方法:**为了优化上述方法，想法是使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)找到 **K** 的可能值，并使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)找到长度为**K**T9】的每个子阵列的[和。按照以下步骤解决问题:](https://www.geeksforgeeks.org/sum-of-all-subarrays-of-size-k/)

*   [建立一个线段树，在所有可能的范围中找到最大值](https://www.geeksforgeeks.org/segment-tree-set-2-range-maximum-query-node-update/)。
*   在范围**【0，N】**上执行**二分搜索法**，以找到子阵列的最大可能尺寸。
    *   将**低电平**初始化为 **0** ，将**高电平**初始化为 **N** 。
    *   求**中间**的值为**(低+高)/2** 。
    *   通过检查给定的条件，检查是否有可能获得子阵列的最大尺寸为**中间**。如果发现是真的，那么更新最大长度为**中**和**低**为**(中+ 1)** 。
    *   否则，将**高**更新为**(中-1)**。
*   完成上述步骤后，打印存储的最大长度值。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Stores the segment tree node values
int seg[10000];

// Function to find maximum element
// in the given range
int getMax(int b[], int ss, int se, int qs,
           int qe, int index)
{

    // If the query is out of bounds
    if (se < qs || ss > qe)
        return INT_MIN / 2;

    // If the segment is completely
    // inside the query range
    if (ss >= qs && se <= qe)
        return seg[index];

    // Calculate the mid
    int mid = ss + (se - ss) / 2;

    // Return maximum in left & right
    // of the segment tree recursively
    return max(
        getMax(b, ss, mid, qs,
               qe, 2 * index + 1),
        getMax(b, mid + 1, se,
               qs, qe, 2 * index + 2));
}

// Function to check if it is possible
// to have such a subarray of length K
bool possible(int a[], int b[], int n,
              int c, int k)
{
    int sum = 0;

    // Check for first window of size K
    for(int i = 0; i < k; i++)
    {
        sum += a[i];
    }

    // Calculate the total cost and
    // check if less than equal to c
    int total_cost = sum * k + getMax(
                     b, 0, n - 1,
                        0, k - 1, 0);

    // If it satisfy the condition
    if (total_cost <= c)
        return true;

    // Find the sum of current subarray
    // and calculate total cost
    for(int i = k; i < n; i++)
    {

        // Include the new element
        // of current subarray
        sum += a[i];

        // Discard the element
        // of last subarray
        sum -= a[i - k];

        // Calculate total cost
        // and check <=c
        total_cost = sum * k + getMax(
                     b, 0, n - 1,
                       i - k + 1, i, 0);

        // If possible, then
        // return true
        if (total_cost <= c)
            return true;
    }

    // If it is not possible
    return false;
}

// Function to find maximum length
// of subarray such that sum of
// maximum element in subarray in brr[] and
// sum of subarray in arr[] * K is at most C
int maxLength(int a[], int b[], int n, int c)
{

    // Base Case
    if (n == 0)
        return 0;

    // Let maximum length be 0
    int max_length = 0;

    int low = 0, high = n;

    // Perform Binary search
    while (low <= high)
    {

        // Find mid value
        int mid = low + (high - low) / 2;

        // Check if the current mid
        // satisfy the given condition
        if (possible(a, b, n, c, mid) != false)
        {

            // If yes, then store length
            max_length = mid;
            low = mid + 1;
        }

        // Otherwise
        else
            high = mid - 1;
    }

    // Return maximum length stored
    return max_length;
}

// Function that builds segment Tree
void build(int b[], int index, int s, int e)
{

    // If there is only one element
    if (s == e)
    {
        seg[index] = b[s];
        return;
    }

    // Find the value of mid
    int mid = s + (e - s) / 2;

    // Build left and right parts
    // of segment tree recursively
    build(b, 2 * index + 1, s, mid);
    build(b, 2 * index + 2, mid + 1, e);

    // Update the value at current
    // index
    seg[index] = max(
        seg[2 * index + 1],
        seg[2 * index + 2]);
}

// Function that initializes the
// segment Tree
void initialiseSegmentTree(int N)
{
    int seg[4 * N];
}

// Driver Code
int main()
{
    int A[] = { 1, 2, 1, 6, 5, 5, 6, 1 };
    int B[] = { 14, 8, 15, 15, 9, 10, 7, 12 };

    int C = 40;

    int N = sizeof(A) / sizeof(A[0]);

    // Initialize and Build the
    // Segment Tree
    initialiseSegmentTree(N);
    build(B, 0, 0, N - 1);

    // Function Call
    cout << (maxLength(A, B, N, C));
}

// This code is contributed by susmitakundugoaldanga
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;
class GFG {

    // Stores the segment tree node values
    static int seg[];

    // Function to find maximum length
    // of subarray such that sum of
    // maximum element in subarray in brr[] and
    // sum of subarray in arr[] * K is at most C
    public static int maxLength(
        int a[], int b[], int n, int c)
    {
        // Base Case
        if (n == 0)
            return 0;

        // Let maximum length be 0
        int max_length = 0;

        int low = 0, high = n;

        // Perform Binary search
        while (low <= high) {

            // Find mid value
            int mid = low + (high - low) / 2;

            // Check if the current mid
            // satisfy the given condition
            if (possible(a, b, n, c, mid)) {

                // If yes, then store length
                max_length = mid;
                low = mid + 1;
            }

            // Otherwise
            else
                high = mid - 1;
        }

        // Return maximum length stored
        return max_length;
    }

    // Function to check if it is possible
    // to have such a subarray of length K
    public static boolean possible(
        int a[], int b[], int n,
        int c, int k)
    {
        int sum = 0;

        // Check for first window of size K
        for (int i = 0; i < k; i++) {
            sum += a[i];
        }

        // Calculate the total cost and
        // check if less than equal to c
        int total_cost
            = sum * k + getMax(b, 0, n - 1,
                               0, k - 1, 0);

        // If it satisfy the condition
        if (total_cost <= c)
            return true;

        // Find the sum of current subarray
        // and calculate total cost
        for (int i = k; i < n; i++) {

            // Include the new element
            // of current subarray
            sum += a[i];

            // Discard the element
            // of last subarray
            sum -= a[i - k];

            // Calculate total cost
            // and check <=c
            total_cost
                = sum * k
                  + getMax(b, 0, n - 1,
                           i - k + 1, i, 0);

            // If possible, then
            // return true
            if (total_cost <= c)
                return true;
        }

        // If it is not possible
        return false;
    }

    // Function that builds segment Tree
    public static void build(
        int b[], int index, int s, int e)
    {
        // If there is only one element
        if (s == e) {
            seg[index] = b[s];
            return;
        }

        // Find the value of mid
        int mid = s + (e - s) / 2;

        // Build left and right parts
        // of segment tree recursively
        build(b, 2 * index + 1, s, mid);
        build(b, 2 * index + 2, mid + 1, e);

        // Update the value at current
        // index
        seg[index] = Math.max(
            seg[2 * index + 1],
            seg[2 * index + 2]);
    }

    // Function to find maximum element
    // in the given range
    public static int getMax(
        int b[], int ss, int se, int qs,
        int qe, int index)
    {
        // If the query is out of bounds
        if (se < qs || ss > qe)
            return Integer.MIN_VALUE / 2;

        // If the segment is completely
        // inside the query range
        if (ss >= qs && se <= qe)
            return seg[index];

        // Calculate the mid
        int mid = ss + (se - ss) / 2;

        // Return maximum in left & right
        // of the segment tree recursively
        return Math.max(
            getMax(b, ss, mid, qs,
                   qe, 2 * index + 1),
            getMax(b, mid + 1, se,
                   qs, qe, 2 * index + 2));
    }

    // Function that initializes the
    // segment Tree
    public static void
    initialiseSegmentTree(int N)
    {
        seg = new int[4 * N];
    }

    // Driver Code
    public static void main(String[] args)
    {
        int A[] = { 1, 2, 1, 6, 5, 5, 6, 1 };
        int B[] = { 14, 8, 15, 15, 9, 10, 7, 12 };

        int C = 40;

        int N = A.length;

        // Initialize and Build the
        // Segment Tree
        initialiseSegmentTree(N);
        build(B, 0, 0, N - 1);

        // Function Call
        System.out.println(maxLength(A, B, N, C));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Stores the segment tree node values
seg = [0 for x in range(10000)]
INT_MIN = int(-10000000)

# Function to find maximum element
# in the given range
def getMax(b, ss, se, qs, qe, index):

    # If the query is out of bounds
    if (se < qs or ss > qe):
        return int(INT_MIN / 2)

    # If the segment is completely
    # inside the query range
    if (ss >= qs and se <= qe):
        return seg[index]

    # Calculate the mid
    mid = int(int(ss) + int((se - ss) / 2))

    # Return maximum in left & right
    # of the segment tree recursively
    return max(getMax(b, ss, mid, qs,
                      qe, 2 * index + 1),
               getMax(b, mid + 1, se, qs,
                      qe, 2 * index + 2))

# Function to check if it is possible
# to have such a subarray of length K
def possible(a,  b, n, c, k):

    sum = int(0)

    # Check for first window of size K
    for i in range(0, k):
        sum += a[i]

    # Calculate the total cost and
    # check if less than equal to c
    total_cost = int(sum * k +
              getMax(b, 0, n - 1,
                        0, k - 1, 0))

    # If it satisfy the condition
    if (total_cost <= c):
        return 1

    # Find the sum of current subarray
    # and calculate total cost
    for i in range (k, n):

        # Include the new element
        # of current subarray
        sum += a[i]

        # Discard the element
        # of last subarray
        sum -= a[i - k]

        # Calculate total cost
        # and check <=c
        total_cost = int(sum * k + getMax(
               b, 0, n - 1,i - k + 1, i, 0))

        # If possible, then
        # return true
        if (total_cost <= c):
            return 1

    # If it is not possible
    return 0

# Function to find maximum length
# of subarray such that sum of
# maximum element in subarray in brr[] and
# sum of subarray in arr[] * K is at most C
def maxLength(a, b, n, c):

    # Base Case
    if (n == 0):
        return 0

    # Let maximum length be 0
    max_length = int(0)

    low = 0
    high = n

    # Perform Binary search
    while (low <= high):

        # Find mid value
        mid = int(low + int((high - low) / 2))

        # Check if the current mid
        # satisfy the given condition
        if (possible(a, b, n, c, mid) != 0):

            # If yes, then store length
            max_length = mid
            low = mid + 1

        # Otherwise
        else:
            high = mid - 1

    # Return maximum length stored
    return max_length

# Function that builds segment Tree
def build(b, index, s, e):

    # If there is only one element
    if (s == e):
        seg[index] = b[s]
        return

    # Find the value of mid
    mid = int(s + int((e - s) / 2))

    # Build left and right parts
    # of segment tree recursively
    build(b, 2 * index + 1, s, mid)
    build(b, 2 * index + 2, mid + 1, e)

    # Update the value at current
    # index
    seg[index] = max(seg[2 * index + 1],
                     seg[2 * index + 2])

#  Driver Code
A = [ 1, 2, 1, 6, 5, 5, 6, 1 ]
B = [ 14, 8, 15, 15, 9, 10, 7, 12 ]    

C = int(40)
N = len(A) 

# Initialize and Build the
# Segment Tree
build(B, 0, 0, N - 1)

# Function Call
print((maxLength(A, B, N, C)))

# This code is contributed by Stream_Cipher
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Stores the segment tree node values
static int[] seg;

// Function to find maximum length
// of subarray such that sum of
// maximum element in subarray in brr[] and
// sum of subarray in arr[] * K is at most C
static int maxLength(int[] a, int[] b,
                     int n, int c)
{

    // Base Case
    if (n == 0)
        return 0;

    // Let maximum length be 0
    int max_length = 0;

    int low = 0, high = n;

    // Perform Binary search
    while (low <= high)
    {

        // Find mid value
        int mid = low + (high - low) / 2;

        // Check if the current mid
        // satisfy the given condition
        if (possible(a, b, n, c, mid))
        {

            // If yes, then store length
            max_length = mid;
            low = mid + 1;
        }

        // Otherwise
        else
            high = mid - 1;
    }

    // Return maximum length stored
    return max_length;
}

// Function to check if it is possible
// to have such a subarray of length K
static bool possible(int[] a, int[] b, int n,
                     int c, int k)
{
    int sum = 0;

    // Check for first window of size K
    for(int i = 0; i < k; i++)
    {
        sum += a[i];
    }

    // Calculate the total cost and
    // check if less than equal to c
    int total_cost = sum * k +
              getMax(b, 0, n - 1,
                        0, k - 1, 0);

    // If it satisfy the condition
    if (total_cost <= c)
        return true;

    // Find the sum of current subarray
    // and calculate total cost
    for(int i = k; i < n; i++)
    {

        // Include the new element
        // of current subarray
        sum += a[i];

        // Discard the element
        // of last subarray
        sum -= a[i - k];

        // Calculate total cost
        // and check <=c
        total_cost = sum * k +
              getMax(b, 0, n - 1,
                       i - k + 1, i, 0);

        // If possible, then
        // return true
        if (total_cost <= c)
            return true;
    }

    // If it is not possible
    return false;
}

// Function that builds segment Tree
static void build(int[] b, int index,
                  int s, int e)
{

    // If there is only one element
    if (s == e)
    {
        seg[index] = b[s];
        return;
    }

    // Find the value of mid
    int mid = s + (e - s) / 2;

    // Build left and right parts
    // of segment tree recursively
    build(b, 2 * index + 1, s, mid);
    build(b, 2 * index + 2, mid + 1, e);

    // Update the value at current
    // index
    seg[index] = Math.Max(
        seg[2 * index + 1],
        seg[2 * index + 2]);
}

// Function to find maximum element
// in the given range
public static int getMax(int[] b, int ss,
                         int se, int qs,
                         int qe, int index)
{

    // If the query is out of bounds
    if (se < qs || ss > qe)
        return Int32.MinValue / 2;

    // If the segment is completely
    // inside the query range
    if (ss >= qs && se <= qe)
        return seg[index];

    // Calculate the mid
    int mid = ss + (se - ss) / 2;

    // Return maximum in left & right
    // of the segment tree recursively
    return Math.Max(
        getMax(b, ss, mid, qs,
               qe, 2 * index + 1),
        getMax(b, mid + 1, se,
               qs, qe, 2 * index + 2));
}

// Function that initializes the
// segment Tree
static void initialiseSegmentTree(int N)
{
    seg = new int[4 * N];
}

// Driver Code   
static void Main()
{
    int[] A = { 1, 2, 1, 6, 5, 5, 6, 1 };
    int[] B = { 14, 8, 15, 15, 9, 10, 7, 12 };

    int C = 40;

    int N = A.Length;

    // Initialize and Build the
    // Segment Tree
    initialiseSegmentTree(N);
    build(B, 0, 0, N - 1);

    // Function Call
    Console.WriteLine(maxLength(A, B, N, C));
}
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>
// javascript program for the above approach
    // Stores the segment tree node values
    var seg;

    // Function to find maximum length
    // of subarray such that sum of
    // maximum element in subarray in brr and
    // sum of subarray in arr * K is at most C
    function maxLength(a , b , n , c) {
        // Base Case
        if (n == 0)
            return 0;

        // Let maximum length be 0
        var max_length = 0;

        var low = 0, high = n;

        // Perform Binary search
        while (low <= high) {

            // Find mid value
            var mid = low + parseInt((high - low) / 2);

            // Check if the current mid
            // satisfy the given condition
            if (possible(a, b, n, c, mid)) {

                // If yes, then store length
                max_length = mid;
                low = mid + 1;
            }

            // Otherwise
            else
                high = mid - 1;
        }

        // Return maximum length stored
        return max_length;
    }

    // Function to check if it is possible
    // to have such a subarray of length K
    function possible(a , b , n , c , k) {
        var sum = 0;

        // Check for first window of size K
        for (i = 0; i < k; i++) {
            sum += a[i];
        }

        // Calculate the total cost and
        // check if less than equal to c
        var total_cost = sum * k + getMax(b, 0, n - 1, 0, k - 1, 0);

        // If it satisfy the condition
        if (total_cost <= c)
            return true;

        // Find the sum of current subarray
        // and calculate total cost
        for (i = k; i < n; i++) {

            // Include the new element
            // of current subarray
            sum += a[i];

            // Discard the element
            // of last subarray
            sum -= a[i - k];

            // Calculate total cost
            // and check <=c
            total_cost = sum * k + getMax(b, 0, n - 1, i - k + 1, i, 0);

            // If possible, then
            // return true
            if (total_cost <= c)
                return true;
        }

        // If it is not possible
        return false;
    }

    // Function that builds segment Tree
    function build(b , index , s , e) {
        // If there is only one element
        if (s == e) {
            seg[index] = b[s];
            return;
        }

        // Find the value of mid
        var mid = s + parseInt((e - s) / 2);

        // Build left and right parts
        // of segment tree recursively
        build(b, 2 * index + 1, s, mid);
        build(b, 2 * index + 2, mid + 1, e);

        // Update the value at current
        // index
        seg[index] = Math.max(seg[2 * index + 1], seg[2 * index + 2]);
    }

    // Function to find maximum element
    // in the given range
    function getMax(b , ss , se , qs , qe , index) {
        // If the query is out of bounds
        if (se < qs || ss > qe)
            return parseInt(Number.MIN_VALUE / 2);

        // If the segment is completely
        // inside the query range
        if (ss >= qs && se <= qe)
            return seg[index];

        // Calculate the mid
        var mid = ss + (se - ss) / 2;

        // Return maximum in left & right
        // of the segment tree recursively
        return Math.max(getMax(b, ss, mid, qs, qe, 2 * index + 1), getMax(b, mid + 1, se, qs, qe, 2 * index + 2));
    }

    // Function that initializes the
    // segment Tree
    function initialiseSegmentTree(N) {
        seg = Array(4 * N).fill(0);
    }

    // Driver Code

        var A = [ 1, 2, 1, 6, 5, 5, 6, 1 ];
        var B = [ 14, 8, 15, 15, 9, 10, 7, 12 ];

        var C = 40;

        var N = A.length;

        // Initialize and Build the
        // Segment Tree
        initialiseSegmentTree(N);
        build(B, 0, 0, N - 1);

        // Function Call
        document.write(maxLength(A, B, N, C));

// This code contributed by aashish1995
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N *(log N)<sup>2</sup>)*
***辅助空间:** O(N)*

**高效方法:**为了优化上述方法，想法是通过使用[单调队列](https://www.geeksforgeeks.org/design-a-queue-data-structure-to-get-minimum-or-maximum-in-o1-time/)来使用[德奎](https://www.geeksforgeeks.org/deque-set-1-introduction-applications/)，使得对于固定长度的每个子阵列，我们可以在 O(1)时间内找到最大值。对于[i，I+K–1]范围内的任何子阵列，要计算的值表达式由下式给出:

> ![max(B[i, i + K - 1]) + (\sum_{j = i}^{j = i + K - 1}arr[j])*K ](img/be038e5415a620bdb11122f5413ed925.png "Rendered by QuickLaTeX.com")

以下是步骤:

*   在范围**【0，N】**内执行二分搜索法运算，以找到子阵列的最大可能尺寸。
    *   将**低电平**初始化为 **0** ，将**高电平**初始化为 **N** 。
    *   求**中间**的值为**(低+高)/2** 。
    *   检查是否有可能将子阵列的最大尺寸设为**中间**或者不设为:
        *   使用**德格**到[找到数组**brr【】**中大小为 K](https://www.geeksforgeeks.org/sliding-window-maximum-maximum-of-all-subarrays-of-size-k/) 的每个子数组中的最大元素。
        *   求表达式的值，如果最多 **C** ，则脱离这个条件。
        *   否则检查所有可能的子阵列大小**中间**和表达式的值，如果它最多 **C** 那么打破这个条件。
        *   如果以上条件都不满足，则返回 false。
    *   如果当前**中间**满足给定条件，则将最大长度更新为**中间**，将**低**更新为**(中间+ 1)** 。
    *   否则更新**高**为**(中-1)**。
*   完成上述步骤后，打印存储的最大长度值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible
// to have such a subarray of length K
bool possible(int a[], int b[], int n, int c,
                        int k)
{

    // Finds the maximum element
    // in each window of size k
    deque <int> dq;

    // Check for window of size K
    int sum = 0;

    // For all possible subarrays of
    // length k
    for (int i = 0; i < k; i++)
    {
        sum += a[i];

        // Until deque is empty
        while (dq.size() > 0 && b[i] > b[dq.back()])
            dq.pop_back();
        dq.push_back(i);
    }

    // Calculate the total cost and
    // check if less than equal to c
    int total_cost = sum * k + b[dq.front()];
    if (total_cost <= c)
        return true;

    // Find sum of current subarray
    // and the total cost
    for (int i = k; i < n; i++)
    {

        // Include the new element
        // of current subarray
        sum += a[i];

        // Discard the element
        // of last subarray
        sum -= a[i - k];

        // Remove all the elements
        // in the old window
        while (dq.size() > 0 && dq.front() <= i - k)
            dq.pop_front();
        while (dq.size() > 0 && b[i] > b[dq.back()])
            dq.pop_back();     
        dq.push_back(i);

        // Calculate total cost
        // and check <=c
        total_cost = sum * k + b[dq.front()];

        // If current subarray
        // length satisfies
        if (total_cost <= c)
            return true;
    }

    // If it is not possible
    return false;
}

// Function to find maximum length
// of subarray such that sum of
// maximum element in subarray in brr[] and
// sum of subarray in arr[] * K is at most C
int maxLength(int a[], int b[], int n, int c)
{

    // Base Case
    if (n == 0)
        return 0;

    // Let maximum length be 0
    int max_length = 0;
    int low = 0, high = n;

    // Perform Binary search
    while (low <= high)
    {

        // Find mid value
        int mid = low + (high - low) / 2;

        // Check if the current mid
        // satisfy the given condition
        if (possible(a, b, n, c, mid))
        {

            // If yes, then store length
            max_length = mid;
            low = mid + 1;
        }

        // Otherwise
        else
            high = mid - 1;
    }

    // Return maximum length stored
    return max_length;
}

// Driver Code
int main()
{

    int A[] = { 1, 2, 1, 6, 5, 5, 6, 1 };
    int B[] = { 14, 8, 15, 15, 9, 10, 7, 12 };
    int N = sizeof(A)/sizeof(A[0]);
    int C = 40;
    cout << maxLength(A, B, N, C);
    return 0;
}

// This code is contributed by Dharanendra L V
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;
class GFG {

    // Function to find maximum length
    // of subarray such that sum of
    // maximum element in subarray in brr[] and
    // sum of subarray in arr[] * K is at most C
    public static int maxLength(
        int a[], int b[], int n, int c)
    {
        // Base Case
        if (n == 0)
            return 0;

        // Let maximum length be 0
        int max_length = 0;

        int low = 0, high = n;

        // Perform Binary search
        while (low <= high) {

            // Find mid value
            int mid = low + (high - low) / 2;

            // Check if the current mid
            // satisfy the given condition
            if (possible(a, b, n, c, mid)) {

                // If yes, then store length
                max_length = mid;
                low = mid + 1;
            }

            // Otherwise
            else
                high = mid - 1;
        }

        // Return maximum length stored
        return max_length;
    }

    // Function to check if it is possible
    // to have such a subarray of length K
    public static boolean possible(
        int a[], int b[], int n, int c, int k)
    {

        // Finds the maximum element
        // in each window of size k
        Deque<Integer> dq
            = new LinkedList<Integer>();

        // Check for window of size K
        int sum = 0;

        // For all possible subarrays of
        // length k
        for (int i = 0; i < k; i++) {

            sum += a[i];

            // Until deque is empty
            while (dq.size() > 0
                   && b[i] > b[dq.peekLast()])
                dq.pollLast();
            dq.addLast(i);
        }

        // Calculate the total cost and
        // check if less than equal to c
        int total_cost = sum * k
                         + b[dq.peekFirst()];
        if (total_cost <= c)
            return true;

        // Find sum of current subarray
        // and the total cost
        for (int i = k; i < n; i++) {

            // Include the new element
            // of current subarray
            sum += a[i];

            // Discard the element
            // of last subarray
            sum -= a[i - k];

            // Remove all the elements
            // in the old window
            while (dq.size() > 0
                   && dq.peekFirst()
                          <= i - k)
                dq.pollFirst();

            while (dq.size() > 0
                   && b[i]
                          > b[dq.peekLast()])
                dq.pollLast();

            dq.add(i);

            // Calculate total cost
            // and check <=c
            total_cost = sum * k
                         + b[dq.peekFirst()];

            // If current subarray
            // length satisfies
            if (total_cost <= c)
                return true;
        }

        // If it is not possible
        return false;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int A[] = { 1, 2, 1, 6, 5, 5, 6, 1 };
        int B[] = { 14, 8, 15, 15, 9, 10, 7, 12 };

        int N = A.length;

        int C = 40;

        System.out.println(
            maxLength(A, B, N, C));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find maximum length
# of subarray such that sum of
# maximum element in subarray in brr[] and
# sum of subarray in []arr * K is at most C
def maxLength(a, b, n, c):

    # Base Case
    if(n == 0):
        return 0

    # Let maximum length be 0
    max_length = 0
    low = 0
    high = n

    # Perform Binary search
    while(low <= high):

        # Find mid value
        mid = int(low + (high - low) / 2)

        # Check if the current mid
        # satisfy the given condition
        if(possible(a, b, n, c, mid)):

            # If yes, then store length
            max_length = mid
            low = mid + 1

        # Otherwise
        else:
            high = mid - 1

    # Return maximum length stored
    return max_length

# Function to check if it is possible
# to have such a subarray of length K
def possible(a, b, n, c, k):

    # Finds the maximum element
    # in each window of size k
    dq = []

    # Check for window of size K
    Sum = 0

    # For all possible subarrays of
    # length k
    for i in range(k):
        Sum += a[i]

        # Until deque is empty
        while(len(dq) > 0 and b[i] > b[dq[len(dq) - 1]]):
            dq.pop(len(dq) - 1)
        dq.append(i)

    # Calculate the total cost and
    # check if less than equal to c
    total_cost = Sum * k + b[dq[0]]
    if(total_cost <= c):
        return True

    # Find sum of current subarray
    # and the total cost
    for i in range(k, n):

        # Include the new element
        # of current subarray
        Sum += a[i]

        # Discard the element
        # of last subarray
        Sum -= a[i - k]

        # Remove all the elements
        # in the old window
        while(len(dq) > 0 and dq[0] <= i - k):
            dq.pop(0)
        while(len(dq) > 0 and b[i] > b[dq[len(dq) - 1]]):
            dq.pop(len(dq) - 1)
        dq.append(i)

        # Calculate total cost
        # and check <=c
        total_cost = Sum * k + b[dq[0]]

        # If current subarray
        # length satisfies
        if(total_cost <= c):
            return True

    # If it is not possible
    return False

# Driver Code
A = [1, 2, 1, 6, 5, 5, 6, 1]
B = [14, 8, 15, 15, 9, 10, 7, 12]
N = len(A)
C = 40
print(maxLength(A, B, N, C))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG {

    // Function to find maximum length
    // of subarray such that sum of
    // maximum element in subarray in brr[] and
    // sum of subarray in []arr * K is at most C
    public static int maxLength(
        int []a, int []b, int n, int c)
    {
        // Base Case
        if (n == 0)
            return 0;

        // Let maximum length be 0
        int max_length = 0;

        int low = 0, high = n;

        // Perform Binary search
        while (low <= high) {

            // Find mid value
            int mid = low + (high - low) / 2;

            // Check if the current mid
            // satisfy the given condition
            if (possible(a, b, n, c, mid)) {

                // If yes, then store length
                max_length = mid;
                low = mid + 1;
            }

            // Otherwise
            else
                high = mid - 1;
        }

        // Return maximum length stored
        return max_length;
    }

    // Function to check if it is possible
    // to have such a subarray of length K
    public static bool possible(
        int []a, int []b, int n, int c, int k)
    {

        // Finds the maximum element
        // in each window of size k
        List<int> dq
            = new List<int>();

        // Check for window of size K
        int sum = 0;

        // For all possible subarrays of
        // length k
        for (int i = 0; i < k; i++) {

            sum += a[i];

            // Until deque is empty
            while (dq.Count > 0
                   && b[i] > b[dq[dq.Count - 1]])
                dq.RemoveAt(dq.Count - 1);
            dq.Add(i);
        }

        // Calculate the total cost and
        // check if less than equal to c
        int total_cost = sum * k
                         + b[dq[0]];
        if (total_cost <= c)
            return true;

        // Find sum of current subarray
        // and the total cost
        for (int i = k; i < n; i++) {

            // Include the new element
            // of current subarray
            sum += a[i];

            // Discard the element
            // of last subarray
            sum -= a[i - k];

            // Remove all the elements
            // in the old window
            while (dq.Count > 0
                   && dq[0]
                          <= i - k)
                dq.RemoveAt(0);

            while (dq.Count > 0
                   && b[i]
                          > b[dq[dq.Count - 1]])
                dq.RemoveAt(dq.Count - 1);

            dq.Add(i);

            // Calculate total cost
            // and check <=c
            total_cost = sum * k
                         + b[dq[0]];

            // If current subarray
            // length satisfies
            if (total_cost <= c)
                return true;
        }

        // If it is not possible
        return false;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int []A = { 1, 2, 1, 6, 5, 5, 6, 1 };
        int []B = { 14, 8, 15, 15, 9, 10, 7, 12 };

        int N = A.Length;

        int C = 40;

        Console.WriteLine(
            maxLength(A, B, N, C));
    }
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to check if it is possible
    // to have such a subarray of length K
    function possible(a, b, n, c, k)
    {

        // Finds the maximum element
        // in each window of size k
        let dq = [];

        // Check for window of size K
        let sum = 0;

        // For all possible subarrays of
        // length k
        for (let i = 0; i < k; i++)
        {
            sum += a[i];

            // Until deque is empty
            while (dq.length > 0 && b[i] > b[dq[dq.length - 1]])
                dq.pop();
            dq.push(i);
        }

        // Calculate the total cost and
        // check if less than equal to c
        let total_cost = sum * k + b[dq[0]];
        if (total_cost <= c)
            return true;

        // Find sum of current subarray
        // and the total cost
        for (let i = k; i < n; i++)
        {

            // Include the new element
            // of current subarray
            sum += a[i];

            // Discard the element
            // of last subarray
            sum -= a[i - k];

            // Remove all the elements
            // in the old window
            while (dq.length > 0 && dq[0] <= i - k)
                dq.pop();
            while (dq.length > 0 && b[i] > b[dq[dq.length - 1]])
                dq.pop();    
            dq.push(i);

            // Calculate total cost
            // and check <=c
            total_cost = sum * k + b[dq[0]];

            // If current subarray
            // length satisfies
            if (total_cost <= c)
                return true;
        }

        // If it is not possible
        return false;
    }

    // Function to find maximum length
    // of subarray such that sum of
    // maximum element in subarray in brr[] and
    // sum of subarray in arr[] * K is at most C
    function maxLength(a, b, n, c)
    {

        // Base Case
        if (n == 0)
            return 0;

        // Let maximum length be 0
        let max_length = 0;
        let low = 0, high = n;

        // Perform Binary search
        while (low <= high)
        {

            // Find mid value
            let mid = low + parseInt((high - low) / 2, 10);

            // Check if the current mid
            // satisfy the given condition
            if (possible(a, b, n, c, mid))
            {

                // If yes, then store length
                max_length = mid;
                low = mid + 1;
            }

            // Otherwise
            else
                high = mid - 1;
        }

        // Return maximum length stored
        return max_length;
    }

    let A = [ 1, 2, 1, 6, 5, 5, 6, 1 ];
    let B = [ 14, 8, 15, 15, 9, 10, 7, 12 ];
    let N = A.length;
    let C = 40;
    document.write(maxLength(A, B, N, C));

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*