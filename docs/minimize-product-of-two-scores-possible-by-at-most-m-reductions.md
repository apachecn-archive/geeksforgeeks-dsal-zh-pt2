# 通过最多 M 次减少来最小化两个分数的乘积

> 原文:[https://www . geeksforgeeks . org/最大限度地减少两个分数的乘积-最多 m 个可能的减少量/](https://www.geeksforgeeks.org/minimize-product-of-two-scores-possible-by-at-most-m-reductions/)

给定两个整数 **R1、R2** 分别表示两名球员得分的跑位， **B1、B2** 分别表示他们面对的球，任务是找到**的最小**值 **R1 * R2** 可以得到使得 **R1** 和 **R2** 可以减少满足条件 **R1 ≥ B1** 和 **R2 ≥ B2** 的 **M** 跑位。

**示例:**

> **输入:** R1 = 21，B1 = 10，R2 = 13，B2 = 11，M = 3
> **输出:** 220
> **说明:**能得到的最小乘积是 R1 减 1，R2 减 2，即(21–1)x(13–2)= 220。
> 
> **输入:** R1 = 7，B1 = 6，R2 = 9，B1 = 9，M = 4
> T3】输出: 54

**方法:**将数完全减少到极限即可得到最小乘积。将 **R1** 降低到极限 **B1** 然后尽可能少的降低 **R2** (不超过 **M** )。同样，将 **R2** 减少到最多 B2，然后尽可能少的减少 **R2** (不超过 **M** )。在这两种情况下得到的最小乘积就是要求的答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to find the minimum
// product of R1 and R2 possible
int minProductUtil(int R1, int B1, int R2,
                   int B2, int M)
{
    int x = min(R1-B1, M);

    M -= x;

    // Reaching to its limit
    R1 -= x;

    // If M is remaining
    if (M > 0)
    {
        int y = min(R2 - B2, M);
        M -= y;
        R2 -= y;
    }
    return R1 * R2;
}

// Function to find the minimum
// product of R1 and R2
int minProduct(int R1, int B1, int R2, int B2, int M)
{

    // Case 1 - R1 reduces first
    int res1 = minProductUtil(R1, B1, R2, B2, M);

    // Case 2 - R2 reduces first
    int res2 = minProductUtil(R2, B2, R1, B1, M);

    return min(res1, res2);
}

// Driver Code
int main()
{

    // Given Input
    int R1 = 21, B1 = 10, R2 = 13, B2 = 11, M = 3;

    // Function Call
    cout << (minProduct(R1, B1, R2, B2, M));
    return 0;
}

// This code is contributed by maddler
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG{

// Utility function to find the minimum
// product of R1 and R2 possible
static int minProductUtil(int R1, int B1, int R2,
                   int B2, int M)
{
    int x = Math.min(R1-B1, M);

    M -= x;

    // Reaching to its limit
    R1 -= x;

    // If M is remaining
    if (M > 0)
    {
        int y = Math.min(R2 - B2, M);
        M -= y;
        R2 -= y;
    }
    return R1 * R2;
}

// Function to find the minimum
// product of R1 and R2
static int minProduct(int R1, int B1, int R2, int B2, int M)
{

    // Case 1 - R1 reduces first
    int res1 = minProductUtil(R1, B1, R2, B2, M);

    // Case 2 - R2 reduces first
    int res2 = minProductUtil(R2, B2, R1, B1, M);

    return Math.min(res1, res2);
}

// Driver Code
public static void main (String[] args)
{

    // Given Input
    int R1 = 21, B1 = 10, R2 = 13, B2 = 11, M = 3;

    // Function Call
    System.out.print((minProduct(R1, B1, R2, B2, M)));
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python program for the above approach

# Utility function to find the minimum
# product of R1 and R2 possible
def minProductUtil(R1, B1, R2, B2, M):

    x = min(R1-B1, M)

    M -= x

    # Reaching to its limit
    R1 -= x

    # If M is remaining
    if M > 0:
        y = min(R2-B2, M)
        M -= y
        R2 -= y

    return R1 * R2

# Function to find the minimum
# product of R1 and R2
def minProduct(R1, B1, R2, B2, M):

    # Case 1 - R1 reduces first
    res1 = minProductUtil(R1, B1, R2, B2, M)

    # case 2 - R2 reduces first
    res2 = minProductUtil(R2, B2, R1, B1, M)

    return min(res1, res2)

# Driver Code
if __name__ == '__main__':

    # Given Input
    R1 = 21; B1 = 10; R2 = 13; B2 = 11; M = 3

    # Function Call
    print(minProduct(R1, B1, R2, B2, M))
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Utility function to find the minimum
// product of R1 and R2 possible
static int minProductUtil(int R1, int B1, int R2,
                   int B2, int M)
{
    int x = Math.Min(R1-B1, M);

    M -= x;

    // Reaching to its limit
    R1 -= x;

    // If M is remaining
    if (M > 0)
    {
        int y = Math.Min(R2 - B2, M);
        M -= y;
        R2 -= y;
    }
    return R1 * R2;
}

// Function to find the minimum
// product of R1 and R2
static int minProduct(int R1, int B1, int R2, int B2, int M)
{

    // Case 1 - R1 reduces first
    int res1 = minProductUtil(R1, B1, R2, B2, M);

    // Case 2 - R2 reduces first
    int res2 = minProductUtil(R2, B2, R1, B1, M);

    return Math.Min(res1, res2);
}

// Driver Code
public static void Main (String[] args)
{

    // Given Input
    int R1 = 21, B1 = 10, R2 = 13, B2 = 11, M = 3;

    // Function Call
    Console.Write((minProduct(R1, B1, R2, B2, M)));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Utility function to find the minimum
// product of R1 and R2 possible
function minProductUtil(R1, B1, R2, B2, M)
{
    let x = Math.min(R1 - B1, M);
    M -= x;

    // Reaching to its limit
    R1 -= x;

    // If M is remaining
    if (M > 0)
    {
        let y = Math.min(R2 - B2, M);
        M -= y;
        R2 -= y;
    }
    return R1 * R2;
}

// Function to find the minimum
// product of R1 and R2
function minProduct(R1, B1, R2, B2, M)
{

    // Case 1 - R1 reduces first
    let res1 = minProductUtil(R1, B1, R2, B2, M);

    // Case 2 - R2 reduces first
    let res2 = minProductUtil(R2, B2, R1, B1, M);

    return Math.min(res1, res2);
}

// Driver Code

// Given Input
let R1 = 21, B1 = 10, R2 = 13, B2 = 11, M = 3;

// Function Call
document.write((minProduct(R1, B1, R2, B2, M)));

// This code is contributed by code_hunt

</script>
```

**Output:** 

```
220
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)