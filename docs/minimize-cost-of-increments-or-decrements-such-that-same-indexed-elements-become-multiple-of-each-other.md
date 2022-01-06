# 最小化增量或减量的成本，使得相同的索引元素成为彼此的倍数

> 原文:[https://www . geeksforgeeks . org/最小化增量或减量成本，使得相同的索引元素成为彼此的倍数/](https://www.geeksforgeeks.org/minimize-cost-of-increments-or-decrements-such-that-same-indexed-elements-become-multiple-of-each-other/)

给定两个由 **N** 整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**和**B【】**，任务是通过 **1** 最小化数组元素递增或递减的总成本，使得对于每个 i <sup>第</sup>个元素，**A【I】**是**B【I】**的倍数，反之亦然。

**示例:**

> **输入:** A[] = {3，6，3}，B[] = {4，8，13}
> **输出:** 4
> **解释:**
> 将 A[0]递增 1 (3 + 1 = 4)使其为 B[0](= 4)的倍数。
> 将 A[1]加 2 (6 + 2 = 8)等于 B[1](= 8)的倍数。
> 将 B[2]减 1(13–1 = 12)等于 A[2](= 3)的倍数。
> 因此，总成本= 1 + 2 + 1 = 4。
> 
> **输入:** A[] = {13，2，31，7}，B[] = {6，8，11，3 }
> T3】输出: 4

**进场:**给定的问题可以解决[贪婪的](https://www.geeksforgeeks.org/greedy-algorithms/)。按照以下步骤解决问题:

*   初始化一个变量，比如**成本**，存储所需的最小成本。
*   [同时遍历阵列](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **A[]** 和 **B[]** ，并执行以下步骤:
    *   **案例 1:** 找到更新 **A[i]** 的成本，使其成为 **B[i]** 的倍数，这是 **(B[i] % A[i])** 和**(A[I]–B[I]% A[I])**的最小值。
    *   **案例二:**找到更新 **B[i]** 的成本，使其成为 **A[i]** 的倍数，这是 **(A[i] % B[i])** 和**(B[I]–A[I]% B[I])**的最小值。
    *   对于每个数组元素，将上述两个成本中的最小值添加到变量**成本**中。
*   完成上述步骤后，打印**成本**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum cost to
// make A[i] multiple of B[i] or
// vice-versa for every array element
int MinimumCost(int A[], int B[],
                int N)
{
    // Stores the minimum cost
    int totalCost = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Case 1: Update A[i]
        int mod_A = B[i] % A[i];
        int totalCost_A = min(mod_A,
                              A[i] - mod_A);

        // Case 2: Update B[i]
        int mod_B = A[i] % B[i];
        int totalCost_B = min(mod_B,
                              B[i] - mod_B);

        // Add the minimum of
        // the above two cases
        totalCost += min(totalCost_A,
                         totalCost_B);
    }

    // Return the resultant cost
    return totalCost;
}

// Driver Code
int main()
{
    int A[] = { 3, 6, 3 };
    int B[] = { 4, 8, 13 };
    int N = sizeof(A) / sizeof(A[0]);

    cout << MinimumCost(A, B, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the minimum cost to
// make A[i] multiple of B[i] or
// vice-versa for every array element
static int MinimumCost(int A[], int B[], int N)
{

    // Stores the minimum cost
    int totalCost = 0;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Case 1: Update A[i]
        int mod_A = B[i] % A[i];
        int totalCost_A = Math.min(mod_A,
                            A[i] - mod_A);

        // Case 2: Update B[i]
        int mod_B = A[i] % B[i];
        int totalCost_B = Math.min(mod_B,
                            B[i] - mod_B);

        // Add the minimum of
        // the above two cases
        totalCost += Math.min(totalCost_A,
                              totalCost_B);
    }

    // Return the resultant cost
    return totalCost;
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 3, 6, 3 };
    int B[] = { 4, 8, 13 };
    int N = A.length;

    System.out.print(MinimumCost(A, B, N));
}
}

// This code is contributed by souravmahato348
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the minimum cost to
# make A[i] multiple of B[i] or
# vice-versa for every array element
def MinimumCost(A, B, N):

    # Stores the minimum cost
    totalCost = 0

    # Traverse the array
    for i in range(N):

        # Case 1: Update A[i]
        mod_A = B[i] % A[i]
        totalCost_A = min(mod_A, A[i] - mod_A)

        # Case 2: Update B[i]
        mod_B = A[i] % B[i]
        totalCost_B = min(mod_B, B[i] - mod_B)

        # Add the minimum of
        # the above two cases
        totalCost += min(totalCost_A, totalCost_B)

    # Return the resultant cost
    return totalCost

# Driver Code
A = [3, 6, 3]
B =  [4, 8, 13]
N = len(A)

print(MinimumCost(A, B, N))

# This code is contributed by shubhamsingh10
```

## C#

```
// C# program for the above approach
using System;

class GFG {

    // Function to find the minimum cost to
    // make A[i] multiple of B[i] or
    // vice-versa for every array element
    static int MinimumCost(int[] A, int[] B, int N)
    {

        // Stores the minimum cost
        int totalCost = 0;

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // Case 1: Update A[i]
            int mod_A = B[i] % A[i];
            int totalCost_A = Math.Min(mod_A, A[i] - mod_A);

            // Case 2: Update B[i]
            int mod_B = A[i] % B[i];
            int totalCost_B = Math.Min(mod_B, B[i] - mod_B);

            // Add the minimum of
            // the above two cases
            totalCost += Math.Min(totalCost_A, totalCost_B);
        }

        // Return the resultant cost
        return totalCost;
    }

    // Driver Code
    public static void Main()
    {
        int[] A = { 3, 6, 3 };
        int[] B = { 4, 8, 13 };
        int N = A.Length;

        Console.Write(MinimumCost(A, B, N));
    }
}

// This code is contributed by rishavmahato348
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Function to find the minimum cost to
    // make A[i] multiple of B[i] or
    // vice-versa for every array element
    function MinimumCost(A , B , N) {

        // Stores the minimum cost
        var totalCost = 0;

        // Traverse the array
        for (i = 0; i < N; i++) {

            // Case 1: Update A[i]
            var mod_A = B[i] % A[i];
            var totalCost_A = Math.min(mod_A, A[i] - mod_A);

            // Case 2: Update B[i]
            var mod_B = A[i] % B[i];
            var totalCost_B = Math.min(mod_B, B[i] - mod_B);

            // Add the minimum of
            // the above two cases
            totalCost += Math.min(totalCost_A, totalCost_B);
        }

        // Return the resultant cost
        return totalCost;
    }

    // Driver Code

        var A = [ 3, 6, 3 ];
        var B = [ 4, 8, 13 ];
        var N = A.length;

        document.write(MinimumCost(A, B, N));

// This code contributed by aashish1995
</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)