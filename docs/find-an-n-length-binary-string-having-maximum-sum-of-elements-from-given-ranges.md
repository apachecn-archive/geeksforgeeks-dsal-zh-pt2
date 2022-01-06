# 从给定的范围内找到一个元素和最大的 N 长度二进制字符串

> 原文:[https://www . geeksforgeeks . org/find-an-n-length-binary-string-具有给定范围的最大元素总和/](https://www.geeksforgeeks.org/find-an-n-length-binary-string-having-maximum-sum-of-elements-from-given-ranges/)

给定一组大小为 **M** 的[对](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/) **范围[]** 和一个整数 **N** ，任务是找到长度为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)，使得来自给定范围的[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/)的元素之和最大可能。

**例:**

> ***输入:** N = 5，M = 3，范围[] = {{1，3}，{2，4}，{2，5}}*
> ***输出:** 01100*
> ***解释:***
> *范围[1，3]:0 的 Freq = 1，1 的 Freq = 2。总和= 1*2 = 2*
> *范围[2，4]:0 的频率= 1，1 的频率= 2。总和= 1*2 = 2*
> *范围[2，5]:0 的频率= 2，1 的频率= 2。求和= 2*2 = 4*
> *因此，所需求和= 2 + 2 + 4 = 8，这是最大可能。*
> 
> ***输入:** N = 6，M = 1，范围= {{1，6}}*
> ***输出:** 000111*

**方法:**给定的问题可以通过在每个范围内尽可能小地找到**0**的计数和**1**的计数之间的[绝对差](https://www.geeksforgeeks.org/absolute-difference-of-all-pairwise-consecutive-elements-in-an-array/)来解决。因此，想法是将两者，即 **0** 和 **1** 以几乎相等的频率放置在[串](https://www.geeksforgeeks.org/category/data-structures/c-strings/)中。最好的方法是交替放置 **0s** 和 **1s** 。

因此，从上面的观察来看，为了生成结果字符串，想法是使用变量 **i** 在范围**【1，N】**上迭代，如果 **i** 的值是奇数，则打印 **0，**否则打印 **1** 。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find an N-length binary
// string having maximum sum of
// elements from all given ranges
void printBinaryString(int arr[][3], int N)
{
    // Iterate over the range [1, N]
    for (int i = 1; i <= N; i++) {

        // If i is odd, then print 0
        if (i % 2) {
            cout << 0;
        }

        // Otherwise, print 1
        else {
            cout << 1;
        }
    }
}

// Driver Code
int main()
{
    int N = 5, M = 3;
    int arr[][3] = { { 1, 3 },
                     { 2, 4 },
                     { 2, 5 } };

    // Function Call
    printBinaryString(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

  // Function to find an N-length binary
// string having maximum sum of
// elements from all given ranges
static void printBinaryString(int arr[][], int N)
{

    // Iterate over the range [1, N]
    for (int i = 1; i <= N; i++) {

        // If i is odd, then print 0
        if (i % 2 == 1) {
             System.out.print(0);
        }

        // Otherwise, print 1
        else {
            System.out.print(1);
        }
    }
}

// Driver Code
    public static void main (String[] args) {
        int N = 5, M = 3;
    int arr[][] = { { 1, 3 },
                     { 2, 4 },
                     { 2, 5 } };

    // Function Call
    printBinaryString(arr, N);
    }
}

// This code is contributed by Lokeshpotta20.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find an N-length binary
# string having maximum sum of
# elements from all given ranges
def printBinaryString(arr, N):
    # Iterate over the range [1, N]
    for i in range(1, N + 1):

        # If i is odd, then print 0
        if (i % 2):
            print(0, end="");

        # Otherwise, print 1
        else:
            print(1, end="");

# Driver Code
N = 5;
M = 3;
arr = [ [ 1, 3 ], [ 2, 4 ], [ 2, 5 ] ];

# Function Call
printBinaryString(arr, N);

# This code is contributed by _saurabh_jaiswal.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find an N-length binary
// string having maximum sum of
// elements from all given ranges
static void printBinaryString(int [,]arr, int N)
{

    // Iterate over the range [1, N]
    for (int i = 1; i <= N; i++) {

        // If i is odd, then print 0
        if (i % 2 == 1) {
           Console.Write(0);
        }

        // Otherwise, print 1
        else {
            Console.Write(1);
        }
    }
}

// Driver Code
public static void Main()
{
    int N = 5;
    int [,]arr = { { 1, 3 },
                     { 2, 4 },
                     { 2, 5 } };

    // Function Call
    printBinaryString(arr, N);
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find an N-length binary
// string having maximum sum of
// elements from all given ranges
function printBinaryString(arr, N)
{
    // Iterate over the range [1, N]
    for (let i = 1; i <= N; i++) {

        // If i is odd, then print 0
        if (i % 2) {
            document.write(0);
        }

        // Otherwise, print 1
        else {
            document.write(1);
        }
    }
}

// Driver Code
    let N = 5, M = 3;
    let arr = [ [ 1, 3 ],
                     [ 2, 4 ],
                     [ 2, 5 ] ];

    // Function Call
    printBinaryString(arr, N);

// This code is contributed by subhammahato348.
</script>
```

**Output:** 

```
01010
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)