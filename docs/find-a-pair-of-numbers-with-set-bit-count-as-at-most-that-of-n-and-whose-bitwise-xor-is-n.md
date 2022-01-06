# 找出一对位数最多为 N 的数字，其按位异或为 N

> 原文:[https://www . geeksforgeeks . org/find-a-一对位计数为最多 n 的数字，其位异或为 n/](https://www.geeksforgeeks.org/find-a-pair-of-numbers-with-set-bit-count-as-at-most-that-of-n-and-whose-bitwise-xor-is-n/)

给定一个正整数 **N** ，任务是找到整数对 **(X，Y)** ，使得 **X** 和 **Y** 的[按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)为 **N** 和 **X * Y** 最大，其中 **X** 和 **Y** 中的位数小于或等于 **N** 。

**示例:**

> **输入:** N = 10
> **输出:** 13 7
> **说明:**X = 13，Y = 7 的情况是最优的选择，因为 13 xor 7 = 10，13 * 7 = 91 是最大可能。
> 
> **输入:**N = 45
> T3】输出: 50 31

**方法:**给定的问题可以使用以下观察结果来解决:

*   如果 **N** 的 **i <sup>第</sup>T3】位是 **0** ，那么 **X** 和 **Y** 的 **i <sup>第</sup>位必须是 **0** 或 **1** 位。为了最大化产品，设置 **1** 这样的位。****
*   如果 **N** 的 **i <sup>第</sup>T3】位为 **1** ，那么 **X** 或 **Y** 的 **i <sup>第</sup>T11】位中的一位必须为 **1** ，另一位必须为 **0** 。由于 **N** 必须有恒定数量的设置位，因此 X 和 Y 的和必须是恒定的。****
*   如果两个数的和是常数，当两个数的差最小时，它们的乘积最大。

根据以上观察，将两个整数 **X** 和 **Y** 初始化为 0。为了使 **X** 和 **Y** 之间的差异最小化， **X** 必须等于**MSB<sub>N</sub>T13】和 **Y** 必须等于**N–MSB<sub>N</sub>T19】，其中 **MSB** 代表[最高有效位](https://www.geeksforgeeks.org/find-significant-set-bit-number/)。另外，对于 **N** 中的所有 **0** 位，将 **X** 和 **Y** 中的相应位设置为 **1** 。****

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the pair (X, Y) such
// that X xor Y = N and the count of set
// bits in X and Y is less than count of
// set bit in N
void maximizeProduct(int N)
{
    // Stores MSB (Most Significant Bit)
    int MSB = (int)log2(N);

    // Stores the value of X
    int X = 1 << MSB;

    // Stores the value of Y
    int Y = N - (1 << MSB);

    // Traversing over all bits of N
    for (int i = 0; i < MSB; i++) {

        // If ith bit of N is 0
        if (!(N & (1 << i))) {

            // Set ith bit of X to 1
            X += 1 << i;

            // Set ith bit of Y to 1
            Y += 1 << i;
        }
    }

    // Print Answer
    cout << X << " " << Y;
}

// Driver Code
int main()
{
    int N = 45;
    maximizeProduct(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

// Function to find the pair (X, Y) such
// that X xor Y = N and the count of set
// bits in X and Y is less than count of
// set bit in N
static void maximizeProduct(int N)
{
    // Stores MSB (Most Significant Bit)
    int MSB = (int)(Math.log(N) / Math.log(2));

    // Stores the value of X
    int X = 1 << MSB;

    // Stores the value of Y
    int Y = N - (1 << MSB);

    // Traversing over all bits of N
    for (int i = 0; i < MSB; i++) {

        // If ith bit of N is 0
        if ((N & (1 << i))==0) {

            // Set ith bit of X to 1
            X += 1 << i;

            // Set ith bit of Y to 1
            Y += 1 << i;
        }
    }

    // Print Answer
    System.out.println(X+" "+Y);
}
// Driver Code
public static void main(String[] args)
{
    int N = 45;
    maximizeProduct(N);
}
}

// This code is contributed by dwivediyash
```

## 蟒蛇 3

```
# python 3 program for the above approach
import math

# Function to find the pair (X, Y) such
# that X xor Y = N and the count of set
# bits in X and Y is less than count of
# set bit in N
def maximizeProduct(N):

    # Stores MSB (Most Significant Bit)
    MSB = (int)(math.log2(N))

    # Stores the value of X
    X = 1 << MSB

    # / Stores the value of Y
    Y = N - (1 << MSB)

    # Traversing over all bits of N
    for i in range(MSB):

        # If ith bit of N is 0
        if (not (N & (1 << i))):

            # / Set ith bit of X to 1
            X += 1 << i

            # Set ith bit of Y to 1
            Y += 1 << i

    # Print Answer
    print(X, Y)

# Driver Code
if __name__ == "__main__":
    N = 45
    maximizeProduct(N)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;

class GFG {

// Function to find the pair (X, Y) such
// that X xor Y = N and the count of set
// bits in X and Y is less than count of
// set bit in N
static void maximizeProduct(int N)
{

    // Stores MSB (Most Significant Bit)
    int MSB = (int)(Math.Log(N) / Math.Log(2));

    // Stores the value of X
    int X = 1 << MSB;

    // Stores the value of Y
    int Y = N - (1 << MSB);

    // Traversing over all bits of N
    for (int i = 0; i < MSB; i++) {

        // If ith bit of N is 0
        if ((N & (1 << i))==0) {

            // Set ith bit of X to 1
            X += 1 << i;

            // Set ith bit of Y to 1
            Y += 1 << i;
        }
    }

    // Print Answer
    Console.Write(X+" "+Y);
}

    // Driver Code
    public static void Main()
    {
        int N = 45;
        maximizeProduct(N);
    }
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the pair (X, Y) such
        // that X xor Y = N and the count of set
        // bits in X and Y is less than count of
        // set bit in N
        function maximizeProduct(N)
        {

            // Stores MSB (Most Significant Bit)
            let MSB = Math.log2(N);

            // Stores the value of X
            let X = 1 << MSB;

            // Stores the value of Y
            let Y = N - (1 << MSB);

            // Traversing over all bits of N
            for (let i = 0; i < MSB; i++) {

                // If ith bit of N is 0
                if (!(N & (1 << i))) {

                    // Set ith bit of X to 1
                    X += 1 << i;

                    // Set ith bit of Y to 1
                    Y += 1 << i;
                }
            }

            // Print Answer
            document.write(X + " " + Y);
        }

        // Driver Code

        let N = 45;
        maximizeProduct(N);

// This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
50 31
```

***时间复杂度:** O(log N)*
***辅助空间:** O(N)*