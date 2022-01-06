# 最小化交换两个给定阵列的成本

> 原文:[https://www . geesforgeks . org/最小化交换两个给定阵列的成本/](https://www.geeksforgeeks.org/minimize-cost-to-swap-two-given-arrays/)

给定两个由不同元素组成的 **N** 大小的[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/) **A[]** 和 **B[]** ，任务是找到交换两个给定阵列的最小成本。交换两个元素**A[I]****B[j]**的成本为 **min(A[i]，A[j])** 。总成本是所有交换操作成本的累计总和。

**注意:**这里，元素的顺序可以与交换后的原始数组不同。

**示例:**

> **输入:** N = 3，A[] = {1，4，2}，B[] = {10，6，12}
> **输出:** 5
> **解释:**
> 以下互换操作将给出最小成本:
> 互换(A[0]，B[2]):成本= min(A[0]，B[2]) = 1，A[ ] = {12，4，2}，B[ ] = {10，6，1}
> B[0]):成本=分钟(A[2]，B[0]) = 1，A[ ] = {12，4，10}，B[ ] = {1，6，2}
> 交换(A[1]，B[0]):成本=分钟(A[1]，B[0]) = 1，A[ ] = {12，1，10}，B[ ] = {4，6，2}
> 交换(A[1]，B[1]):成本=分钟(A[1]，B[1]):成本=分钟 交换两个数组的最小成本= 1 + 1 + 1 + 1 + 1 = 5
> **输入:** N = 2，A[] = {9，12}，B[] = {3，15}
> **输出:** 9

**方法:**
按照以下步骤解决问题:

*   同时遍历数组并从中找到最小元素，比如 **K** 。
*   现在，每个元素都有 K，直到两个数组被交换。因此，所需的互换数量为**2 * N–1**。
*   打印**K *(2 * N–1)**作为答案。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate and return the
// minimum cost required to swap two arrays
int getMinCost(vector<int> A, vector<int> B,
               int N)
{

    int mini = INT_MAX;
    for (int i = 0; i < N; i++) {
        mini = min(mini, min(A[i], B[i]));
    }

    // Return the total minimum cost
    return mini * (2 * N - 1);
}

// Driver Code
int main()
{
    int N = 3;

    vector<int> A = { 1, 4, 2 };
    vector<int> B = { 10, 6, 12 };

    cout << getMinCost(A, B, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to calculate and return the
// minimum cost required to swap two arrays
static int getMinCost(int [] A, int [] B,
                                   int N)
{
    int mini = Integer.MAX_VALUE;
    for (int i = 0; i < N; i++)
    {
        mini = Math.min(mini,
               Math.min(A[i], B[i]));
    }

    // Return the total minimum cost
    return mini * (2 * N - 1);
}

// Driver Code
public static void main(String[] args)
{
    int N = 3;

    int [] A = { 1, 4, 2 };
    int [] B = { 10, 6, 12 };

    System.out.print(getMinCost(A, B, N));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import sys

# Function to calculate and return the
# minimum cost required to swap two arrays
def getMinCost(A, B, N):

    mini = sys.maxsize
    for i in range(N):
        mini = min(mini, min(A[i], B[i]))

    # Return the total minimum cost
    return mini * (2 * N - 1)

# Driver Code
N = 3

A = [ 1, 4, 2 ]
B = [ 10, 6, 12 ]

print(getMinCost(A, B, N))

# This code is contributed by chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

    // Function to calculate and return the
    // minimum cost required to swap two arrays
    static int getMinCost(int[] A, int[] B, int N)
    {
        int mini = int.MaxValue;
        for (int i = 0; i < N; i++)
        {
            mini = Math.Min(mini, Math.Min(A[i], B[i]));
        }

        // Return the total minimum cost
        return mini * (2 * N - 1);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int N = 3;
          int[] A = {1, 4, 2};
        int[] B = {10, 6, 12};
          Console.Write(getMinCost(A, B, N));
    }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Java script program to implement
// the above approach
function  getMinCost(A,B,N)
{
    let mini = Number.MAX_VALUE;
    for (let i = 0; i < N; i++)
    {
        mini = Math.min(mini,
            Math.min(A[i], B[i]));
    }

    // Return the total minimum cost
    return mini * (2 * N - 1);
}

// Driver Code

    let N = 3;

    let A = [ 1, 4, 2 ];
    let B = [ 10, 6, 12 ];

    document.write(getMinCost(A, B, N));

// This code is contributed by manoj
</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*