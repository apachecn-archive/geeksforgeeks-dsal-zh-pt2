# 给定数字之间的最小位交换，使其按位“或”等于按位“与”

> 原文:[https://www . geeksforgeeks . org/给定数字之间的最小位交换使其按位或等于按位与/](https://www.geeksforgeeks.org/minimum-bit-swaps-between-given-numbers-to-make-their-bitwise-or-equal-to-bitwise-and/)

给定两个正整数 **A** 和 **B，**的任务是计算所需的最小操作数，使得 **A** 和 **B** 的[按位 OR](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 等于 **A** 和 **B** 的[按位 AND](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 相等，即 **(A & B)=(A|B)** ，其中， 在每个操作中，选择两个索引 **i** 和 **j** ，并将 **A** 的 **i <sup>第</sup>位**位<sup>和</sup>位与 **B 的 **j <sup>第</sup>位**位交换。如果无法使**(A&B)=(A | B)**打印-1。**

**示例:**

> **输入:** A = 1，B = 2
> **输出:** 2
> **说明:**
> A<sub>10</sub>01<sub>2</sub>，B<sub>10</sub>10<sub>2</sub>T17】可以进行以下顺序的移动:
> 
> *   i = 1，j = 1⇒ A = 11， B = 00 （A|B = 3，A&B = 0）。
> *   i = 1，j = 0⇒ A = 01， B = 01 （A|B = 1，A&B = 1）。
> 
> 因此，需要 2 次移动。
> 
> **输入:** A = 27，B = 5
> **输出:** 3
> **说明:**
> A<sub>10</sub>≡11011<sub>2</sub>，B<sub>10</sub>≡00101<sub>2</sub>
> 可进行以下顺序的移动:
> 
> *   i = 4，j = 3⇒ A = 01011， B = 01101 （A|B = 15，A&B = 9）。
> *   i = 2.j = 2⇒ A = 01111， B = 01001 （A|B = 15，A&B = 9）。
> *   i = 2，j = 1⇒ A = 01011， B = 01011 （A|B = 11，A&B = 11）。
> 
> 因此，需要 3 次移动。

**逼近** :
**观察:**解决这个问题的主要观察是，对于(A & B)=(A|B)来说，A 必须等于 B，因为如果只设置了两位，那么只有它们的[按位 AND](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 和[按位 OR](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 相等。

按照以下步骤解决问题:

1.  [统计 **A** 和 **B** 中的总设定位数](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)。
2.  如果计数是奇数，这两个数字不能相等，所以打印-1。
3.  初始化两个计数器**一零** =0 和**零一** =0
4.  遍历 **A** 和 **B** 的位，并执行以下操作:
    *   如果 **A** 的当前位被置位，而 **B** 的当前位未置位，即(1，0)，则增加**一零**。
    *   如果 **A** 的当前位未置位且 **B** 的当前位被置位，即(0，1)，则递增**零一**。
5.  为了使所需操作的数量最小化，最好选择两个(1，0)或两个(0，1)索引，并交换其中的任何一个，即只需要一半的 **oneZero** 和 **zeroOne** 操作。
6.  如果 **oneZero** 是奇数(这意味着 **zeroOne** 也是奇数)，将需要两个以上的操作来将(0，1)和(1，0)转到(1，1)和(0，0)
7.  那么，最终的答案是**(one zero/2)+(zero one/2)+(one zero % 2？2:0).**

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;
// Function for counting number of set bit
int countSetBits(int n)
{
    int count = 0;
    while (n) {
        n = n & (n - 1);
        count++;
    }
    return count;
}
// Function to return the count of
// minimum operations required
int minOperations(int A, int B)
{
    // cnt to count the number of bits
    // set in A and in B
    int cnt1 = 0, cnt2 = 0;
    cnt1 += countSetBits(A);
    cnt2 += countSetBits(B);

    // if odd numbers of total set bits
    if ((cnt1 + cnt2) % 2 != 0)
        return -1;
    // one_zero = 1 in A and 0 in B at ith bit
    // similarly for zero_one
    int oneZero = 0, zeroOne = 0;
    int ans = 0;

    for (int i = 0; i < max(cnt1, cnt2); i++) {
        int bitpos = 1 << i;
        // When bitpos is set in B, unset in B
        if ((!(bitpos & A)) && (bitpos & B))
            zeroOne++;
        // When bitpos is set in A, unset in B
        if ((bitpos & A) && (!(bitpos & B)))
            oneZero++;
    }
    // number of moves is half of
    // number pairs of each group
    ans = (zeroOne / 2) + (oneZero / 2);
    // odd number pairs
    if (zeroOne % 2 != 0)
        ans += 2;

    return ans;
}

// Driver code
int main()
{

    // Input
    int A = 27, B = 5;

    // Function call to compute the result
    cout << minOperations(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG{

// Function for counting number of set bit
static int countSetBits(int n)
{
    int count = 0;
    while (n != 0) {
        n = n & (n - 1);
        count++;
    }
    return count;
}
// Function to return the count of
// minimum operations required
static int minOperations(int A, int B)
{

    // cnt to count the number of bits
    // set in A and in B
    int cnt1 = 0, cnt2 = 0;
    cnt1 += countSetBits(A);
    cnt2 += countSetBits(B);

    // if odd numbers of total set bits
    if ((cnt1 + cnt2) % 2 != 0)
        return -1;

    // one_zero = 1 in A and 0 in B at ith bit
    // similarly for zero_one
    int oneZero = 0, zeroOne = 0;
    int ans = 0;

    for (int i = 0; i < Math.max(cnt1, cnt2); i++) {
        int bitpos = 1 << i;

        // When bitpos is set in B, unset in B
        if (((bitpos & A) == 0) && ((bitpos & B) != 0))
            zeroOne++;

        // When bitpos is set in A, unset in B
        if (((bitpos & A) != 0) && ((bitpos & B) == 0))
            oneZero++;
    }
    // number of moves is half of
    // number pairs of each group
    ans = (zeroOne / 2) + (oneZero / 2);

    // odd number pairs
    if (zeroOne % 2 != 0)
        ans += 2;

    return ans;
}

// Driver Code
public static void main(String args[])
{

    // Input
    int A = 27, B = 5;

    // Function call to compute the result
    System.out.println( minOperations(A, B));
}
}

// This code is contributed by splevel62.
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function for counting number of set bit
def countSetBits(n):

    count = 0
    while (n):
        n = n & (n - 1)
        count += 1

    return count

# Function to return the count of
# minimum operations required
def minOperations(A, B):

    # cnt to count the number of bits
    # set in A and in B
    cnt1 = 0
    cnt2 = 0
    cnt1 += countSetBits(A)
    cnt2 += countSetBits(B)

    # If odd numbers of total set bits
    if ((cnt1 + cnt2) % 2 != 0):
        return -1

    # one_zero = 1 in A and 0 in B at ith bit
    # similarly for zero_one
    oneZero = 0
    zeroOne = 0
    ans = 0

    for i in range(max(cnt1, cnt2)):
        bitpos = 1 << i

        # When bitpos is set in B, unset in B
        if ((not(bitpos & A)) and (bitpos & B)):
            zeroOne += 1

        # When bitpos is set in A, unset in B
        if ((bitpos & A) and (not(bitpos & B))):
            oneZero += 1

    # Number of moves is half of
    # number pairs of each group
    ans = (zeroOne // 2) + (oneZero // 2)

    # Odd number pairs
    if (zeroOne % 2 != 0):
        ans += 2

    return ans

# Driver code
if __name__ == '__main__':

    # Input
    A = 27
    B = 5

    # Function call to compute the result
    print(minOperations(A, B))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function for counting number of set bit
static int countSetBits(int n)
{
    int count = 0;
    while (n > 0)
    {
        n = n & (n - 1);
        count++;
    }
    return count;
}

// Function to return the count of
// minimum operations required
static int minOperations(int A, int B)
{

    // cnt to count the number of bits
    // set in A and in B
    int cnt1 = 0, cnt2 = 0;
    cnt1 += countSetBits(A);
    cnt2 += countSetBits(B);

    // If odd numbers of total set bits
    if ((cnt1 + cnt2) % 2 != 0)
        return -1;

    // one_zero = 1 in A and 0 in B at ith bit
    // similarly for zero_one
    int oneZero = 0, zeroOne = 0;
    int ans = 0;

    for(int i = 0; i < Math.Max(cnt1, cnt2); i++)
    {
        int bitpos = 1 << i;

        // When bitpos is set in B, unset in B
        if (((bitpos & A) == 0) && (bitpos & B) != 0)
            zeroOne++;

        // When bitpos is set in A, unset in B
        if ((bitpos & A) != 0 && ((bitpos & B) == 0))
            oneZero++;
    }

    // Number of moves is half of
    // number pairs of each group
    ans = (zeroOne / 2) + (oneZero / 2);

    // Odd number pairs
    if (zeroOne % 2 != 0)
        ans += 2;

    return ans;
}

// Driver code
public static void Main()
{

    // Input
    int A = 27, B = 5;

    // Function call to compute the result
    Console.Write(minOperations(A, B));
}
}

// This code is contributed by bgangwar59
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function for counting number of set bit
function countSetBits(n)
{
    let count = 0;
    while (n) {
        n = n & (n - 1);
        count++;
    }
    return count;
}
// Function to return the count of
// minimum operations required
function minOperations(A, B)
{
    // cnt to count the number of bits
    // set in A and in B
    let cnt1 = 0, cnt2 = 0;
    cnt1 += countSetBits(A);
    cnt2 += countSetBits(B);

    // if odd numbers of total set bits
    if ((cnt1 + cnt2) % 2 != 0)
        return -1;
    // one_zero = 1 in A and 0 in B at ith bit
    // similarly for zero_one
    let oneZero = 0, zeroOne = 0;
    let ans = 0;

    for (let i = 0; i < Math.max(cnt1, cnt2); i++) {
        let bitpos = 1 << i;
        // When bitpos is set in B, unset in B
        if ((!(bitpos & A)) && (bitpos & B))
            zeroOne++;
        // When bitpos is set in A, unset in B
        if ((bitpos & A) && (!(bitpos & B)))
            oneZero++;
    }
    // number of moves is half of
    // number pairs of each group
    ans = parseInt(zeroOne / 2) + parseInt(oneZero / 2);
    // odd number pairs
    if (zeroOne % 2 != 0)
        ans += 2;

    return ans;
}

// Driver code

    // Input
    let A = 27, B = 5;

    // Function call to compute the result
    document.write(minOperations(A, B));

</script>
```

**Output**

```
3
```

***时间复杂度:**O(Log<sub>2</sub>N)*
***辅助空间:** O(1)*