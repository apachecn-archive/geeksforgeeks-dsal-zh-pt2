# 计数方式将阵列分割成两个子阵列，GCD 相等

> 原文:[https://www . geesforgeks . org/count-way-to-split-array-to-two-subarray-with-equal-gcd/](https://www.geeksforgeeks.org/count-ways-to-split-array-into-two-subarrays-with-equal-gcd/)

给定一个大小为 **N** 的[阵列](https://www.geeksforgeeks.org/array-data-structure/)、 **arr[]** ，任务是计算将给定的[阵列](https://www.geeksforgeeks.org/arrays-in-c-cpp/)元素拆分为两个[子阵列](https://www.geeksforgeeks.org/tag/subarray/)的方式数，使得两个[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的 [GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 相等。

**示例:**

> **输入:** arr[] = {8，4，4，8，12}
> **输出:** 2
> **解释:**
> 将数组拆分为两组相等的 GCD 的可能方式有:{{arr[0]，arr[1]}，{arr[2]，arr[3]，arr[4]}}，{{arr[0]，arr[1]，arr[2]}，{arr[3]，arr[4]}} }。
> 因此，要求的输出为 2。
> 
> **输入:** arr[] = {1，2，4，6，5}
> 输出: 2

**天真方法:**解决这个问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，在每个数组索引处，将[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)划分为两个子数组，检查两个子数组的 [GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 是否相等。如果发现为真，则增加这些子阵列的计数。最后，打印计数。

***时间复杂度:** O(N <sup>2</sup> )*
**辅助空间:O(N)**

**高效途径:**优化上述途径，思路是使用[前缀和数组技术](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。按照以下步骤解决问题:

*   初始化一个变量，比如**cntway**来存储将数组拆分为两个子数组的方式数，这样两个子数组的 GCD 相等。
*   初始化一个[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)，比如说**前缀 GCD[]** 来存储数组元素的前缀 [GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 。
*   初始化一个[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)，说**后缀**来存储数组元素的后缀 [GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 。
*   [使用变量 **i** 遍历前缀 GCD[]和后缀 GCD[]数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，检查**前缀 GCD[i]** 和**后缀 GCD[i + 1]** 是否相等。如果发现为真，则增加**的值并返回**。
*   最后，打印**cntway**的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count number of ways to split
// array into two groups with equal GCD value.
int cntWaysToSplitArrayTwo(int arr[], int N)
{
    // Stores prefix GCD
    // of the array
    int prefixGCD[N];

    // Update prefixGCD[0]
    prefixGCD[0] = arr[0];

    // Stores suffix GCD
    // of the array
    int suffixGCD[N];

    // Update suffixGCD[N - 1]
    suffixGCD[N - 1] = arr[N - 1];

    // Traverse the array
    for (int i = 1; i < N; i++) {

        // Update prefixGCD[i]
        prefixGCD[i]
            = __gcd(prefixGCD[i - 1],
                    arr[i]);
    }

    // Traverse the array
    for (int i = N - 2; i >= 0; i--) {

        // Update prefixGCD[i]
        suffixGCD[i]
            = __gcd(suffixGCD[i + 1],
                    arr[i]);
    }

    // Stores count of ways to split array
    // into two groups with equal GCD
    int cntWays = 0;

    // Traverse prefixGCD[] and suffixGCD[]
    for (int i = 0; i < N - 1; i++) {

        // If GCD of both groups equal
        if (prefixGCD[i]
            == suffixGCD[i + 1]) {

            // Update cntWays
            cntWays += 1;
        }
    }

    return cntWays;
}

// Driver Code
int main()
{
    int arr[] = { 8, 4, 4, 8, 12 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << cntWaysToSplitArrayTwo(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG{

static int gcd(int a, int b)
{

    // Everything divides 0
    if (a == 0)
      return b;
    if (b == 0)
      return a;

    // Base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return gcd(a - b, b);

    return gcd(a, b - a);
}

// Function to count number of ways to split
// array into two groups with equal GCD value.
static int cntWaysToSplitArrayTwo(int arr[],
                                  int N)
{

    // Stores prefix GCD
    // of the array
    int prefixGCD[] = new int[N];

    // Update prefixGCD[0]
    prefixGCD[0] = arr[0];

    // Stores suffix GCD
    // of the array
    int suffixGCD[] = new int[N];

    // Update suffixGCD[N - 1]
    suffixGCD[N - 1] = arr[N - 1];

    // Traverse the array
    for(int i = 1; i < N; i++)
    {

        // Update prefixGCD[i]
        prefixGCD[i] = gcd(prefixGCD[i - 1],
                                 arr[i]);
    }

    // Traverse the array
    for(int i = N - 2; i >= 0; i--)
    {

        // Update prefixGCD[i]
        suffixGCD[i] = gcd(suffixGCD[i + 1],
                                 arr[i]);
    }

    // Stores count of ways to split array
    // into two groups with equal GCD
    int cntWays = 0;

    // Traverse prefixGCD[] and suffixGCD[]
    for(int i = 0; i < N - 1; i++)
    {

        // If GCD of both groups equal
        if (prefixGCD[i] == suffixGCD[i + 1])
        {

            // Update cntWays
            cntWays += 1;
        }
    }
    return cntWays;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 8, 4, 4, 8, 12 };
    int N = arr.length;

    System.out.print(cntWaysToSplitArrayTwo(arr, N));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import math

# Function to count number of ways to split
# array into two groups with equal GCD value.
def cntWaysToSplitArrayTwo(arr, N):

    # Stores prefix GCD
    # of the array
    prefixGCD = [0] * N

    # Update prefixGCD[0]
    prefixGCD[0] = arr[0]

    # Stores suffix GCD
    # of the array
    suffixGCD = [0] * N

    # Update suffixGCD[N - 1]
    suffixGCD[N - 1] = arr[N - 1]

    # Traverse the array
    for i in range(N):

        # Update prefixGCD[i]
        prefixGCD[i] = math.gcd(prefixGCD[i - 1], arr[i])

    # Traverse the array
    for i in range(N - 2, -1, -1):

        # Update prefixGCD[i]
        suffixGCD[i] = math.gcd(suffixGCD[i + 1], arr[i])

    # Stores count of ways to split array
    # into two groups with equal GCD
    cntWays = 0

    # Traverse prefixGCD[] and suffixGCD[]
    for i in range(N - 1):

        # If GCD of both groups equal
        if (prefixGCD[i] == suffixGCD[i + 1]):

            # Update cntWays
            cntWays += 1

    return cntWays

# Driver Code
arr = [ 8, 4, 4, 8, 12 ]
N = len(arr)

print(cntWaysToSplitArrayTwo(arr, N))

# This code is contributed by susmitakundugoaldanga
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

static int gcd(int a, int b)
{

    // Everything divides 0
    if (a == 0)
      return b;
    if (b == 0)
      return a;

    // Base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return gcd(a - b, b);

    return gcd(a, b - a);
}

// Function to count number of ways to split
// array into two groups with equal GCD value.
static int cntWaysToSplitArrayTwo(int []arr,
                                  int N)
{

    // Stores prefix GCD
    // of the array
    int []prefixGCD = new int[N];

    // Update prefixGCD[0]
    prefixGCD[0] = arr[0];

    // Stores suffix GCD
    // of the array
    int []suffixGCD = new int[N];

    // Update suffixGCD[N - 1]
    suffixGCD[N - 1] = arr[N - 1];

    // Traverse the array
    for(int i = 1; i < N; i++)
    {

        // Update prefixGCD[i]
        prefixGCD[i] = gcd(prefixGCD[i - 1],
                                 arr[i]);
    }

    // Traverse the array
    for(int i = N - 2; i >= 0; i--)
    {

        // Update prefixGCD[i]
        suffixGCD[i] = gcd(suffixGCD[i + 1],
                                 arr[i]);
    }

    // Stores count of ways to split array
    // into two groups with equal GCD
    int cntWays = 0;

    // Traverse prefixGCD[] and suffixGCD[]
    for(int i = 0; i < N - 1; i++)
    {

        // If GCD of both groups equal
        if (prefixGCD[i] == suffixGCD[i + 1])
        {

            // Update cntWays
            cntWays += 1;
        }
    }
    return cntWays;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 8, 4, 4, 8, 12 };
    int N = arr.Length;

    Console.Write(cntWaysToSplitArrayTwo(arr, N));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach
function gcd(a, b)
{

    // Everything divides 0
    if (a == 0)
      return b;
    if (b == 0)
      return a;

    // Base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return gcd(a - b, b);

    return gcd(a, b - a);
}

// Function to count number of ways to split
// array into two groups with equal GCD value.
function cntWaysToSplitArrayTwo(arr, N)
{

    // Stores prefix GCD
    // of the array
    let prefixGCD = [];

    // Update prefixGCD[0]
    prefixGCD[0] = arr[0];

    // Stores suffix GCD
    // of the array
    let suffixGCD = [];

    // Update suffixGCD[N - 1]
    suffixGCD[N - 1] = arr[N - 1];

    // Traverse the array
    for(let i = 1; i < N; i++)
    {

        // Update prefixGCD[i]
        prefixGCD[i] = gcd(prefixGCD[i - 1],
                                 arr[i]);
    }

    // Traverse the array
    for(let i = N - 2; i >= 0; i--)
    {

        // Update prefixGCD[i]
        suffixGCD[i] = gcd(suffixGCD[i + 1],
                                 arr[i]);
    }

    // Stores count of ways to split array
    // into two groups with equal GCD
    let cntWays = 0;

    // Traverse prefixGCD[] and suffixGCD[]
    for(let i = 0; i < N - 1; i++)
    {

        // If GCD of both groups equal
        if (prefixGCD[i] == suffixGCD[i + 1])
        {

            // Update cntWays
            cntWays += 1;
        }
    }
    return cntWays;
}

// Driver code
let arr = [ 8, 4, 4, 8, 12 ];
let N = arr.length;

document.write(cntWaysToSplitArrayTwo(arr, N));

// This code is contributed by code_hunt

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)