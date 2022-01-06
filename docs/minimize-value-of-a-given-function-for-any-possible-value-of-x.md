# 对于任何可能的 X 值，最小化给定函数的值

> 原文:[https://www . geeksforgeeks . org/最小化给定函数的任何可能的 x 值/](https://www.geeksforgeeks.org/minimize-value-of-a-given-function-for-any-possible-value-of-x/)

给定一个由 **N** 个整数( *1 基索引*)组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **A[]** ，任务是为 **X** 的任何可能值找到函数![\sum_{i = 1}^{N}(A[i] - (X + i)) ](img/3173ee2a2f57a9722c07f2bd47404611.png "Rendered by QuickLaTeX.com")的最小值。

**示例:**

> **输入:** A[] = {1，2，3，4}
> **输出:** 0
> **说明:**
> 把 X 的值看作 0，那么给定函数的值就是(1–1+2–2+3–3+4–4)= 0，这是最小值。
> 
> **输入:** A[] = {5，3，9 }
> T3】输出: 5

**方法:**给定的问题可以基于以下观察来解决:

*   考虑一个函数为**(B[I]= A[I]—I)**，然后为了使![\sum_{i = 1}^{N}(B[i] - X)](img/4e35102df63c0cbeebe839a4ffbcf84b.png "Rendered by QuickLaTeX.com")的值最小化，思路是选择 **X** 的值作为数组**B【】**的中值，使得和最小化。

按照以下步骤解决问题:

*   初始化一个数组，比如说 **B[]** ，它为数组 **A[]** 的每个可能值存储**(A[I]–I)**的值。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **A[]** ，对于每个索引 **i** ，将**B【I】**的值更新为**(A[I]–I)**。
*   [将数组 **B[]** 按照升序](https://www.geeksforgeeks.org/sort-array-according-order-defined-another-array/)排序，找到值 **X** 作为数组 **B[]** 的[中值。](https://www.geeksforgeeks.org/median/)
*   完成以上步骤后，求给定函数![\sum_{i = 1}^{N}(A[i] - (X + i)) ](img/3173ee2a2f57a9722c07f2bd47404611.png "Rendered by QuickLaTeX.com")的值为 **X** 的计算值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum value of
// the given function
int minimizeFunction(int A[], int N)
{
    // Stores the value of A[i] - i
    int B[N];

    // Traverse the given array A[]
    for (int i = 0; i < N; i++) {

        // Update the value of B[i]
        B[i] = A[i] - i - 1;
    }

    // Sort the array B[]
    sort(B, B + N);

    // Calculate the median of the
    // array B[]
    int median = (B[int(floor((N - 1) / 2.0))]
                  + B[int(ceil((N - 1) / 2.0))])
                 / 2;

    // Stores the minimum value of
    // the function
    int minValue = 0;

    for (int i = 0; i < N; i++) {

        // Update the minValue
        minValue += abs(A[i] - (median + i + 1));
    }

    // Return the minimum value
    return minValue;
}

// Driver Code
int main()
{
    int A[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
    int N = sizeof(A) / sizeof(A[0]);
    cout << minimizeFunction(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.io.*;
import java.lang.Math;
import java.util.*;

class GFG {
    public static int minimizeFunction(int A[], int N)
    {

        // Stores the value of A[i] - i
        int B[] = new int[N];

        // Traverse the given array A[]
        for (int i = 0; i < N; i++) {

            // Update the value of B[i]
            B[i] = A[i] - i - 1;
        }

        // Sort the array B[]
        Arrays.sort(B);

        // Calculate the median of the
        // array B[]
        int median = (B[(int)(Math.floor((N - 1) / 2.0))]
                      + B[(int)(Math.ceil((N - 1) / 2.0))])
                     / 2;

        // Stores the minimum value of
        // the function
        int minValue = 0;

        for (int i = 0; i < N; i++) {

            // Update the minValue
            minValue += Math.abs(A[i] - (median + i + 1));
        }

        // Return the minimum value
        return minValue;
    }

    public static void main(String[] args)
    {
        int A[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
        int N = A.length;
        System.out.println(minimizeFunction(A, N));
    }
}
// This code is contributed by sam_2200.
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import floor, ceil

# Function to find minimum value of
# the given function

def minimizeFunction(A, N):

    # Stores the value of A[i] - i
    B = [0] * N

    # Traverse the given array A[]
    for i in range(N):

        # Update the value of B[i]
        B[i] = A[i] - i - 1

    # Sort the array B[]
    B = sorted(B)

    # Calculate the median of the
    # array B[]
    x, y = int(floor((N - 1) / 2.0)), int(ceil((N - 1) / 2.0))

    median = (B[x] + B[y]) / 2

    # Stores the minimum value of
    # the function
    minValue = 0

    for i in range(N):

        # Update the minValue
        minValue += abs(A[i] - (median + i + 1))

    # Return the minimum value
    return int(minValue)

# Driver Code
if __name__ == '__main__':

    A = [1, 2, 3, 4, 5, 6, 7, 8, 9]
    N = len(A)

    print(minimizeFunction(A, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG {
    public static int minimizeFunction(int[] A, int N)
    {

        // Stores the value of A[i] - i
        int[] B = new int[N];

        // Traverse the given array A[]
        for (int i = 0; i < N; i++) {

            // Update the value of B[i]
            B[i] = A[i] - i - 1;
        }

        // Sort the array B[]
        Array.Sort(B);

        // Calculate the median of the
        // array B[]
        int median = (B[(int)(Math.Floor((N - 1) / 2.0))] + B[(int)(Math.Ceiling((N - 1) / 2.0))])
                     / 2;

        // Stores the minimum value of
        // the function
        int minValue = 0;

        for (int i = 0; i < N; i++) {

            // Update the minValue
            minValue += Math.Abs(A[i] - (median + i + 1));
        }

        // Return the minimum value
        return minValue;
    }

    static void Main()
    {
        int []A = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
        int N = A.Length;
        Console.WriteLine(minimizeFunction(A, N));
    }
}
// This code is contributed by SoumikMondal.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

function minimizeFunction(A, N){

        // Stores the value of A[i] - i
        let B = Array.from({length: N}, (_, i) => 0);

        // Traverse the given array A[]
        for (let i = 0; i < N; i++) {

            // Update the value of B[i]
            B[i] = A[i] - i - 1;
        }

        // Sort the array B[]
        B.sort();

        // Calculate the median of the
        // array B[]
        let median = (B[(Math.floor((N - 1) / 2.0))]
                      + B[(Math.ceil((N - 1) / 2.0))])
                     / 2;

        // Stores the minimum value of
        // the function
        let minValue = 0;

        for (let i = 0; i < N; i++) {

            // Update the minValue
            minValue += Math.abs(A[i] - (median + i + 1));
        }

        // Return the minimum value
        return minValue;
    }

// Driver Code

    let A = [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ];
    let N = A.length;
    document.write(minimizeFunction(A, N));

</script>
```

**Output:** 

```
0
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(N)*