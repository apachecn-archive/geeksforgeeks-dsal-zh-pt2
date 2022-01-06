# 计算一个数的二进制表示中的 0 和 1 的程序

> 原文:[https://www . geeksforgeeks . org/c-程序对数字的二进制表示中的 0 和 1 进行计数/](https://www.geeksforgeeks.org/c-program-to-count-zeros-and-ones-in-binary-representation-of-a-number/)

给定一个数字 **N** ，任务是编写 [C 程序](https://www.geeksforgeeks.org/c-programming-language/)来统计 **N** 的[二进制表示中 **0s** 和 **1s** 的个数。](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)

**示例:**

> **输入:** N = 5
> **输出:**
> 计数 0:1
> 计数 1:2
> **说明:**5 的二进制表示为“101”。
> **输入:** N = 22
> **输出:**
> 计数为 0:2
> 计数为 1:3
> **说明:**22 的二进制表示为“10110”。

**方法 1–天真方法:**想法是迭代 **N** 的二进制表示中的所有位，如果当前位为**‘0’**则增加 **0s** 的计数，否则增加 **1s** 的计数。

下面是上述方法的实现:

## C

```
// C program for the above approach
#include <stdio.h>

// Function to count the number of 0s
// and 1s in binary representation of N
void count1s0s(int N)
{
    // Initialise count variables
    int count0 = 0, count1 = 0;

    // Iterate through all the bits
    while (N > 0) {

        // If current bit is 1
        if (N & 1) {
            count1++;
        }

        // If current bit is 0
        else {
            count0++;
        }

        N = N >> 1;
    }

    // Print the count
    printf("Count of 0s in N is %d\n", count0);
    printf("Count of 1s in N is %d\n", count1);
}

// Driver Code
int main()
{
    // Given Number
    int N = 9;

    // Function Call
    count1s0s(N);
    return 0;
}
```

**Output**

```
Count of 0s in N is 2
Count of 1s in N is 2
```

**时间复杂度:** *O(对数 N)*

**方法 2–递归方法:**上述方法也可以使用[递归](https://www.geeksforgeeks.org/recursion/)来实现。

下面是上述方法的实现:

## C

```
// C program for the above approach
#include <math.h>
#include <stdio.h>

// Recursive approach to find the
// number of set bit in 1
int recursiveCount(int N)
{

    // Base Case
    if (N == 0) {
        return 0;
    }

    // Return recursively
    return (N & 1) + recursiveCount(N >> 1);
}

// Function to find 1s complement
int onesComplement(int n)
{
    // Find number of bits in the
    // given integer
    int N = floor(log2(n)) + 1;

    // XOR the given integer with
    // pow(2, N) - 1
    return ((1 << N) - 1) ^ n;
}

// Function to count the number of 0s
// and 1s in binary representation of N
void count1s0s(int N)
{
    // Initialise the count variables
    int count0, count1;

    // Function call to find the number
    // of set bits in N
    count1 = recursiveCount(N);

    // Function call to find 1s complement
    N = onesComplement(N);

    // Function call to find the number
    // of set bits in 1s complement of N
    count0 = recursiveCount(N);

    // Print the count
    printf("Count of 0s in N is %d\n", count0);
    printf("Count of 1s in N is %d\n", count1);
}

// Driver Code
int main()
{
    // Given Number
    int N = 5;

    // Function Call
    count1s0s(N);
    return 0;
}
```

**Output**

```
Count of 0s in N is 1
Count of 1s in N is 2
```

**时间复杂度:** *O(对数 N)*

**方法 3–使用布莱恩·克尼根的算法**
我们可以通过以下步骤找到集合位的计数:

*   初始化计数至 **0** 。
*   如果 **N > 0** ，则更新 N 为**N&(N–1)**，因为这将从右侧取消设置最多的位，如下所示:

```
if N = 10;
Binary representation of N     = 1010
Binary representation of N - 1 = 1001
-------------------------------------
Logical AND of N and N - 1     = 1000
```

*   增加上述步骤的计数，并重复上述步骤，直到 N 变为 0。

要找到 N 的[二进制表示中 0 的计数，请找到 **N** 的](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)[补码](https://www.geeksforgeeks.org/1s-2s-complement-binary-number/)，并使用上述方法找到集合位的计数。

下面是上述方法的实现:

## C

```
// C program for the above approach
#include <math.h>
#include <stdio.h>

// Function to find 1s complement
int onesComplement(int n)
{
    // Find number of bits in the
    // given integer
    int N = floor(log2(n)) + 1;

    // XOR the given integer with
    // pow(2, N) - 1
    return ((1 << N) - 1) ^ n;
}

// Function to implement count of
// set bits using Brian Kernighan’s
// Algorithm
int countSetBits(int n)
{
    // Initialise count
    int count = 0;

    // Iterate until n is 0
    while (n) {
        n &= (n - 1);
        count++;
    }

    // Return the final count
    return count;
}

// Function to count the number of 0s
// and 1s in binary representation of N
void count1s0s(int N)
{
    // Initialise the count variables
    int count0, count1;

    // Function call to find the number
    // of set bits in N
    count1 = countSetBits(N);

    // Function call to find 1s complement
    N = onesComplement(N);

    // Function call to find the number
    // of set bits in 1s complement of N
    count0 = countSetBits(N);

    // Print the count
    printf("Count of 0s in N is %d\n", count0);
    printf("Count of 1s in N is %d\n", count1);
}

// Driver Code
int main()
{
    // Given Number
    int N = 5;

    // Function Call
    count1s0s(N);
    return 0;
}
```

**Output**

```
Count of 0s in N is 1
Count of 1s in N is 2
```

**时间复杂度:** *O(对数 N)*