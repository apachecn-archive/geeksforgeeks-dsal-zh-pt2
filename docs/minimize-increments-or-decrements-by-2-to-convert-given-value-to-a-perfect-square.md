# 将增量或减量最小化 2，将给定值转换为完美的平方

> 原文:[https://www . geesforgeks . org/最小化增量或减量 2，将给定值转换为完美平方/](https://www.geeksforgeeks.org/minimize-increments-or-decrements-by-2-to-convert-given-value-to-a-perfect-square/)

给定一个整数 **N** ，任务是计算 **N** 需要递增或递减 **2** 的最小次数，将其转换为[完美平方](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)。

**示例:**

> **输入:** N = 18
> **输出:** 1
> **解释:**N–2 = 16(= 4<sup>2</sup>)。因此，需要一次减量操作。
> 
> **输入:** N = 15
> **输出:** 3
> **解释:**
> N–2 * 3 = 15–6 = 9(= 3<sup>2</sup>)。因此，需要 3 次减量操作。
> N + 2 * 5 = 25 (= 5 <sup>2</sup> )。因此，需要 5 次增量操作。
> 因此，所需的最小操作次数为 3 次。

**方法:**按照以下步骤解决这个问题:

*   计算操作总数，通过将 **N** 的值减 **2** 来表示 **N** 成为[完美平方数](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)所需的 **cntDecr** 。
*   通过将 **N** 的值增加 **2** 来计算操作总数，例如将 **N** 作为[完美平方数](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)所需的**计数**。
*   最后，打印 [min(cntIncr，cntDecr)](https://www.geeksforgeeks.org/stdmin-in-cpp/) 的值。

下面是上述方法的实现。

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of operations required to make
// N a perfect square
int MinimumOperationReq(int N)
{
    // Stores count of operations
    // by performing decrements
    int cntDecr = 0;

    // Stores value of N
    int temp = N;

    // Decrement the value of temp
    while (temp > 0) {

        // Stores square root of temp
        int X = sqrt(temp);

        // If temp is a perfect square
        if (X * X == temp) {
            break;
        }

        // Update temp
        temp = temp - 2;
        cntDecr += 1;
    }

    // Store count of operations
    // by performing increments
    int cntIncr = 0;

    // Increment the value of N
    while (true) {

        // Stores sqrt of N
        int X = sqrt(N);

        // If N is a perfect square
        if (X * X == N) {
            break;
        }

        // Update temp
        N = N + 2;
        cntIncr += 1;
    }

    // Return the minimum count
    return min(cntIncr, cntDecr);
}

// Driver Code
int main()
{

    int N = 15;
    cout << MinimumOperationReq(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to find the minimum number
// of operations required to make
// N a perfect square
static int MinimumOperationReq(int N)
{

    // Stores count of operations
    // by performing decrements
    int cntDecr = 0;

    // Stores value of N
    int temp = N;

    // Decrement the value of temp
    while (temp > 0)
    {

        // Stores square root of temp
        int X = (int)Math.sqrt(temp);

        // If temp is a perfect square
        if (X * X == temp)
        {
            break;
        }

        // Update temp
        temp = temp - 2;
        cntDecr += 1;
    }

    // Store count of operations
    // by performing increments
    int cntIncr = 0;

    // Increment the value of N
    while (true)
    {

        // Stores sqrt of N
        int X = (int)Math.sqrt(N);

        // If N is a perfect square
        if (X * X == N)
        {
            break;
        }

        // Update temp
        N = N + 2;
        cntIncr += 1;
    }

    // Return the minimum count
    return Math.min(cntIncr, cntDecr);
}

// Driver code
public static void main (String args[])
{
    int N = 15;

    System.out.print(MinimumOperationReq(N)); 
}
}

// This code is contributed by ajaykr00kj
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the minimum number
# of operations required to make
# N a perfect square
def MinimumOperationReq(N):

    # Stores count of operations
    # by performing decrements
    cntDecr = 0;

    # Stores value of N
    temp = N;

    # Decrement the value of
    # temp
    while (temp > 0):

        # Stores square root of
        # temp
        X = int(pow(temp, 1 / 2))

        # If temp is a perfect
        # square
        if (X * X == temp):
            break;

        # Update temp
        temp = temp - 2;
        cntDecr += 1;

    # Store count of operations
    # by performing increments
    cntIncr = 0;

    # Increment the value of N
    while (True):

        # Stores sqrt of N
        X = int(pow(N, 1 / 2))

        # If N is a perfect
        # square
        if (X * X == N):
            break;

        # Update temp
        N = N + 2;
        cntIncr += 1;

    # Return the minimum
    # count
    return min(cntIncr,
               cntDecr);

# Driver code
if __name__ == '__main__':

    N = 15;
    print(MinimumOperationReq(N));

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to find the minimum number
// of operations required to make
// N a perfect square
static int MinimumOperationReq(int N)
{
  // Stores count of operations
  // by performing decrements
  int cntDecr = 0;

  // Stores value of N
  int temp = N;

  // Decrement the value of
  // temp
  while (temp > 0)
  {

    // Stores square root of temp
    int X = (int)Math.Sqrt(temp);

    // If temp is a perfect square
    if (X * X == temp)
    {
      break;
    }

    // Update temp
    temp = temp - 2;
    cntDecr += 1;
  }

  // Store count of operations
  // by performing increments
  int cntIncr = 0;

  // Increment the value of N
  while (true)
  {
    // Stores sqrt of N
    int X = (int)Math.Sqrt(N);

    // If N is a perfect square
    if (X * X == N)
    {
      break;
    }

    // Update temp
    N = N + 2;
    cntIncr += 1;
  }

  // Return the minimum count
  return Math.Min(cntIncr,
                  cntDecr);
}

// Driver code
public static void Main(String []args)
{
  int N = 15;
  Console.Write(MinimumOperationReq(N)); 
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to find the minimum number
// of operations required to make
// N a perfect square
function MinimumOperationReq(N)
{

    // Stores count of operations
    // by performing decrements
    let cntDecr = 0;

    // Stores value of N
    let temp = N;

    // Decrement the value of temp
    while (temp > 0)
    {

        // Stores square root of temp
        let X = Math.floor(Math.sqrt(temp));

        // If temp is a perfect square
        if (X * X == temp)
        {
            break;
        }

        // Update temp
        temp = temp - 2;
        cntDecr += 1;
    }

    // Store count of operations
    // by performing increments
    let cntIncr = 0;

    // Increment the value of N
    while (true)
    {

        // Stores sqrt of N
        let X = Math.floor(Math.sqrt(N));

        // If N is a perfect square
        if (X * X == N)
        {
            break;
        }

        // Update temp
        N = N + 2;
        cntIncr += 1;
    }

    // Return the minimum count
    return Math.min(cntIncr, cntDecr);
}

    // Driver Code
    let N = 15;

    document.write(MinimumOperationReq(N));

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N * log<sub>2</sub>(N))*
***辅助空间:** O(1)*