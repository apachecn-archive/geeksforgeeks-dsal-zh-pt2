# 求非线性方程 2X + 5Y = N 的积分解

> 原文:[https://www . geesforgeks . org/find-一个非线性方程的积分解-2x-5y-n/](https://www.geeksforgeeks.org/find-an-integral-solution-of-the-non-linear-equation-2x-5y-n/)

给定一个整数 **N** 表示形式为 **2 <sup>X</sup> + 5 <sup>Y</sup> = N** 的[非线性方程](https://en.wikipedia.org/wiki/Nonlinear_system)，任务是找到满足给定方程的整数对( **X** ， **Y** )。如果存在多个解决方案，则打印其中任何一个。否则，打印 **-1** 。

**示例:**

> **输入:** N = 29
> **输出:** X = 2，Y = 2
> **说明:**
> 既然，2<sup>2</sup>+5<sup>2</sup>= 29
> 所以，X = 2，Y = 2 满足给定方程。
> 
> **输入:** N = 81
> **输出:** -1

**方法:**按照以下步骤解决问题:

*   初始化一个变量，说 **xMax** 存储 **X** 的最大可能值。
*   将 **xMax** 更新为**日志 <sub>2</sub> N** 。
*   初始化一个变量，比如说 **yMax** 来存储最大可能的 **Y** 。
*   更新 **yMax** 到**日志 <sub>5</sub> N**
*   迭代 **X** 和 **Y** 的所有可能值，对于 **X** 和 **Y** 的每个值，检查每对是否满足给定的等式。如果发现为真，则打印 **X** 和 **Y** 的对应值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the value
// of power(X, N)
long long power(long long x,
                long long N)
{

    // Stores the value
    // of (X ^ N)
    long long res = 1;

    // Calculate the value of
    // power(x, N)
    while (N > 0) {

        // If N is odd
        if (N & 1) {

            // Update res
            res = (res * x) ;
        }

        // Update x
        x = (x * x) ;

        // Update N
        N = N >> 1;
    }
    return res;
}

// Function to find the value of
// X and Y that satisfy the condition
void findValX_Y(long long N)
{

    // Base Case
    if (N <= 1) {
    cout<<-1<<endl;
    return;
    }

    // Stores maximum possible
    // of X.
    int xMax;

    // Update xMax
    xMax = log2(N);

    // Stores maximum possible
    // of Y.
    int yMax;

    // Update yMax
    yMax = (log2(N) / log2(5.0));

    // Iterate over all possible
    // values of X
    for (long long i = 1;
            i <= xMax; i++) {

        // Iterate over all possible
        // values of Y
        for (long long j=1;
            j <= yMax; j++) {

            // Stores value of 2^i
            long long a
            = power(2, i);

            // Stores value of 5^j
            long long b
            = power(5, j);

            // If the pair (i, j)
            // satisfy the equation
            if (a + b == N) {

                cout<<i<<" "
                <<j<<endl;
                return;
            }
        }
    }

    // If no solution exists
    cout<<-1<<endl;

}

// Driver Code
int main()
{
    long long N = 129;

    findValX_Y(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find the value
// of power(X, N)
static int power(int x, int N)
{

    // Stores the value
    // of (X ^ N)
    int res = 1;

    // Calculate the value of
    // power(x, N)
    while (N > 0)
    {

        // If N is odd
        if ((N & 1) != 0)
        {

            // Update res
            res = (res * x);
        }

        // Update x
        x = (x * x);

        // Update N
        N = N >> 1;
    }
    return res;
}

// Function to find the value of
// X and Y that satisfy the condition
static void findValX_Y(int N)
{

    // Base Case
    if (N <= 1)
    {
        System.out.println(-1);
        return;
    }

    // Stores maximum possible
    // of X.
    int xMax;

    // Update xMax
    xMax = (int)Math.log(N);

    // Stores maximum possible
    // of Y.
    int yMax;

    // Update yMax
    yMax = (int)(Math.log(N) / Math.log(5.0));

    // Iterate over all possible
    // values of X
    for(int i = 1; i <= xMax; i++)
    {

        // Iterate over all possible
        // values of Y
        for(int j = 1; j <= yMax; j++)
        {

            // Stores value of 2^i
            int a = power(2, i);

            // Stores value of 5^j
            int b = power(5, j);

            // If the pair (i, j)
            // satisfy the equation
            if (a + b == N)
            {
                System.out.print(i + " " + j);
                return;
            }
        }
    }

    // If no solution exists
    System.out.println("-1");
}

// Driver Code
public static void main(String args[])
{
    int N = 129;

    findValX_Y(N);
}
}

// This code is contributed by bgangwar59
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
from math import log2

# Function to find the value
# of power(X, N)
def power(x, N):

    # Stores the value
    # of (X ^ N)
    res = 1

    # Calculate the value of
    # power(x, N)
    while (N > 0):

        # If N is odd
        if (N & 1):

            # Update res
            res = (res * x)

        # Update x
        x = (x * x)

        # Update N
        N = N >> 1

    return res

# Function to find the value of
# X and Y that satisfy the condition
def findValX_Y(N):

    # Base Case
    if (N <= 1):
       print(-1)
       return

    # Stores maximum possible
    # of X
    xMax = 0

    # Update xMax
    xMax = int(log2(N))

    # Stores maximum possible
    # of Y
    yMax = 0

    # Update yMax
    yMax = int(log2(N) / log2(5.0))

    # Iterate over all possible
    # values of X
    for i in range(1, xMax + 1):

        # Iterate over all possible
        # values of Y
        for j in range(1, yMax + 1):

            # Stores value of 2^i
            a = power(2, i)

            # Stores value of 5^j
            b = power(5, j)

            # If the pair (i, j)
            # satisfy the equation
            if (a + b == N):
                print(i, j)
                return

    # If no solution exists
    print(-1)

# Driver Code
if __name__ == '__main__':

    N = 129

    findValX_Y(N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to find the
// value of power(X, N)
static int power(int x,
                 int N)
{   
  // Stores the value
  // of (X ^ N)
  int res = 1;

  // Calculate the value
  // of power(x, N)
  while (N > 0)
  {        
    // If N is odd
    if ((N & 1) != 0)
    {

      // Update res
      res = (res * x);
    }

    // Update x
    x = (x * x);

    // Update N
    N = N >> 1;
  }
  return res;
}

// Function to find the
// value of X and Y that
// satisfy the condition
static void findValX_Y(int N)
{    
  // Base Case
  if (N <= 1)
  {
    Console.WriteLine(-1);
    return;
  }

  // Stores maximum
  // possible of X.
  int xMax;

  // Update xMax
  xMax = (int)Math.Log(N);

  // Stores maximum possible
  // of Y.
  int yMax;

  // Update yMax
  yMax = (int)(Math.Log(N) /
               Math.Log(5.0));

  // Iterate over all possible
  // values of X
  for(int i = 1; i <= xMax; i++)
  {
    // Iterate over all possible
    // values of Y
    for(int j = 1; j <= yMax; j++)
    {
      // Stores value of 2^i
      int a = power(2, i);

      // Stores value of 5^j
      int b = power(5, j);

      // If the pair (i, j)
      // satisfy the equation
      if (a + b == N)
      {
        Console.Write(i + " " + j);
        return;
      }
    }
  }

  // If no solution exists
  Console.WriteLine("-1");
}

// Driver Code
public static void Main()
{
  int N = 129;
  findValX_Y(N);
}
}

// This code is contributed by surendra_gangwar
```

## java 描述语言

```
<script>

// JavaScript program to implement the above approach

// Function to find the value
// of power(X, N)
function power(x, N)
{

    // Stores the value
    // of (X ^ N)
    let res = 1;

    // Calculate the value of
    // power(x, N)
    while (N > 0)
    {

        // If N is odd
        if ((N & 1) != 0)
        {

            // Update res
            res = (res * x);
        }

        // Update x
        x = (x * x);

        // Update N
        N = N >> 1;
    }
    return res;
}

// Function to find the value of
// X and Y that satisfy the condition
function findValX_Y(N)
{

    // Base Case
    if (N <= 1)
    {
        document.write(-1);
        return;
    }

    // Stores maximum possible
    // of X.
    let xMax;

    // Update xMax
    xMax = Math.log(N);

    // Stores maximum possible
    // of Y.
    let yMax;

    // Update yMax
    yMax = Math.log(N) / Math.log(5.0);

    // Iterate over all possible
    // values of X
    for(let i = 1; i <= xMax; i++)
    {

        // Iterate over all possible
        // values of Y
        for(let j = 1; j <= yMax; j++)
        {

            // Stores value of 2^i
            let a = power(2, i);

            // Stores value of 5^j
            let b = power(5, j);

            // If the pair (i, j)
            // satisfy the equation
            if (a + b == N)
            {
                document.write(i + " " + j);
                return;
            }
        }
    }

    // If no solution exists
    document.write("-1");
}

// Driver Code

    let N = 129;
    findValX_Y(N);

    // This code is contributed by susmitakundugoaldanga.
</script>
```

**输出:**

```
2 3
```

***时间复杂度:**O(log<sub>2</sub>N * log<sub>5</sub>N)*
***辅助空间:** O(1)*