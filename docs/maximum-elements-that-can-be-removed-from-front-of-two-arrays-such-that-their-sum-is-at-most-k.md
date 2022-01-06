# 可以从两个数组前面移除的最大元素，使得它们的和最多为 K

> 原文:[https://www . geeksforgeeks . org/从两个数组的前面移除最多的元素，这样它们的总和最多为 k/](https://www.geeksforgeeks.org/maximum-elements-that-can-be-removed-from-front-of-two-arrays-such-that-their-sum-is-at-most-k/)

给定一个整数 **K** 和两个由 **N** 和 **M** 整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **A[]** 和 **B[]** ，任务是根据以下规则最大化可以从任一数组前面移除的元素数量:

*   从阵列 **A[]** 和 **B[]** 的前面移除一个元素，这样被移除元素的值最多只能是**。**
*   **将 **K** 的值减少被移除元素的值。**

****示例:****

> ****输入:** K = 7，A[] = {2，4，7，3}，B[] = {1，9，3，4，5}
> **输出:** 3
> **解释:**
> **操作 1:** 从数组 A[]中选择元素，将 K 减 A[0](=2)，则 K 的值变为=(7–2)= 5。
> **操作 2:** 从数组 B[]中选择元素，将 K 减 B[0](=1)，则 K 的值变为=(5–1)= 4。
> **操作 3:** 从数组 A[]中选择元素，将 K 减 A[1](=4)，则 K 的值变为=(4–4)= 4。
> 上述操作后，不能再去除任何元素。因此，打印 3。**
> 
> ****输入:** K = 9，A[] = {12，10，1，2，3}，B[] = {15，19，3，4，5}
> **输出:** 0**

****方法:**给定的问题可以通过使用[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)和[二分搜索法](https://www.geeksforgeeks.org/binary-search/)在从堆栈 **A** 中取出 **i** 项后，从堆栈 **B** 中找出可能的总项 **j** 并返回结果作为 **(i + j)** 的最大值来解决。按照以下步骤解决给定的问题:**

*   **求[数组的前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) **A[]** 和 **B[]** 。**
*   **初始化一个变量，比如说**把**算成 **0** ，这个变量存储了最多能拿的物品。**
*   **[使用变量 **i** 在范围**【0，N】**内遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)、 **A[]** ，并执行以下步骤:

    *   如果**A【I】**的值大于 **K** ，则[脱离回路](https://www.geeksforgeeks.org/break-statement-cc/)。
    *   将从堆栈 **A** 中取出 **i** 项后的剩余金额存储在变量 **rem** 中，作为**K–A【I】**。
    *   对数组 **B** 执行一次[二分搜索法](https://www.geeksforgeeks.org/binary-search/)，找到最大的项目，比如说 **j** 可以从堆栈 **B** 中取出 **rem** 数量(从堆栈 **A** 中取出 **i** 元素之后)。
    *   将 **i + j** 的最大值存储在变量**计数**中。** 
*   **完成上述步骤后，打印**计数**的值作为结果。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum number
// of items that can be removed from
// both the arrays
void maxItems(int n, int m, int a[],
              int b[], int K)
{
    // Stores the maximum item count
    int count = 0;

    // Stores the prefix sum of the
    // cost of items
    int A[n + 1];
    int B[m + 1];

    // Insert the item cost 0 at the
    // front of the arrays
    A[0] = 0;
    B[0] = 0;

    // Build the prefix sum for
    // the array A[]
    for (int i = 1; i <= n; i++) {

        // Update the value of A[i]
        A[i] = a[i - 1] + A[i - 1];
    }

    // Build the prefix sum for
    // the array B[]
    for (int i = 1; i <= m; i++) {

        // Update the value of B[i]
        B[i] = b[i - 1] + B[i - 1];
    }

    // Iterate through each item
    // of the array A[]
    for (int i = 0; i <= n; i++) {

        // If A[i] exceeds K
        if (A[i] > K)
            break;

        // Store the remaining amount
        // after taking top i elements
        // from the array A
        int rem = K - A[i];

        // Store the number of items
        // possible to take from the
        // array B[]
        int j = 0;

        // Store low and high bounds
        // for binary search
        int lo = 0, hi = m;

        // Binary search to find
        // number of item that
        // can be taken from stack
        // B in rem amount
        while (lo <= hi) {

            // Calculate the mid value
            int mid = (lo + hi) / 2;
            if (B[mid] <= rem) {

                // Update the value
                // of j and lo
                j = mid;
                lo = mid + 1;
            }
            else {

                // Update the value
                // of the hi
                hi = mid - 1;
            }
        }

        // Store the maximum of total
        // item count
        count = max(j + i, count);
    }

    // Print the result
    cout << count;
}

// Driver Code
int main()
{
    int n = 4, m = 5, K = 7;
    int A[n] = { 2, 4, 7, 3 };
    int B[m] = { 1, 9, 3, 4, 5 };
    maxItems(n, m, A, B, K);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to find the maximum number
// of items that can be removed from
// both the arrays
static void maxItems(int n, int m, int a[],
                     int b[], int K)
{

    // Stores the maximum item count
    int count = 0;

    // Stores the prefix sum of the
    // cost of items
    int A[] = new int[n + 1];
    int B[] = new int[m + 1];

    // Insert the item cost 0 at the
    // front of the arrays
    A[0] = 0;
    B[0] = 0;

    // Build the prefix sum for
    // the array A[]
    for(int i = 1; i <= n; i++)
    {

        // Update the value of A[i]
        A[i] = a[i - 1] + A[i - 1];
    }

    // Build the prefix sum for
    // the array B[]
    for(int i = 1; i <= m; i++)
    {

        // Update the value of B[i]
        B[i] = b[i - 1] + B[i - 1];
    }

    // Iterate through each item
    // of the array A[]
    for(int i = 0; i <= n; i++)
    {

        // If A[i] exceeds K
        if (A[i] > K)
            break;

        // Store the remaining amount
        // after taking top i elements
        // from the array A
        int rem = K - A[i];

        // Store the number of items
        // possible to take from the
        // array B[]
        int j = 0;

        // Store low and high bounds
        // for binary search
        int lo = 0, hi = m;

        // Binary search to find
        // number of item that
        // can be taken from stack
        // B in rem amount
        while (lo <= hi)
        {

            // Calculate the mid value
            int mid = (lo + hi) / 2;
            if (B[mid] <= rem)
            {

                // Update the value
                // of j and lo
                j = mid;
                lo = mid + 1;
            }
            else
            {

                // Update the value
                // of the hi
                hi = mid - 1;
            }
        }

        // Store the maximum of total
        // item count
        count = Math.max(j + i, count);
    }

    // Print the result
    System.out.print(count);
}

// Driver Code
public static void main (String[] args)
{
    int n = 4, m = 5, K = 7;
    int A[] = { 2, 4, 7, 3 };
    int B[] = { 1, 9, 3, 4, 5 };

    maxItems(n, m, A, B, K);
}
}

// This code is contributed by sanjoy_62
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to find the maximum number
# of items that can be removed from
# both the arrays
def maxItems(n, m, a, b, K):

    # Stores the maximum item count
    count = 0

    # Stores the prefix sum of the
    # cost of items
    A = [0 for i in range(n + 1)]
    B = [0 for i in range(m + 1)]

    # Build the prefix sum for
    # the array A[]
    for i in range(1, n + 1, 1):

        # Update the value of A[i]
        A[i] = a[i - 1] + A[i - 1]

    # Build the prefix sum for
    # the array B[]
    for i in range(1, m + 1, 1):

        # Update the value of B[i]
        B[i] = b[i - 1] + B[i - 1]

    # Iterate through each item
    # of the array A[]
    for i in range(n + 1):

        # If A[i] exceeds K
        if (A[i] > K):
            break

        # Store the remaining amount
        # after taking top i elements
        # from the array A
        rem = K - A[i]

        # Store the number of items
        # possible to take from the
        # array B[]
        j = 0

        # Store low and high bounds
        # for binary search
        lo = 0
        hi = m

        # Binary search to find
        # number of item that
        # can be taken from stack
        # B in rem amount
        while (lo <= hi):

            # Calculate the mid value
            mid = (lo + hi) // 2

            if (B[mid] <= rem):

                # Update the value
                # of j and lo
                j = mid
                lo = mid + 1

            else:

                # Update the value
                # of the hi
                hi = mid - 1

        # Store the maximum of total
        # item count
        count = max(j + i, count)

    # Print the result
    print(count)

# Driver Code
if __name__ == '__main__':

    n = 4
    m = 5
    K = 7
    A = [ 2, 4, 7, 3 ]
    B = [ 1, 9, 3, 4, 5 ]

    maxItems(n, m, A, B, K)

# This code is contributed by bgangwar59
```

## **C#**

```
// C# program for the above approach
using System;

class GFG
{   

// Function to find the maximum number
// of items that can be removed from
// both the arrays
static void maxItems(int n, int m, int[] a,
                     int[] b, int K)
{

    // Stores the maximum item count
    int count = 0;

    // Stores the prefix sum of the
    // cost of items
    int[] A = new int[n + 1];
    int[] B= new int[m + 1];

    // Insert the item cost 0 at the
    // front of the arrays
    A[0] = 0;
    B[0] = 0;

    // Build the prefix sum for
    // the array A[]
    for(int i = 1; i <= n; i++)
    {

        // Update the value of A[i]
        A[i] = a[i - 1] + A[i - 1];
    }

    // Build the prefix sum for
    // the array B[]
    for(int i = 1; i <= m; i++)
    {

        // Update the value of B[i]
        B[i] = b[i - 1] + B[i - 1];
    }

    // Iterate through each item
    // of the array A[]
    for(int i = 0; i <= n; i++)
    {

        // If A[i] exceeds K
        if (A[i] > K)
            break;

        // Store the remaining amount
        // after taking top i elements
        // from the array A
        int rem = K - A[i];

        // Store the number of items
        // possible to take from the
        // array B[]
        int j = 0;

        // Store low and high bounds
        // for binary search
        int lo = 0, hi = m;

        // Binary search to find
        // number of item that
        // can be taken from stack
        // B in rem amount
        while (lo <= hi)
        {

            // Calculate the mid value
            int mid = (lo + hi) / 2;
            if (B[mid] <= rem)
            {

                // Update the value
                // of j and lo
                j = mid;
                lo = mid + 1;
            }
            else
            {

                // Update the value
                // of the hi
                hi = mid - 1;
            }
        }

        // Store the maximum of total
        // item count
        count = Math.Max(j + i, count);
    }

    // Print the result
    Console.Write(count);
}

// Driver code
public static void Main(String []args)
{
    int n = 4, m = 5, K = 7;
    int[] A = { 2, 4, 7, 3 };
    int[] B = { 1, 9, 3, 4, 5 };

    maxItems(n, m, A, B, K);

}
}

// This code is contributed by code_hunt.
```

## **java 描述语言**

```
<script>

// javascript program for the above approach

// Function to find the maximum number
// of items that can be removed from
// both the arrays
function maxItems(n, m, a, b, K)
{
    // Stores the maximum item count
    var count = 0;

    // Stores the prefix sum of the
    // cost of items
    var A = new Array(n + 1);
    var B = new Array(m + 1);

    // Insert the item cost 0 at the
    // front of the arrays
    A[0] = 0;
    B[0] = 0;

    var i;
    // Build the prefix sum for
    // the array A[]
    for (i = 1; i <= n; i++) {

        // Update the value of A[i]
        A[i] = a[i - 1] + A[i - 1];
    }

    // Build the prefix sum for
    // the array B[]
    for (i = 1; i <= m; i++) {

        // Update the value of B[i]
        B[i] = b[i - 1] + B[i - 1];
    }

    // Iterate through each item
    // of the array A[]
    for (i = 0; i <= n; i++) {

        // If A[i] exceeds K
        if (A[i] > K)
            break;

        // Store the remaining amount
        // after taking top i elements
        // from the array A
        var rem = K - A[i];

        // Store the number of items
        // possible to take from the
        // array B[]
        var j = 0;

        // Store low and high bounds
        // for binary search
        var lo = 0, hi = m;

        // Binary search to find
        // number of item that
        // can be taken from stack
        // B in rem amount
        while (lo <= hi) {

            // Calculate the mid value
            var mid = parseInt((lo + hi) / 2);
            if (B[mid] <= rem) {

                // Update the value
                // of j and lo
                j = mid;
                lo = mid + 1;
            }
            else {

                // Update the value
                // of the hi
                hi = mid - 1;
            }
        }

        // Store the maximum of total
        // item count
        count = Math.max(j + i, count);
    }

    // Print the result
    document.write(count);
}

// Driver Code
    var n = 4, m = 5, K = 7;
    var A = [2, 4, 7, 3];
    var B = [1, 9, 3, 4, 5];
    maxItems(n, m, A, B, K);

// This code is contributed by SURENDRA_GANGWAR.
</script>
```

****Output:** 

```
3
```** 

*****时间复杂度:** O(N * log(M))*
***辅助空间:** O(N + M)***