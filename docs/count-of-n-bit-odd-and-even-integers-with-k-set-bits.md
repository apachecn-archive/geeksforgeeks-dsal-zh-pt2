# K 组位 N 位奇偶整数计数

> 原文:[https://www . geesforgeks . org/带 k 位集的 n 位奇数和偶数整数计数/](https://www.geeksforgeeks.org/count-of-n-bit-odd-and-even-integers-with-k-set-bits/)

给定两个正整数 **N** 和 **K** ，任务是统计由 **N** 位组成的偶数和奇数个数，其中 **K** 位被置位。

**示例:**

> **输入:** N = 5，K = 2
> **输出:** 3 1
> **解释:**
> 具有 2 个设定位的 5 位偶整数为:10010(= 18)、10100(= 20)、11000(= 24)。所以，计数是 3。
> 具有 2 个设定位的 5 位奇数是 10001(=17)。所以，计数是 1。
> 
> **输入:** N = 5，K = 5
> T3】输出: 0 1

**方法:**给定的问题可以使用以下观察结果来解决:

*   对于任何 **N** 位整数， **N <sup>第</sup>T5】位([最高有效位](https://www.geeksforgeeks.org/find-significant-set-bit-number/))必须是设定位。**
*   对于任何奇数位的 **N** 位整数，**1<sup>ST</sup>T5 位([最低有效位](https://www.geeksforgeeks.org/print-kth-least-significant-bit-number/))必须是设定位。**
*   对于任何偶数的 **N** 位整数，**1<sup>ST</sup>T5】位(最低有效位)不得为设置位。**

因此，将 **N <sup>第</sup>T3】位固定为 **1** 位，将**1<sup>ST</sup>T9】位固定为 **0** 位，计算剩余位的排列方式数，即可得到偶数的个数。同样，将 **1 <sup>st</sup>** 和 **N <sup>th</sup>** 位固定为 **1** 即可得到奇数个数。****

排列具有 **Y** 设定位的 **X** 位的不同方式的总数由下式给出:

> ![\frac{X!}{Y!(X - Y)!}        ](img/2a5f7103e166f77b91a67b0d0831acaf.png "Rendered by QuickLaTeX.com")

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
long long factorial(int n)
{
    long long ans = 1;
    while (n >= 1) {
        ans *= n;
        n--;
    }
    return ans;
}

// Function to find the count of odd and
// even integers having N bits and K
// set bits
void Binary_Num(int n, int k)
{
    long long num_even, num_odd;

    // Find the count of even integers
    if (n - k - 1 >= 0 && k - 1 >= 0) {
        num_even
            = factorial(n - 2)
              / (factorial(k - 1) * factorial(n - k - 1));
    }
    else {
        num_even = 0;
    }

    // Find the count of odd integers
    if (k - 2 >= 0) {
        num_odd = factorial(n - 2)
                  / (factorial(k - 2) * factorial(n - k));
    }
    else {
        num_odd = 0;
    }
    // Print the total count
    cout << num_even << " " << num_odd << endl;
}

// Driver code
int main()
{

    int N = 9, K = 6;
    Binary_Num(N, K);
    return 0;
}

// This code is contributed by maddler.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG {
static long  factorial(int n)
{
    long  ans = 1;
    while (n >= 1) {
        ans *= n;
        n--;
    }
    return ans;
}

// Function to find the count of odd and
// even integers having N bits and K
// set bits
static void Binary_Num(int n, int k)
{
    long num_even, num_odd;

    // Find the count of even integers
    if (n - k - 1 >= 0 && k - 1 >= 0) {
        num_even
            = factorial(n - 2)
              / (factorial(k - 1) * factorial(n - k - 1));
    }
    else {
        num_even = 0;
    }

    // Find the count of odd integers
    if (k - 2 >= 0) {
        num_odd = factorial(n - 2)
                  / (factorial(k - 2) * factorial(n - k));
    }
    else {
        num_odd = 0;
    }
    // Print the total count
    System.out.println( num_even +" " +num_odd );
}

    // Driver Code
    public static void main(String[] args)
    {
         int N = 9, K = 6;
    Binary_Num(N, K);
    }
}

// This code is contributed by dwivediyash
```

## 蟒蛇 3

```
# Python program for the above approach

import math

# Function to find the count of odd and
# even integers having N bits and K
# set bits

def Binary_Num(N, K):

    # Find the count of even integers
    if N-K-1 >= 0 and K-1 >= 0:
        num_even = math.factorial(
            N-2)/(math.factorial(K-1)
                  * math.factorial(N-K-1))
    else:
        num_even = 0

    # Find the count of odd integers
    if K-2 >= 0:
        num_odd = math.factorial(N-2) \
            / (math.factorial(K-2)
               * math.factorial(N-K))
    else:
        num_odd = 0

    # Print the total count
    print(int(num_even), int(num_odd))

# Driver Code
if __name__ == "__main__":

    N = 9
    K = 6

    Binary_Num(N, K)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

static int factorial(int n)
{
    int ans = 1;
    while (n >= 1) {
        ans *= n;
        n--;
    }
    return ans;
}

// Function to find the count of odd and
// even integers having N bits and K
// set bits
static void Binary_Num(int n, int k)
{
    int num_even, num_odd;

    // Find the count of even integers
    if (n - k - 1 >= 0 && k - 1 >= 0) {
        num_even
            = factorial(n - 2)
              / (factorial(k - 1) * factorial(n - k - 1));
    }
    else {
        num_even = 0;
    }

    // Find the count of odd integers
    if (k - 2 >= 0) {
        num_odd = factorial(n - 2)
                  / (factorial(k - 2) * factorial(n - k));
    }
    else {
        num_odd = 0;
    }
    // Print the total count
    Console.Write(num_even + " " + num_odd);
}

// Driver code
public static void Main()
{

    int N = 9, K = 6;
    Binary_Num(N, K);
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        function factorial(n) {
            let ans = 1;
            while (n >= 1) {
                ans *= n;
                n--;
            }
            return ans;
        }

        // Function to find the count of odd and
        // even integers having N bits and K
        // set bits
        function Binary_Num(n, k) {
            let num_even, num_odd;

            // Find the count of even integers
            if (n - k - 1 >= 0 && k - 1 >= 0) {
                num_even
                    = Math.floor(factorial(n - 2)
                        / (factorial(k - 1) * factorial(n - k - 1)));
            }
            else {
                num_even = 0;
            }

            // Find the count of odd integers
            if (k - 2 >= 0) {
                num_odd = Math.floor(factorial(n - 2)
                    / (factorial(k - 2) * factorial(n - k)));
            }
            else {
                num_odd = 0;
            }

            // Print the total count
            document.write(num_even + " " + num_odd + "<br>");
        }

        // Driver code
        let N = 9, K = 6;
        Binary_Num(N, K);

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
21 35
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**注意:**对于多个查询，预计算数组中的[阶乘值，这将导致每个查询 O(1)次，预计算 O(N)。](https://www.geeksforgeeks.org/factorial-of-an-array-of-integers/)