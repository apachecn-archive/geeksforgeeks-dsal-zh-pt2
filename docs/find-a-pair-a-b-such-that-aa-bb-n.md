# 找到一对(a，b)，使得 Aa + Bb = N

> 原文:[https://www . geesforgeks . org/find-a-pair-a-B- so-aa-bb-n/](https://www.geeksforgeeks.org/find-a-pair-a-b-such-that-aa-bb-n/)

给定三个整数 **N** 、 **A** 、**T5】和 **B** ，任务是找到一对正整数 **(a，b)** ，使得**A<sup>A</sup>+B<sup>B</sup>= N**。如果不存在这样的配对，打印 **-1** 。**

**示例:**

> **输入:** N = 106，A = 3，B = 5
> **输出:** 4 2
> **说明:**对(4，2)满足答案即 3 <sup>4</sup> +5 <sup>2</sup> 等于 106
> 
> **输入:** N = 60467200，A = 6，B = 4
> **输出:** 10 5
> **说明:**对(10，5)满足答案即 6 <sup>10</sup> +4 <sup>5</sup> 等于 60467200

**方法:**思路是计算 **log <sub>A</sub> N** 和 **log <sub>B</sub> N** 并检查每一个**对(I，j)** (0 ≤ i ≤ log <sub>A</sub> N 和 0 ≤ j ≤ log <sub>B</sub> N)，是否**A<sup>I</sup>+B<sup>j</sup>**按照以下步骤解决问题:

*   首先[求大于 N 的 A 和 B 的最小幂](https://www.geeksforgeeks.org/smallest-power-of-2-greater-than-or-equal-to-n/)分别存储在变量 **X** 和 **Y** 中。
*   检查每个对 **(i，j)** ，使得 **0≤i≤X** 和 **0≤j≤Y** 、如果**A<sup>I</sup>+B<sup>j</sup>**等于 **N** ，打印**对(I，j)** 。
*   如果没有找到这样的配对，打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the minimum
// power of A and B greater than N
int power(long long int A, long long int N)
{
    // Stores the power of A which
    // is greater than N
    int count = 0;
    if (A == 1)
        return 0;

    while (N) {

        // Increment count by 1
        count++;

        // Divide N by A
        N /= A;
    }
    return count;
}

// Function to find a pair (a, b)
// such that A^a + B^b = N
void Pairs(long long int N, long long int A,
           long long int B)
{
    int powerA, powerB;

    // Calculate the minimum power
    // of A greater than N
    powerA = power(A, N);

    // Calculate the minimum power
    // of B greater than N
    powerB = power(B, N);

    // Make copy of A and B
    long long int intialB = B, intialA = A;

    // Traverse for every pair (i, j)
    A = 1;
    for (int i = 0; i <= powerA; i++) {

        B = 1;
        for (int j = 0; j <= powerB; j++) {

            // Check if B^j + A^i = N
            // To overcome the overflow problem
            // use B=N-A rather than B+A=N
            if (B == N - A) {
                cout << i << " " << j << endl;
                return;
            }

            // Increment power B by 1
            B *= intialB;
        }

        // Increment power A by 1
        A *= intialA;
    }

    // Finally print -1 if no pair
    // is found
    cout << -1 << endl;
    return;
}

// Driver Code
int main()
{

    // Given A, B and N
    long long int N = 106, A = 3, B = 5;

    // Function Call
    Pairs(N, A, B);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to calculate the minimum
// power of A and B greater than N
static int power(int A, int N)
{

    // Stores the power of A which
    // is greater than N
    int count = 0;

    if (A == 1)
        return 0;

    while (N > 0)
    {

        // Increment count by 1
        count++;

        // Divide N by A
        N /= A;
    }
    return count;
}

// Function to find a pair (a, b)
// such that A^a + B^b = N
static void Pairs(int N, int A, int B)
{
    int powerA, powerB;

    // Calculate the minimum power
    // of A greater than N
    powerA = power(A, N);

    // Calculate the minimum power
    // of B greater than N
    powerB = power(B, N);

    // Make copy of A and B
    int intialB = B, intialA = A;

    // Traverse for every pair (i, j)
    A = 1;
    for(int i = 0; i <= powerA; i++)
    {

        B = 1;
        for(int j = 0; j <= powerB; j++)
        {

            // Check if B^j + A^i = N
            // To overcome the overflow problem
            // use B=N-A rather than B+A=N
            if (B == N - A)
            {
                System.out.println(i + " " + j);
                return;
            }

            // Increment power B by 1
            B *= intialB;
        }

        // Increment power A by 1
        A *= intialA;
    }

    // Finally print -1 if no pair
    // is found
    System.out.println("-1");
    return;
}

// Driver Code
public static void main(String args[])
{

    // Given A, B and N
    int N = 106, A = 3, B = 5;

    // Function Call
    Pairs(N, A, B);
}
}

// This code is contributed by 18bhupenderyadav18
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to calculate the minimum
# power of A and B greater than N
def power(A, N):

    # Stores the power of A which
    # is greater than N
    count = 0;
    if (A == 1):
        return 0;
    while (N > 0):

        # Increment count by 1
        count += 1;

        # Divide N by A
        N //= A;
    return int(count);

# Function to find a pair (a, b)
# such that A^a + B^b = N
def Pairs(N, A, B):
    powerA, powerB = 0, 0;

    # Calculate the minimum power
    # of A greater than N
    powerA = power(A, N);

    # Calculate the minimum power
    # of B greater than N
    powerB = power(B, N);

    # Make copy of A and B
    intialB = B;
    intialA = A;

    # Traverse for every pair (i, j)
    A = 1;
    for i in range(powerA + 1):
        B = 1;
        for j in range(powerB + 1):

            # Check if B^j + A^i = N
            # To overcome the overflow problem
            # use B=N-A rather than B+A=N
            if (B == N - A):
                print(i , " " , j);
                return;

            # Increment power B by 1
            B *= intialB;

        # Increment power A by 1
        A *= intialA;

    # Finally pr-1 if no pair
    # is found
    print("-1");
    return;

# Driver Code
if __name__ == '__main__':

  # Given A, B and N
    N = 106;
    A = 3;
    B = 5;

    # Function Call
    Pairs(N, A, B);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

// Function to calculate the minimum
// power of A and B greater than N
static int power(int A, int N)
{

    // Stores the power of A which
    // is greater than N
    int count = 0;

    if (A == 1)
        return 0;
    while (N > 0)
    {

        // Increment count by 1
        count++;

        // Divide N by A
        N /= A;
    }
    return count;
}

// Function to find a pair (a, b)
// such that A^a + B^b = N
static void Pairs(int N, int A, int B)
{
    int powerA, powerB;

    // Calculate the minimum power
    // of A greater than N
    powerA = power(A, N);

    // Calculate the minimum power
    // of B greater than N
    powerB = power(B, N);

    // Make copy of A and B
    int intialB = B, intialA = A;

    // Traverse for every pair (i, j)
    A = 1;
    for(int i = 0; i <= powerA; i++)
    {

        B = 1;
        for(int j = 0; j <= powerB; j++)
        {

            // Check if B^j + A^i = N
            // To overcome the overflow problem
            // use B=N-A rather than B+A=N
            if (B == N - A)
            {
                Console.WriteLine(i + " " + j);
                return;
            }

            // Increment power B by 1
            B *= intialB;
        }

        // Increment power A by 1
        A *= intialA;
    }

    // Finally print -1 if no pair
    // is found
    Console.WriteLine("-1");
    return;
}

// Driver Code
public static void Main(String []args)
{

    // Given A, B and N
    int N = 106, A = 3, B = 5;

    // Function Call
    Pairs(N, A, B);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to calculate the minimum
// power of A and B greater than N
function power(A, N)
{

    // Stores the power of A which
    // is greater than N
    let count = 0;

    if (A == 1)
        return 0;

    while (N > 0)
    {

        // Increment count by 1
        count++;

        // Divide N by A
        N /= A;
    }
    return count;
}

// Function to find a pair (a, b)
// such that A^a + B^b = N
function Pairs(N, A, B)
{
    let powerA, powerB;

    // Calculate the minimum power
    // of A greater than N
    powerA = power(A, N);

    // Calculate the minimum power
    // of B greater than N
    powerB = power(B, N);

    // Make copy of A and B
    let letialB = B, letialA = A;

    // Traverse for every pair (i, j)
    A = 1;
    for(let i = 0; i <= powerA; i++)
    {

        B = 1;
        for(let j = 0; j <= powerB; j++)
        {

            // Check if B^j + A^i = N
            // To overcome the overflow problem
            // use B=N-A rather than B+A=N
            if (B == N - A)
            {
                document.write(i + " " + j);
                return;
            }

            // Increment power B by 1
            B *= letialB;
        }

        // Increment power A by 1
        A *= letialA;
    }

    // Finally print -1 if no pair
    // is found
    document.write("-1");
    return;
}

// driver function

    // Given A, B and N
    let N = 106, A = 3, B = 5;

    // Function Call
    Pairs(N, A, B);

    // This code is contributed by splevel62.
</script>   
```

**Output:** 

```
4 2
```

***时间复杂度:**O((log<sub>A</sub>N)*(log<sub>B</sub>N))*
***辅助空间:** O(1)*