# 最大化表达式|位操作

> 原文:[https://www . geeksforgeeks . org/最大化表达式位操作/](https://www.geeksforgeeks.org/maximize-the-expression-bit-manipulation/)

给定两个正整数 **A** 和 **B** 。让我们定义 **D** 使得 **B 和 D = D** 。任务是最大化表达式 **A XOR D** 。
**举例:**

```
Input: A = 11 B = 4
Output: 15
Take D = 4 as (B AND D) = (4 AND 4) = 4.
Also, (A XOR D) = (11 XOR 4) = 15 which is the 
maximum according to the given condition.

Input: A = 9 and B = 13
Output: 13
```

**天真的做法:**由于 **B 和 D = D** ， **D** 将始终小于或等于 **B** 。因此，可以运行从 **1** 到 **B** 的循环，并检查给定条件是否满足。
**高效方法:**不用运行循环并检查每个 **D** ，表达式**(异或 D)** 的最大值可以使用位操作技术轻松计算。
我们举个例子来了解一下处理问题的方法:

```
A = 11 = 1011, B = 14 = 1110
Let's assume D = abcd in base 2 notation

B AND D:     1110           A XOR D:     1011
             abcd                        abcd   
            ------                      ------
             abcd                        ????

At 0th place: (0 AND d) = d implies d = 0 
At 1st place: (1 AND c) = c implies c = 0, 1 but to maximize (A XOR D), take c = 0
At 2nd place: (1 AND b) = b implies b = 0, 1 but to maximize (A XOR D), take b = 1
At 3rd place: (1 AND a) = a implies a = 0, 1 but to maximize (A XOR D), take a = 0

Hence, D = 0100 = 4 and maximum value of (A XOR D) = (11 XOR 4) = 15.
```

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

#define MAX 32

// Function to return the value of
// the maximized expression
int maximizeExpression(int a, int b)
{
    int result = a;

    // int can have 32 bits
    for (int bit = MAX - 1; bit >= 0; bit--) {

        // Consider the ith bit of D to be 1
        int bitOfD = 1 << bit;

        // Calculate the value of (B AND bitOfD)
        int x = b & bitOfD;

        // Check if bitOfD satisfies (B AND D = D)
        if (x == bitOfD) {

            // Check if bitOfD can maximize (A XOR D)
            int y = result & bitOfD;
            if (y == 0) {
                result = result ^ bitOfD;
            }
        }

        // Note that we do not need to consider ith bit of D
        // to be 0 because if above condition are not satisfied
        // then value of result will not change
        // which is similar to considering bitOfD = 0
        // as result XOR 0 = result
    }

    return result;
}

// Driver code
int main()
{
    int a = 11, b = 14;

    cout << maximizeExpression(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    final static int MAX = 32;

    // Function to return the value of
    // the maximized expression
    static int maximizeExpression(int a, int b)
    {
        int result = a;

        // int can have 32 bits
        for (int bit = MAX - 1; bit >= 0; bit--)
        {

            // Consider the ith bit of D to be 1
            int bitOfD = 1 << bit;

            // Calculate the value of (B AND bitOfD)
            int x = b & bitOfD;

            // Check if bitOfD satisfies (B AND D = D)
            if (x == bitOfD) {

                // Check if bitOfD can maximize (A XOR D)
                int y = result & bitOfD;
                if (y == 0)
                {
                    result = result ^ bitOfD;
                }
            }

            // Note that we do not need to consider ith bit of D
            // to be 0 because if above condition are not satisfied
            // then value of result will not change
            // which is similar to considering bitOfD = 0
            // as result XOR 0 = result
        }
        return result;
    }

    // Driver code
    public static void main (String[] args)
    {
        int a = 11, b = 14;

        System.out.println(maximizeExpression(a, b));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX = 32

# Function to return the value of
# the maximized expression
def maximizeExpression(a, b) :

    result = a

    # int can have 32 bits
    for bit in range(MAX - 1, -1, -1) :

        # Consider the ith bit of D to be 1
        bitOfD = 1 << bit

        # Calculate the value of (B AND bitOfD)
        x = b & bitOfD

        # Check if bitOfD satisfies (B AND D = D)
        if (x == bitOfD) :

            # Check if bitOfD can maximize (A XOR D)
            y = result & bitOfD
            if (y == 0) :
                result = result ^ bitOfD

        # Note that we do not need to consider ith bit of D
        # to be 0 because if above condition are not satisfied
        # then value of result will not change
        # which is similar to considering bitOfD = 0
        # as result XOR 0 = result

    return result

# Driver code
a = 11
b = 14
print(maximizeExpression(a, b))

# This code is contributed by divyamohan123
```

## C#

```
// C# implementation of the above approach
using System;
class GFG
{
    static int MAX = 32;

    // Function to return the value of
    // the maximized expression
    static int maximizeExpression(int a, int b)
    {
        int result = a;

        // int can have 32 bits
        for (int bit = MAX - 1; bit >= 0; bit--)
        {

            // Consider the ith bit of D to be 1
            int bitOfD = 1 << bit;

            // Calculate the value of (B AND bitOfD)
            int x = b & bitOfD;

            // Check if bitOfD satisfies (B AND D = D)
            if (x == bitOfD)
            {

                // Check if bitOfD can maximize (A XOR D)
                int y = result & bitOfD;
                if (y == 0)
                {
                    result = result ^ bitOfD;
                }
            }

            // Note that we do not need to consider
            // ith bit of D to be 0 because if
            // above condition are not satisfied then
            // value of result will not change which is
            // similar to considering bitOfD = 0 as
            // result XOR 0 = result
        }
        return result;
    }

    // Driver code
    public static void Main (String []args)
    {
        int a = 11, b = 14;

        Console.WriteLine(maximizeExpression(a, b));
    }
}

// This code is contributed by Arnab Kundu
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

let MAX = 32;

// Function to return the value of
// the maximized expression
function maximizeExpression(a, b)
{
    let result = a;

    // int can have 32 bits
    for (let bit = MAX - 1; bit >= 0; bit--)
    {

        // Consider the ith bit of D to be 1
        let bitOfD = 1 << bit;

        // Calculate the value of (B AND bitOfD)
        let x = b & bitOfD;

        // Check if bitOfD satisfies (B AND D = D)
        if (x == bitOfD) {

            // Check if bitOfD can maximize (A XOR D)
            let y = result & bitOfD;
            if (y == 0) {
                result = result ^ bitOfD;
            }
        }

        // Note that we do not need
        // to consider ith bit of D
        // to be 0 because if above
        // condition are not satisfied
        // then value of result will not change
        // which is similar to considering bitOfD = 0
        // as result XOR 0 = result
    }

    return result;
}

// Driver code
    let a = 11, b = 14;

    document.write(maximizeExpression(a, b));

</script>
```

**Output:** 

```
15
```

时间复杂度:0(最大值)

辅助空间:0(1)