# 计数小于 N 的数字，其与 N 的位与为零

> 原文:[https://www . geesforgeks . org/count-numbers-小于-n-with-n 的位与-0/](https://www.geeksforgeeks.org/count-numbers-less-than-n-whose-bitwise-and-with-n-is-zero/)

给定一个正整数 **N** ，任务是用 **N** 对所有小于 **N** 和[位](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)的数字进行计数，所有这些数字都为零。

**示例:**

> **输入:** N = 5
> **输出:** 2
> **说明:**
> 小于 N(= 5)的整数，其与 5 的位“与”为 0，则为 0 和 2。因此，总数是 2。
> 
> **输入:**N = 9
> T3】输出: 4

**方法:**给定的问题可以基于以下观察来解决:[在 **N** 中设置的所有位都将在任何具有](https://www.geeksforgeeks.org/check-bits-number-set/)[位与](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)的数字中取消设置，其中 **N** 等于 **0** 。按照以下步骤解决问题:

*   初始化一个变量，比如**未设置位**，等于给定整数 **N** 中[未设置位的总数](https://www.geeksforgeeks.org/count-unset-bits-number/)。
*   现在， **N** 中的每一个未设置位都可以在相应的位置有 **0** 或 **1** ，因为 **N** 有未设置位的任何位置的按位“与”将始终等于 **0** 。因此，不同可能性的总数将由 **2** 提升至**的幂，而非**。
*   因此，将 [2 的值打印为**的幂，并取消设置**T3 作为结果。](https://www.geeksforgeeks.org/multiplication-power-2/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count number of
// unset bits in the integer N
int countUnsetBits(int N)
{
    // Stores the number of unset
    // bits in N
    int c = 0;

    while (N) {

        // Check if N is even
        if (N % 2 == 0) {

            // Increment the value of c
            c += 1;
        }

        // Right shift N by 1
        N = N >> 1;
    }

    // Return the value of
    // count of unset bits
    return c;
}

// Function to count numbers whose
// Bitwise AND with N equal to 0
void countBitwiseZero(int N)
{
    // Stores the number
    // of unset bits in N
    int unsetBits = countUnsetBits(N);

    // Print the value of 2 to the
    // power of unsetBits
    cout << (1 << unsetBits);
}

// Driver Code
int main()
{
    int N = 9;
    countBitwiseZero(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count number of
// unset bits in the integer N
static int countUnsetBits(int N)
{
    // Stores the number of unset
    // bits in N
    int c = 0;

    while (N != 0) {

        // Check if N is even
        if (N % 2 == 0) {

            // Increment the value of c
            c += 1;
        }

        // Right shift N by 1
        N = N >> 1;
    }

    // Return the value of
    // count of unset bits
    return c;
}

// Function to count numbers whose
// Bitwise AND with N equal to 0
static void countBitwiseZero(int N)
{
    // Stores the number
    // of unset bits in N
    int unsetBits = countUnsetBits(N);

    // Print the value of 2 to the
    // power of unsetBits
    System.out.print(1 << unsetBits);
}

// Driver Code
public static void main(String[] args)
{
     int N = 9;
    countBitwiseZero(N);
}
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to count number of
# unset bits in the integer N
def countUnsetBits(N):

    # Stores the number of unset
    # bits in N
    c = 0

    while (N):

        # Check if N is even
        if (N % 2 == 0):

            # Increment the value of c
            c += 1

        # Right shift N by 1
        N = N >> 1

    # Return the value of
    # count of unset bits
    return c

# Function to count numbers whose
# Bitwise AND with N equal to 0
def countBitwiseZero(N):

    # Stores the number
    # of unset bits in N
    unsetBits = countUnsetBits(N)

    # Print value of 2 to the
    # power of unsetBits
    print ((1 << unsetBits))

# Driver Code
if __name__ == '__main__':
    N = 9
    countBitwiseZero(N)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count number of
// unset bits in the integer N
static int countUnsetBits(int N)
{

    // Stores the number of unset
    // bits in N
    int c = 0;

    while (N != 0)
    {

        // Check if N is even
        if (N % 2 == 0)
        {

            // Increment the value of c
            c += 1;
        }

        // Right shift N by 1
        N = N >> 1;
    }

    // Return the value of
    // count of unset bits
    return c;
}

// Function to count numbers whose
// Bitwise AND with N equal to 0
static void countBitwiseZero(int N)
{

    // Stores the number
    // of unset bits in N
    int unsetBits = countUnsetBits(N);

    // Print the value of 2 to the
    // power of unsetBits
    Console.Write(1 << unsetBits);
}

// Driver Code
public static void Main(String[] args)
{
    int N = 9;

    countBitwiseZero(N);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// Javascript program for the above approach
// Function to count number of
// unset bits in the integer N
function countUnsetBits( N)
{
    // Stores the number of unset
    // bits in N
    let c = 0;

    while (N != 0) {

        // Check if N is even
        if (N % 2 == 0) {

            // Increment the value of c
            c += 1;
        }

        // Right shift N by 1
        N = N >> 1;
    }

    // Return the value of
    // count of unset bits
    return c;
}

// Function to count numbers whose
// Bitwise AND with N equal to 0
function countBitwiseZero( N)
{
    // Stores the number
    // of unset bits in N
    let unsetBits = countUnsetBits(N);

    // Print the value of 2 to the
    // power of unsetBits
    document.write(1 << unsetBits);
}

// Driver Code
    let N = 9;
    countBitwiseZero(N);

// This code is contributed by shivansinghss2110
</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*