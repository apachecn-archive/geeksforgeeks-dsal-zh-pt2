# 在第二个数组中找到额外的元素

> 原文:[https://www . geesforgeks . org/find-第二个数组中的额外元素/](https://www.geeksforgeeks.org/find-extra-element-in-the-second-array/)

给定两个数组 **A[]** 和 **B[]** 。第二阵 **B[]** 包含 **A[]** 除 **1** 外的所有元素。任务是找到额外的元素。
**举例:**

> **输入:** A[] = { 1，2，3 }，B[] = {1，2，3，4}
> **输出:** 4
> 元素 4 不在数组
> **输入:** A[] = {10，15，5}，B[] = {10，100，15，5}
> **输出:** 100

**天真的方法:**运行嵌套循环，在 **B[]** 中找到元素，而在 **A[]** 中则没有。该方法的时间复杂度为 **O(n <sup>2</sup> )** 。
**有效方法:**如果 **A[]** 和 **B[]** 的所有元素都被异或在一起，那么 **A[]** 的每个元素将给出 **0** ，其出现在 **B[]** 中，当与 **0** 异或时，额外的元素说 **X** 将给出 **(X 异或 0) = X**
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the extra
// element in B[]
int extraElement(int A[], int B[], int n)
{

    // To store the result
    int ans = 0;

    // Find the XOR of all the element
    // of array A[] and array B[]
    for (int i = 0; i < n; i++)
        ans ^= A[i];
    for (int i = 0; i < n + 1; i++)
        ans ^= B[i];

    return ans;
}

// Driver code
int main()
{
    int A[] = { 10, 15, 5 };
    int B[] = { 10, 100, 15, 5 };
    int n = sizeof(A) / sizeof(int);

    cout << extraElement(A, B, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the extra
    // element in B[]
    static int extraElement(int A[], int B[], int n)
    {

        // To store the result
        int ans = 0;

        // Find the XOR of all the element
        // of array A[] and array B[]
        for (int i = 0; i < n; i++)
            ans ^= A[i];
        for (int i = 0; i < n + 1; i++)
            ans ^= B[i];

        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        int A[] = { 10, 15, 5 };
        int B[] = { 10, 100, 15, 5 };
        int n = A.length;

        System.out.println(extraElement(A, B, n));
    }
}

// This code is contributed by kanugargng
```

## 蟒蛇 3

```
# Python3 implementation of the approach
# Function to return the extra
# element in B[]
def extraElement(A, B, n):

    # To store the result
    ans = 0;

    # Find the XOR of all the element
    # of array A[] and array B[]
    for i in range(n):
        ans ^= A[i];
    for i in range(n + 1):
        ans ^= B[i];

    return ans;

# Driver code
A = [ 10, 15, 5 ];
B = [ 10, 100, 15, 5 ];
n = len(A);

print(extraElement(A, B, n));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the extra
    // element in B[]
    static int extraElement(int []A,
                            int []B, int n)
    {

        // To store the result
        int ans = 0;

        // Find the XOR of all the element
        // of array A[] and array B[]
        for (int i = 0; i < n; i++)
            ans ^= A[i];
        for (int i = 0; i < n + 1; i++)
            ans ^= B[i];

        return ans;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int []A = { 10, 15, 5 };
        int []B = { 10, 100, 15, 5 };
        int n = A.Length;

        Console.WriteLine(extraElement(A, B, n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the extra
// element in B[]
function extraElement(A, B, n)
{

    // To store the result
    let ans = 0;

    // Find the XOR of all the element
    // of array A[] and array B[]
    for (let i = 0; i < n; i++)
        ans ^= A[i];
    for (let i = 0; i < n + 1; i++)
        ans ^= B[i];

    return ans;
}

// Driver code
    let A = [ 10, 15, 5 ];
    let B = [ 10, 100, 15, 5 ];
    let n = A.length;

    document.write(extraElement(A, B, n));

// This code is contributed by subhammahato348.
</script>
```

**Output:** 

```
100
```

**时间复杂度:**O(N)
T3】空间复杂度: O(1)