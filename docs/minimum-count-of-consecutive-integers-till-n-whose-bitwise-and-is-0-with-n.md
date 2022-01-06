# 按位“与”为 0 的 N 个连续整数的最小计数

> 原文:[https://www . geeksforgeeks . org/连续整数的最小计数-third-n-with-n 的按位 and-is-0/](https://www.geeksforgeeks.org/minimum-count-of-consecutive-integers-till-n-whose-bitwise-and-is-0-with-n/)

给定一个正整数 **N** ，任务是打印小于 **N** 的连续数字的最小计数，使得这些连续元素的[位](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)，包括整数 **N** ，等于 **0** 。

**示例:**

> **输入:** N = 18
> **输出:** 3
> **解释:**
> 一种可能的方式是形成{15，16，17，18}的序列。给定数字的按位“与”等于 0。
> 因此，对 4 个连续元素的序列进行按位“与”运算至少需要 3 个数字，包括 18 到 0。
> 
> **输入:** N = 4
> **输出:** 1
> **解释:**
> 一种可能的方式是形成{4，3}的序列。给定数字的按位“与”等于 0。
> 因此，对包含 4 到 0 的 2 个连续元素的序列进行按位“与”运算至少需要 1 个数字。

**天真方法:**最简单的方法是[迭代直到](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/) **N** 大于 **0** ，在每次迭代中检查到目前为止数字的[位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)是否等于 **0** 。如果没有，则增加 **1** 计数。

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**有效方法:**给定的问题可以基于以下观察来解决:

1.  要使包含 **N** 的序列的[位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)等于 **0** ，需要使编号 **N** 的 [MSB 位等于 **0** 。](https://www.geeksforgeeks.org/find-significant-set-bit-number/)
2.  所以思路是把大于等于 **(2 <sup>MSB</sup> -1)** 且小于 **N** 的所有整数都包含在序列中，会给出最小计数。

按照以下步骤解决问题:

*   [找到整数的最高有效集位 **N**](https://www.geeksforgeeks.org/find-significant-set-bit-number/) 并将其存储在变量 say **m** 中。
*   那么将包括的最大最小值是 **(2 <sup>m</sup> -1)** 。
*   最后，将计数打印为 **(N- (2 <sup>m</sup> -1))** 。

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach
#include <bits/stdc++.h>
using namespace std;
int decimalToBinary(int N)
{

    // To store the binary number
    int B_Number = 0;
    int cnt = 0;
    while (N != 0)
    {
        int rem = N % 2;
        double c = pow(10, cnt);
        B_Number += rem * c;
        N /= 2;

        // Count used to store exponent value
        cnt++;
    }

    return B_Number;
}
    // Function to count the minimum count of
    // integers such that bitwise AND of that
    // many consecutive elements is equal to 0
    int count(int N)
    {

        // Stores the binary
        // representation of N
        string a = to_string(decimalToBinary(N));

        // Stores the MSB bit
        int m = a.size() - 1;

        // Stores the count
        // of numbers
        int res = (N - (pow(2, m) - 1));

        // Return res
        return res;

    }

// Driver Code
int main() {

    // Given Input
    int N = 18;

    // Function Call
    cout<< count(N);
return 0;
}

// This code is contributed by shikhasingrajput
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

    // Function to count the minimum count of
    // integers such that bitwise AND of that
    // many consecutive elements is equal to 0
    static int count(int N)
    {

        // Stores the binary
        // representation of N
        String a = Integer.toBinaryString(N);

        // Stores the MSB bit
        int m = a.length() - 1;

        // Stores the count
        // of numbers
        int res = (int) (N - (Math.pow(2, m) - 1));

        // Return res
        return res;

    }

    // Driver Code
    public static void main(String[] args) {

        // Given Input
        int N = 18;

        // Function Call
        System.out.println(count(N));
    }
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to count the minimum count of
# integers such that bitwise AND of that
# many consecutive elements is equal to 0

def count(N):

    # Stores the binary
    # representation of N
    a = bin(N)

    # Excludes first two
    # characters "0b"
    a = a[2:]

    # Stores the MSB bit
    m = len(a)-1

    # Stores the count
    # of numbers
    res = N - (2**m-1)

    # Return res
    return res

# Driver Code
# Given Input
N = 18

# Function Call
print(count(N))
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
public class GFG
{

    // Function to count the minimum count of
    // integers such that bitwise AND of that
    // many consecutive elements is equal to 0
    static int count(int N)
    {

        // Stores the binary
        // representation of N
        String a = Convert.ToString(N, 2);

        // Stores the MSB bit
        int m = a.Length - 1;

        // Stores the count
        // of numbers
        int res = (int) (N - (Math.Pow(2, m) - 1));

        // Return res
        return res;

    }

    // Driver Code
    public static void Main(String[] args) {

        // Given Input
        int N = 18;

        // Function Call
        Console.WriteLine(count(N));
    }
}

// This code is contributed by umadevi9616
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Function to count the minimum count of
    // integers such that bitwise AND of that
    // many consecutive elements is equal to 0
    function count(N)
    {

        // Stores the binary
        // representation of N
        var a = N.toString(2);

        // Stores the MSB bit
        var m = a.length - 1;

        // Stores the count
        // of numbers
        var res = N - (Math.pow(2, m) - 1);

        // Return res
        return res;

    }

    // Driver Code

        // Given Input
        var N = 18;

        // Function Call
        document.write(count(N));

// This code is contributed by shikhasingrajput
</script>
```

**Output**

```
3
```

***时间复杂度:** O(log(N))*
***辅助空间:** O(1)*