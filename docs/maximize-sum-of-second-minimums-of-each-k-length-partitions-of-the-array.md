# 最大化数组中每 K 个长度分区的第二最小值之和

> 原文:[https://www . geeksforgeeks . org/最大化每 k 个长度数组分区的秒总和最小值/](https://www.geeksforgeeks.org/maximize-sum-of-second-minimums-of-each-k-length-partitions-of-the-array/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**A【】**和一个正整数 **K** (它将始终是 **N** 的一个因子)，任务是通过将数组划分为大小相等的 **(N / K)** 个分区来找到数组每个分区的次小元素的最大可能和。

**示例:**

> **输入:** A[] = {2，3，1，4，7，5，6，1}，K = 4
> **输出:** 7
> **说明:**将数组拆分为{1，2，3，4}和{1，5，6，7}。因此，总和= 2 + 5 = 7，这是最大可能总和。
> 
> **输入:** A[] = {12，43，15，32，45，23}，K = 3
> **输出:** 66
> **说明:**将数组拆分为{12，23，32}和{15，43，45}。因此，总和= 23 + 43 = 66，这是最大可能总和。

**方法:**思路是[按照升序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)给定数组排序，为了最大化所需的和，将**A【】**的第一个 **N / K** 元素划分到每个数组中作为第一项，然后从 **N/K** 开始选择**A【】**的每一个**(K–1)<sup>第</sup>个**元素。

按照以下步骤解决问题:

*   [按递增顺序对数组 **A[]** 进行排序。](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)
*   用 **0** 初始化**总和**以存储所需的总和。
*   现在，用 **N / K** 初始化一个变量 **i** 。
*   当 **i** 小于 **N** 时，执行以下步骤:
    *   用**A【I】**增加**和**。
    *   将 **i** 增加**K–1**。
*   遍历后，打印**和**作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of
// second smallest of each partition
// of size K
void findSum(int A[], int N, int K)
{

    // Sort the array A[]
    // in ascending order
    sort(A, A + N);

    // Store the maximum sum of second
    // smallest of each partition
    // of size K
    int sum = 0;

    // Select every (K-1)th element as
    // second smallest element
    for (int i = N / K; i < N; i += K - 1) {

        // Update sum
        sum += A[i];
    }

    // Print the maximum sum
    cout << sum;
}

// Driver Code
int main()
{

    // Given size of partitions
    int K = 4;

    // Given array A[]
    int A[] = { 2, 3, 1, 4, 7, 5, 6, 1 };

    // Size of the given array
    int N = sizeof(A) / sizeof(A[0]);

    // Function Call
    findSum(A, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the maximum sum of
// second smallest of each partition
// of size K
static void findSum(int A[], int N, int K)
{

    // Sort the array A[]
    // in ascending order
    Arrays.sort(A);

    // Store the maximum sum of second
    // smallest of each partition
    // of size K
    int sum = 0;

    // Select every (K-1)th element as
    // second smallest element
    for(int i = N / K; i < N; i += K - 1)
    {

        // Update sum
        sum += A[i];
    }

    // Print the maximum sum
    System.out.print(sum);
}

// Driver Code
public static void main(String[] args)
{

    // Given size of partitions
    int K = 4;

    // Given array A[]
    int A[] = { 2, 3, 1, 4, 7, 5, 6, 1 };

    // Size of the given array
    int N = A.length;

    // Function Call
    findSum(A, N, K);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum sum of
# second smallest of each partition
# of size K
def findSum(A, N, K):

    # Sort the array A
    # in ascending order
    A.sort();

    # Store the maximum sum of second
    # smallest of each partition
    # of size K
    sum = 0;

    # Select every (K-1)th element as
    # second smallest element
    for i in range(N // K, N, K - 1):

        # Update sum
        sum += A[i];

    # Print the maximum sum
    print(sum);

# Driver Code
if __name__ == '__main__':

    # Given size of partitions
    K = 4;

    # Given array A
    A = [2, 3, 1, 4, 7, 5, 6, 1];

    # Size of the given array
    N = len(A);

    # Function Call
    findSum(A, N, K);

    # This code contributed by shikhasingrajput
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum sum of
// second smallest of each partition
// of size K
static void findSum(int []A, int N, int K)
{

    // Sort the array []A
    // in ascending order
    Array.Sort(A);

    // Store the maximum sum of second
    // smallest of each partition
    // of size K
    int sum = 0;

    // Select every (K-1)th element as
    // second smallest element
    for(int i = N / K; i < N; i += K - 1)
    {

        // Update sum
        sum += A[i];
    }

    // Print the maximum sum
    Console.Write(sum);
}

// Driver Code
public static void Main(String[] args)
{

    // Given size of partitions
    int K = 4;

    // Given array []A
    int []A = { 2, 3, 1, 4, 7, 5, 6, 1 };

    // Size of the given array
    int N = A.Length;

    // Function Call
    findSum(A, N, K);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program of the above approach

// Function to find the maximum sum of
// second smallest of each partition
// of size K
function findSum(A, N, K)
{

    // Sort the array A[]
    // in ascending order
    A.sort();

    // Store the maximum sum of second
    // smallest of each partition
    // of size K
    let sum = 0;

    // Select every (K-1)th element as
    // second smallest element
    for(let i = N / K; i < N; i += K - 1)
    {

        // Update sum
        sum += A[i];
    }

    // Print the maximum sum
    document.write(sum);
}

// Driver Code

// Given size of partitions
let K = 4;

// Given array A[]
let A = [ 2, 3, 1, 4, 7, 5, 6, 1 ];

// Size of the given array
let N = A.length;

// Function Call
findSum(A, N, K);

// This code is contributed by chinmoy1997pal

</script>
```

**Output:** 

```
7
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(N)*