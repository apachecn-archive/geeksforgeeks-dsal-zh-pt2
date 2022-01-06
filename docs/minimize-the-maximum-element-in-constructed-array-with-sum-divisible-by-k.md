# 用可被 K 整除的和最小化构造数组中的最大元素

> 原文:[https://www . geeksforgeeks . org/最小化被 k 整除的构造数组中的最大元素/](https://www.geeksforgeeks.org/minimize-the-maximum-element-in-constructed-array-with-sum-divisible-by-k/)

给定两个整数 **N** 和 **K** ，任务是找到由正整数组成的大小为 **N** 的数组的最大元素的最小值，该数组的元素之和可被 **K** 整除。

**示例:**

> **输入:** N = 4，K = 3
> **输出:** 2
> **解释:**
> 让数组为[2，2，1，1]。这里，这个数组的元素之和可以被 K=3 整除，最大元素是 2。
> 
> **输入:** N = 3，K = 5
> T3】输出: 2

**方法:**要找到大小为 N 且和可被 K 整除的数组的最小最大值，请尝试创建一个和可能最小的数组。

*   可被 K 整除的 N 个元素(**的最小值大于 0** )之和为:

```
sum = K * ceil(N/K)
```

*   现在，如果和能被 N 整除，那么最大元素就是**和/N** ，否则就是**(和/N + 1)。**

下面是上述方法的实现。

## C++

```
// C++ program for the above approach.

#include <iostream>
using namespace std;

// Function to find smallest maximum number
// in an array whose sum is divisible by K.
int smallestMaximum(int N, int K)
{
    // Minimum possible sum possible
    // for an array of size N such that its
    // sum is divisible by K
    int sum = ((N + K - 1) / K) * K;

    // If sum is not divisible by N
    if (sum % N != 0)
        return (sum / N) + 1;

    // If sum is divisible by N
    else
        return sum / N;
}

// Driver code.
int main()
{
    int N = 4;
    int K = 3;

    cout << smallestMaximum(N, K) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to find smallest maximum number
// in an array whose sum is divisible by K.
static int smallestMaximum(int N, int K)
{
    // Minimum possible sum possible
    // for an array of size N such that its
    // sum is divisible by K
    int sum = ((N + K - 1) / K) * K;

    // If sum is not divisible by N
    if (sum % N != 0)
        return (sum / N) + 1;

    // If sum is divisible by N
    else
        return sum / N;
}

// Driver code
public static void main(String args[])
{
    int N = 4;
    int K = 3;

    System.out.println(smallestMaximum(N, K));
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# python program for the above approach.
# Function to find smallest maximum number
# in an array whose sum is divisible by K.
def smallestMaximum(N,K):

    # Minimum possible sum possible
    # for an array of size N such that its
    # sum is divisible by K
    sum = ((N + K - 1) // K) * K

    # If sum is not divisible by N
    if (sum % N != 0):
        return (sum // N) + 1

    # If sum is divisible by N
    else:
        return sum // N

# Driver code.
if __name__ == "__main__":
    N = 4
    K = 3

    print(smallestMaximum(N, K))

# This code is contributed by anudeep23042002.
```

## C#

```
// C# program for the above approach.
using System;
using System.Collections.Generic;

class GFG{

// Function to find smallest maximum number
// in an array whose sum is divisible by K.
static int smallestMaximum(int N, int K)
{
    // Minimum possible sum possible
    // for an array of size N such that its
    // sum is divisible by K
    int sum = ((N + K - 1) / K) * K;

    // If sum is not divisible by N
    if (sum % N != 0)
        return (sum / N) + 1;

    // If sum is divisible by N
    else
        return sum / N;
}

// Driver code.
public static void Main()
{
    int N = 4;
    int K = 3;
    Console.Write(smallestMaximum(N, K));
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find smallest maximum number
        // in an array whose sum is divisible by K.
        function smallestMaximum(N, K)
        {

            // Minimum possible sum possible
            // for an array of size N such that its
            // sum is divisible by K
            let sum = Math.floor((N + K - 1) / K) * K;

            // If sum is not divisible by N
            if (sum % N != 0)
                return Math.floor(sum / N) + 1;

            // If sum is divisible by N
            else
                return Math.floor(sum / N);
        }

        // Driver code.

        let N = 4;
        let K = 3;

        document.write(smallestMaximum(N, K));

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
2
```

***时间复杂度:*** O(1)
***辅助空间:*** O(1)