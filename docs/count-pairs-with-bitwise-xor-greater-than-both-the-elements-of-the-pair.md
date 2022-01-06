# 对大于对的两个元素进行按位异或运算的对进行计数

> 原文:[https://www . geesforgeks . org/count-pairs-with-bitwise-xor-大于-two-of-the-elements-of-the-pair/](https://www.geeksforgeeks.org/count-pairs-with-bitwise-xor-greater-than-both-the-elements-of-the-pair/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是计算其[按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)大于对中两个元素的对的数量。

**示例:**

> **输入:** arr[] = {2，4，3}
> **输出:** 2
> **解释:**只有 2 对元素的按位异或大于对中的两个元素:
> 1) **(2，4):** 按位异或= 2 ^ 4 = 6，大于 2 和 4。
> 2) **(4，3):** 按位异或= 4 ^ 3 = 7，大于 4 和 3。
> 
> **输入:** arr[] = {2，2，2}
> **输出:** 0
> **解释:**由于所有数组元素都相同，所有可能对的按位异或都为 0。因此，不存在这样的配对

**方法**:最简单的方法是[从给定的数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)中生成所有可能的对，并对那些**按位异或**大于两个元素的对进行计数。仅在检查所有对一次后打印计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that counts the pairs whose
// Bitwise XOR is greater than both
// the elements of pair
void countPairs(int A[], int N)
{
    // Stores the count of pairs
    int count = 0;

    // Generate all possible pairs
    for (int i = 0; i < N; i++) {

        for (int j = i + 1; j < N; j++) {

            // Find the Bitwise XOR
            int xo = (A[i] ^ A[j]);

            // Find the maximum of two
            int mx = max(A[i], A[j]);

            // If xo < mx, increment count
            if (xo > mx) {
                count++;
            }
        }
    }

    // Print the value of count
    cout << count;
}

// Driver Code
int main()
{
    int arr[] = { 2, 4, 3 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    countPairs(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function that counts the pairs whose
// Bitwise XOR is greater than both
// the elements of pair
static void countPairs(int[] A, int N)
{

    // Stores the count of pairs
    int count = 0;

    // Generate all possible pairs
    for(int i = 0; i < N; i++)
    {
        for(int j = i + 1; j < N; j++)
        {

            // Find the Bitwise XOR
            int xo = (A[i] ^ A[j]);

            // Find the maximum of two
            int mx = Math.max(A[i], A[j]);

            // If xo < mx, increment count
            if (xo > mx)
            {
                count++;
            }
        }
    }

    // Print the value of count
    System.out.println(count);
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 2, 4, 3 };

    int N = arr.length;

    // Function Call
    countPairs(arr, N);
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that counts the pairs whose
# Bitwise XOR is greater than both
# the elements of pair
def countPairs(A, N):

    # Stores the count of pairs
    count = 0

    # Generate all possible pairs
    for i in range(0, N):
        for j in range(i + 1, N):

            # Find the Bitwise XOR
            xo = (A[i] ^ A[j])

            # Find the maximum of two
            mx = max(A[i], A[j])

            # If xo < mx, increment count
            if (xo > mx):
                count += 1

    # Print the value of count
    print(count)

# Driver Code
if __name__ == '__main__':

    arr = [ 2, 4, 3 ]

    N = len(arr)

    # Function Call
    countPairs(arr, N)

# This code is contributed by akhilsaini
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function that counts the pairs whose
// Bitwise XOR is greater than both
// the elements of pair
static void countPairs(int[] A, int N)
{

    // Stores the count of pairs
    int count = 0;

    // Generate all possible pairs
    for(int i = 0; i < N; i++)
    {
        for(int j = i + 1; j < N; j++)
        {

            // Find the Bitwise XOR
            int xo = (A[i] ^ A[j]);

            // Find the maximum of two
            int mx = Math.Max(A[i], A[j]);

            // If xo < mx, increment count
            if (xo > mx)
            {
                count++;
            }
        }
    }

    // Print the value of count
    Console.WriteLine(count);
}

// Driver Code
public static void Main()
{
    int[] arr = { 2, 4, 3 };

    int N = arr.Length;

    // Function Call
    countPairs(arr, N);
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// javascript program for the above approach   
// Function that counts the pairs whose
    // Bitwise XOR is greater than both
    // the elements of pair
    function countPairs(A , N) {

        // Stores the count of pairs
        var count = 0;

        // Generate all possible pairs
        for (i = 0; i < N; i++) {
            for (j = i + 1; j < N; j++) {

                // Find the Bitwise XOR
                var xo = (A[i] ^ A[j]);

                // Find the maximum of two
                var mx = Math.max(A[i], A[j]);

                // If xo < mx, increment count
                if (xo > mx) {
                    count++;
                }
            }
        }

        // Print the value of count
        document.write(count);
    }

    // Driver Code

        var arr = [ 2, 4, 3 ];

        var N = arr.length;

        // Function Call
        countPairs(arr, N);

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
2
```

**时间复杂度:***O(N<sup>2</sup>)*
T7】辅助空间: O(1)

**高效途径:**优化上述途径，思路是使用[位操作](https://www.geeksforgeeks.org/bits-manipulation-important-tactics/)。考虑 **X = A^B** 和 **A < B** ，让 **K** 成为数字 A 的[最高有效位。现在，如果 **X** 大于元素 **A** 和 **B** 当且仅当 **B** 的第 **K <sup>位</sup>T21 为 **0** 。如果一个整数的第 **K <sup>位</sup>位**已经是第 **0** 位，那么计算数字，使得第 **K <sup>位</sup>位**是另一个整数的第 **MSB 位**。以下是步骤:**](https://www.geeksforgeeks.org/find-significant-set-bit-number/)

*   初始化一个变量**计数**来存储对的计数和一个数组，比如大小为 **32** 和[的**位[]** ，对给定的数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)进行排序。
*   [遍历](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) 数组，并执行以下操作:
    *   如果当前元素为 **0** ，则检查下一个元素。
    *   否则遍历当前元素的所有位，如果在位置 **j** 的任何位被设置，那么将**计数**增加**位【j】**。
    *   完成上述步骤后，通过 **1** 更新**位【日志 <sub>2</sub> (当前元素)】**。
*   完成上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count pairs whose XOR
// is greater than the pair itself
void countPairs(int A[], int N)
{
    // Stores the count of pairs
    int count = 0;

    // Sort the array
    sort(A, A + N);

    int bits[32] = { 0 };

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If current element is 0,
        // then ignore it
        if (A[i] == 0) {
            continue;
        }

        // Traverse all the bits of
        // element A[i]
        for (int j = 0; j < 32; j++) {

            // If current bit is set
            // then update the count
            if (!((1LL << j) & A[i])) {
                count += bits[j];
            }
        }

        // Update bits[] at the most
        // significant bit of A[i]
        ++bits[(int)(log2l(A[i]))];
    }

    // Print the count
    cout << count;
}

// Driver Code
int main()
{
    int arr[] = { 2, 4, 3 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    countPairs(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to count pairs whose XOR
// is greater than the pair itself
static void countPairs(int[] A, int N)
{

    // Stores the count of pairs
    int count = 0;

    // Sort the array
    Arrays.sort(A);

    int[] bits = new int[32];

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // If current element is 0,
        // then ignore it
        if (A[i] == 0)
        {
            continue;
        }

        // Traverse all the bits of
        // element A[i]
        for(int j = 0; j < 32; j++)
        {

            // If current bit is set
            // then update the count
            if (((1 << j) & A[i]) == 0)
            {
                count += bits[j];
            }
        }

        // Update bits[] at the most
        // significant bit of A[i]
        ++bits[(int)((int)(Math.log(A[i]) /
                           Math.log(2)))];
    }

    // Print the count
    System.out.println(count);
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 2, 4, 3 };

    int N = arr.length;

    // Function Call
    countPairs(arr, N);
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to count pairs whose XOR
# is greater than the pair itself
def countPairs(A, N):

    # Stores the count of pairs
    count = 0

    # Sort the array
    A.sort()

    bits = [0] * 32

    # Traverse the array
    for i in range(0, N):

        # If current element is 0,
        # then ignore it
        if (A[i] == 0):
            continue

        # Traverse all the bits of
        # element A[i]
        for j in range(0, 32):

            # If current bit is set
            # then update the count
            if (((1 << j) & A[i]) == 0):
                count += bits[j]

        # Update bits[] at the most
        # significant bit of A[i]
        bits[(int)(math.log(A[i], 2))] += 1

    # Print the count
    print(count)

# Driver Code
if __name__ == '__main__':

    arr = [ 2, 4, 3 ]

    N = len(arr)

    # Function Call
    countPairs(arr, N)

# This code is contributed by akhilsaini
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count pairs whose XOR
// is greater than the pair itself
static void countPairs(int[] A, int N)
{

    // Stores the count of pairs
    int count = 0;

    // Sort the array
    Array.Sort(A);

    int[] bits = new int[32];

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // If current element is 0,
        // then ignore it
        if (A[i] == 0)
        {
            continue;
        }

        // Traverse all the bits of
        // element A[i]
        for(int j = 0; j < 32; j++)
        {

            // If current bit is set
            // then update the count
            if (((1 << j) & A[i]) == 0)
            {
                count += bits[j];
            }
        }

        // Update bits[] at the most
        // significant bit of A[i]
        ++bits[(int)((int)(Math.Log(A[i]) /
                           Math.Log(2)))];
    }

    // Print the count
    Console.WriteLine(count);
}

// Driver Code
public static void Main()
{
    int[] arr = { 2, 4, 3 };

    int N = arr.Length;

    // Function Call
    countPairs(arr, N);
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>
// javascript program for the above approach   
// Function to count pairs whose XOR
    // is greater than the pair itself
    function countPairs(A , N) {

        // Stores the count of pairs
        var count = 0;

        // Sort the array
        A.sort();

        var bits = Array(32).fill(0);

        // Traverse the array
        for (i = 0; i < N; i++) {

            // If current element is 0,
            // then ignore it
            if (A[i] == 0) {
                continue;
            }

            // Traverse all the bits of
            // element A[i]
            for (j = 0; j < 32; j++) {

                // If current bit is set
                // then update the count
                if (((1 << j) & A[i]) == 0) {
                    count += bits[j];
                }
            }

            // Update bits at the most
            // significant bit of A[i]
            bits[parseInt(Math.log(A[i]) / Math.log(2))]++;
        }

        // Prvar the count
        document.write(count);
    }

    // Driver Code
    var arr = [ 2, 4, 3 ];
    var N = arr.length;

    // Function Call
    countPairs(arr, N);

// This code is contributed by Rajput-Ji.
</script>
```

**Output:** 

```
2
```

**时间复杂度:***O(N * log N)*
T5】辅助空间: *O(1)*