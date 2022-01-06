# 将 N 减 1 所需的适当除数的最小减量或除法

> 原文:[https://www . geeksforgeeks . org/最小减或除以所需除数将 n 减 1/](https://www.geeksforgeeks.org/minimum-decrements-or-division-by-a-proper-divisor-required-to-reduce-n-to-1/)

给定一个正整数 **N** ，任务是通过重复将 **N** 除以其[适当因子](https://www.geeksforgeeks.org/sum-proper-divisors-natural-numbers-array/)或将 **N** 除以 **1** ，找到将 **N** 减少到 **1** 所需的最小操作数。

**示例:**

> **输入:** N = 9
> **输出:** 3
> **说明:**
> N(= 9)的适当除数为{1，3}。执行以下操作以将 N 减少到 1:
> **操作 1:** 将 N(= 9)除以 3(这是 N(= 9)的适当除数)将 N 的值修改为 9/3 = 1。
> **操作 2:** 将 N(= 3)的值减 1 会将 N 的值修改为 3–1 = 2。
> **操作 3:** 将 N(= 2)的值减 1 会将 N 的值修改为 2–1 = 1。
> 因此，所需操作总数为 3。
> 
> **输入:**N = 4
> T3】输出: 2

**方法:**给定的问题可以基于以下观察来解决:

*   如果 **N** 的值为偶数，则可以通过将 **N** 除以 **N / 2** ，然后将 **2** 递减至 **1** 来将其减少至数值 **2** 。因此，所需的最小步数为 **2** 。
*   否则，即使减少 **N** 的值也可以使其变小，并且可以使用上述步骤将其减少到 **1** 。

按照下面给出的步骤解决问题

*   初始化一个变量，将 **cnt** 设为 **0** ，以存储将 **N** 减少到 **1** 所需的最小步数。
*   重复一个循环，直到 **N** 减少到 **1** ，并执行以下步骤:
    *   如果 **N** 的值等于 **2** 或 [N 为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则更新**N = N–1**的值，并将 **cnt** 增加 **1** 。
    *   否则，更新 **N = N / (N / 2)** 的值，并将 **cnt** 增加 1。
*   完成上述步骤后，打印 **cnt** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of steps required to reduce N to 1
int reduceToOne(long long int N)
{
    // Stores the number
    // of steps required
    int cnt = 0;

    while (N != 1) {

        // If the value of N
        // is equal to 2 or N is odd
        if (N == 2 or (N % 2 == 1)) {

            // Decrement N by 1
            N = N - 1;

            // Increment cnt by 1
            cnt++;
        }

        // If N is even
        else if (N % 2 == 0) {

            // Update N
            N = N / (N / 2);

            // Increment cnt by 1
            cnt++;
        }
    }

    // Return the number
    // of steps obtained
    return cnt;
}

// Driver Code
int main()
{
    long long int N = 35;
    cout << reduceToOne(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the minimum number
// of steps required to reduce N to 1
static int reduceToOne(long N)
{

    // Stores the number
    // of steps required
    int cnt = 0;

    while (N != 1)
    {

        // If the value of N
        // is equal to 2 or N is odd
        if (N == 2 || (N % 2 == 1))
        {

            // Decrement N by 1
            N = N - 1;

            // Increment cnt by 1
            cnt++;
        }

        // If N is even
        else if (N % 2 == 0)
        {

            // Update N
            N = N / (N / 2);

            // Increment cnt by 1
            cnt++;
        }
    }

    // Return the number
    // of steps obtained
    return cnt;
}

// Driver Code
public static void main(String[] args)
{
    long N = 35;

    System.out.println(reduceToOne(N));
}
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find the minimum number
# of steps required to reduce N to 1
def reduceToOne(N):

    # Stores the number
    # of steps required
    cnt = 0

    while (N != 1):

        # If the value of N
        # is equal to 2 or N is odd
        if (N == 2 or (N % 2 == 1)):

            # Decrement N by 1
            N = N - 1

            # Increment cnt by 1
            cnt += 1

        # If N is even
        elif (N % 2 == 0):

            # Update N
            N = N / (N / 2)

            # Increment cnt by 1
            cnt += 1

    # Return the number
    # of steps obtained
    return cnt

# Driver Code
if __name__ == '__main__':
    N = 35
    print (reduceToOne(N))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

// Function to find the minimum number
// of steps required to reduce N to 1
static int reduceToOne(long N)
{

    // Stores the number
    // of steps required
    int cnt = 0;

    while (N != 1)
    {

        // If the value of N
        // is equal to 2 or N is odd
        if (N == 2 || (N % 2 == 1))
        {

            // Decrement N by 1
            N = N - 1;

            // Increment cnt by 1
            cnt++;
        }

        // If N is even
        else if (N % 2 == 0)
        {

            // Update N
            N = N / (N / 2);

            // Increment cnt by 1
            cnt++;
        }
    }

    // Return the number
    // of steps obtained
    return cnt;
}

// Driver Code
public static void Main()
{
    long N = 35;

    Console.WriteLine(reduceToOne(N));
}
}

// This code s contributed by code_hunt.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the minimum number
// of steps required to reduce N to 1
function reduceToOne( N)
{
    // Stores the number
    // of steps required
    let cnt = 0;

    while (N != 1) {

        // If the value of N
        // is equal to 2 or N is odd
        if (N == 2 || (N % 2 == 1)) {

            // Decrement N by 1
            N = N - 1;

            // Increment cnt by 1
            cnt++;
        }

        // If N is even
        else if (N % 2 == 0) {

            // Update N
            N = Math.floor(N / Math.floor(N / 2));

            // Increment cnt by 1
            cnt++;
        }
    }

    // Return the number
    // of steps obtained
    return cnt;
}

// Driver Code
let N = 35;
document.write(reduceToOne(N));

// This code is contributed by jana_sayantan.
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)