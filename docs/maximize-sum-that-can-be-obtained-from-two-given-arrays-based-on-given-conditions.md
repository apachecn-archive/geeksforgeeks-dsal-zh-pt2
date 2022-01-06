# 根据给定条件最大化从两个给定数组中获得的和

> 原文:[https://www . geesforgeks . org/最大化基于给定条件从两个给定数组中获得的总和/](https://www.geeksforgeeks.org/maximize-sum-that-can-be-obtained-from-two-given-arrays-based-on-given-conditions/)

给定两个大小分别为 **N** 的[阵列](https://www.geeksforgeeks.org/array-data-structure/) **A[]** 和 **B[]** ，任务是基于以下条件找到可获得的最大和:

*   **A【I】**和**B【I】**都不能计入总和(*****0≤I≤N–1***)。**
*   **如果将 **B[i]** 加到总和中，则**B[I–1]**和**A[I–1]**不能包含在总和中(***0≤I≤N–1***)。**

****示例:****

> ****输入:** A[] = {10，20，5}，B[] = {5，5，45}
> **输出:** 55
> **说明:**最大化和的最佳方式是将 A[0] (= 10)和 B[2] (= 45)包含在和中。因此，sum = 10 + 45 = 55。**
> 
> ****输入:** A[] = {10，1，10，10}，B[] = {5，50，1，5 }
> T3】输出: 70**

****逼近:**这个问题有[最优子结构](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)和[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)。所以可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)来解决问题。
按照以下步骤解决问题:**

*   **初始化一个[数组](https://www.geeksforgeeks.org/array-data-structure/)，比如 **dp[n][2]，**，其中 **dp[i][0]** 存储最大和，如果考虑到元素 **A[i]** ，如果考虑到 **dp[i][1]** 存储最大和。**
*   **[使用变量在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**中迭代，说出 **i，**并执行以下步骤:

    *   如果 **i** 等于 **0** ，则将 **dp[i][0]** 的值修改为 **A[i]** ，将 **dp[i][1]** 修改为 **B[i]** 。
    *   否则，请执行以下操作:
        *   将 **dp[i][0]** 的值修改为**最大值(DP[I–1][0]，DP[I–1][1])+A[I]**。
        *   将 **dp[i][1]** 的值修改为**最大值(DP[I–1]、最大值(DP[I–1][0]、最大值(DP[I–2][0]、DP[I–2][1])+B[I])**。** 
*   **完成以上步骤后，打印 **max(dp[N-1][0]，dp[N-1][1])** 作为答案。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum
// that can be obtained from two given
// based on the following conditions
int MaximumSum(int a[], int b[], int n)
{
    // Stores the maximum
    // sum from 0 to i
    int dp[n][2];

    // Initialize the value of
    // dp[0][0] and dp[0][1]
    dp[0][0] = a[0];
    dp[0][1] = b[0];

    // Traverse the array A[] and B[]
    for (int i = 1; i < n; i++) {
        // If A[i] is considered
        dp[i][0] = max(dp[i - 1][0], dp[i - 1][1]) + a[i];

        // If B[i] is not considered
        dp[i][1] = max(dp[i - 1][0], dp[i - 1][1]);

        // If B[i] is considered
        if (i - 2 >= 0) {
            dp[i][1] = max(dp[i][1],
                           max(dp[i - 2][0],
                               dp[i - 2][1])
                               + b[i]);
        }
        else {
            // If i = 1, then consider the
            // value of  dp[i][1] as b[i]
            dp[i][1] = max(dp[i][1], b[i]);
        }
    }

    // Return maximum Sum
    return max(dp[n - 1][0], dp[n - 1][1]);
}

// Driver Code
int main()
{
    // Given Input
    int A[] = { 10, 1, 10, 10 };
    int B[] = { 5, 50, 1, 5 };
    int N = sizeof(A) / sizeof(A[0]);

    // Function Call
    cout << MaximumSum(A, B, N);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach

class GFG {
    // Function to find the maximum sum
    // that can be obtained from two given
    // based on the following conditions
    public static int MaximumSum(int a[], int b[], int n) {
        // Stores the maximum
        // sum from 0 to i
        int[][] dp = new int[n][2];

        // Initialize the value of
        // dp[0][0] and dp[0][1]
        dp[0][0] = a[0];
        dp[0][1] = b[0];

        // Traverse the array A[] and B[]
        for (int i = 1; i < n; i++) {
            // If A[i] is considered
            dp[i][0] = Math.max(dp[i - 1][0], dp[i - 1][1]) + a[i];

            // If B[i] is not considered
            dp[i][1] = Math.max(dp[i - 1][0], dp[i - 1][1]);

            // If B[i] is considered
            if (i - 2 >= 0) {
                dp[i][1] = Math.max(dp[i][1], Math.max(dp[i - 2][0], dp[i - 2][1]) + b[i]);
            } else
            {

                // If i = 1, then consider the
                // value of dp[i][1] as b[i]
                dp[i][1] = Math.max(dp[i][1], b[i]);
            }
        }

        // Return maximum Sum
        return Math.max(dp[n - 1][0], dp[n - 1][1]);
    }

    // Driver Code
    public static void main(String args[]) {
        // Given Input
        int A[] = { 10, 1, 10, 10 };
        int B[] = { 5, 50, 1, 5 };
        int N = A.length;

        // Function Call
        System.out.println(MaximumSum(A, B, N));
    }
}

// This  code is contributed by _saurabh_jaiswal.
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to find the maximum sum
# that can be obtained from two given
# arrays based on the following conditions
def MaximumSum(a, b, n):

    # Stores the maximum
    # sum from 0 to i
    dp = [[-1 for j in range(2)]
              for i in range(n)]

    # Initialize the value of
    # dp[0][0] and dp[0][1]
    dp[0][0] = a[0]
    dp[0][1] = b[0]

    # Traverse the array A[] and B[]
    for i in range(1, n):

        # If A[i] is considered
        dp[i][0] = max(dp[i - 1][0],
                       dp[i - 1][1]) + a[i]

        # If B[i] is not considered
        dp[i][1] = max(dp[i - 1][0],
                       dp[i - 1][1])

        # If B[i] is considered
        if (i - 2 >= 0):
            dp[i][1] = max(dp[i][1], max(dp[i - 2][0],
                                         dp[i - 2][1]) + b[i])
        else:

            # If i = 1, then consider the
            # value of  dp[i][1] as b[i]
            dp[i][1] = max(dp[i][1], b[i])

    # Return maximum sum
    return max(dp[n - 1][0], dp[n - 1][1])

# Driver code
if __name__ == '__main__':

    # Given input
    A = [ 10, 1, 10, 10 ]
    B = [ 5, 50, 1, 5 ]
    N = len(A)

    # Function call
    print(MaximumSum(A, B, N))

# This code is contributed by MuskanKalra1
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the maximum sum
// that can be obtained from two given
// based on the following conditions
static int MaximumSum(int []a, int []b, int n)
{

    // Stores the maximum
    // sum from 0 to i
    int [,]dp = new int[n,2];

    // Initialize the value of
    // dp[0][0] and dp[0][1]
    dp[0,0] = a[0];
    dp[0,1] = b[0];

    // Traverse the array A[] and B[]
    for (int i = 1; i < n; i++)
    {

        // If A[i] is considered
        dp[i,0] = Math.Max(dp[i - 1,0], dp[i - 1,1]) + a[i];

        // If B[i] is not considered
        dp[i,1] = Math.Max(dp[i - 1,0], dp[i - 1,1]);

        // If B[i] is considered
        if (i - 2 >= 0) {
            dp[i,1] = Math.Max(dp[i,1],
                           Math.Max(dp[i - 2,0],
                               dp[i - 2,1])
                               + b[i]);
        }
        else
        {

            // If i = 1, then consider the
            // value of  dp[i][1] as b[i]
            dp[i,1] = Math.Max(dp[i,1], b[i]);
        }
    }

    // Return maximum Sum
    return Math.Max(dp[n - 1,0], dp[n - 1,1]);
}

// Driver Code
public static void Main()
{
    // Given Input
    int []A = { 10, 1, 10, 10 };
    int []B = { 5, 50, 1, 5 };
    int N = A.Length;

    // Function Call
    Console.Write(MaximumSum(A, B, N));
}
}

// This code is contributed by ipg2016107.
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// Function to find the maximum sum
// that can be obtained from two given
// based on the following conditions
function MaximumSum(a, b, n)
{

    // Stores the maximum
    // sum from 0 to i
    let dp = new Array(n).fill(0).map(
       () => new Array(2));

    // Initialize the value of
    // dp[0][0] and dp[0][1]
    dp[0][0] = a[0];
    dp[0][1] = b[0];

    // Traverse the array A[] and B[]
    for(let i = 1; i < n; i++)
    {

        // If A[i] is considered
        dp[i][0] = Math.max(dp[i - 1][0],
                            dp[i - 1][1]) + a[i];

        // If B[i] is not considered
        dp[i][1] = Math.max(dp[i - 1][0],
                            dp[i - 1][1]);

        // If B[i] is considered
        if (i - 2 >= 0)
        {
            dp[i][1] = Math.max(dp[i][1],
                Math.max(dp[i - 2][0],
                          dp[i - 2][1]) + b[i]);
        }
        else
        {

            // If i = 1, then consider the
            // value of  dp[i][1] as b[i]
            dp[i][1] = Math.max(dp[i][1], b[i]);
        }
    }

    // Return maximum Sum
    return Math.max(dp[n - 1][0], dp[n - 1][1]);
}

// Driver Code

// Given Input
let A = [ 10, 1, 10, 10 ];
let B = [ 5, 50, 1, 5 ];
let N = A.length;

// Function Call
document.write(MaximumSum(A, B, N));

// This code is contributed by gfgking

</script>
```

****Output:** 

```
70
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(N)**