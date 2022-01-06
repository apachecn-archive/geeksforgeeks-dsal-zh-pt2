# 需要翻转的最小位数，使得 A 和 B 的位“或”等于 C

> 原文:[https://www . geesforgeks . org/需要翻转的最小位数，这样 a 和 b 的按位或等于 c/](https://www.geeksforgeeks.org/minimum-number-of-bits-required-to-be-flipped-such-that-bitwise-or-of-a-and-b-is-equal-to-c/)

给定三个正整数 **A** 、 **B** 和 **C** ，任务是计算 **A** 和 **B** 中所需的最小翻转位数，使得 **A** 和 **B** 的[位“或”与 **C** 相等或不相等。](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)

**示例:**

> **输入:** A = 2，B = 2，C = 3
> **输出:** 1
> **说明:**
> A 的二进制表示为 010，B 为 010，C 为 011。
> 翻转 A 或 B 的第三位，使 A | B = C，即 011 | 010 = 011。
> 因此，所需的翻转总数为 1。
> 
> **输入:** A = 2，B = 6，C = 5
> T3】输出: 3

**方法:**按照以下步骤解决问题:

*   初始化一个变量，比如 **res** ，它存储所需的最小翻转位数。
*   [迭代 **A** 、 **B** 和 **C** 的每个位](https://www.geeksforgeeks.org/find-position-of-the-only-set-bit/)，并执行以下步骤:
    *   如果未设置 **C** 的**I<sup>th</sup>T3】位，则检查以下内容:**
        *   如果设置了 **A** 的 **i <sup>第</sup>T3】位，则用 **1** 递增 **res** ，需要翻转 **A** 的 **i <sup>第</sup>T13】位。****
        *   如果设置了 **B** 的 **i <sup>第</sup>T3】位，则用 **1** 递增 **res** ，需要翻转 **B** 的 **i <sup>第</sup>T13】位。****
    *   如果设置了 **C** 的**I<sup>th</sup>T3】位，则检查以下内容:**
        *   如果未设置 **A** 和 **B** 的 **i <sup>第</sup>T3】位，则用 **1** 递增 **res** ，任一位都需要翻转。**
        *   如果设置了 **A** 和 **B** 的 **i <sup>第</sup>T3】位，我们就不需要翻转任何位。**
*   完成上述步骤后，打印 **res** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// bit flips required on A and B
// such that Bitwise OR of A and B is C
int minimumFlips(int A, int B, int C)
{
    // Stores the count of flipped bit
    int res = 0;

    // Iterate over the range [0, 32]
    for (int i = 0; i < 32; i++) {

        int x = 0, y = 0, z = 0;

        // Check if i-th bit of A is set
        if (A & (1 << i)) {
            x = 1;
        }

        // Check if i-th bit of B is
        // set or not
        if (B & (1 << i)) {
            y = 1;
        }

        // Check if i-th bit of C is
        // set or not
        if (C & (1 << i)) {
            z = 1;
        }

        // If i-th bit of C is unset
        if (z == 0) {

            // Check if i-th bit of
            // A is set or not
            if (x) {
                res++;
            }

            // Check if i-th bit of
            // B is set or not
            if (y) {
                res++;
            }
        }

        // Check if i-th bit of C
        // is set or not
        if (z == 1) {

            // Check if i-th bit of
            // both A and B is set
            if (x == 0 && y == 0) {
                res++;
            }
        }
    }

    // Return the count
    // of bits flipped
    return res;
}

// Driver Code
int main()
{
    int A = 2, B = 6, C = 5;
    cout << minimumFlips(A, B, C);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to count the number of
// bit flips required on A and B
// such that Bitwise OR of A and B is C
static int minimumFlips(int A, int B, int C)
{

    // Stores the count of flipped bit
    int res = 0;

    // Iterate over the range [0, 32]
    for(int i = 0; i < 32; i++)
    {
        int x = 0, y = 0, z = 0;

        // Check if i-th bit of A is set
        if ((A & (1 << i)) != 0)
        {
            x = 1;
        }

        // Check if i-th bit of B is
        // set or not
        if ((B & (1 << i)) != 0)
        {
            y = 1;
        }

        // Check if i-th bit of C is
        // set or not
        if ((C & (1 << i)) != 0)
        {
            z = 1;
        }

        // If i-th bit of C is unset
        if (z == 0)
        {

            // Check if i-th bit of
            // A is set or not
            if (x == 1)
            {
                res++;
            }

            // Check if i-th bit of
            // B is set or not
            if (y == 1)
            {
                res++;
            }
        }

        // Check if i-th bit of C
        // is set or not
        if (z == 1)
        {

            // Check if i-th bit of
            // both A and B is set
            if (x == 0 && y == 0)
            {
                res++;
            }
        }
    }

    // Return the count
    // of bits flipped
    return res;
}

// Driver Code
public static void main(String[] args)
{
    int A = 2, B = 6, C = 5;

    System.out.println(minimumFlips(A, B, C));
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of
# bit flips required on A and B
# such that Bitwise OR of A and B is C
def minimumFlips(A, B, C):

    # Stores the count of flipped bit
    res = 0

    # Iterate over the range [0, 32]
    for i in range(32):
        x, y, z = 0, 0, 0

        # Check if i-th bit of A is set
        if (A & (1 << i)):
            x = 1

        # Check if i-th bit of B is
        # set or not
        if (B & (1 << i)):
            y = 1

        # Check if i-th bit of C is
        # set or not
        if (C & (1 << i)):
            z = 1

        # If i-th bit of C is unset
        if (z == 0):

            # Check if i-th bit of
            # A is set or not
            if (x):
                res += 1

            # Check if i-th bit of
            # B is set or not
            if (y):
                res += 1

        # Check if i-th bit of C
        # is set or not
        if (z == 1):

            # Check if i-th bit of
            # both A and B is set
            if (x == 0 and y == 0):
                res += 1

    # Return the count
    # of bits flipped
    return res

# Driver Code
if __name__ == '__main__':

    A, B, C = 2, 6, 5

    print(minimumFlips(A, B, C))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG {

    // Function to count the number of
    // bit flips required on A and B
    // such that Bitwise OR of A and B is C
    static int minimumFlips(int A, int B, int C)
    {

        // Stores the count of flipped bit
        int res = 0;

        // Iterate over the range [0, 32]
        for (int i = 0; i < 32; i++) {
            int x = 0, y = 0, z = 0;

            // Check if i-th bit of A is set
            if ((A & (1 << i)) != 0) {
                x = 1;
            }

            // Check if i-th bit of B is
            // set or not
            if ((B & (1 << i)) != 0) {
                y = 1;
            }

            // Check if i-th bit of C is
            // set or not
            if ((C & (1 << i)) != 0) {
                z = 1;
            }

            // If i-th bit of C is unset
            if (z == 0) {

                // Check if i-th bit of
                // A is set or not
                if (x == 1) {
                    res++;
                }

                // Check if i-th bit of
                // B is set or not
                if (y == 1) {
                    res++;
                }
            }

            // Check if i-th bit of C
            // is set or not
            if (z == 1) {

                // Check if i-th bit of
                // both A and B is set
                if (x == 0 && y == 0) {
                    res++;
                }
            }
        }

        // Return the count
        // of bits flipped
        return res;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int A = 2, B = 6, C = 5;

        Console.WriteLine(minimumFlips(A, B, C));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// javascript program for the above approach
    // Function to count the number of
    // bit flips required on A and B
    // such that Bitwise OR of A and B is C
    function minimumFlips(A , B , C) {

        // Stores the count of flipped bit
        var res = 0;

        // Iterate over the range [0, 32]
        for (i = 0; i < 32; i++) {
            var x = 0, y = 0, z = 0;

            // Check if i-th bit of A is set
            if ((A & (1 << i)) != 0) {
                x = 1;
            }

            // Check if i-th bit of B is
            // set or not
            if ((B & (1 << i)) != 0) {
                y = 1;
            }

            // Check if i-th bit of C is
            // set or not
            if ((C & (1 << i)) != 0) {
                z = 1;
            }

            // If i-th bit of C is unset
            if (z == 0) {

                // Check if i-th bit of
                // A is set or not
                if (x == 1) {
                    res++;
                }

                // Check if i-th bit of
                // B is set or not
                if (y == 1) {
                    res++;
                }
            }

            // Check if i-th bit of C
            // is set or not
            if (z == 1) {

                // Check if i-th bit of
                // both A and B is set
                if (x == 0 && y == 0) {
                    res++;
                }
            }
        }

        // Return the count
        // of bits flipped
        return res;
    }

    // Driver Code
        var A = 2, B = 6, C = 5;
        document.write(minimumFlips(A, B, C));

// This code is contributed by aashish1995
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)