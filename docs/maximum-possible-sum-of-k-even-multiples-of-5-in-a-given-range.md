# 给定范围内 K 的 5 的偶数倍数的最大可能和

> 原文:[https://www . geesforgeks . org/给定范围内最大可能 k 的偶数倍数之和/](https://www.geeksforgeeks.org/maximum-possible-sum-of-k-even-multiples-of-5-in-a-given-range/)

给定三个整数 **L，R** 和 **K** ，任务是从范围**【L，R】**中找出 **K** 的最大和，甚至是 **5** 的倍数。

**示例:**

> **输入:** L = 7，R = 48，K = 3
> **输出:** 90
> **说明:**在[7，48] = 40 + 30 + 20 = 90 范围内的 3 个 5 的偶数倍数的最大和
> 
> **输入:** L = 16，R= 60，K = 4
> **输出:** 180
> **说明:**在[16，60] = 60 + 50 + 40 + 30 = 180 范围内的 4 个 5 的偶数倍数的最大和

**天真方法:**最简单的方法是迭代从 **R** 到 **L** 的所有偶数元素，对于每个元素，[检查它是否能被 5 整除](https://www.geeksforgeeks.org/check-large-number-divisible-5-not/)。如果发现是真的，将该元素加到总和中，并递减 **K** 。当 **K** 达到 0 时，[断开循环](https://www.geeksforgeeks.org/break-statement-cc/)并打印得到的和。

**时间复杂度:** O(N)，其中 N=R-L
**辅助空间:** O(1)

**高效方法:**上述方法可以基于以下观察进行优化:

> 范围[1，X]内 5 的偶数倍数计数= X / 10
> 范围[L，R]内 5 的偶数倍数计数=(R/10–L/10)+1 = N(说)
> 范围[L，R]
> 内 5 的 K 个偶数倍数的最大和=范围[1，R]内 5 的偶数倍数之和–范围[1， R–K]
> = 10 *(N *(N+1)/2–M *(M+1)/2，其中 M = R–K

按照以下步骤解决问题:

*   初始化**N =(R/10–L/10)+1**存储**【L，R】**范围内 5 的偶数倍数的计数。
*   如果 **K > N** ，打印 **-1** 表示在**【L，R】**范围内有小于 **K** 的 **5** 的偶倍数。
*   否则:
    *   初始化**M = R–K**。
    *   存储**总和= 10 *(N *(N+1)/2–M *(M+1)/2)**。
    *   打印**和**。

下面是上述方法的实现:

## C++14

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of K
// even multiples of 5 in the range [L, R]
void maxksum(int L, int R, int K)
{
    // Store the total number of even
    // multiples of 5 in the range [L, R]
    int N = (R / 10 - L / 10) + 1;

    // Check if K > N
    if (K > N) {

        // If true, print -1 and return
        cout << -1;
        return;
    }

    // Otherwise, divide R by 10
    R = R / 10;

    // Store the sum using the formula
    int X = R - K;
    int sum = 10 * ((R * (R + 1)) / 2
                    - (X * (X + 1)) / 2);

    // Print the sum
    cout << sum;
}

// Driver Code
int main()
{

    // Given L, R and K
    int L = 16, R = 60, K = 4;

    // Function Call
    maxksum(L, R, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find the maximum sum of K
// even multiples of 5 in the range [L, R]
static void maxksum(int L, int R, int K)
{

    // Store the total number of even
    // multiples of 5 in the range [L, R]
    int N = (R / 10 - L / 10) + 1;

    // Check if K > N
    if (K > N)
    {

        // If true, print -1 and return
        System.out.print("-1");
        return;
    }

    // Otherwise, divide R by 10
    R = R / 10;

    // Store the sum using the formula
    int X = R - K;
    int sum = 10 * ((R * (R + 1)) / 2 -
                    (X * (X + 1)) / 2);

    // Print the sum
    System.out.print( sum);
}

// Driver Code
public static void main(String[] args)
{

    // Given L, R and K
    int L = 16, R = 60, K = 4;

    // Function Call
    maxksum(L, R, K);
}
}

// This code is contributed by Stream_Cipher
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the maximum sum of K
# even multiples of 5 in the range [L, R]
def maxksum(L, R, K) :

    # Store the total number of even
    # multiples of 5 in the range [L, R]
    N = (R // 10 - L // 10) + 1;

    # Check if K > N
    if (K > N) :

        # If true, print -1 and return
        print(-1);
        return;

    # Otherwise, divide R by 10
    R = R // 10;

    # Store the sum using the formula
    X = R - K;
    sum = 10 * ((R * (R + 1)) // 2 - (X * (X + 1)) // 2);

    # Print the sum
    print(sum);

# Driver Code
if __name__ == "__main__" :

    # Given L, R and K
    L = 16; R = 60; K = 4;

    # Function Call
    maxksum(L, R, K);

    # This code is contributed by AnkThon
```

## C#

```
// C# program to implement
// the above approach 
using System;
class GFG
{

// Function to find the maximum sum of K
// even multiples of 5 in the range [L, R]
static void maxksum(int L, int R, int K)
{

    // Store the total number of even
    // multiples of 5 in the range [L, R]
    int N = (R / 10 - L / 10) + 1;

    // Check if K > N
    if (K > N)
    {

        // If true, print -1 and return
        Console.Write("-1");
        return;
    }

    // Otherwise, divide R by 10
    R = R / 10;

    // Store the sum using the formula
    int X = R - K;
    int sum = 10 * ((R * (R + 1)) / 2 -
                    (X * (X + 1)) / 2);

    // Print the sum
    Console.Write( sum);
}

// Driver code
public static void Main()
{

    // Given L, R and K
    int L = 16, R = 60, K = 4;

    // Function Call
    maxksum(L, R, K);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find the maximum sum of K
// even multiples of 5 in the range [L, R]
function maxksum(L, R, K)
{

    // Store the total number of even
    // multiples of 5 in the range [L, R]
    let N = (R / 10 - L / 10) + 1;

    // Check if K > N
    if (K > N)
    {

        // If true, print -1 and return
        document.write("-1");
        return;
    }

    // Otherwise, divide R by 10
    R = R / 10;

    // Store the sum using the formula
    let X = R - K;
    let sum = 10 * ((R * (R + 1)) / 2 -
                    (X * (X + 1)) / 2);

    // Print the sum
    document.write(sum);
}

// Driver Code

// Given L, R and K
let L = 16, R = 60, K = 4;

// Function Call
maxksum(L, R, K);

// This code is contributed by splevel62

</script>
```

**Output:** 

```
180
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)