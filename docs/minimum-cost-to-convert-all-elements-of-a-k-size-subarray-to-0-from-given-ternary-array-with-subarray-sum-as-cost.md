# 将 K 尺寸子阵列的所有元素从给定的三值阵列转换为 0 的最小成本，子阵列和作为成本

> 原文:[https://www . geeksforgeeks . org/最小成本-将 k 尺寸子阵列的所有元素转换为 0-从给定的三进制阵列加上子阵列的总和作为成本/](https://www.geeksforgeeks.org/minimum-cost-to-convert-all-elements-of-a-k-size-subarray-to-0-from-given-ternary-array-with-subarray-sum-as-cost/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，其中每个数组元素或者是 **0，1，**或者是 **2** ，以及一个整数 **K** ，任务是通过选择一个大小为 **K** 的子数组并将该子数组的任意数组元素转换为**0**来打印将该数组的所有元素转换为 **0** s 所需的最小成本

**示例:**

> **输入:** arr[] = {2，0，1，1，0，2}，K = 3
> **输出:** 3
> **解释:**
> 执行以下步骤:
> 
> 1.  选择范围[1，3]内的子阵列，然后以 2 为代价将 arr[2](= 1)翻转为 0。数组修改为 arr[] = {2，0，0，1，0，2}。
> 2.  选择范围[1，3]内的子阵列，然后以 1 为代价将 arr[3](= 1)翻转为 0。数组修改为 arr[] = {2，0，0，0，0，2}。
> 3.  选择[0，2]范围内的子阵列，然后以 2 为代价将 arr[0](= 2)翻转为 0。数组修改为 arr[] = {0，0，0，0，0，2}。
> 4.  选择范围[3，5]内的子阵列，然后以 2 为代价将 arr[5](= 2)翻转为 0。数组修改为 arr[] = {0，0，0，0，0，0}。
> 
> 因此，需要的总成本是(2+1+2+2 = 7)。这也是所需的最低成本。
> 
> **输入:** arr[] = {1，0，2，1}，K = 4
> T3】输出: 7

**方法:**给定的问题可以基于以下观察来解决:

> 1.  First of all, it is best to convert all elements of **2** s with the lowest cost and the largest number into **0** in the subarray with the size of **k** .
> 2.  Let **x** be the count of **1** s, and **y** be the count of **2** s in the subarray with the lowest cost. Then convert all **2** s into **0** and then all **1** s into **0** to give the minimum cost of converting the subarray into **0** .
> 3.  The cost of converting all **2** s into **0** is:
>     *   **(X+2 * Y-2)+(X+2 * Y-4)+……+(X+2 * Y-2 *(Y-1))**
>         **= Y *(X+2 * Y)–Y *(0+2 *(Y-1))/2**
>         T42
>         T7】= X * Y+2 * Y<sup>2</sup>-Y<sup>2</sup>+Y = Y<sup>2</sup>+X * Y+Y【T11
> 4.  The cost of converting all remaining **1** s into **0** is:
>     *   **x+(x-1)+(x-1) The cost of converting all elements of a sub-array with **x** **1** s and **y** **2** s is equal to**
>     *   **Now, the remaining elements can be converted to [T90**
>     ***   Therefore, if the sum of **is the sum of arrays, then the minimum cost will be equal to:**
>         *   **之和-(X+2 * Y)+****Y<sup>2</sup>+X * Y+Y+(X *(X+1))/2****

**按照以下步骤解决问题:**

*   **初始化两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，比如 **pcount1[]** 和 **pcount2[]** 为 **{0}** ，其中 **pcount1[i]** 和 **pcount2[i]** 存储 **1** s 和 **2** s 在前缀范围**【0，I】内的计数。****
*   **[遍历数组，](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)T2【arr】使用变量 **i** 并执行以下操作:

    *   将 **pcount1[i]** 分配给 **pcount1[i+1]** ，将 **pcount2[i]** 分配给 **pcount2[i+1]** 。
    *   如果 **arr[i]** 为 **1** ，则递增**pcount 1【I+1】**。否则，如果 **arr[i]** 为 **2** ，则 **pcount2[i+1]** 的增量计数。** 
*   **[求数组的和](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)并存储在变量中，比如**和。****
*   **初始化两个变量，比如 **X** 和 **Y** ，将 **1** s 和 **2** s 的计数存储在子阵列中，大小之和最小 **K** 。**
*   **使用变量 **i** 迭代范围**【K，N】**，并执行以下步骤:

    *   初始化两个变量，比如 **A** 和 **B** ，存储子阵中 **1** s 和 **2** s 在**【I-K，K-1】范围内的计数。**
    *   将 **pcount1[i]-pcount1[i-K]** 分配给 **A** ，将 **pcount2[i]-pcount2[i-K]** 分配给 **B** 。
    *   如果 **A+2*B** 小于 **X+2*Y** ，则更新 **X** 到 **A** 和 **Y** 到 **B** 。** 
*   **最后，完成上述步骤后，将总成本打印为，**sum-(X+2 * Y)+****Y<sup>2</sup>+X * Y+Y+(X *(X+1))/2。****

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the min cost
int minCost(int arr[], int N, int K)
{
    // Stores the prefix count of 1s
    int pcount1[N + 1] = { 0 };
    // Stores the prefix count of 2s
    int pcount2[N + 1] = { 0 };

    // Traverse the array arr[]
    for (int i = 1; i <= N; i++) {
        pcount1[i] = pcount1[i - 1] + (arr[i - 1] == 1);
        pcount2[i] = pcount2[i - 1] + (arr[i - 1] == 2);
    }

    // Stores total sum of the array arr[]
    int sum = pcount1[N] + 2 * pcount2[N];

    // Stores the count of 1s in a subarray
    int X = N;

    // Stores the count of 2s in a subarray
    int Y = N;

    // Iterate over the range [K, N]
    for (int i = K; i <= N; i++) {
        int A = pcount1[i] - pcount1[i - K];
        int B = pcount2[i] - pcount2[i - K];

        // If current subarray sum is less
        // than X+2*Y
        if (A + 2 * B < X + 2 * Y) {
            X = A;
            Y = B;
        }
    }

    // Stores the total cost
    int total = sum - (X + 2 * Y) + Y * Y + X * Y + Y
                + (X * (X + 1)) / 2;
    // Return total
    return total;
}

// Driver Code
int main()
{

    // Input
    int arr[] = { 2, 0, 1, 1, 0, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 3;
    // Function call
    cout << minCost(arr, N, K);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java Program for the above approach
import java.io.*;
import java.util.Arrays;
class GFG
{

    // Function to find the min cost
    static int minCost(int arr[], int N, int K)
    {

        // Stores the prefix count of 1s
        int pcount1[] = new int[N + 1];

        // Stores the prefix count of 2s
        int pcount2[] = new int[N + 1];
        Arrays.fill(pcount1, 0);
        Arrays.fill(pcount2, 0);

        // Traverse the array arr[]
        for (int i = 1; i <= N; i++) {
            int k = 0;
            int l = 0;
            if (arr[i - 1] == 1)
                k = 1;

            if (arr[i - 1] == 2)
                l = 1;

            pcount1[i] = pcount1[i - 1] + k;
            pcount2[i] = pcount2[i - 1] + l;
        }

        // Stores total sum of the array arr[]
        int sum = pcount1[N] + 2 * pcount2[N];

        // Stores the count of 1s in a subarray
        int X = N;

        // Stores the count of 2s in a subarray
        int Y = N;

        // Iterate over the range [K, N]
        for (int i = K; i <= N; i++) {
            int A = pcount1[i] - pcount1[i - K];
            int B = pcount2[i] - pcount2[i - K];

            // If current subarray sum is less
            // than X+2*Y
            if (A + 2 * B < X + 2 * Y) {
                X = A;
                Y = B;
            }
        }

        // Stores the total cost
        int total = sum - (X + 2 * Y) + Y * Y + X * Y + Y
                    + (X * (X + 1)) / 2;
        // Return total
        return total;
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Input
        int arr[] = { 2, 0, 1, 1, 0, 2 };
        int N = arr.length;
        int K = 3;
        // Function call

        System.out.println(minCost(arr, N, K));

    }
}

      // This code is contributed by Potta Lokesh
```

## **蟒蛇 3**

```
# Py program for the above approach

# Function to find the min cost
def minCost(arr, N, K):

    # Stores the prefix count of 1s
    pcount1 = [0] * (N + 1)

    # Stores the prefix count of 2s
    pcount2 = [0] * (N+1)

    # Traverse the array arr[]
    for i in range(1,N+1):
        pcount1[i] = pcount1[i - 1] + (arr[i - 1] == 1)
        pcount2[i] = pcount2[i - 1] + (arr[i - 1] == 2)

    # Stores total sum of the array arr[]
    sum = pcount1[N] + 2 * pcount2[N]

    # Stores the count of 1s in a subarray
    X = N

    # Stores the count of 2s in a subarray
    Y = N

    # Iterate over the range [K, N]
    for i in range(K, N + 1):
        A = pcount1[i] - pcount1[i - K]
        B = pcount2[i] - pcount2[i - K]

        # If current subarray sum is less
        # than X+2*Y
        if (A + 2 * B < X + 2 * Y):
            X = A
            Y = B

    # Stores the total cost
    total = sum - (X + 2 * Y) + Y * Y + X * Y + Y + (X * (X + 1)) // 2
    # Return total
    return total

# Driver Code
if __name__ == '__main__':

    # Input
    arr= [2, 0, 1, 1, 0, 2]
    N =  len(arr)
    K = 3

    # Function call
    print (minCost(arr, N, K))

# This code is contributed by mohit kumar 29.
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the min cost
static int minCost(int []arr, int N, int K)
{
    // Stores the prefix count of 1s
    int []pcount1 = new int[N + 1];
    Array.Clear(pcount1, 0, N + 1);

    // Stores the prefix count of 2s
    int []pcount2 = new int[N + 1];
    Array.Clear(pcount2, 0, N + 1);

    // Traverse the array arr[]
    for (int i = 1; i <= N; i++) {
        if(arr[i - 1] == 1){
          pcount1[i] = pcount1[i - 1] + 1;
        }
        else
          pcount1[i] = pcount1[i - 1];

         if(arr[i - 1] == 2){
          pcount2[i] = pcount2[i - 1] + 1;
        }
        else
          pcount2[i] = pcount2[i - 1];

    }

    // Stores total sum of the array arr[]
    int sum = pcount1[N] + 2 * pcount2[N];

    // Stores the count of 1s in a subarray
    int X = N;

    // Stores the count of 2s in a subarray
    int Y = N;

    // Iterate over the range [K, N]
    for (int i = K; i <= N; i++) {
        int A = pcount1[i] - pcount1[i - K];
        int B = pcount2[i] - pcount2[i - K];

        // If current subarray sum is less
        // than X+2*Y
        if (A + 2 * B < X + 2 * Y) {
            X = A;
            Y = B;
        }
    }

    // Stores the total cost
    int total = sum - (X + 2 * Y) + Y * Y + X * Y + Y
                + (X * (X + 1)) / 2;
    // Return total
    return total;
}

// Driver Code
public static void Main()
{

    // Input
    int []arr = { 2, 0, 1, 1, 0, 2 };
    int N = arr.Length;
    int K = 3;

    // Function call
    Console.Write(minCost(arr, N, K));
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## **java 描述语言**

```
// Javascript program for the above approach

// Function to find the min cost
function minCost(arr, N, K)
{

    // Stores the prefix count of 1s
    let pcount1 = new Array(N + 1).fill(0);

    // Stores the prefix count of 2s
    let pcount2 = new Array(N + 1).fill(0);

    // Traverse the array arr[]
    for (let i = 1; i <= N; i++) {
        pcount1[i] = pcount1[i - 1] + (arr[i - 1] == 1);
        pcount2[i] = pcount2[i - 1] + (arr[i - 1] == 2);
    }

    // Stores total sum of the array arr[]
    let sum = pcount1[N] + 2 * pcount2[N];

    // Stores the count of 1s in a subarray
    let X = N;

    // Stores the count of 2s in a subarray
    let Y = N;

    // Iterate over the range [K, N]
    for (let i = K; i <= N; i++) {
        let A = pcount1[i] - pcount1[i - K];
        let B = pcount2[i] - pcount2[i - K];

        // If current subarray sum is less
        // than X+2*Y
        if (A + 2 * B < X + 2 * Y) {
            X = A;
            Y = B;
        }
    }

    // Stores the total cost
    let total = sum - (X + 2 * Y) + Y * Y + X * Y + Y
        + (X * (X + 1)) / 2;

    // Return total
    return total;
}

// Driver Code

// Input
let arr = [2, 0, 1, 1, 0, 2];
let N = arr.length;
let K = 3;

// Function call
document.write(minCost(arr, N, K));

// This code is contributed by gfgking.
```

****Output**

```
7
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(N)**