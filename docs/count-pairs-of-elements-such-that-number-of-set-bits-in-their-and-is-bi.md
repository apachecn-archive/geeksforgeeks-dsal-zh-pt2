# 对元素对进行计数，使得它们的“与”中的设置位的数量为 B[i]

> 原文:[https://www . geeksforgeeks . org/count-对元素进行计数-这样，它们的集位数是-bi/](https://www.geeksforgeeks.org/count-pairs-of-elements-such-that-number-of-set-bits-in-their-and-is-bi/)

给定两个分别由 **N** 元素组成的数组 **A[]** 和 **B[]** 。任务是找到索引对 **(i，j)** 的数量，使得 **i ≤ j** 和 **F(A[i] & A[j]) = B[j]** ，其中 **F(X)** 是 **X** 的二进制表示中的设置位的计数。
**举例:**

> **输入:** A[] = {2，3，1，4，5}，B[] = {2，2，1，4，2}
> **输出:** 4
> 所有可能的对都是(3，3)，(3，1)，(1，1)和(5，5)
> **输入:** A[] = {1，2，3，4，5}，B[] = {2，2，2，2，2}
> **输出:【T11**

**方法:**迭代所有可能的对(I，j)，并检查它们的“与”值中的设置位的计数。如果计数等于 B[j]，则增加计数。
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
            // in the AND value is B[j]
            if (__builtin_popcount(A[i] & A[j]) == B[j]) {
                cnt++;
            }

    return cnt;
}

// Driver code
int main()
{
    int A[] = { 2, 3, 1, 4, 5 };
    int B[] = { 2, 2, 1, 4, 2 };
    int size = sizeof(A) / sizeof(A[0]);

    cout << solve(A, B, size);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GFG
{

    // Function to return the count of pairs
    // which satisfy the given condition
    static int solve(int A[], int B[], int n)
    {
        int cnt = 0;

        for (int i = 0; i < n; i++)
        {
            for (int j = i; j < n; j++) // Check if the count of set bits
            // in the AND value is B[j]
            {
                if (Integer.bitCount(A[i] & A[j]) == B[j])
                {
                    cnt++;
                }
            }
        }

        return cnt;
    }

    // Driver code
    public static void main(String[] args)
    {
        int A[] = {2, 3, 1, 4, 5};
        int B[] = {2, 2, 1, 4, 2};
        int size = A.length;

        System.out.println(solve(A, B, size));
    }
}

/* This code contributed by PrinciRaj1992 */
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
            # in the AND value is B[j]
            c = A[i] & A[j]
            if (bin(c).count('1') == B[j]) :
                cnt += 1;
    return cnt;

# Driver code
if __name__ == "__main__" :

    A = [ 2, 3, 1, 4, 5 ];
    B = [ 2, 2, 1, 4, 2 ];

    size = len(A);

    print(solve(A, B, size));

# This code is contributed
# by AnkitRai01
```

## C#

```
// C# Implementation of the above approach
using System;

class GFG
{

    // Function to return the count of pairs
    // which satisfy the given condition
    static int solve(int []A, int []B, int n)
    {
        int cnt = 0;

        for (int i = 0; i < n; i++)
        {
            for (int j = i; j < n; j++)
            // Check if the count of set bits
            // in the AND value is B[j]
            {
                if (countSetBits(A[i] & A[j]) == B[j])
                {
                    cnt++;
                }
            }
        }

        return cnt;
    }

    // Function to get no of set
    // bits in binary representation
    // of positive integer n
    static int countSetBits(int n)
    {
        int count = 0;
        while (n > 0)
        {
            count += n & 1;
            n >>= 1;
        }
        return count;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []A = {2, 3, 1, 4, 5};
        int []B = {2, 2, 1, 4, 2};
        int size = A.Length;

        Console.WriteLine(solve(A, B, size));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript Implementation of the above approach

// Function to return the count of pairs
// which satisfy the given condition
function solve(A, B, n)
{
    var cnt = 0;
    for (var i = 0; i < n; i++)
    {
        for (var j = i; j < n; j++)

        // Check if the count of set bits
        // in the AND value is B[j]
        {
            if (countSetBits(A[i] & A[j]) == B[j])
            {
                cnt++;
            }
        }
    }
    return cnt;
}

// Function to get no of set
// bits in binary representation
// of positive integer n
function countSetBits(n)
{
    var count = 0;
    while (n > 0)
    {
        count += n & 1;
        n >>= 1;
    }
    return count;
}

// Driver code
var A = [2, 3, 1, 4, 5];
var B = [2, 2, 1, 4, 2];
var size = A.length;
document.write(solve(A, B, size));

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
4
```

时间复杂度:O(n <sup>2</sup> )

辅助空间:0(1)