# 找到一个数字 M < N，这样它们的异或和与之间的差值最大

> 原文:[https://www . geesforgeks . org/find-a-number-m-n-so-and-xor-and-is-max/](https://www.geeksforgeeks.org/find-a-number-m-n-such-that-difference-between-their-xor-and-and-is-maximum/)

给定一个自然数 **N** ，任务是找到一个比 **N** 小的数 **M** ，使得它们的[按位异或](https://www.geeksforgeeks.org/tag/xor/) ( **N ^ M** )和[按位与](https://www.geeksforgeeks.org/bitwise-and-or-of-a-range/) ( **N & M** )之间的差值最大。

**示例:**

> **输入:** N = 4
> **输出:** 3
> **解释:**
> (4 ^ 0)–(4&0)= 4
> (4 ^ 1)–(4&1)= 5
> (4 ^ 2)–(4&2)= 6
> (4 ^ 3)–(4&3)= 7
> 因此，m 的值为 3。
> 
> **输入:** N = 6
> **输出:** 1
> **解释:**
> n ^ m 和 N & M 的差值在 M = 1 时最大。

**天真的方法:**想法是迭代小于 **N** 的每个元素，找到 **M** ,其中**n^m–n&m**最大。以下是步骤:

*   初始化一个变量比如说 *maxDiff* 用 0，M 用-1。
*   从 0 迭代到 N-1，计算 **diff = N^i -N & i** 。
*   如果 diff 大于或等于 *maxDiff* ，则分配 M = i，maxDiff = diff。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return M<N such that
// N^M - N&M is maximum
int getMaxDifference(int N)
{
    // Initialize variables
    int M = -1;
    int maxDiff = 0;

    // Iterate for all values < N
    for (int i = 0; i < N; i++) {

        // Find the difference between
        // Bitwise XOR and AND
        int diff = (N ^ i) - (N & i);

        // Check if new difference is
        // greater than previous maximum
        if (diff >= maxDiff) {

            // Update variables
            maxDiff = diff;
            M = i;
        }
    }

    // Return the answer
    return M;
}

// Driver Code
int main()
{
    // Given Number N
    int N = 6;

    // Function Call
    cout << getMaxDifference(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to return M<N such that
// N^M - N&M is maximum
static int getMaxDifference(int N)
{
    // Initialize variables
    int M = -1;
    int maxDiff = 0;

    // Iterate for all values < N
    for (int i = 0; i < N; i++)
    {

        // Find the difference between
        // Bitwise XOR and AND
        int diff = (N ^ i) - (N & i);

        // Check if new difference is
        // greater than previous maximum
        if (diff >= maxDiff)
        {

            // Update variables
            maxDiff = diff;
            M = i;
        }
    }

    // Return the answer
    return M;
}

// Driver Code
public static void main(String[] args)
{
    // Given Number N
    int N = 6;

    // Function Call
    System.out.print(getMaxDifference(N));
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to return M<N such that
# N^M - N&M is maximum
def getMaxDifference(N):

    # Initialize variables
    M = -1;
    maxDiff = 0;

    # Iterate for all values < N
    for i in range(N):

        # Find the difference between
        # Bitwise XOR and AND
        diff = (N ^ i) - (N & i);

        # Check if new difference is
        # greater than previous maximum
        if (diff >= maxDiff):

            # Update variables
            maxDiff = diff;
            M = i;

    # Return the answer
    return M;

# Driver Code
if __name__ == '__main__':

    # Given number N
    N = 6;

    # Function call
    print(getMaxDifference(N));

# This code is contributed by amal kumar choubey
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to return M<N such that
// N^M - N&M is maximum
static int getMaxDifference(int N)
{

    // Initialize variables
    int M = -1;
    int maxDiff = 0;

    // Iterate for all values < N
    for(int i = 0; i < N; i++)
    {

        // Find the difference between
        // Bitwise XOR and AND
        int diff = (N ^ i) - (N & i);

        // Check if new difference is
        // greater than previous maximum
        if (diff >= maxDiff)
        {

            // Update variables
            maxDiff = diff;
            M = i;
        }
    }

    // Return the answer
    return M;
}

// Driver Code
public static void Main(String[] args)
{

    // Given number N
    int N = 6;

    // Function call
    Console.Write(getMaxDifference(N));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript program for the above approach   
// Function to return M<N such that
    // N^M - N&M is maximum
    function getMaxDifference(N) {
        // Initialize variables
        var M = -1;
        var maxDiff = 0;

        // Iterate for all values < N
        for (i = 0; i < N; i++) {

            // Find the difference between
            // Bitwise XOR and AND
            var diff = (N ^ i) - (N & i);

            // Check if new difference is
            // greater than previous maximum
            if (diff >= maxDiff) {

                // Update variables
                maxDiff = diff;
                M = i;
            }
        }

        // Return the answer
        return M;
    }

    // Driver Code

        // Given Number N
        var N = 6;

        // Function Call
        document.write(getMaxDifference(N));

// This code contributed by aashish1995
</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**高效方法:**思路是观察[按位异或和按位与](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)的差值最大，如果两个数的按位与是最小可能数，最小可能数是 **0** 。
当且仅当两个数互补时，两个数之间的按位“与”为零。因此 **M** 的可能值必须是给定数 **N** 的[补码。
以下是上述方法的实施:](https://www.geeksforgeeks.org/find-ones-complement-integer/) 

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to flip all bits of N
int findM(int N)
{
    int M = 0;

    // Finding most significant bit of N
    int MSB = (int)log2(N);

    // Calculating required number
    for (int i = 0; i < MSB; i++) {

        if (!(N & (1 << i)))
            M += (1 << i);
    }

    // Return the answer
    return M;
}

// Driver Code
int main()
{
    // Given Number
    int N = 6;

    // Function Call
    cout << findM(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to flip all bits of N
static int findM(int N)
{
    int M = 0;

    // Finding most significant bit of N
    int MSB = (int)Math.log(N);

    // Calculating required number
    for(int i = 0; i < MSB; i++)
    {
        if ((N & (1 << i)) == 0)
            M += (1 << i);
    }

    // Return the answer
    return M;
}

// Driver Code
public static void main(String[] args)
{

    // Given number
    int N = 6;

    // Function call
    System.out.print(findM(N));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to flip all bits of N
def findM(N):

    M = 0;

    # Finding most significant bit of N
    MSB = int(math.log(N));

    # Calculating required number
    for i in range(MSB):
        if ((N & (1 << i)) == 0):
            M += (1 << i);

    # Return the answer
    return M;

# Driver Code
if __name__ == '__main__':

    # Given number
    N = 6;

    # Function call
    print(findM(N));

# This code is contributed by Amit Katiyar
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to flip all bits of N
static int findM(int N)
{
    int M = 0;

    // Finding most significant bit of N
    int MSB = (int)Math.Log(N);

    // Calculating required number
    for(int i = 0; i < MSB; i++)
    {
        if ((N & (1 << i)) == 0)
            M += (1 << i);
    }

    // Return the answer
    return M;
}

// Driver Code
public static void Main(String[] args)
{

    // Given number
    int N = 6;

    // Function call
    Console.Write(findM(N));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// javascript program for the above approach   
// Function to flip all bits of N
    function findM(N) {
        var M = 0;

        // Finding most significant bit of N
        var MSB = parseInt( Math.log(N));

        // Calculating required number
        for (i = 0; i < MSB; i++) {
            if ((N & (1 << i)) == 0)
                M += (1 << i);
        }

        // Return the answer
        return M;
    }

    // Driver Code

        // Given number
        var N = 6;

        // Function call
        document.write(findM(N));

// This code is contributed by Rajput-Ji
</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(log<sub>2</sub>N)*
***辅助空间:** O(1)*