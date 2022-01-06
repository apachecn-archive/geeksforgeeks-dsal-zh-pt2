# 对元素对进行计数，使得它们的“或”中的设置位的数量为 B[i]

> 原文:[https://www . geeksforgeeks . org/count-对元素进行计数-这样设置位的数量-in-or-is-bi/](https://www.geeksforgeeks.org/count-pairs-of-elements-such-that-number-of-set-bits-in-their-or-is-bi/)

给定两个分别由 **N** 元素组成的数组 **A[]** 和 **B[]** 。任务是找到索引对 **(i，j)** 的数量，使得 **i ≤ j** 和 **F(A[i] | A[j]) = B[j]** ，其中 **F(X)** 是 **X** 的二进制表示中的设置位的计数。
**示例**

> **输入:** A[] = {5，3，2，4，6，1}，B[] = {2，2，1，4，2，3}
> **输出:** 7
> 所有可能的对都是(5，5)，(3，3)，(2，2)，
> (2，6)，(4，6)，(6，6)和(6，1)。
> **输入:** A[] = {4，3，5，6，7}，B[] = {1，3，2，4，5}
> **输出:** 4

**方法:**迭代所有可能的对(I，j)，并检查它们的或值中设置位的计数。如果计数等于 B[j]，则增加计数。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of pairs
// which satisfy the given condition
int solve(int A[], int B[], int n)
{
    int cnt = 0;

    for (int i = 0; i < n; i++)
        for (int j = i; j < n; j++)

            // Check if the count of set bits
            // in the OR value is B[j]
            if (__builtin_popcount(A[i] | A[j]) == B[j]) {
                cnt++;
            }

    return cnt;
}

// Driver code
int main()
{
    int A[] = { 5, 3, 2, 4, 6, 1 };
    int B[] = { 2, 2, 1, 4, 2, 3 };
    int size = sizeof(A) / sizeof(A[0]);

    cout << solve(A, B, size);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count of pairs
// which satisfy the given condition
static int solve(int A[], int B[], int n)
{
    int cnt = 0;

    for (int i = 0; i < n; i++)
        for (int j = i; j < n; j++)

            // Check if the count of set bits
            // in the OR value is B[j]
            if (Integer.bitCount(A[i] | A[j]) == B[j])
            {
                cnt++;
            }

    return cnt;
}

// Driver code
public static void main(String args[])
{
    int A[] = { 5, 3, 2, 4, 6, 1 };
    int B[] = { 2, 2, 1, 4, 2, 3 };
    int size = A.length;

    System.out.println(solve(A, B, size));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of pairs
# which satisfy the given condition
def solve(A, B, n) :

    cnt = 0;
    for i in range(n) :
        for j in range(i, n) :

            # Check if the count of set bits
            # in the OR value is B[j]
            if (bin(A[i] | A[j]).count('1') == B[j]) :
                cnt += 1;

    return cnt

# Driver code
if __name__ == "__main__" :

    A = [ 5, 3, 2, 4, 6, 1 ];
    B = [ 2, 2, 1, 4, 2, 3 ];
    size = len(A);

    print(solve(A, B, size));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of pairs
// which satisfy the given condition
static int solve(int []A, int []B, int n)
{
    int cnt = 0;

    for (int i = 0; i < n; i++)
        for (int j = i; j < n; j++)

            // Check if the count of set bits
            // in the OR value is B[j]
            if (bitCount(A[i] | A[j]) == B[j])
            {
                cnt++;
            }

    return cnt;
}

static int bitCount(long x)
{
    // To store the count
    // of set bits
    int setBits = 0;
    while (x != 0)
    {
        x = x & (x - 1);
        setBits++;
    }
    return setBits;
}

// Driver code
public static void Main(String []args)
{
    int []A = { 5, 3, 2, 4, 6, 1 };
    int []B = { 2, 2, 1, 4, 2, 3 };
    int size = A.Length;

    Console.WriteLine(solve(A, B, size));
}
}

/* This code is contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the count of pairs
// which satisfy the given condition
function solve(A,B,n)
{
    let cnt = 0;

    for (let i = 0; i < n; i++)
        for (let j = i; j < n; j++)

            // Check if the count of set bits
            // in the OR value is B[j]
            if (bitCount(A[i] | A[j]) == B[j])
            {
                cnt++;
            }

    return cnt;
}

function bitCount(x)
{
    // To store the count
    // of set bits
    let setBits = 0;
    while (x != 0)
    {
        x = x & (x - 1);
        setBits++;
    }
    return setBits;
}

// Driver code
let A=[5, 3, 2, 4, 6, 1 ];
let B=[2, 2, 1, 4, 2, 3 ];
let size = A.length;
document.write(solve(A, B, size));

// This code is contributed by rag2127

</script>
```

**Output:** 

```
7
```