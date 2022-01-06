# 将 N 减少到 0 所需执行的给定操作的最小次数

> 原文:[https://www . geesforgeks . org/最小给定操作数-需要执行的操作-将 n 减少到 0/](https://www.geeksforgeeks.org/minimum-number-of-given-operations-required-to-be-performed-to-reduce-n-to-0/)

给定一个整数 **N** ，任务是在最小操作数内将 **N** 减少到 0，使用以下操作任意次数:

*   更改 **N** 二进制表示中最右边的(0 <sup>第</sup>位)。
*   如果第**(I-1)**位设置为 1 且第**(I-2)**至第**0**位设置为 0，则更改第 **i <sup>第</sup>T3 位在第 **N** 二进制表示中的位置。**

**示例:**

> **输入:** N = 3
> **输出:** 2
> **说明:**3 的二进制表示为“11”。
> “11”→“01”，第二次操作，因为第 0 位为 1。
> “01”→“00 ”,第一次操作。
> 
> **输入:** N = 6
> **输出:** 4
> **说明:**6 的二进制表示为“110”。
> “110”→“010”，第二次操作，因为第一位是 1，第 0 到第 0 位是 0。
> “010”→“011”，第一次操作。
> “011”→“001”，第二次操作，因为第 0 位为 1。
> “001”→“000”，第一次操作。

**方法:**该想法基于以下观察:

*   1 → 0 需要 1 次操作。
    2 → 0 即 10 → 11 → 01 → 0 需要 3 次操作。
    4 → 0 即100→101→111→110→010→11→01→0*需要 7 次操作。
    因此可以推广为 2 的任意次方，即 2 <sup>k</sup> 需要 2 <sup>(k+1)</sup> -1 次运算。*
*   *如果 a → b 需要 k 运算，b → a 也需要 k 运算。*

*从 2 <sup>n</sup> 到 2 <sup>(n-1)</sup> 的中间数包含 2 <sup>n</sup> 和 2 <sup>(n-1)</sup> 之间的所有数字，这表明任何给定的非负整数都可以转换为 0。设 f(n)为函数，求所需的最小运算次数。递推关系为:
f(n)= f(2<sup>k</sup>)–f(n 异或 2 <sup>k</sup> ，其中 k = n 的[最高有效位的下一位。](https://www.geeksforgeeks.org/find-significant-set-bit-number/)*

*想法是用[递归](https://www.geeksforgeeks.org/recursion/)。按照以下步骤解决问题:*

*   *创建一个以数字 **N** 为参数的[递归函数](https://www.geeksforgeeks.org/recursive-functions/)。

    *   如果 **N** 的值等于 **0** ，则返回 **0** 。
    *   否则，找到小于或等于 2 的最高幂[**N**](https://www.geeksforgeeks.org/highest-power-2-less-equal-given-number/)并将其存储在变量 **X** 中。
    *   将递归调用函数 **(X^(X/2)^N)** 返回的值存储在变量 **S** 中。
    *   将 **X** 的值加到 **S** 上返回。* 

*下面是上述方法的实现:*

## *C++*

```
*// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum
// operations required to convert
// N to 0
int minimumOneBitOperations(int n, int res = 0)
{
    // Base Case
    if (n == 0)
        return res;

    // Store the highest power of 2
    // less than or equal to n
    int b = 1;
    while ((b << 1) <= n)
        b = b << 1;

    // Return the result
    return minimumOneBitOperations(
        (b >> 1) ^ b ^ n, res + b);
}

// Driver Code
int main()
{
    // Given Input
    int N = 6;

    // Function call
    cout << minimumOneBitOperations(N);

    return 0;
}*
```

## *Java 语言(一种计算机语言，尤用于创建网站)*

```
*// Java program for the above approach
class GFG {

    // Function to find minimum
    // operations required to convert
    // N to 0
    public static int minimumOneBitOperations(int n, int res)
    {

        // Base Case
        if (n == 0)
            return res;

        // Store the highest power of 2
        // less than or equal to n
        int b = 1;
        while ((b << 1) <= n)
            b = b << 1;

        // Return the result
        return minimumOneBitOperations((b >> 1) ^ b ^ n, res + b);
    }

    // Driver Code
    public static void main(String args[])
    {

        // Given Input
        int N = 6;

        // Function call
        System.out.println(minimumOneBitOperations(N, 0));
    }
}

// This code is contributed by gfgking.*
```

## *蟒蛇 3*

```
*# Python program for the above approach

# Function to find minimum
# operations required to convert
# N to 0
def minimumOneBitOperations(n, res):

  # Base case
    if n == 0:
        return res

     # Store the highest power of 2
    # less than or equal to n 
    b = 1
    while (b << 1) <= n:
        b = b << 1

    # Return the result
    return minimumOneBitOperations((b >> 1) ^ b ^ n, res + b)

# Driver code
N = 6
print(minimumOneBitOperations(N, 0))

# This code is contributed by Parth Manchanda*
```

## *C#*

```
*// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find minimum
// operations required to convert
// N to 0
static int minimumOneBitOperations(int n, int res)
{
    // Base Case
    if (n == 0)
        return res;

    // Store the highest power of 2
    // less than or equal to n
    int b = 1;
    while ((b << 1) <= n)
        b = b << 1;

    // Return the result
    return minimumOneBitOperations(
        (b >> 1) ^ b ^ n, res + b);
}

// Driver Code
public static void Main()
{
    // Given Input
    int N = 6;

    // Function call
    Console.Write(minimumOneBitOperations(N,0));
}
}

// This code is contributed by SURENDRA_GANGWAR.*
```

## *java 描述语言*

```
*<script>
    // Javascript program for the above approach

// Function to find minimum
// operations required to convert
// N to 0
function minimumOneBitOperations( n,  res = 0)
{
    // Base Case
    if (n == 0)
        return res;

    // Store the highest power of 2
    // less than or equal to n
    let b = 1;
    while ((b << 1) <= n)
        b = b << 1;

    // Return the result
    return minimumOneBitOperations((b >> 1) ^ b ^ n, res + b);
}

// Driver Code

    // Given Input
    let N = 6;

    // Function call
    document.write(minimumOneBitOperations(N));

// This code is contributed by
// Potta Lokesh

    </script>*
```

***Output:** 

```
4
```* 

****时间复杂度:** O(log(N))*
***辅助空间:** O(1)**