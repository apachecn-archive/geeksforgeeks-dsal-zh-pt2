# 创建一个数组，使得长度为 K 的子数组的异或为 X

> 原文:[https://www . geeksforgeeks . org/create-a-array-so-xor-of-length-k-is-x/](https://www.geeksforgeeks.org/create-an-array-such-that-xor-of-subarrays-of-length-k-is-x/)

给定三个整数 **N** 、 **K** 和 **X** ，任务是构造一个长度为 **N** 的数组，其中每个长度为 **K** 的相邻子数组的所有元素的**异或**为 **X** 。
**举例:**

> **输入:** N = 5，K = 1，X = 4
> **输出:** 4 4 4 4 4
> **说明:**
> 长度为 1 的每个子阵都有等于 4 的 Xor 值。
> **输入:** N = 5，K = 2，X = 4
> **输出:** 4 0 4 0 4
> **说明:**
> 长度为 2 的每个子阵都有等于 4 的 Xor 值。

**进场:**
要解决上面提到的问题，我们需要按照下面给出的步骤:

*   [任意数字的逐位异或](https://www.geeksforgeeks.org/tag/xor/)， **X** 与 **0** 等于数字本身。所以，如果我们将数组的第一个元素 **A** 设置为 X，下一个**K–1**元素设置为 **0** ，那么我们将对长度为 K 的第一个子数组的元素进行异或运算，等于 X。
*   如果我们将 **A[K]** 设置为 **A[0]** ，那么我们将有 XOR(A[1]，…，A[K]) = X。同样，如果我们将 **A[K + 1]** 设置为 **A[1]** ，那么我们将有 XOR(A[2]，…，A[K+1]) = X
*   继续以这种方式，我们可以观察到通式可以描述如下:

以下是上述方法的实现:

## C++

```
// C++ implementation to Create an array
// in which the XOR of all elements of
// each contiguous sub-array of
// length K is X

#include <bits/stdc++.h>
using namespace std;

// Function to construct the array
void constructArray(int N, int K, int X)
{

    // Creating a vector of size K,
    // initialised with 0
    vector<int> ans(K, 0);

    // Initialising the first element
    // with the given XOR
    ans[0] = X;

    for (int i = 0; i < N; ++i) {
        cout << ans[i % K] << " ";
    }

    cout << endl;
}

// Driver code
int main()
{
    int N = 5, K = 2, X = 4;

    constructArray(N, K, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to create an array
// in which the XOR of all elements of
// each contiguous sub-array of
// length K is X
class GFG{

// Function to construct the array
public static void constructArray(int N, int K,
                                         int X)
{

    // Creating an array of size K,
    // initialised with 0
    int[] ans = new int[K];

    // Initialising the first element
    // with the given XOR
    ans[0] = X;

    for(int i = 0; i < N; ++i)
    {
       System.out.print(ans[i % K] + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    int N = 5, K = 2, X = 4;

    constructArray(N, K, X);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 implementation to create an array
# in which the XOR of all elements of
# each contiguous sub-array of
# length K is X

# Function to construct the array
def constructArray(N, K, X):

    # Creating a list of size K,
    # initialised with 0
    ans = []

    for i in range(0, K):
        ans.append(0)

    # Initialising the first element
    # with the given XOR
    ans[0] = X

    for i in range(0, N):
        print(ans[i % K], end = " ")

# Driver code
N = 5
K = 2
X = 4

# Function call
constructArray(N, K, X)

# This code is contributed by ishayadav181
```

## C#

```
// C# implementation to create an array
// in which the XOR of all elements of
// each contiguous sub-array of
// length K is X
using System;

class GFG{

// Function to construct the array
public static void constructArray(int N, int K,
                                         int X)
{

    // Creating an array of size K,
    // initialised with 0
    int[] ans = new int[K];

    // Initialising the first element
    // with the given XOR
    ans[0] = X;

    for(int i = 0; i < N; ++i)
    {
        Console.Write(ans[i % K] + " ");
    }
}

// Driver code
public static void Main(string[] args)
{
    int N = 5, K = 2, X = 4;

    constructArray(N, K, X);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript implementation to Create an array
// in which the XOR of all elements of
// each contiguous sub-array of
// length K is X

// Function to construct the array
function constructArray(N, K, X)
{

    // Creating a vector of size K,
    // initialised with 0
    let ans = new Array(K).fill(0);

    // Initialising the first element
    // with the given XOR
    ans[0] = X;

    for (let i = 0; i < N; ++i) {
        document.write(ans[i % K] + " ");
    }

    document.write("<br>");
}

// Driver code
    let N = 5, K = 2, X = 4;

    constructArray(N, K, X);

</script>
```

**Output:** 

```
4 0 4 0 4
```

**时间复杂度:**O(N)
T3】辅助空间: O(K)