# 两个二进制数相加的进位操作计数

> 原文:[https://www . geeksforgeeks . org/二进制数相加运算计数/](https://www.geeksforgeeks.org/count-of-carry-operations-on-adding-two-binary-numbers/)

给定两个十进制数 **num1** 和 **num2** ，任务是在将两个给定的数以[二进制形式](https://www.geeksforgeeks.org/program-decimal-binary-conversion/)相加的同时，计算需要进位操作的次数。

**示例:**

> **输入:** num1 = 15，num2 = 10
> **输出:** 3
> **解释:**
> 给出的数字相加为:
> 15->1 1 1 1
> 10->1 0 1 0
> 进位->1 1 1–
> ———T13】25->1 0 1
> 
> **输入:** num1 = 14 num2 = 4
> **输出:** 2
> **解释:**
> 给出的数字相加为:
> 14->1 1 1 0
> 4->0 1 0
> 进位->1–––
> ————
> 18->1 0 1 0 1 0

**天真的做法:**天真的想法是把数字转换成二进制，从[最低有效位](https://www.geeksforgeeks.org/print-kth-least-significant-bit-number/)开始一个一个地加一位，检查是否产生进位。每当产生进位时，将计数增加 1。完成所有步骤后，携带**打印计数。**

***时间复杂度:** O(K)，其中 K 是 x 的二进制表示中位数的计数。*
***辅助空间:** O(log N)*

**高效方法:**想法是使用[按位异或和与。](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)以下是步骤:

*   使用“异或”和“与”将[两个二进制数相加。](https://www.geeksforgeeks.org/find-xor-of-two-number-without-using-xor-operator/)
*   现在，两个数按位“与”中的 1 的[数显示了该步中携带位的**数。**](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)
*   将上一步各阶段的数相加，得到**进位**运算的最终计数。

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of carry
// operations to add two binary numbers
int carryCount(int num1, int num2)
{
    // To Store the carry count
    int count = 0;

    // Iterate till there is no carry
    while (num2 != 0) {

        // Carry now contains common
        // set bits of x and y
        int carry = num1 & num2;

        // Sum of bits of x and y where at
        // least one of the bits is not set
        num1 = num1 ^ num2;

        // Carry is shifted by one
        // so that adding it to x
        // gives the required sum
        num2 = carry << 1;

        // Adding number of 1's of
        // carry to final count
        count += __builtin_popcount(num2);
    }

    // Return the final count
    return count;
}

// Driver Code
int main()
{
    // Given two numbers
    int A = 15, B = 10;

    // Function Call
    cout << carryCount(15, 10);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to count the number of carry
// operations to add two binary numbers
static int carryCount(int num1, int num2)
{

    // To Store the carry count
    int count = 0;

    // Iterate till there is no carry
    while (num2 != 0)
    {

        // Carry now contains common
        // set bits of x and y
        int carry = num1 & num2;

        // Sum of bits of x and y where at
        // least one of the bits is not set
        num1 = num1 ^ num2;

        // Carry is shifted by one
        // so that adding it to x
        // gives the required sum
        num2 = carry << 1;

        // Adding number of 1's of
        // carry to final count
        count += Integer.bitCount(num2);
    }

    // Return the final count
    return count;
}

// Driver Code
public static void main(String[] args)
{

    // Given two numbers
    int A = 15, B = 10;

    // Function call
    System.out.print(carryCount(A, B));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of carry
# operations to add two binary numbers
def carryCount(num1, num2):

    # To Store the carry count
    count = 0

    # Iterate till there is no carry
    while(num2 != 0):

        # Carry now contains common
        # set bits of x and y
        carry = num1 & num2

        # Sum of bits of x and y where at
        # least one of the bits is not set
        num1 = num1 ^ num2

        # Carry is shifted by one
        # so that adding it to x
        # gives the required sum
        num2 = carry << 1

        # Adding number of 1's of
        # carry to final count
        count += bin(num2).count('1')

    # Return the final count
    return count

# Driver Code

# Given two numbers
A = 15
B = 10

# Function call
print(carryCount(A, B))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;
class GFG{

static int countSetBits(int x)
{
    int setBits = 0;
    while (x != 0)
    {
        x = x & (x - 1);
        setBits++;
    }
    return setBits;
}
// Function to count the number of carry
// operations to add two binary numbers
static int carryCount(int num1, int num2)
{

    // To Store the carry count
    int count = 0;

    // Iterate till there is no carry
    while (num2 != 0)
    {

        // Carry now contains common
        // set bits of x and y
        int carry = num1 & num2;

        // Sum of bits of x and y where at
        // least one of the bits is not set
        num1 = num1 ^ num2;

        // Carry is shifted by one
        // so that adding it to x
        // gives the required sum
        num2 = carry << 1;

        // Adding number of 1's of
        // carry to readonly count
        count += countSetBits(num2);
    }

    // Return the readonly count
    return count;
}

// Driver Code
public static void Main(String[] args)
{

    // Given two numbers
    int A = 15, B = 10;

    // Function call
    Console.Write(carryCount(A, B));
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>
// JavaScript program for the
// above approach

function countSetBits(x)
{
    let setBits = 0;
    while (x != 0)
    {
        x = x & (x - 1);
        setBits++;
    }
    return setBits;
}

// Function to count the number of carry
// operations to add two binary numbers
function carryCount(num1, num2)
{

    // To Store the carry count
    let count = 0;

    // Iterate till there is no carry
    while (num2 != 0)
    {

        // Carry now contains common
        // set bits of x and y
        let carry = num1 & num2;

        // Sum of bits of x and y where at
        // least one of the bits is not set
        num1 = num1 ^ num2;

        // Carry is shifted by one
        // so that adding it to x
        // gives the required sum
        num2 = carry << 1;

        // Adding number of 1's of
        // carry to readonly count
        count += countSetBits(num2);
    }

    // Return the readonly count
    return count;
}

// Driver Code

    // Given two numbers
    let A = 15, B = 10;

    // Function call
    document.write(carryCount(A, B));

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(log<sub>2</sub>(N))*
***辅助空间:** O(1)*