# 重新排列一个给定数组使其等于另一个给定数组所需的最小成本

> 原文:[https://www . geeksforgeeks . org/重新排列给定数组以使其等于另一个给定数组所需的最小成本/](https://www.geeksforgeeks.org/minimum-cost-required-to-rearrange-a-given-array-to-make-it-equal-to-another-given-array/)

给定两个分别由 **N** 和 **M** 整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**A【】**和**B【】**，以及一个整数 **C** ，任务是通过对数组**A【】**执行以下操作，找到使序列 **A** 与 **B** 完全相同(仅由不同的元素组成)所需的最小成本:

*   从数组中移除任何成本为 **0** 的元素。
*   在数组的任何地方插入一个新的元素，代价为 **C** 。

**示例:**

> **输入:** A[] = {1，6，3，5，10}，B[] = {3，1，5}，C = 2
> **输出:** 2
> **解释:**
> 从数组中移除元素 1，6 和 10 的成本为 0。数组 A[]变成{3，5}。
> 在 3 和 5 之间加 1，数组 arr[]变成{3，1，5}，和数组 B[]一样。
> 以上操作费用为 2。
> 
> **输入:** A[] = {10，5，2，4，10，5}，B[] = {5，1，2，10，4}，C = 3
> **输出:** 6
> **解释:**
> 从数组中移除元素 10，10 和 5 的成本为 0。数组 A[]变成{5，2，4}。
> 在数组中添加元素 1 和 10 作为{5，1，2，10，4}，与数组 B[]相同。
> 以上操作成本为 3*2 = 6。

**天真方法:**最简单的方法是通过使用两个 for 循环来擦除数组 **A[]** 中不存在于数组 **B[]** 中的所有元素。之后[生成数组](https://www.geeksforgeeks.org/heaps-algorithm-for-generating-permutations/)中剩余元素的所有排列，并针对每个序列检查最小成本，使得数组 **A[]** 与数组 **B[]** 相同。打印相同的最低成本。

***时间复杂度:** O(N！*N*M)，其中 N 是数组 A[]的大小，M 是数组 B[]的大小。*
***辅助空间:** O(1)*

**高效法:**对上述方法进行优化，思路是先求出数组 **A[]** 和 **B[]** 的[最长公共子序列](https://www.geeksforgeeks.org/longest-common-subsequence-dp-4/)的长度，再从数组 **B[]** 的大小中减去，得到数组 **A[]** 中需要添加的元素个数。每增加一个新元素，成本中增加 **C** 的金额。因此，总成本由下式给出:

> 成本= C *(N–LCS(A，B))
> 其中，
> LCS 是数组 A[]和 B[]中最长的公共子序列，
> N 是数组 A[]的长度，
> C 是数组 B[]中每个元素相加的成本。

按照以下步骤解决问题:

*   创建一个新数组，比如说**索引[]** ，并用 **-1** 和一个数组 **nums[]** 初始化它。
*   将数组 **B[]** 的每个元素映射到数组**索引[]** 中对应的索引。
*   [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**A[]【T3]，并将值及其映射值(即索引号)插入数组 **nums[]** 数组，如果索引号不是 **-1** 。**
*   现在求数组的[最长递增子序列](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/) **nums[]** 得到两个给定数组的最长公共子序列的长度。
*   在以上步骤中找到 LCS 之后，使用上面讨论的公式找到成本值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find length of the
// longest common subsequence
int findLCS(int* nums, int N)
{
    int k = 0;
    for (int i = 0; i < N; i++) {

        // Find position where element
        // is to be inserted
        int pos = lower_bound(nums, nums + k,
                              nums[i])
                  - nums;
        nums[pos] = nums[i];
        if (k == pos) {
            k = pos + 1;
        }
    }

    // Return the length of LCS
    return k;
}

// Function to find the minimum cost
// required to convert the sequence A
// exactly same as B
int minimumCost(int* A, int* B, int M,
                int N, int C)
{
    // Auxiliary array
    int nums[1000000];

    // Stores positions of elements of A[]
    int index[1000000];

    // Initialize index array with -1
    memset(index, -1, sizeof(index));

    for (int i = 0; i < N; i++) {

        // Update the index array with
        // index of corresponding
        // elements of B
        index[B[i]] = i;
    }

    int k = 0;

    for (int i = 0; i < M; i++) {

        // Place only A's array values
        // with its mapped values
        // into nums array
        if (index[A[i]] != -1) {
            nums[k++] = index[A[i]];
        }
    }

    // Find LCS
    int lcs_length = findLCS(nums, k);

    // No of elements to be added
    // in array A[]
    int elements_to_be_added
        = N - lcs_length;

    // Stores minimum cost
    int min_cost
        = elements_to_be_added * C;

    // Print the minimum cost
    cout << min_cost;
}

// Driver Code
int main()
{
    // Given array A[]
    int A[] = { 1, 6, 3, 5, 10 };
    int B[] = { 3, 1, 5 };

    // Given C
    int C = 2;

    // Size of arr A
    int M = sizeof(A) / sizeof(A[0]);

    // Size of arr B
    int N = sizeof(B) / sizeof(B[0]);

    // Function Call
    minimumCost(A, B, M, N, C);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find lower_bound
static int LowerBound(int a[], int k,
                      int x)
{
    int l = -1;
    int r = k;

    while (l + 1 < r)
    {
        int m = (l + r) >>> 1;
        if (a[m] >= x)
        {
            r = m;
        }
        else
        {
            l = m;
        }
    }
    return r;
}

// Function to find length of the
// longest common subsequence
static int findLCS(int[] nums, int N)
{
    int k = 0;
    for(int i = 0; i < N; i++)
    {

        // Find position where element
        // is to be inserted
        int pos = LowerBound(nums, k,
                             nums[i]);
        nums[pos] = nums[i];
        if (k == pos)
        {
            k = pos + 1;
        }
    }

    // Return the length of LCS
    return k;
}

// Function to find the minimum cost
// required to convert the sequence A
// exactly same as B
static int  minimumCost(int[] A, int[] B,
                        int M, int N, int C)
{

    // Auxiliary array
    int[] nums = new int[100000];

    // Stores positions of elements of A[]
    int[] index = new int[100000];

    // Initialize index array with -1
    for(int i = 0; i < 100000; i++)
        index[i] = -1;

    for(int i = 0; i < N; i++)
    {

        // Update the index array with
        // index of corresponding
        // elements of B
        index[B[i]] = i;
    }

    int k = 0;

    for(int i = 0; i < M; i++)
    {

        // Place only A's array values
        // with its mapped values
        // into nums array
        if (index[A[i]] != -1)
        {
            nums[k++] = index[A[i]];
        }
    }

    // Find LCS
    int lcs_length = findLCS(nums, k);

    // No of elements to be added
    // in array A[]
    int elements_to_be_added = N - lcs_length;

    // Stores minimum cost
    int min_cost = elements_to_be_added * C;

    // Print the minimum cost
    System.out.println( min_cost);
    return 0;
}

// Driver code
public static void main(String[] args)
{

    // Given array A[]
    int[] A = { 1, 6, 3, 5, 10 };
    int[] B = { 3, 1, 5 };

    // Given C
    int C = 2;

    // Size of arr A
    int M = A.length;

    // Size of arr B
    int N = B.length;

    // Function call
    minimumCost(A, B, M, N, C);
}
}

// This code is contributed by sallagondaavinashreddy7
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find lower_bound
def LowerBound(a, k, x):

    l = -1
    r = k

    while (l + 1 < r):
        m = (l + r) >> 1

        if (a[m] >= x):
            r = m
        else:
            l = m

    return r

# Function to find length of the
# longest common subsequence
def findLCS(nums, N):

    k = 0
    for i in range(N):

        # Find position where element
        # is to be inserted
        pos = LowerBound(nums, k, nums[i])
        nums[pos] = nums[i]

        if (k == pos):
            k = pos + 1

    # Return the length of LCS
    return k

# Function to find the minimum cost
# required to convert the sequence A
# exactly same as B
def  minimumCost(A, B, M, N, C):

    # Auxiliary array
    nums = [0] * 100000

    # Stores positions of elements of A[]
    # Initialize index array with -1
    index = [-1] * 100000

    for i in range(N):

        # Update the index array with
        # index of corresponding
        # elements of B
        index[B[i]] = i

    k = 0

    for i in range(M):

        # Place only A's array values
        # with its mapped values
        # into nums array
        if (index[A[i]] != -1):
            k += 1
            nums[k] = index[A[i]]

    # Find LCS
    lcs_length = findLCS(nums, k)

    # No of elements to be added
    # in array A[]
    elements_to_be_added = N - lcs_length

    # Stores minimum cost
    min_cost = elements_to_be_added * C

    # Print the minimum cost
    print( min_cost)

# Driver Code

# Given array A[]
A = [ 1, 6, 3, 5, 10 ]
B = [ 3, 1, 5 ]

# Given C
C = 2

# Size of arr A
M = len(A)

# Size of arr B
N = len(B)

# Function call
minimumCost(A, B, M, N, C)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find lower_bound
static int LowerBound(int[] a, int k,
                      int x)
{
    int l = -1;
    int r = k;

    while (l + 1 < r)
    {
        int m = (l + r) >> 1;
        if (a[m] >= x)
        {
            r = m;
        }
        else
        {
            l = m;
        }
    }
    return r;
}

// Function to find length of the
// longest common subsequence
static int findLCS(int[] nums, int N)
{
    int k = 0;

    for(int i = 0; i < N; i++)
    {

        // Find position where element
        // is to be inserted
        int pos = LowerBound(nums, k,
                             nums[i]);
        nums[pos] = nums[i];

        if (k == pos)
        {
            k = pos + 1;
        }
    }

    // Return the length of LCS
    return k;
}

// Function to find the minimum cost
// required to convert the sequence A
// exactly same as B
static int  minimumCost(int[] A, int[] B,
                        int M, int N, int C)
{

    // Auxiliary array
    int[] nums = new int[100000];

    // Stores positions of elements of A[]
    int[] index = new int[100000];

    // Initialize index array with -1
    for(int i = 0; i < 100000; i++)
        index[i] = -1;

    for(int i = 0; i < N; i++)
    {

        // Update the index array with
        // index of corresponding
        // elements of B
        index[B[i]] = i;
    }

    int k = 0;

    for(int i = 0; i < M; i++)
    {

        // Place only A's array values
        // with its mapped values
        // into nums array
        if (index[A[i]] != -1)
        {
            nums[k++] = index[A[i]];
        }
    }

    // Find LCS
    int lcs_length = findLCS(nums, k);

    // No of elements to be added
    // in array A[]
    int elements_to_be_added = N - lcs_length;

    // Stores minimum cost
    int min_cost = elements_to_be_added * C;

    // Print the minimum cost
    Console.WriteLine(min_cost);
    return 0;
}

// Driver code
public static void Main()
{

    // Given array A[]
    int[] A = { 1, 6, 3, 5, 10 };
    int[] B = { 3, 1, 5 };

    // Given C
    int C = 2;

    // Size of arr A
    int M = A.Length;

    // Size of arr B
    int N = B.Length;

    // Function call
    minimumCost(A, B, M, N, C);
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Function to find lower_bound
    function LowerBound(a , k , x) {
        var l = -1;
        var r = k;

        while (l + 1 < r) {
            var m = (l + r) >>> 1;
            if (a[m] >= x) {
                r = m;
            } else {
                l = m;
            }
        }
        return r;
    }

    // Function to find length of the
    // longest common subsequence
    function findLCS(nums , N) {
        var k = 0;
        for (i = 0; i < N; i++) {

            // Find position where element
            // is to be inserted
            var pos = LowerBound(nums, k, nums[i]);
            nums[pos] = nums[i];
            if (k == pos) {
                k = pos + 1;
            }
        }

        // Return the length of LCS
        return k;
    }

    // Function to find the minimum cost
    // required to convert the sequence A
    // exactly same as B
    function minimumCost(A,  B , M , N , C) {

        // Auxiliary array
        var nums = Array(100000).fill(0);

        // Stores positions of elements of A
        var index = Array(100000).fill(0);

        // Initialize index array with -1
        for (i = 0; i < 100000; i++)
            index[i] = -1;

        for (i = 0; i < N; i++) {

            // Update the index array with
            // index of corresponding
            // elements of B
            index[B[i]] = i;
        }

        var k = 0;

        for (i = 0; i < M; i++) {

            // Place only A's array values
            // with its mapped values
            // into nums array
            if (index[A[i]] != -1) {
                nums[k++] = index[A[i]];
            }
        }

        // Find LCS
        var lcs_length = findLCS(nums, k);

        // No of elements to be added
        // in array A
        var elements_to_be_added = N - lcs_length;

        // Stores minimum cost
        var min_cost = elements_to_be_added * C;

        // Print the minimum cost
        document.write(min_cost);
        return 0;
    }

    // Driver code

        // Given array A
        var A = [ 1, 6, 3, 5, 10 ];
        var B = [ 3, 1, 5 ];

        // Given C
        var C = 2;

        // Size of arr A
        var M = A.length;

        // Size of arr B
        var N = B.length;

        // Function call
        minimumCost(A, B, M, N, C);

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N * Log N)*
***辅助空间:** O(N)*