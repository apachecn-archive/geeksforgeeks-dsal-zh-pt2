# 所有元素都是 K 的因子的最长子阵列

> 原文:[https://www . geesforgeks . org/最长子阵列，其中所有元素都是 k 的因子/](https://www.geeksforgeeks.org/longest-subarray-in-which-all-elements-are-a-factor-of-k/)

给定一个大小为 **N** 的[阵列](https://www.geeksforgeeks.org/array-data-structure/)**A【】**和一个正整数 **K** ，任务是找到最长的[子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)的长度，使得子阵列的所有元素都是 **K** 的因子。

**示例:**

> **输入:** A[] = {2，8，3，10，6，7，4，9}，K = 60
> **输出:** 3
> **说明:**所有元素都是 K (= 60)因子的最长子阵是{3，10，6}。因此，所需的输出为 3。
> 
> **输入:** A[] = {7，20，8，10，5}，K = 20
> **输出:** 2
> **说明:**所有元素都是 K 的因子(= 20)的最长子阵是{10，5}。因此，所需的输出为 2。

**天真方法:**解决这个问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[生成给定数组的所有可能的子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)。对于每个子阵列，检查其所有元素是否都是 **K** 的因子。如果发现是真的，则存储子阵列的长度，如果它是在此之前获得的最大值。最后，打印获得的最大长度作为所需答案。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效途径:**优化上述途径，思路是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)检查**arr【I】**是否为 **K** 的因子。如果发现为真，则增加子阵列的长度。否则，如果子阵列的长度是目前获得的最大值，则存储该长度，并重置为 **0** 。按照以下步骤解决问题:

*   初始化一个变量，比如 **MaxLen** ，来存储最长子阵列的长度，使得子阵列中的每个元素都是 **K** 的因子。
*   初始化一个变量，比如 **Len** ，来存储当前子阵列的长度。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并检查 **K % arr[i] = 0** 与否。如果发现为真，则增加 **Len** 的值并更新 **MaxLen = max(Len，MaxLen)的值。**
*   最后打印 **MaxLen** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the length of the longest
// subarray in which all elements are a factor of K
int find_longest_subarray(int A[], int N, int K)
{

    // Stores length of the longest subarray
    // in which all elements are a factor of K
    int MaxLen = 0;

    // Stores length of
    // the current subarray
    int Len = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // If A[i] is a factor of K
        if (K % A[i] == 0) {

            // Update Len
            Len++;

            // Update MaxLen
            MaxLen = max(MaxLen, Len);
        }

        else {
            // Reset Len
            Len = 0;
        }
    }

    return MaxLen;
}

// Driver Code
int main()
{
    int A[] = { 2, 8, 3, 10, 6, 7, 4, 9 };
    int N = sizeof(A) / sizeof(A[0]);
    ;
    int K = 60;

    cout << find_longest_subarray(A, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

import java.util.*;

class GFG {

    // Function to find the length of the longest
    // subarray in which all elements are a factor of K
    static int find_longest_subarray(int[] A, int N,
                                     int K)
    {
        // Stores length of the longest subarray
        // in which all elements are a factor of K
        int MaxLen = 0;

        // Stores length of
        // the current subarray
        int Len = 0;

        // Traverse the array arr[]
        for (int i = 0; i < N; i++) {

            // If A[i] is a
            // factor of K
            if (K % A[i] == 0) {

                // Update Len
                Len++;

                // Update MaxLen
                MaxLen = Math.max(
                    MaxLen, Len);
            }

            // If A[i] is not a
            // factor of K
            else {

                // Update Len
                Len = 0;
            }
        }

        return MaxLen;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] A = { 2, 8, 3, 10, 6, 7, 4, 9 };
        int N = A.length;
        int K = 60;
        System.out.println(
            find_longest_subarray(A, N, K));
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the length of the
# longest subarray in which all
# elements are a factor of K
def find_longest_subarray(A, N, K):

    # Stores length of the longest
    # subarray in which all elements
    # are a factor of K
    MaxLen = 0

    # Stores length of the
    # current subarray
    Len = 0

    # Traverse the array arr[]
    for i in range(N):

        # If A[i] is a factor of K
        if (K % A[i] == 0):

            # Update Len
            Len += 1

            # Update MaxLen
            MaxLen = max(MaxLen, Len)

        # If A[i] is not a
        # factor of K  
        else:

            # Reset Len
            Len = 0

    return MaxLen

# Driver Code
A = [ 2, 8, 3, 10, 6, 7, 4, 9 ]
N = len(A)

K = 60

print(find_longest_subarray(A, N, K))

# This code is contributed by susmitakundugoaldanga
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to find the length of the longest
// subarray in which all elements are a factor of K
static int find_longest_subarray(int[] A, int N,
                                 int K)
{

    // Stores length of the longest subarray
    // in which all elements are a factor of K
    int MaxLen = 0;

    // Stores length of
    // the current subarray
    int Len = 0;

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // If A[i] is a
        // factor of K
        if (K % A[i] == 0)
        {

            // Update Len
            Len++;

            // Update MaxLen
            MaxLen = Math.Max(MaxLen, Len);
        }

        // If A[i] is not a
        // factor of K
        else
        {

            // Update Len
            Len = 0;
        }
    }
    return MaxLen;
}

// Driver Code
public static void Main(string[] args)
{
    int[] A = { 2, 8, 3, 10, 6, 7, 4, 9 };
    int N = A.Length;
    int K = 60;

    Console.WriteLine(find_longest_subarray(
        A, N, K));
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find the length of the longest
// subarray in which all elements are a factor of K
function find_longest_subarray(A, N, K)
{

    // Stores length of the longest subarray
    // in which all elements are a factor of K
    let MaxLen = 0;

    // Stores length of
    // the current subarray
    let Len = 0;

    // Traverse the array arr[]
    for(let i = 0; i < N; i++)
    {

        // If A[i] is a
        // factor of K
        if (K % A[i] == 0)
        {

            // Update Len
            Len++;

            // Update MaxLen
            MaxLen = Math.max(MaxLen, Len);
        }

        // If A[i] is not a
        // factor of K
        else
        {

            // Update Len
            Len = 0;
        }
    }
    return MaxLen;
}

// Driver code
let A = [ 2, 8, 3, 10, 6, 7, 4, 9 ];
let N = A.length;
let K = 60;

document.write(find_longest_subarray(A, N, K));

// This code is contributed by code_hunt

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)