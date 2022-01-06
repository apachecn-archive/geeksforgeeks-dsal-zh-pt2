# 找出和等于 N 且平方和最大的 K 个数

> 原文:[https://www . geeksforgeeks . org/find-k-numbers-sum-equal-n-and-sum-of-squares-maximized/](https://www.geeksforgeeks.org/find-k-numbers-with-sum-equal-to-n-and-sum-of-their-squares-maximized/)

给定两个整数 **N** 和 **K** ，任务是找到 **K** 号( **A <sub>1</sub> 、A <sub>2</sub> 、…、A <sub>K</sub>** )使得**∑<sub>I = 1</sub><sup>K</sup>A<sub>I</sub>T21】等于 **N**
**例:**** 

> **输入:** N = 3，K = 2
> **输出:** 1 2
> **说明:**两个数之和等于 N，1 <sup>2</sup> + 2 <sup>2</sup> 最大。
> **输入:** N = 10，K = 3
> **输出:** 1 8 1

**进场:**思路为取号 **1** 、**K–1**次，取号**N–K+1**一次。这些数的和等于 **N** ，这些数的平方和总是最大的。对于任意两个非负数 **a** 和 **b** ，**(a<sup>2</sup>+b<sup>2</sup>)**始终小于**1+(a+b–1)<sup>2</sup>**。
以下是上述方法的实施:

## C++

```
// C++ program to find K numbers
// with sum equal to N and the
// sum of their squares maximized
#include <bits/stdc++.h>
using namespace std;

// Function that prints the
// required K numbers
void printKNumbers(int N, int K)
{
    // Print 1, K-1 times
    for (int i = 0; i < K - 1; i++)
        cout << 1 << " ";

    // Print (N-K+1)
    cout << (N - K + 1);
}

// Driver Code
int main()
{
    int N = 10, K = 3;

    printKNumbers(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find K numbers
// with sum equal to N and the
// sum of their squares maximized
class GFG{

// Function that prints the
// required K numbers
static void printKNumbers(int N, int K)
{
    // Print 1, K-1 times
    for(int i = 0; i < K - 1; i++)
        System.out.print(1 + " ");

    // Print (N - K + 1)
    System.out.print(N - K + 1);
}

// Driver Code
public static void main(String[] args)
{
    int N = 10, K = 3;
    printKNumbers(N, K);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to find K numbers
# with a sum equal to N and the
# sum of their squares maximized

# Function that prints the
# required K numbers
def printKNumbers(N, K):

    # Print 1, K-1 times
    for i in range(K - 1):
        print(1, end = ' ')

    # Print (N-K+1)
    print(N - K + 1)

# Driver code
if __name__=='__main__':

    (N, K) = (10, 3)

    printKNumbers(N, K)

# This code is contributed by rutvik_56
```

## C#

```
// C# program to find K numbers
// with sum equal to N and the
// sum of their squares maximized
using System;

class GFG{

// Function that prints the
// required K numbers
static void printKNumbers(int N, int K)
{

    // Print 1, K-1 times
    for(int i = 0; i < K - 1; i++)
        Console.Write(1 + " ");

    // Print (N - K + 1)
    Console.Write(N - K + 1);
}

// Driver code
public static void Main(String[] args)
{
    int N = 10, K = 3;

    printKNumbers(N, K);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

    // Javascript program to find K numbers
    // with sum equal to N and the
    // sum of their squares maximized

    // Function that prints the
    // required K numbers
    function printKNumbers(N, K)
    {
        // Print 1, K-1 times
        for (let i = 0; i < K - 1; i++)
            document.write(1 + " ");

        // Print (N-K+1)
        document.write(N - K + 1);
    }

     let N = 10, K = 3;

    printKNumbers(N, K);

</script>
```

**Output:** 

```
1 1 8
```

**时间复杂度:***O(K)*
T5】辅助空间: *O(1)*