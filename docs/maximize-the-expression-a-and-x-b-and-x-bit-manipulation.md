# 最大化表达式(A 和 X) * (B 和 X) |位操作

> 原文:[https://www . geeksforgeeks . org/最大化-表达式-a-和-x-B-和-x-位操作/](https://www.geeksforgeeks.org/maximize-the-expression-a-and-x-b-and-x-bit-manipulation/)

给定两个正整数 **A** 和 **B** ，这样 **A！= B** ，任务是找到一个最大化表达式 **(A AND X) * (B AND X)** 的正整数 **X** 。
**例:**

> **输入:** A = 9 B = 8
> **输出:** 8
> (9 AND 8) * (8 AND 8) = 8 * 8 = 64(最大可能)
> **输入:** A = 11 和 B = 13
> **输出:** 9

**天真的方法:**一个人可以从 **1** 到 **max(A，B)** 运行一个循环，并且可以很容易地找到最大化给定表达式的 **X** 。
**高效途径:**众所周知，

> **(a–b)<sup>2</sup>≥0**
> 意为**(a+b)<sup>2</sup>–4 * a * b≥0**
> 意为**a * b≤(a+b)<sup>2</sup>/4**
> 因此， 其结论是 **a * b** 将在**A * B =(A+B)<sup>2</sup>/4**
> 时达到最大值，这意味着 **a = b**
> 从上述结果来看， **(A AND X) * (B AND X)** 将在 **(A AND X) = (B AND X)**
> 时达到最大值

现在可以发现 X 为:

> A = 11 = 1011
> B = 13 = 1101
> X =？= abcd
> 排在第 0 位:(1 AND d) = (1 AND d)表示 d = 0，1 但是最大化(A AND X) * (B AND X) d = 1
> 排在第 1 位:(1 AND d) = (0 AND d)表示 c = 0
> 排在第 2 位:(0 AND d) = (1 AND d)表示 b = 0
> 排在第 3 位:(1 AND d) = (1 AND d)表示 a = 0，1 但是最大化(A AND X) * (B AND X) a = 1
> 因此，X

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define MAX 32

// Function to find X according
// to the given conditions
int findX(int A, int B)
{
    int X = 0;

    // int can have 32 bits
    for (int bit = 0; bit < MAX; bit++) {

        // Temporary ith bit
        int tempBit = 1 << bit;

        // Compute ith bit of X according to
        // given conditions
        // Expression below is the direct
        // conclusion from the illustration
        // we had taken earlier
        int bitOfX = A & B & tempBit;

        // Add the ith bit of X to X
        X += bitOfX;
    }

    return X;
}

// Driver code
int main()
{
    int A = 11, B = 13;

    cout << findX(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
static int MAX = 32;

// Function to find X according
// to the given conditions
static int findX(int A, int B)
{
    int X = 0;

    // int can have 32 bits
    for (int bit = 0; bit < MAX; bit++)
    {

        // Temporary ith bit
        int tempBit = 1 << bit;

        // Compute ith bit of X according to
        // given conditions
        // Expression below is the direct
        // conclusion from the illustration
        // we had taken earlier
        int bitOfX = A & B & tempBit;

        // Add the ith bit of X to X
        X += bitOfX;
    }
    return X;
}

// Driver code
public static void main(String []args)
{
    int A = 11, B = 13;

    System.out.println(findX(A, B));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX = 32

# Function to find X according
# to the given conditions
def findX(A, B) :

    X = 0;

    # int can have 32 bits
    for bit in range(MAX) :

        # Temporary ith bit
        tempBit = 1 << bit;

        # Compute ith bit of X according to
        # given conditions
        # Expression below is the direct
        # conclusion from the illustration
        # we had taken earlier
        bitOfX = A & B & tempBit;

        # Add the ith bit of X to X
        X += bitOfX;

    return X;

# Driver code
if __name__ == "__main__" :

    A = 11; B = 13;
    print(findX(A, B));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int MAX = 32;

// Function to find X according
// to the given conditions
static int findX(int A, int B)
{
    int X = 0;

    // int can have 32 bits
    for (int bit = 0; bit < MAX; bit++)
    {

        // Temporary ith bit
        int tempBit = 1 << bit;

        // Compute ith bit of X according to
        // given conditions
        // Expression below is the direct
        // conclusion from the illustration
        // we had taken earlier
        int bitOfX = A & B & tempBit;

        // Add the ith bit of X to X
        X += bitOfX;
    }
    return X;
}

// Driver code
public static void Main(String []args)
{
    int A = 11, B = 13;

    Console.WriteLine(findX(A, B));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find X according
// to the given conditions
function findX( A,  B)
{
    var X = 0;
    var MAX = 32;

    // int can have 32 bits
    for (var bit = 0; bit < MAX; bit++)
    {

        // Temporary ith bit

        var tempBit = 1 << bit;

        // Compute ith bit of X according to
        // given conditions
        // Expression below is the direct
        // conclusion from the illustration
        // we had taken earlier

        var bitOfX = A & B & tempBit;

        // Add the ith bit of X to X
        X += bitOfX;
    }
    return X;
}

// Driver code
    var A = 11, B = 13;
    document.write(findX(A, B));

  // This code is contributed by bunnyram19.
</script>
```

**Output:** 

```
9
```

时间复杂度:0(最大值)

辅助空间:0(1)