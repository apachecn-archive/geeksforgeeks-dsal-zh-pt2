# 两个数组异或之间偶设置位的计数

> 原文:[https://www . geeksforgeeks . org/两个数组异或的偶集位数/](https://www.geeksforgeeks.org/count-of-even-set-bits-between-xor-of-two-arrays/)

给定两个分别具有 **N** 和 **M** 正元素的[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/) **A[]和 B[]** 。任务是计算数组 A 中的元素数量，对于数组 b 中的每个元素，在异或运算中设置偶数个位。
**示例:**

> **输入:** A[] = { 4，2，15，9，8，8 }，B[] = { 3，4，22 }
> **输出:**2 4 4
> T6】解释:
> A 元素的二进制表示为:100，10，1111，1001，1000，1000
> B 元素的二进制表示为:11，101，1010
> 现在
> 3^4 = 11^100 = 111
> 3^2 = 11^10 = 01
> 3^15 = 11^1111 = 1100
> 3^9 = 11^1001 = 1111
> 3 8 = 11 1000 = 1011
> 3 8 = 11 1000 = 1011
> a[]中只有 2 个元素{15，9}存在于元素 3 中，因此 XOR 之后的设置位计数为偶数。 所以计数是 2。
> 同样，元素 4 和 22 的计数为 4。
> **输入:** A[] = { 1，2，3，4，5，6，7，8，9，10 }，B[] = { 4 }
> **输出:** 5
> **解释:**
> A[]中的元素使得异或后的设置位计数为偶数为{ 1，2，4，7，8}。所以计数是 5。

**天真方法:**想法是计算[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**B【】**中每个元素与数组**A【】**中每个元素的异或，并计算偶数设置位的个数。
**时间复杂度:** O(N*M)，其中 N 和 M 分别是数组 **A[]** 和 **B[]** 的长度。
**高效方法:**思路是利用异或的性质。对于任何两个数字，如果两个数字的设置位计数都是偶数或奇数，那么两个数字异或后的设置位计数是**偶数**。
以下是基于上述属性的步骤:

1.  计算具有偶数(比如说 **a** )和奇数(比如说 **b** )组比特数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**中的元素数。
2.  对于数组中的每个元素 **B[]** :
    *   如果当前元素具有偶数计数的设置位，则与当前元素具有偶数计数的设置位异或的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**中的数字元素为 **a** 。
    *   如果当前元素有奇数个设置位，那么与当前元素异或偶数个设置位的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **中的数字元素为 **b** 。**

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that count the XOR of B[]
// with all the element in A[] having
// even set bit
void countEvenBit(int A[], int B[], int n, int m)
{
    int i, j, cntOdd = 0, cntEven = 0;
    for (i = 0; i < n; i++) {

        // Count the set bits in A[i]
        int x = __builtin_popcount(A[i]);

        // check for even or Odd
        if (x & 1) {
            cntEven++;
        }
        else {
            cntOdd++;
        }
    }

    // To store the count of element for
    // B[] such that XOR with all the
    // element in A[] having even set bit
    int CountB[m];

    for (i = 0; i < m; i++) {

        // Count set bit for B[i]
        int x = __builtin_popcount(B[i]);

        // check for Even or Odd
        if (x & 1) {
            CountB[i] = cntEven;
        }
        else {
            CountB[i] = cntOdd;
        }
    }

    for (i = 0; i < m; i++) {
        cout << CountB[i] << ' ';
    }
}

// Driver Code
int main()
{
    int A[] = { 4, 2, 15, 9, 8, 8 };
    int B[] = { 3, 4, 22 };

    countEvenBit(A, B, 6, 3);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function that count the XOR of B[]
// with all the element in A[] having
// even set bit
static void countEvenBit(int A[], int B[], int n, int m)
{
    int i, j, cntOdd = 0, cntEven = 0;
    for (i = 0; i < n; i++) {

        // Count the set bits in A[i]
        int x = Integer.bitCount(A[i]);

        // check for even or Odd
        if (x % 2 == 1) {
            cntEven++;
        }
        else {
            cntOdd++;
        }
    }

    // To store the count of element for
    // B[] such that XOR with all the
    // element in A[] having even set bit
    int []CountB = new int[m];

    for (i = 0; i < m; i++) {

        // Count set bit for B[i]
        int x = Integer.bitCount(B[i]);

        // check for Even or Odd
        if (x%2 == 1) {
            CountB[i] = cntEven;
        }
        else {
            CountB[i] = cntOdd;
        }
    }

    for (i = 0; i < m; i++) {
        System.out.print(CountB[i] +" ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 4, 2, 15, 9, 8, 8 };
    int B[] = { 3, 4, 22 };

    countEvenBit(A, B, 6, 3);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that count the XOR of B
# with all the element in A having
# even set bit
def countEvenBit(A, B, n, m):

    i, j, cntOdd = 0, 0, 0
    cntEven = 0
    for i in range(n):

        # Count the set bits in A[i]
        x = bin(A[i])[2:].count('1')

        # check for even or Odd
        if (x & 1):
            cntEven += 1

        else :
            cntOdd += 1

    # To store the count of element for
    # B such that XOR with all the
    # element in A having even set bit
    CountB = [0]*m

    for i in range(m):

        # Count set bit for B[i]
        x = bin(B[i])[2:].count('1')

        # check for Even or Odd
        if (x & 1):
            CountB[i] = cntEven

        else:
            CountB[i] = cntOdd

    for i in range(m):
        print(CountB[i], end=" ")

# Driver Code
if __name__ == '__main__':

    A = [ 4, 2, 15, 9, 8, 8]
    B = [ 3, 4, 22 ]

    countEvenBit(A, B, 6, 3)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function that count the XOR of []B
// with all the element in []A having
// even set bit
static void countEvenBit(int []A, int []B, int n, int m)
{
    int i, cntOdd = 0, cntEven = 0;
    for (i = 0; i < n; i++)
    {

        // Count the set bits in A[i]
        int x = bitCount(A[i]);

        // check for even or Odd
        if (x % 2 == 1) {
            cntEven++;
        }
        else {
            cntOdd++;
        }
    }

    // To store the count of element for
    // []B such that XOR with all the
    // element in []A having even set bit
    int []CountB = new int[m];

    for (i = 0; i < m; i++) {

        // Count set bit for B[i]
        int x = bitCount(B[i]);

        // check for Even or Odd
        if (x % 2 == 1) {
            CountB[i] = cntEven;
        }
        else {
            CountB[i] = cntOdd;
        }
    }

    for (i = 0; i < m; i++) {
        Console.Write(CountB[i] +" ");
    }
}
static int bitCount(int x)
{
    int setBits = 0;
    while (x != 0) {
        x = x & (x - 1);
        setBits++;
    }
    return setBits;
}

// Driver Code
public static void Main(String[] args)
{
    int []A = { 4, 2, 15, 9, 8, 8 };
    int []B = { 3, 4, 22 };

    countEvenBit(A, B, 6, 3);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function that count the XOR of B[]
// with all the element in A[] having
// even set bit
function countEvenBit(A, B, n, m)
{
    let i, j, cntOdd = 0, cntEven = 0;
    for (i = 0; i < n; i++) {

        // Count the set bits in A[i]
        let x = bitCount(A[i]);

        // check for even or Odd
        if (x & 1) {
            cntEven++;
        }
        else {
            cntOdd++;
        }
    }

    // To store the count of element for
    // B[] such that XOR with all the
    // element in A[] having even set bit
    let CountB = new Array(m);

    for (i = 0; i < m; i++) {

        // Count set bit for B[i]
        let x = bitCount(B[i]);

        // check for Even or Odd
        if (x & 1) {
            CountB[i] = cntEven;
        }
        else {
            CountB[i] = cntOdd;
        }
    }

    for (i = 0; i < m; i++) {
        document.write(CountB[i] + " ");
    }
}

function bitCount(x)
{
    let setBits = 0;
    while (x != 0) {
        x = x & (x - 1);
        setBits++;
    }
    return setBits;
}

// Driver Code
    let A = [ 4, 2, 15, 9, 8, 8 ];
    let B = [ 3, 4, 22 ];

    countEvenBit(A, B, 6, 3);

</script>
```

**Output:** 

```
2 4 4
```

**时间复杂度:** O(N + M)，其中 N 和 M 分别是给定的两个数组的长度。