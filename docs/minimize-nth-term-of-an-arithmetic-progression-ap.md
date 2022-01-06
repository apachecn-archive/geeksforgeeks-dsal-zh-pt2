# 最小化等差数列的第 n 项

> 原文:[https://www . geesforgeks . org/minimum-n 次算术级数-ap/](https://www.geeksforgeeks.org/minimize-nth-term-of-an-arithmetic-progression-ap/)

给定两个整数 **A** 、 **B** ，它们是[等差数列](https://www.geeksforgeeks.org/arithmetic-progression/)的任意两个项，以及一个整数 **N** ，任务是最小化该等差数列的 **N** <sup>第</sup>项。

***注意:**一个 AP 系列的所有元素必须是正的。*

**示例:**

> **输入:** A = 1，B = 6，N = 3
> **输出:** 11
> **说明:**给定等差数列的前三项为:{1，6，11}。
> 因此，要求的输出是 11。
> 
> **输入:** A = 20，B = 50，N = 5
> **输出:** 50
> **说明:**给定等差数列的前五项为:{10，20，30，40，50}。
> 因此，要求输出为 50。

**方法:**通过将 **A** 和 **B** 放置在算术级数中所有可能的位置，并检查生成最少可能的**N**T8 项，可以解决该问题。考虑到 **A** 和 **B** 的位置分别为 **i** 和 **j** ，则需要进行以下计算:

> AP 的公共差(D)=(B–A)/(j–I)
> AP 的第一项= A –( I–1)* D
> AP 的第 N 项=第一项+(N–1)* D

最后，返回获得的最小**N**T2 项。
按照以下步骤解决问题:

1.  初始化一个变量，说 **res** 来存储算术级数第**N**T4 项的最小可能值。
2.  使用两个嵌套循环，将 **A** 和 **B** 放置在 AP 中所有可能的位置，并使用上述计算计算**N**T6 项。继续更新 **res** 以存储 **N** <sup>第</sup>项获得的最小值。
3.  最后，打印 **res** 的值作为所需答案。

以下是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest
// Nth term of an AP possible
int smallestNth(int A, int B, int N)
{
    // Stores the smallest Nth term
    int res = INT_MAX;

    for (int i = 1; i < N; i++) {
        for (int j = N; j > i; j--) {

            // Check if common difference
            // of AP is an integer
            if ((B - A) % (j - i) == 0) {

                // Store the common
                // difference
                int D = (B - A) / (j - i);

                // Store the First Term
                // of that AP
                int FirstTerm = A - (i - 1) * D;

                // Store the Nth term of
                // that AP
                int NthTerm = FirstTerm + (N - 1) * D;

                // Check if all elements of
                // an AP are positive
                if (FirstTerm > 0)
                    res = min(res, NthTerm);
            }
        }
    }

    // Return the least
    // Nth term obtained
    return res;
}

// Driver Code
int main()
{
    int N = 3;
    int A = 1;
    int B = 6;
    cout << smallestNth(A, B, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;

class GFG{

// Function to find the smallest
// Nth term of an AP possible
static int smallestNth(int A, int B, int N)
{

    // Stores the smallest Nth term
    int res = Integer.MAX_VALUE;

    for(int i = 1; i < N; i++)
    {
        for(int j = N; j > i; j--)
        {

            // Check if common difference
            // of AP is an integer
            if ((B - A) % (j - i) == 0)
            {

                // Store the common
                // difference
                int D = (B - A) / (j - i);

                // Store the First Term
                // of that AP
                int FirstTerm = A - (i - 1) * D;

                // Store the Nth term of
                // that AP
                int NthTerm = FirstTerm + (N - 1) * D;

                // Check if all elements of
                // an AP are positive
                if (FirstTerm > 0)
                    res = Math.min(res, NthTerm);
            }
        }
    }

    // Return the least
    // Nth term obtained
    return res;
}

// Driver Code
public static void main (String[] args)
{
    int N = 3;
    int A = 1;
    int B = 6;

    System.out.print(smallestNth(A, B, N));
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import sys

# Function to find the smallest
# Nth term of an AP possible
def smallestNth(A, B, N):

    # Stores the smallest Nth term
    res = sys.maxsize

    for i in range(1, N):
        for j in range(N, i, -1):

            # Check if common difference
            # of AP is an integer
            if ((B - A) % (j - i) == 0):

                # Store the common
                # difference
                D = (B - A) // (j - i)

                # Store the First Term
                # of that AP
                FirstTerm = A - (i - 1) * D

                # Store the Nth term of
                # that AP
                NthTerm = FirstTerm + (N - 1) * D

                # Check if all elements of
                # an AP are positive
                if (FirstTerm > 0):
                    res = min(res, NthTerm)

    # Return the least
    # Nth term obtained
    return res

# Driver Code
if __name__ == '__main__':

    N = 3
    A = 1
    B = 6

    print(smallestNth(A, B, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to find the smallest
// Nth term of an AP possible
static int smallestNth(int A, int B, int N)
{

    // Stores the smallest Nth term
    int res = Int32.MaxValue;

    for(int i = 1; i < N; i++)
    {
        for(int j = N; j > i; j--)
        {

            // Check if common difference
            // of AP is an integer
            if ((B - A) % (j - i) == 0)
            {

                // Store the common
                // difference
                int D = (B - A) / (j - i);

                // Store the First Term
                // of that AP
                int FirstTerm = A - (i - 1) * D;

                // Store the Nth term of
                // that AP
                int NthTerm = FirstTerm + (N - 1) * D;

                // Check if all elements of
                // an AP are positive
                if (FirstTerm > 0)
                    res = Math.Min(res, NthTerm);
            }
        }
    }

    // Return the least
    // Nth term obtained
    return res;
}

// Driver Code
public static void Main ()
{
    int N = 3;
    int A = 1;
    int B = 6;

    Console.Write(smallestNth(A, B, N));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find the smallest
// Nth term of an AP possible
function smallestNth(A, B, N)
{

    // Stores the smallest Nth term
    let res = Number.MAX_VALUE;

    for(let i = 1; i < N; i++)
    {
        for(let j = N; j > i; j--)
        {

            // Check if common difference
            // of AP is an integer
            if ((B - A) % (j - i) == 0)
            {

                // Store the common
                // difference
                let D = (B - A) / (j - i);

                // Store the First Term
                // of that AP
                let FirstTerm = A - (i - 1) * D;

                // Store the Nth term of
                // that AP
                let NthTerm = FirstTerm + (N - 1) * D;

                // Check if all elements of
                // an AP are positive
                if (FirstTerm > 0)
                    res = Math.min(res, NthTerm);
            }
        }
    }

    // Return the least
    // Nth term obtained
    return res;
}

// Driver code
    let N = 3;
    let A = 1;
    let B = 6;

    document.write(smallestNth(A, B, N));

// This code is contributed by target_2.
</script>
```

**Output:** 

```
11
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(1)