# 将所有相邻元素的按位异或中的设置位计数至 N

> 原文:[https://www . geesforgeks . org/count-set-bits-in-bits-by-xor-of-all-neighbor-up-n/](https://www.geeksforgeeks.org/count-set-bits-in-bitwise-xor-of-all-adjacent-elements-upto-n/)

给定一个正整数 **N** ，任务是通过对范围**【0，N】**中所有可能的相邻元素执行[按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)来计算设置位的总[计数。](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)

**示例:**

> **输入:** N = 4
> **输出:** 7
> **解释:**
> 0 和 1 的按位异或= 001 和集合位计数= 1
> 1 和 2 的按位异或= 011 和集合位计数= 2
> 2 和 3 的按位异或= 001 和集合位计数= 1
> 3 和 4 的按位异或= 111 和集合位计数= 3
> 因此， 通过对范围[0，N] = (1 + 2 + 1 + 3) = 7 的所有可能的相邻元素执行异或运算得到的设置位的总计数
> 
> **输入:**N = 7
> T3】输出: 11

**天真方法:**解决这个问题最简单的方法是[迭代范围**【0，N】**](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)，并通过对范围**【0，N】**内的每个相邻元素执行[按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)来计算所有可能的设置位。最后，打印所有可能设置位的总数。

***时间复杂度:**O(N * log<sub>2</sub>N)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，该想法基于以下观察:

> 如果 **X** 的最右边设置位的位置是 **K** ，那么**(x ^(x–1))**中设置位的计数必须是 **K** 。

按照以下步骤解决问题:

*   初始化一个变量，说出**位位置**来存储[最右边位](https://www.geeksforgeeks.org/position-of-rightmost-set-bit/)在范围**【0，N】**内的所有可能值。
*   初始化一个变量，比如说 **total_set_bits** 通过对范围**【0，N】**内所有可能的相邻元素执行[逐位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)运算来存储所有可能的设置位之和。
*   [迭代范围**【0，N】**](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)并更新**N = N –( N+1)/2**和**total _ set _ bits+=((N+1)/2 * bit _ position)**。
*   最后，打印 **total_set_bits** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count of set bits in Bitwise
// XOR of adjacent elements up to N
int countXORSetBitsAdjElemRange1_N(int N)
{

    // Stores count of set bits by Bitwise
    // XOR on adjacent elements of [0, N]
    int total_set_bits = 0;

    // Stores all possible values on
    // right most set bit over [0, N]
    int bit_Position = 1;

    // Iterate over the range [0, N]
    while (N) {
        total_set_bits += ((N + 1) / 2
                           * bit_Position);

        // Update N
        N -= (N + 1) / 2;

        // Update bit_Position
        bit_Position++;
    }

    return total_set_bits;
}

// Driver Code
int main()
{
    int N = 4;

    cout << countXORSetBitsAdjElemRange1_N(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to count of set bits in Bitwise
// XOR of adjacent elements up to N
static int countXORSetBitsAdjElemRange1_N(int N)
{

    // Stores count of set bits by Bitwise
    // XOR on adjacent elements of [0, N]
    int total_set_bits = 0;

    // Stores all possible values on
    // right most set bit over [0, N]
    int bit_Position = 1;

    // Iterate over the range [0, N]
    while (N != 0)
    {
        total_set_bits += ((N + 1) / 2 *
                           bit_Position);

        // Update N
        N -= (N + 1) / 2;

        // Update bit_Position
        bit_Position++;
    }
    return total_set_bits;
}

// Driver Code
public static void main(String[] args)
{
    int N = 4;

    System.out.println(countXORSetBitsAdjElemRange1_N(N));
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count of set bits in Bitwise
# XOR of adjacent elements up to N
def countXORSetBitsAdjElemRange1_N(N):

    # Stores count of set bits by Bitwise
    # XOR on adjacent elements of [0, N]
    total_set_bits = 0

    # Stores all possible values on
    # right most set bit over [0, N]
    bit_Position = 1

    # Iterate over the range [0, N]
    while (N):
        total_set_bits += ((N + 1) //
                            2 * bit_Position)

        # Update N
        N -= (N + 1) // 2

        # Update bit_Position
        bit_Position += 1

    return total_set_bits

# Driver Code
if __name__ == '__main__':

    N = 4

    print(countXORSetBitsAdjElemRange1_N(N))

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to count of set bits in Bitwise
// XOR of adjacent elements up to N
static int countXORSetBitsAdjElemRange1_N(int N)
{

    // Stores count of set bits by Bitwise
    // XOR on adjacent elements of [0, N]
    int total_set_bits = 0;

    // Stores all possible values on
    // right most set bit over [0, N]
    int bit_Position = 1;

    // Iterate over the range [0, N]
    while (N != 0)
    {
        total_set_bits += ((N + 1) / 2 *
                           bit_Position);

        // Update N
        N -= (N + 1) / 2;

        // Update bit_Position
        bit_Position++;
    }
    return total_set_bits;
}

// Driver Code
public static void Main()
{
    int N = 4;

    Console.Write(countXORSetBitsAdjElemRange1_N(N));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to count of set bits in Bitwise
// XOR of adjacent elements up to N
function countXORSetBitsAdjElemRange1_N(N)
{

    // Stores count of set bits by Bitwise
    // XOR on adjacent elements of [0, N]
    let total_set_bits = 0;

    // Stores all possible values on
    // right most set bit over [0, N]
    let bit_Position = 1;

    // Iterate over the range [0, N]
    while (N) {
        total_set_bits += (Math.floor((N + 1) / 2) * bit_Position);

        // Update N
        N -= Math.floor((N + 1) / 2);

        // Update bit_Position
        bit_Position++;
    }

    return total_set_bits;
}

// Driver Code
let N = 4;

document.write(countXORSetBitsAdjElemRange1_N(N));

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(Log<sub>2</sub>N)*
*T8】辅助空间: O(1)*