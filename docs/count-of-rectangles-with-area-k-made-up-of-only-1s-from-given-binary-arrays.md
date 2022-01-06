# 给定二进制数组中面积为 K 且仅由 1 组成的矩形数

> 原文:[https://www . geeksforgeeks . org/面积为 k 的矩形计数由给定二进制数组中的仅 1 组成/](https://www.geeksforgeeks.org/count-of-rectangles-with-area-k-made-up-of-only-1s-from-given-binary-arrays/)

给定两个长度分别为 **N** 和 **M** 的二进制数组 **A[]** 和 **B[]** ，任务是在两个数组相乘生成的矩阵 **C[][]** 中找到由 **1** 组成的区域 **K** 的矩形数，使得,**C[I][j]= A[I]* B[j]**(1【T16

**示例:**

> **输入:** N= 3，M = 3，A[] = {1，1，0}，B[] = {0，1，1}，K = 2
> **输出:** 4
> **解释:** C[][] = {{0，1，1}，{0，1，1}，{0，0，0}}
> 
> ```
> 0 1 1 0 1 1      0 1 1       0 1 1
> 0 1 1        0 1 1 0 1 1 0 1 1
> 0 0 0        0 0 0      0 0 0       0 0 0
> ```
> 
> 因此，矩阵中有 4 个可能的矩形区域 2。
> **输入:** N = 4，M = 2，A[] = {0，0，1，1}，B[] = {1，0，1}，K = 2
> **输出:** 2
> **解释:** C[][] = {{0，0，0}，{0，0，0}，{1，0，1}，{1，0，1}
> 
> ```
> 0 0 0        0 0 0
> 0 0 0        0 0 0
> 1 0 1        1 0 1
> 1 0 1        1 0 1
> ```
> 
> 因此，矩阵中有 2 个面积为 2 的可能矩形。

**天真方法:**解决问题最简单的方法是**通过将两个数组相乘生成所需的矩阵**，对于每个可能的矩形区域 **K，**检查它是否只包含 1。
***时间复杂度:** O(N * M * K)*
***辅助空间:** O(N * M)*

**高效方法:**为了优化上述方法，需要进行以下观察，而不是生成矩阵:

> *   [The area of a rectangle is equal to the product of its **length** and **width.**](https://www.geeksforgeeks.org/program-area-perimeter-rectangle/)
> *   Using this attribute, the rectangle is visualized as a **submatrix** containing only **1** s. Therefore, this submatrix is the product of two submatrixes of length A and B, where **a * b = k** .
> *   Because the submatrix only contains **1** , it is obvious that these two submatrixes only contain **1** .

因此，问题简化为从阵列 **A[]** 和 **B[]** 中找到仅由所有可能长度的 **1** 组成的子阵列，这些子阵列是 **K** 的适当除子。按照以下步骤解决问题:

*   预先计算可能子阵列的[计数](https://www.geeksforgeeks.org/count-of-possible-subarrays-and-subsequences-using-given-length-of-array/)。
*   遍历 **K** 的所有[因子，对于每一个可能的对( **p，q** ),其中 **p * q = K** ，检查在 A[]和 B[]中是否存在长度为 p，q 的子数组。](https://www.geeksforgeeks.org/number-of-divisors-of-a-given-number-n-which-are-divisible-by-k/)
*   相应地增加这种子阵列的数量，最后打印得到的数量。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the subarrays of
// all possible lengths made up of only 1s
vector<int> findSubarrays(vector<int>& a)
{
    int n = a.size();

    // Stores the frequency
    // of the subarrays
    vector<int> freq(n + 1);

    int count = 0;

    for (int i = 0; i < n; i++) {
        if (a[i] == 0) {

            // Check if the previous
            // value was also 0
            if (count == 0)
                continue;

            // If the previous value was 1
            else {

                int value = count;
                for (int j = 1; j <= count; j++) {

                    // Find the subarrays of
                    // each size from 1 to count
                    freq[j] += value;
                    value--;
                }

                count = 0;
            }
        }

        else
            count++;
    }

    // If A[] is of the form ....111
    if (count > 0) {
        int value = count;
        for (int j = 1; j <= count; j++) {
            freq[j] += value;
            value--;
        }
    }

    return freq;
}

// Function to find the count
// of all possible rectangles
void countRectangles(vector<int>& a,
                     vector<int>& b, int K)
{
    // Size of each of the arrays
    int n = a.size();

    int m = b.size();

    // Stores the count of subarrays
    // of each size consisting of
    // only 1s from array A[]

    vector<int> subA
        = findSubarrays(a);

    // Stores the count of subarrays
    // of each size consisting of
    // only 1s from array B[]
    vector<int> subB
        = findSubarrays(b);

    int total = 0;

    // Iterating over all subarrays
    // consisting of only 1s in A[]
    for (int i = 1; i < subA.size(); i++) {

        // If i is a factor of K, then
        // there is a subarray of size K/i in B[]
        if (K % i == 0 and (K / i) <= m) {
            total = total + subA[i] * subB[K / i];
        }
    }

    cout << total;
}

// Driver Code
int main()
{
    vector<int> a = { 0, 0, 1, 1 };

    vector<int> b = { 1, 0, 1 };
    int K = 2;

    countRectangles(a, b, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
class GFG{

    // Function to find the subarrays of
    // all possible lengths made up of only 1s
    static int[] findSubarrays(int[] a)
    {
        int n = a.length;

        // Stores the frequency
        // of the subarrays
        int[] freq = new int[n + 1];
        int count = 0;
          for (int i = 0; i < n; i++)
        {
            if (a[i] == 0)
            {

                // Check if the previous
                // value was also 0
                if (count == 0)
                    continue;

                // If the previous value was 1
                else
                {
                    int value = count;
                    for (int j = 1; j <= count; j++)
                    {

                        // Find the subarrays of
                        // each size from 1 to count
                        freq[j] += value;
                        value--;
                    }
                    count = 0;
                }
            }
            else
                count++;
        }

        // If A[] is of the form ....111
        if (count > 0)
        {
            int value = count;
            for (int j = 1; j <= count; j++)
            {
                freq[j] += value;
                value--;
            }
        }
        return freq;
    }

    // Function to find the count
    // of all possible rectangles
    static void countRectangles(int[] a, int[] b, int K)
    {
        // Size of each of the arrays
        int n = a.length;
        int m = b.length;

        // Stores the count of subarrays
        // of each size consisting of
        // only 1s from array A[]
        int[] subA = findSubarrays(a);

        // Stores the count of subarrays
        // of each size consisting of
        // only 1s from array B[]
        int[] subB = findSubarrays(b);

        int total = 0;

        // Iterating over all subarrays
        // consisting of only 1s in A[]
        for (int i = 1; i < subA.length; i++)
        {

            // If i is a factor of K, then
            // there is a subarray of size K/i in B[]
            if (K % i == 0 && (K / i) <= m)
            {
                total = total + subA[i] * subB[K / i];
            }
        }
        System.out.print(total);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] a = {0, 0, 1, 1};
        int[] b = {1, 0, 1};
        int K = 2;
        countRectangles(a, b, K);
    }
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the subarrays of
# all possible lengths made up of only 1s
def findSubarrays(a):

    n = len(a)

    # Stores the frequency
    # of the subarrays
    freq = [0] * (n + 1)

    count = 0

    for i in range(n):
        if (a[i] == 0):

            # Check if the previous
            # value was also 0
            if (count == 0):
                continue

            # If the previous value was 1
            else:
                value = count
                for j in range(1, count + 1):

                    # Find the subarrays of
                    # each size from 1 to count
                    freq[j] += value
                    value -= 1

                count = 0

        else:
            count += 1

    # If A[] is of the form ....111
    if (count > 0):
        value = count
        for j in range(1, count + 1):
            freq[j] += value
            value -= 1

    return freq

# Function to find the count
# of all possible rectangles
def countRectangles(a, b, K):

    # Size of each of the arrays
    n = len(a)
    m = len(b)

    # Stores the count of subarrays
    # of each size consisting of
    # only 1s from array A[]
    subA = []
    subA = findSubarrays(a)

    # Stores the count of subarrays
    # of each size consisting of
    # only 1s from array B[]
    subB = []
    subB = findSubarrays(b)

    total = 0

    # Iterating over all subarrays
    # consisting of only 1s in A[]
    for i in range(1, len(subA)):

        # If i is a factor of K, then
        # there is a subarray of size K/i in B[]
        if (K % i == 0 and (K // i) <= m):
            total = total + subA[i] * subB[K // i]

    print(total)

# Driver Code
a = [ 0, 0, 1, 1 ]
b = [ 1, 0, 1 ]

K = 2

countRectangles(a, b, K)

# This code is contributed by code_hunt
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG{

    // Function to find the subarrays of
    // all possible lengths made up of only 1s
    static int[] findSubarrays(int[] a)
    {
        int n = a.Length;

        // Stores the frequency
        // of the subarrays
        int[] freq = new int[n + 1];
        int count = 0;
        for (int i = 0; i < n; i++)
        {
            if (a[i] == 0)
            {
                // Check if the previous
                // value was also 0
                if (count == 0)
                    continue;

                // If the previous value was 1
                else
                {
                    int value = count;
                    for (int j = 1; j <= count; j++)
                    {
                        // Find the subarrays of
                        // each size from 1 to count
                        freq[j] += value;
                        value--;
                    }
                    count = 0;
                }
            }
            else
                count++;
        }

        // If []A is of the form ....111
        if (count > 0)
        {
            int value = count;
            for (int j = 1; j <= count; j++)
            {
                freq[j] += value;
                value--;
            }
        }
        return freq;
    }

    // Function to find the count
    // of all possible rectangles
    static void countRectangles(int[] a, int[] b,
                                int K)
    {
        // Size of each of the arrays
        int n = a.Length;
        int m = b.Length;

        // Stores the count of subarrays
        // of each size consisting of
        // only 1s from array []A
        int[] subA = findSubarrays(a);

        // Stores the count of subarrays
        // of each size consisting of
        // only 1s from array []B
        int[] subB = findSubarrays(b);

        int total = 0;

        // Iterating over all subarrays
        // consisting of only 1s in []A
        for (int i = 1; i < subA.Length; i++)
        {

            // If i is a factor of K, then
            // there is a subarray of size K/i in []B
            if (K % i == 0 && (K / i) <= m)
            {
                total = total + subA[i] *
                        subB[K / i];
            }
        }
        Console.Write(total);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] a = {0, 0, 1, 1};
        int[] b = {1, 0, 1};
        int K = 2;
        countRectangles(a, b, K);
    }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

    // Function to find the subarrays of
    // all possible lengths made up of only 1s
    function findSubarrays(a)
    {
        let n = a.length;

        // Stores the frequency
        // of the subarrays
        let freq = new Array(n+1).fill(0);
        let count = 0;
          for (let i = 0; i < n; i++)
        {
            if (a[i] == 0)
            {

                // Check if the previous
                // value was also 0
                if (count == 0)
                    continue;

                // If the previous value was 1
                else
                {
                    let value = count;
                    for (let j = 1; j <= count; j++)
                    {

                        // Find the subarrays of
                        // each size from 1 to count
                        freq[j] += value;
                        value--;
                    }
                    count = 0;
                }
            }
            else
                count++;
        }

        // If A[] is of the form ....111
        if (count > 0)
        {
            let value = count;
            for (let j = 1; j <= count; j++)
            {
                freq[j] += value;
                value--;
            }
        }
        return freq;
    }

    // Function to find the count
    // of all possible rectangles
    function countRectangles(a, b, K)
    {
        // Size of each of the arrays
        let n = a.length;
        let m = b.length;

        // Stores the count of subarrays
        // of each size consisting of
        // only 1s from array A[]
        let subA = findSubarrays(a);

        // Stores the count of subarrays
        // of each size consisting of
        // only 1s from array B[]
        let subB = findSubarrays(b);

        let total = 0;

        // Iterating over all subarrays
        // consisting of only 1s in A[]
        for (let i = 1; i < subA.length; i++)
        {

            // If i is a factor of K, then
            // there is a subarray of size K/i in B[]
            if (K % i == 0 && (K / i) <= m)
            {
                total = total + subA[i] * subB[K / i];
            }
        }
        document.write(total);
    }

// Driver Code

        let a = [0, 0, 1, 1];
        let b = [1, 0, 1];
        let K = 2;
        countRectangles(a, b, K);

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(D) * O(N + M)，其中 D 为 k 的除数*
***辅助空间:** O(N + M)*