# 元素范围为[0，2^k–1]且按位等于 0 的 n 大小最大和数组的计数

> 原文:[https://www . geesforgeks . org/count-of-n-size-max-sum-arrays-in-range-0-2k-1-and-bitwise-and-equal-0/](https://www.geeksforgeeks.org/count-of-n-size-maximum-sum-arrays-with-elements-in-range-0-2k-1-and-bitwise-and-equal-to-0/)

给定两个正整数 **N** 和 **K** ，任务是找到大小为 **N** 的数组的数量，使得每个数组元素位于范围**【0，2】<sup>K</sup>–1】**内，数组元素的最大[和具有所有数组元素 **0** 的](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)[位与](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。

**示例:**

> **输入:** N = 2 K = 2
> **输出:** 4
> **解释:**
> 所有数组元素的位与为 0 {0，3}、{3，0}、{1，2}、{2，1}的可能最大和数组。这种数组的计数是 4。
> 
> **输入:**N = 5k = 6
> T3】输出: 15625

**方法:**可以通过观察以下事实来解决给定的问题:由于生成的数组的[位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)应该是 **0** ，那么对于范围**【0，K–1】**中的每个 **i** 应该至少有一个元素的 **i <sup>th</sup>** 位等于其 **0** 的[二进制表示](https://www.geeksforgeeks.org/binary-representations-in-digital-logic/)。因此，为了最大化[数组](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)的和，最好正好有 1 个元素的 **i <sup>th</sup>** 位未置位。

因此，对于每一个 **K** 位，有 **<sup>N</sup> C <sub>1</sub>** 种方式使其在一个数组元素中不设置。因此，具有最大和的数组的合成计数由 [**N <sup>K</sup>**](https://www.geeksforgeeks.org/write-an-iterative-olog-y-function-for-powx-y/) 给出。

以下是该方法的实施情况:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the value of X to
// the power Y
int power(int x, unsigned int y)
{
    // Stores the value of X^Y
    int res = 1;

    while (y > 0) {

        // If y is odd, multiply x
        // with result
        if (y & 1)
            res = res * x;

        // Update the value of y and x
        y = y >> 1;
        x = x * x;
    }

    // Return the result
    return res;
}

// Function to count number of arrays
// having element over the range
// [0, 2^K - 1] with Bitwise AND value
// 0 having maximum possible sum
void countArrays(int N, int K)
{
    // Print the value of N^K
    cout << int(power(N, K));
}

// Driver Code
int main()
{
    int N = 5, K = 6;
    countArrays(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG
{

// Function to find the value of X to
// the power Y
static int power(int x, int y)
{

    // Stores the value of X^Y
    int res = 1;

    while (y > 0) {

        // If y is odd, multiply x
        // with result
        if (y%2!=0)
            res = res * x;

        // Update the value of y and x
        y = y >> 1;
        x = x * x;
    }

    // Return the result
    return res;
}

// Function to count number of arrays
// having element over the range
// [0, 2^K - 1] with Bitwise AND value
// 0 having maximum possible sum
static void countArrays(int N, int K)
{

    // Print the value of N^K
   System.out.println((int)(power(N, K)));
}

// Driver Code
public static void main(String args[])
{
    int N = 5, K = 6;
    countArrays(N, K);
}
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python Program for the above approach

# Function to find the value of X to
# the power Y
def power(x, y):
    # Stores the value of X^Y
    res = 1

    while (y > 0):

        # If y is odd, multiply x
        # with result
        if (y & 1):
            res = res * x

        # Update the value of y and x
        y = y >> 1
        x = x * x

    # Return the result
    return res

# Function to count number of arrays
# having element over the range
# [0, 2^K - 1] with Bitwise AND value
# 0 having maximum possible sum
def countArrays(N, K):
    # Print the value of N^K
    print(power(N, K))

# Driver Code

N = 5;
K = 6;
countArrays(N, K)

# This code is contributed by gfgking
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the value of X to
// the power Y
static int power(int x, int y)
{

    // Stores the value of X^Y
    int res = 1;

    while (y > 0)
    {

        // If y is odd, multiply x
        // with result
        if (y % 2 != 0)
            res = res * x;

        // Update the value of y and x
        y = y >> 1;
        x = x * x;
    }

    // Return the result
    return res;
}

// Function to count number of arrays
// having element over the range
// [0, 2^K - 1] with Bitwise AND value
// 0 having maximum possible sum
static void countArrays(int N, int K)
{

    // Print the value of N^K
    Console.WriteLine((int)(power(N, K)));
}

// Driver Code
public static void Main()
{
    int N = 5, K = 6;

    countArrays(N, K);
}
}

// This code is contributed by subhammahato348
```

## java 描述语言

```
<script>
        // JavaScript Program for the above approach

        // Function to find the value of X to
        // the power Y
        function power(x, y) {
            // Stores the value of X^Y
            let res = 1;

            while (y > 0) {

                // If y is odd, multiply x
                // with result
                if (y & 1)
                    res = res * x;

                // Update the value of y and x
                y = y >> 1;
                x = x * x;
            }

            // Return the result
            return res;
        }

        // Function to count number of arrays
        // having element over the range
        // [0, 2^K - 1] with Bitwise AND value
        // 0 having maximum possible sum
        function countArrays(N, K) {
            // Print the value of N^K
            document.write(power(N, K));
        }

        // Driver Code

        let N = 5, K = 6;
        countArrays(N, K);

    // This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
15625
```

***时间复杂度:** O(log K)*
***辅助空间:** O(1)*