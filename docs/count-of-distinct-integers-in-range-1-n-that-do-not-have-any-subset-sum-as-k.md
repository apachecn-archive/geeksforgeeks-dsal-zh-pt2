# 范围[1，N]内不具有任何子集和的不同整数的计数为 K

> 原文:[https://www . geeksforgeeks . org/范围内非重复整数计数-1-n-不具有任何子集-和-as-k/](https://www.geeksforgeeks.org/count-of-distinct-integers-in-range-1-n-that-do-not-have-any-subset-sum-as-k/)

给定两个正整数 **N** 和 **K** ，使得 **K≤N，**的任务是在**【1，N】**的范围内找到不同整数的最大数量，该范围没有和等于 **K** 的子集。如果有多个解决方案，请打印任何一个。

**示例:**

> **输入:** N = 5，K = 3
> **输出:** 1 4 5
> **说明:**有两组大小为 3 的不同数字，它们没有任何子集和为 3。
> 分别是{1，4，5}和{2，4，5}。所以，按任何顺序打印它们。
> 
> **输入:** N = 1，K = 1
> T3】输出: 0

**方法:**该想法基于以下观察:

*   任何大于 **K** 的数都可以被选择，因为它们永远不能贡献给其和为 **K** 的子集。
*   **K** 不能选择。
*   对于小于 **K** 的数字，最多可以选择 **K/2** 的数字。例如:
    *   如果 **K** =5，1+4=5，2+3=5，那么可以选择 1 或 4，同样也可以选择 2 或 3。因此，最多可以选择(5/2=2)个数字。
    *   如果 **K** =6，1+5=6，2+4=6，3+3=6。同样，可以选择 3 个数字，使得没有子集和等于 6。3 总是可以被选择的，因为只有不同的数字被选择，1 或 5 以及类似的 2 或 4 都可以被选择。因此，最多可以选择(6/3=3)个数字。
*   因此，可以选择的不同数字的最大数量是 **(N-K)+(K/2)** 。

按照以下步骤解决问题:

*   可以选择的最大不同位数是 **(N-K)+(K/2)** 。
*   所有大于 **K** 的数字都需要选择，即 **N-K** 从末尾开始数。 **K/2** 元素少于 **K** 也需要选择。
*   因此，一个可能的解决方案是选择 **(N-K)+(K/2)** 个连续的数字，从 **N** 开始，不包括 **K** 。
*   最简单的方法是创建一个[数组](https://www.geeksforgeeks.org/array-data-structure/)，存储从 **1** 到 **N** 的所有值，除了 **K** 、[反转数组](https://www.geeksforgeeks.org/write-a-program-to-reverse-an-array-or-string/)，从头开始打印 **(N-K)+(K/2)** 元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum number of distinct integers
// in [1, N] having no subset with sum equal to K
void findSet(int N, int K)
{
    // Declare a vector to store
    // the required numbers
    vector<int> a;

    // Store all the numbers in [1, N] except K
    for (int i = 1; i <= N; i++) {
        if (i != K)
            a.push_back(i);
    }

    // Store the maximum number
    // of distinct numbers
    int MaxDistinct = (N - K) + (K / 2);

    // Reverse the array
    reverse(a.begin(), a.end());

    // Print the required numbers
    for (int i = 0; i < MaxDistinct; i++)
        cout << a[i] << " ";
}

// Driver Code
int main()
{
    // Given Input
    int N = 5, K = 3;

    // Function Call
    findSet(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find maximum number of distinct
// integers in [1, N] having no subset with
// sum equal to K
static void findSet(int N, int K)
{

    // Declare a vector to store
    // the required numbers
    ArrayList<Integer> a = new ArrayList<Integer>();

    // Store all the numbers in [1, N] except K
    for(int i = 1; i <= N; i++)
    {
        if (i != K)
            a.add(i);
    }

    // Store the maximum number
    // of distinct numbers
    int MaxDistinct = (N - K) + (K / 2);

    // Reverse the array
    Collections.reverse(a);

    // Print the required numbers
    for(int i = 0; i < MaxDistinct; i++)
        System.out.print(a.get(i) + " ");
}

// Driver Code
public static void main(String[] args)
{

    // Given Input
    int N = 5, K = 3;

    // Function Call
    findSet(N, K);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find maximum number of distinct
# integers in [1, N] having no subset with
# sum equal to K
def findSet(N, K):

    # Declare a vector to store
    # the required numbers
    a = []

    # Store all the numbers in [1, N] except K
    for i in range(1, N + 1):
        if (i != K):
            a.append(i)

    # Store the maximum number
    # of distinct numbers
    MaxDistinct = (N - K) + (K // 2)

    # Reverse the array
    a = a[::-1]

    # Print the required numbers
    for i in range(MaxDistinct):
        print(a[i], end = " ")

# Driver Code
if __name__ == '__main__':

    # Given Input
    N = 5
    K = 3

    # Function Call
    findSet(N, K)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find maximum number of distinct
// integers in [1, N] having no subset with
// sum equal to K
static void findSet(int N, int K)
{

    // Declare a vector to store
    // the required numbers
    List<int> a = new List<int>();

    // Store all the numbers in [1, N] except K
    for(int i = 1; i <= N; i++)
    {
        if (i != K)
            a.Add(i);
    }

    // Store the maximum number
    // of distinct numbers
    int MaxDistinct = (N - K) + (K / 2);

    // Reverse the array
    a.Reverse();

    // Print the required numbers
    for(int i = 0; i < MaxDistinct; i++)
        Console.Write(a[i] + " ");
}

// Driver Code
public static void Main()
{
    // Given Input
    int N = 5, K = 3;

    // Function Call
    findSet(N, K);
}
}

// This code is contributed by avijitmondal1998.
```

## java 描述语言

```
  <script>

// JavaScript program for the above approach

// Function to find maximum number of distinct integers
// in [1, N] having no subset with sum equal to K
function findSet( N,  K)
{
    // Declare a vector to store
    // the required numbers
    let a = [];

    // Store all the numbers in [1, N] except K
    for (let i = 1; i <= N; i++) {
        if (i != K)
            a.push(i);
    }

    // Store the maximum number
    // of distinct numbers
    let MaxDistinct = (N - K) + parseInt(K / 2);

    // Reverse the array
    a.reverse();
    // Print the required numbers
    for (let i = 0; i < MaxDistinct; i++)
        document.write(a[i]+" ");
}

// Driver Code
// Given Input
    let N = 5, K = 3;

    // Function Call
    findSet(N, K);

  // This code is contributed by Potta Lokesh

</script>
```

**Output**

```
5 4 2 
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)