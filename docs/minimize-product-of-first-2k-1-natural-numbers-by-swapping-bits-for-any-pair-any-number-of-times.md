# 通过多次交换任意对的位来最小化第一 2^k–1 自然数的乘积

> 原文:[https://www . geesforgeks . org/通过任意对任意次数的位交换来最小化首个 2k-1 自然数的乘积/](https://www.geeksforgeeks.org/minimize-product-of-first-2k-1-natural-numbers-by-swapping-bits-for-any-pair-any-number-of-times/)

给定一个正整数 **K** ，的任务是通过任意次交换任意两个数对应位置的位来最小化第一个**(2<sup>K</sup>–1)**[自然数](https://www.geeksforgeeks.org/natural-numbers/)的正积。

**示例:**

> **输入:** K = 3
> **输出:** 1512
> **说明**:原产品为 5040。给定的二进制数组是{001，010，011，100，101，110，111}
> 
> *   在第一个操作中，交换第二个和第五个元素的最左边的位。得到的数组是[001，110，011，100，001，110，111]。
> *   在第二个操作中，交换第三和第四个元素的中间位。得到的数组是[001，110，001，110，001，110，111]。
> 
> 经过以上操作，数组元素为{1，6，1，6，1，6，7}。因此，乘积为 1 * 6 * 1 * 6 * 1 * 6 * 7 = 1512，这是最小可能的正乘积。
> 
> **输入:** K = 2
> **输出:** 6
> **解释**:二进制记数法中的原始排列为{'00 '，' 01 '，' 10'}。任何交换都将导致产品为零或根本不变。因此 6 是正确的输出。

**方法:**给定的问题可以基于这样的观察来解决，即为了获得最小的正积，数字 **1** 的频率应该通过交换任意两个数字的比特来最大化。按照以下步骤解决给定的问题:

*   求**范围**的值为**(2<sup>K</sup>–1)**。
*   通过将奇数的所有位转换为偶数，将**范围/2** 元素转换为 1，除了 **0 <sup>第</sup>位**。
*   因此，**范围/2** 号为 1，**范围/2** 号为**范围–1**，数组中的最后一个号将保持与**范围**的值相同。
*   求上述步骤中形成的所有数的乘积，作为所得的最小正积。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum positive
// product after swapping bits at the
// similar position for any two numbers
int minimumPossibleProduct(int K)
{
    // Stores the resultant number
    int res = 1;

    int range = (1 << K) - 1;

    // range/2 numbers will be 1 and
    // range/2 numbers will be range-1
    for (int i = 0; i < K; i++) {
        res *= (range - 1);
    }

    // Multiply with the final number
    res *= range;

    // Return the answer
    return res;
}
// Driver Code
int main()
{
    int K = 3;
    cout << minimumPossibleProduct(K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

// Function to find the minimum positive
// product after swapping bits at the
// similar position for any two numbers
static int minimumPossibleProduct(int K)
{
    // Stores the resultant number
    int res = 1;

    int range = (1 << K) - 1;

    // range/2 numbers will be 1 and
    // range/2 numbers will be range-1
    for (int i = 0; i < K; i++) {
        res *= (range - 1);
    }

    // Multiply with the final number
    res *= range;

    // Return the answer
    return res;
}

// Driver Code
public static void main (String[] args) {

    int K = 3;
    System.out.println(minimumPossibleProduct(K));
}
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find the minimum positive
# product after swapping bits at the
# similar position for any two numbers
def minimumPossibleProduct(K):

    # Stores the resultant number
    res = 1
    r = (1 << K) - 1

    # range/2 numbers will be 1 and
    # range/2 numbers will be range-1
    for i in range(0, K):
        res *= (r - 1)

    # Multiply with the final number
    res *= r

    # Return the answer
    return res

# Driver Code
K = 3
print(minimumPossibleProduct(K))

# This code is contributed by amreshkumar3.
```

## C#

```
// C# program for the above approach
using System;

class GFG {

    // Function to find the minimum positive
    // product after swapping bits at the
    // similar position for any two numbers
    static int minimumPossibleProduct(int K)
    {

        // Stores the resultant number
        int res = 1;

        int range = (1 << K) - 1;

        // range/2 numbers will be 1 and
        // range/2 numbers will be range-1
        for (int i = 0; i < K; i++) {
            res *= (range - 1);
        }

        // Multiply with the final number
        res *= range;

        // Return the answer
        return res;
    }

    // Driver Code
    public static void Main(string[] args)
    {

        int K = 3;
        Console.WriteLine(minimumPossibleProduct(K));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the minimum positive
        // product after swapping bits at the
        // similar position for any two numbers
        function minimumPossibleProduct(K)
        {

            // Stores the resultant number
            let res = 1;

            let range = (1 << K) - 1;

            // range/2 numbers will be 1 and
            // range/2 numbers will be range-1
            for (let i = 0; i < K; i++) {
                res *= (range - 1);
            }

            // Multiply with the final number
            res *= range;

            // Return the answer
            return res;
        }

        // Driver Code

        let K = 3;
        document.write(minimumPossibleProduct(K));

     // This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
1512
```

***时间复杂度:** O(K)*
***辅助空间:** O(1)*