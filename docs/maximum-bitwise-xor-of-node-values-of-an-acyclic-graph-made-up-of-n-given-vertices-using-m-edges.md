# 使用 M 条边对由 N 个给定顶点组成的非循环图的节点值进行最大逐位异或运算

> 原文:[https://www . geesforgeks . org/由 n 个给定顶点组成的非循环图的节点值的最大按位异或-使用 m 条边/](https://www.geeksforgeeks.org/maximum-bitwise-xor-of-node-values-of-an-acyclic-graph-made-up-of-n-given-vertices-using-m-edges/)

给定由**【1，N】**取值的 **N** 个节点，一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，使得 **i <sup>第</sup>T13】个节点(*基于 1 的索引*)具有值**arr【I】**和一个整数 **M** ，任务是找到最大值[位](https://www.geeksforgeeks.org/xor-of-two-binary-strings/)**

**示例:**

> **输入:** arr[]= {1，2，3，4}，M = 2
> **输出:** 7
> **解释:**
> 具有 M(= 2)条边的非循环图可以由顶点构成如下:
> 
> 1.  **{1，2，3}:** 顶点按位异或的值是 1^2^3 = 0。
> 2.  **{2，3，4}:** 顶点按位异或的值是 2^3^4 = 5。
> 3.  **{1，2，4}:** 顶点按位异或的值是 1^2^4 = 7。
> 4.  **{1，4，3}:** 顶点按位异或的值是 1^4^3 = 6。
> 
> 因此，所有可能的非循环图之间的最大按位异或是 7。
> 
> **输入:** arr[] = {2，4，8，16}，M = 2
> T3】输出: 28

**方法:**给定的问题可以通过使用具有 **M** 边的非循环图必须具有 **(M + 1)个顶点**的事实来解决。因此，任务简化为[寻找具有 **(M + 1)** 顶点](https://www.geeksforgeeks.org/find-maximum-xor-of-k-elements-in-an-array/)的数组子集 **arr[]** 的最大按位异或。按照以下步骤解决问题:

*   初始化一个变量，比如说 **maxAns** 为 **0** ，它存储一个有 **M** 条边的非循环图的最大位异或。
*   [生成数组的所有可能子集](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/) **arr[]** ，并为每个子集找到子集元素的按位异或，并将**最大值**更新为最大值**最大值**和**按位异或**。
*   完成以上步骤后，打印 **maxAns** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum Bitwise
// XOR of any subset of the array of size K
int maximumXOR(int arr[], int n, int K)
{
    // Number of node must K + 1 for
    // K edges
    K++;

    // Stores the maximum Bitwise XOR
    int maxXor = INT_MIN;

    // Generate all subsets of the array
    for (int i = 0; i < (1 << n); i++) {

        // __builtin_popcount() returns
        // the number of sets bits in
        // an integer
        if (__builtin_popcount(i) == K) {

            // Initialize current xor as 0
            int cur_xor = 0;

            for (int j = 0; j < n; j++) {

                // If jth bit is set in i
                // then include jth element
                // in the current xor
                if (i & (1 << j))
                    cur_xor = cur_xor ^ arr[j];
            }

            // Update the maximum Bitwise
            // XOR obtained so far
            maxXor = max(maxXor, cur_xor);
        }
    }

    // Return the maximum XOR
    return maxXor;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int N = sizeof(arr) / sizeof(int);
    int M = 2;
    cout << maximumXOR(arr, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to find the maximum Bitwise
// XOR of any subset of the array of size K
static int maximumXOR(int arr[], int n, int K)
{

    // Number of node must K + 1 for
    // K edges
    K++;

    // Stores the maximum Bitwise XOR
    int maxXor = Integer.MIN_VALUE;

    // Generate all subsets of the array
    for(int i = 0; i < (1 << n); i++)
    {

        // Integer.bitCount() returns
        // the number of sets bits in
        // an integer
        if (Integer.bitCount(i) == K)
        {

            // Initialize current xor as 0
            int cur_xor = 0;

            for(int j = 0; j < n; j++)
            {

                // If jth bit is set in i
                // then include jth element
                // in the current xor
                if ((i & (1 << j)) != 0)
                    cur_xor = cur_xor ^ arr[j];
            }

            // Update the maximum Bitwise
            // XOR obtained so far
            maxXor = Math.max(maxXor, cur_xor);
        }
    }

    // Return the maximum XOR
    return maxXor;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4 };
    int N = arr.length;
    int M = 2;

    System.out.println(maximumXOR(arr, N, M));
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum Bitwise
# XOR of any subset of the array of size K
def maximumXOR(arr, n, K):

    # Number of node must K + 1 for
    # K edges
    K += 1

    # Stores the maximum Bitwise XOR
    maxXor = -10**9

    # Generate all subsets of the array
    for i in range(1<<n):

        # __builtin_popcount() returns
        # the number of sets bits in
        # an integer
        if (bin(i).count('1') == K):

            # Initialize current xor as 0
            cur_xor = 0

            for j in range(n):

                # If jth bit is set in i
                # then include jth element
                # in the current xor
                if (i & (1 << j)):
                    cur_xor = cur_xor ^ arr[j]

            # Update the maximum Bitwise
            # XOR obtained so far
            maxXor = max(maxXor, cur_xor)

    # Return the maximum XOR
    return maxXor

# Driver Code
if __name__ == '__main__':
    arr= [1, 2, 3, 4 ]
    N = len(arr)
    M = 2
    print (maximumXOR(arr, N, M))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Linq;

class GFG{

// Function to find the maximum Bitwise
// XOR of any subset of the array of size K
static int maximumXOR(int []arr, int n, int K)
{

    // Number of node must K + 1 for
    // K edges
    K++;

    // Stores the maximum Bitwise XOR
    int maxXor = Int32.MinValue;

    // Generate all subsets of the array
    for(int i = 0; i < (1 << n); i++)
    {

        // Finding number of sets
        // bits in an integer
        if (Convert.ToString(i, 2).Count(c => c == '1') == K)
        {

            // Initialize current xor as 0
            int cur_xor = 0;

            for(int j = 0; j < n; j++)
            {

                // If jth bit is set in i
                // then include jth element
                // in the current xor
                if ((i & (1 << j)) != 0)
                    cur_xor = cur_xor ^ arr[j];
            }

            // Update the maximum Bitwise
            // XOR obtained so far
            maxXor = Math.Max(maxXor, cur_xor);
        }
    }

    // Return the maximum XOR
    return maxXor;
}

// Driver code
static void Main()
{
    int [] arr = { 1, 2, 3, 4 };
    int N = arr.Length;
    int M = 2;

    Console.WriteLine(maximumXOR(arr, N, M));
}
}

// This code is contributed by jana_sayantan.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the maximum Bitwise
// XOR of any subset of the array of size K
function maximumXOR(arr, n, K) {
    // Number of node must K + 1 for
    // K edges
    K++;

    // Stores the maximum Bitwise XOR
    let maxXor = Number.MIN_SAFE_INTEGER;

    // Generate all subsets of the array
    for (let i = 0; i < (1 << n); i++) {

        // __builtin_popcount() returns
        // the number of sets bits in
        // an integer
        if ((i).toString(2).split('').
            filter(x => x == '1').length == K) {

            // Initialize current xor as 0
            let cur_xor = 0;

            for (let j = 0; j < n; j++) {

                // If jth bit is set in i
                // then include jth element
                // in the current xor
                if (i & (1 << j))
                    cur_xor = cur_xor ^ arr[j];
            }

            // Update the maximum Bitwise
            // XOR obtained so far
            maxXor = Math.max(maxXor, cur_xor);
        }
    }

    // Return the maximum XOR
    return maxXor;
}

// Driver Code

let arr = [1, 2, 3, 4];
let N = arr.length;
let M = 2;
document.write(maximumXOR(arr, N, M));

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(1)*