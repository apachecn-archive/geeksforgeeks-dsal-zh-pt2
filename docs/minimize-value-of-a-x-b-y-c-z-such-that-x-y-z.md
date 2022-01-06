# 最小化| A–X |+| B–Y |+| C–Z |的值，使得 X * Y = Z

> 原文:[https://www . geesforgeks . org/minimum-value-a-x-b-y-c-z-so-x-y-z/](https://www.geeksforgeeks.org/minimize-value-of-a-x-b-y-c-z-such-that-x-y-z/)

给定三个整数 **A** 、 **B** 和 **C** ，任务是找到**| A–X |+| B–Y |+| C–Z |**的最小可能值，使得 **X * Y = Z** 。

**例**:

> **输入:** A = 19，B = 28，C = 522
> **输出:** 2
> **解释:**对于给定的 A、B 和 C，X、Y 和 Z 的最优选择是 X = 18，Y = 29，Z = 522。等式 X * Y = Z 成立，并且| A–X |+| B–Y |+| C–Z | = 2 的值是最小可能值。
> 
> **输入:** A = 11，B = 11，C = 121
> **输出:** 0
> **说明:**A，B，C 给定值满足 A * B = C，因此最优选择是 X = A，Y = B，Z = C

**方法:**上述问题可以通过以下观察来解决:

*   **| A–X |+| B–Y |+| C–Z |**的最大值可以是 **A + B + C** 代表 **X** 、 **Y** 、 **Z** 等于 **0** 。
*   基于以上观察，迭代 **i * j** 的所有值，使得 **i * j < = 2 * C** 并选择最佳值是最优选择。

因此，在范围**【1，2 * C】**内迭代 **i** 的所有值，对于每个 **i** ，迭代 **j** 的所有值，使得 i *** j < = 2 * C** 并跟踪**| A–I |+| B–j |+| C–I * j |**的最小可能值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum possible
// value of |A - X| + |B - Y| + |C - Z|
// such that X * Y = Z for given A, B and C
int minimizeCost(int A, int B, int C)
{
    // Stores the minimum value of
    // |A - X| + |B - Y| + |C - Z|
    // such that X * Y = Z
    int ans = A + B + C;

    // Iterate over all values of i
    // in the range [1, 2*C]
    for (int i = 1; i <= 2 * C; i++) {
        int j = 0;

        // Iterate over all values of
        // j such that i*j <= 2*c
        while (i * j <= 2 * C) {

            // Update the value of ans
            ans = min(ans, abs(A - i) + abs(B - j)
                               + abs(i * j - C));
            j++;
        }
    }

    // Return answer
    return ans;
}

// Driver Code
int main()
{
    int A = 19, B = 28, C = 522;
    cout << minimizeCost(A, B, C);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG{

// Function to find the minimum possible
// value of |A - X| + |B - Y| + |C - Z|
// such that X * Y = Z for given A, B and C
public static int minimizeCost(int A, int B, int C)
{
    // Stores the minimum value of
    // |A - X| + |B - Y| + |C - Z|
    // such that X * Y = Z
    int ans = A + B + C;

    // Iterate over all values of i
    // in the range [1, 2*C]
    for (int i = 1; i <= 2 * C; i++) {
        int j = 0;

        // Iterate over all values of
        // j such that i*j <= 2*c
        while (i * j <= 2 * C) {

            // Update the value of ans
            ans = Math.min(ans, Math.abs(A - i) + Math.abs(B - j)
                               + Math.abs(i * j - C));
            j++;
        }
    }

    // Return answer
    return ans;
}

// Driver Code
public static void main(String args[])
{
    int A = 19, B = 28, C = 522;
    System.out.print(minimizeCost(A, B, C));

}

}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to find the minimum possible
# value of |A - X| + |B - Y| + |C - Z|
# such that X * Y = Z for given A, B and C
def minimizeCost(A, B, C):

    # Stores the minimum value of
    # |A - X| + |B - Y| + |C - Z|
    # such that X * Y = Z
    ans = A + B + C

    # Iterate over all values of i
    # in the range [1, 2*C]
    for i in range(1, 2 * C + 1):
        j = 0

        # Iterate over all values of
        # j such that i*j <= 2*c
        while (i * j <= 2 * C):

            # Update the value of ans
            ans = min(ans, abs(A - i) + abs(B - j) + abs(i * j - C))
            j += 1

    # Return answer
    return ans

# Driver Code
A = 19
B = 28
C = 522
print(minimizeCost(A, B, C))

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find the minimum possible
// value of |A - X| + |B - Y| + |C - Z|
// such that X * Y = Z for given A, B and C
public static int minimizeCost(int A, int B, int C)
{

    // Stores the minimum value of
    // |A - X| + |B - Y| + |C - Z|
    // such that X * Y = Z
    int ans = A + B + C;

    // Iterate over all values of i
    // in the range [1, 2*C]
    for (int i = 1; i <= 2 * C; i++) {
        int j = 0;

        // Iterate over all values of
        // j such that i*j <= 2*c
        while (i * j <= 2 * C) {

            // Update the value of ans
            ans = Math.Min(ans, Math.Abs(A - i) + Math.Abs(B - j)
                               + Math.Abs(i * j - C));
            j++;
        }
    }

    // Return answer
    return ans;
}

// Driver Code
public static void Main(String []args)
{
    int A = 19, B = 28, C = 522;
    Console.Write(minimizeCost(A, B, C));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the minimum possible
        // value of |A - X| + |B - Y| + |C - Z|
        // such that X * Y = Z for given A, B and C
        function minimizeCost(A, B, C)
        {

            // Stores the minimum value of
            // |A - X| + |B - Y| + |C - Z|
            // such that X * Y = Z
            let ans = A + B + C;

            // Iterate over all values of i
            // in the range [1, 2*C]
            for (let i = 1; i <= 2 * C; i++) {
                let j = 0;

                // Iterate over all values of
                // j such that i*j <= 2*c
                while (i * j <= 2 * C) {

                    // Update the value of ans
                    ans = Math.min(ans, Math.abs(A - i) + Math.abs(B - j)
                        + Math.abs(i * j - C));
                    j++;
                }
            }

            // Return answer
            return ans;
        }

        // Driver Code
        let A = 19, B = 28, C = 522;
        document.write(minimizeCost(A, B, C));

     // This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
2
```

***时间复杂度:** O(C*log C)*
***辅助空间:** O(1)*