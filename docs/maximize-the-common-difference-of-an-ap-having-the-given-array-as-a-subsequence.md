# 最大化具有给定数组作为子序列的接入点的公共差异

> 原文:[https://www . geesforgeks . org/最大化具有给定数组作为子序列的 ap 的公共差异/](https://www.geeksforgeeks.org/maximize-the-common-difference-of-an-ap-having-the-given-array-as-a-subsequence/)

给定一个由 **N** 个不同元素组成的[排序数组](https://www.geeksforgeeks.org/program-check-array-sorted-not-iterative-recursive/)**arr【】**，任务是找到一个[算术级数](https://www.geeksforgeeks.org/arithmetic-progression/)的最大可能公共差，使得给定数组是那个[算术级数](https://en.wikipedia.org/wiki/Arithmetic_progression)的一个[子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)。

**示例:**

> **输入:** arr[] = { 2，4，6，8 }
> **输出:** 2
> **解释:**
> 由于 arr[]是等差数列{ 2，4，6，8，10，…}的一个子数列，所以等差数列的公差是 2。
> 
> **输入:** arr[] = { 2，5，11，23 }
> **输出:** 3
> **解释:**
> 由于 arr[]是等差数列{ 2，5，8，11，14，…，23，…}的子数列，所以等差数列的公差是 2。

**天真方法:**解决这个问题最简单的方法是使用变量 **CD** (公共差)迭代范围**[(arr[N–1]–arr[0])，1]** ，对于该范围内的每个值，检查给定数组是否可以是[算术级数](https://www.geeksforgeeks.org/arithmetic-progression/)的后续数组，第一个元素为 **arr[0]** ，公共差为 **CD** 。这可以通过简单地检查每对相邻阵列元素之间的差是否能被 **CD** 整除来实现。如果发现为真，则打印 **CD** 的值作为最大可能答案。

***时间复杂度:**O(N *(Maxm–Minm))，其中 **Maxm** 和 **Minm** 分别是最后一个和第一个数组元素。*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于以下观察进行优化:

> 如果 arr[i]是第 X <sup>个</sup>项，arr[0]是具有公共差 CD 的算术级数的第一项，那么:
> 
> arr[I]= arr[0]+(X–1)* CD
> =>(arr[I]–arr[0])=(X–1)* CD
> 
> 因此，AP 的最大可能公共差是每对相邻阵列元素的绝对差的 [GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 。

按照以下步骤解决问题:

*   初始化一个变量，比如 **maxCD** ，以存储一个[等差数列](https://www.geeksforgeeks.org/arithmetic-progression/)的最大可能公共差，这样给定的数组就是该等差数列的子序列。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并更新 **maxCD =** [**GCD 的值(maxCD，(arr[I+1]–arr[I])**](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)。
*   最后打印 **maxCD** 的值。

下面是上述方法的实现

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum common
// difference of an AP such that arr[]
// is a subsequence of that AP
int MaxComDiffSubAP(int arr[], int N)
{
    // Stores maximum common difference
    // of an AP with given conditions
    int maxCD = 0;

    // Traverse the array
    for (int i = 0; i < N - 1; i++) {

        // Update maxCD
        maxCD = __gcd(maxCD,
                      arr[i + 1] - arr[i]);
    }

    return maxCD;
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, 7, 9 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << MaxComDiffSubAP(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach 
class GFG
{

  // Recursive function to return gcd of a and b
  static int gcd(int a, int b)
  {

    // Everything divides 0
    if (a == 0)
      return b;
    if (b == 0)
      return a;

    // base case
    if (a == b)
      return a;

    // a is greater
    if (a > b)
      return gcd(a - b, b);

    return gcd(a, b - a);
  }

  // Function to find the maximum common
  // difference of an AP such that arr[]
  // is a subsequence of that AP
  static int MaxComDiffSubAP(int arr[], int N)
  {

    // Stores maximum common difference
    // of an AP with given conditions
    int maxCD = 0;

    // Traverse the array
    for (int i = 0; i < N - 1; i++)
    {

      // Update maxCD
      maxCD = gcd(maxCD,
                  arr[i + 1] - arr[i]);
    }

    return maxCD;
  }

  // Driver Code
  public static void main (String[] args)
  {
    int arr[] = { 1, 3, 7, 9 };
    int N = arr.length;

    System.out.print(MaxComDiffSubAP(arr, N));
  }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
from math import gcd

# Function to find the maximum common
# difference of an AP such that arr[]
# is a subsequence of that AP
def MaxComDiffSubAP(arr, N):

    # Stores maximum common difference
    # of an AP with given conditions
    maxCD = 0

    # Traverse the array
    for i in range(N - 1):

        # Update maxCD
        maxCD = gcd(maxCD, arr[i + 1] - arr[i])

    return maxCD

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 3, 7, 9 ]
    N = len(arr)

    print(MaxComDiffSubAP(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Recursive function to return
// gcd of a and b
static int gcd(int a, int b)
{

    // Everything divides 0
    if (a == 0)
        return b;
    if (b == 0)
        return a;

    // base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return gcd(a - b, b);

    return gcd(a, b - a);
}

// Function to find the maximum common
// difference of an AP such that arr[]
// is a subsequence of that AP
static int MaxComDiffSubAP(int[] arr, int N)
{

    // Stores maximum common difference
    // of an AP with given conditions
    int maxCD = 0;

    // Traverse the array
    for(int i = 0; i < N - 1; i++)
    {

        // Update maxCD
        maxCD = gcd(maxCD,
                    arr[i + 1] - arr[i]);
    }
    return maxCD;
}

// Driver Code
public static void Main ()
{
    int[] arr = { 1, 3, 7, 9 };
    int N = arr.Length;

    Console.WriteLine(MaxComDiffSubAP(arr, N));
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Recursive function to return gcd of a and b
function gcd(a, b)
{

    // Everything divides 0
    if (a == 0)
        return b;
    if (b == 0)
        return a;

    // base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return gcd(a - b, b);

    return gcd(a, b - a);
}

// Function to find the maximum common
// difference of an AP such that arr[]
// is a subsequence of that AP
function MaxComDiffSubAP(arr, N)
{

    // Stores maximum common difference
    // of an AP with given conditions
    let maxCD = 0;

    // Traverse the array
    for(let i = 0; i < N - 1; i++)
    {

        // Update maxCD
        maxCD = gcd(maxCD,
                    arr[i + 1] - arr[i]);
    }
    return maxCD;
}

// Driver Code
let arr = [ 1, 3, 7, 9 ];
let N = arr.length;

document.write(MaxComDiffSubAP(arr, N));

// This code is contributed by splevel62

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)