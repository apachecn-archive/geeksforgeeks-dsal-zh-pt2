# 根据给定条件将整数 N 减少到 1 的最小成本

> 原文:[https://www . geesforgeks . org/按给定条件将整数 n 减 1 的最小成本/](https://www.geeksforgeeks.org/minimum-cost-to-reduce-the-integer-n-to-1-as-per-given-conditions/)

给定四个整数 **N，X，P，**和 **Q** ，任务是通过以下两个操作找到使 **N** 变为 **1** 的最小成本:

*   N 减去 **1，成本为 **P** 。**
*   将 **N 除以 X** (如果 N 可被 X 整除)，成本 **Q** 。

**示例:**

> **输入:** N = 5，X = 2，P = 2，Q = 3
> **输出:** 7
> **说明:**
> 操作 1:5–1->成本= 2
> 操作 2: 4 / 2 - >成本= 3
> 操作 3:2–1->成本= 2
> 最小总成本为 2 + 3 + 2 = 7。
> 
> **输入:** N = 6，X = 6，P = 2，Q = 1
> **输出:** 1
> **解释:**
> 操作 1: 6 / 6，成本= 1，因此这是最小值。

**进场:**这个问题可以用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决。以下是观察结果:

1.  如果 x = 1，那么答案是**(N–1)* P**。
2.  否则如果 **N 小于 X** ，那么只能减 1，所以答案是**(N–1)* P**。
3.  否则，进行第一次操作，直到 **N 不能被 X** 整除。
4.  通过比较第一次和第二次操作，最佳地选择第二次操作，即如果我们可以执行第一次操作，使得将 **N 减少到 1** 的成本最小，否则选择第二次操作。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum cost
// to reduce the integer N to 1
// by the given operations
int min_cost(int n, int x, int p, int q)
{
    // Check if x is 1
    if (x == 1) {

        // Print the answer
        cout << (n - 1) * p << endl;
        return 0;
    }

    // Prestore the answer
    int ans = (n - 1) * p;
    int pre = 0;

    // Iterate till n exists
    while (n > 1) {

        // Divide N by x
        int tmp = n / x;

        if (tmp < 0)
            break;

        pre += (n - tmp * x) * p;

        // Reduce n by x
        n /= x;

        // Add the cost
        pre += q;

        // Update the answer
        ans = min(ans,
                  pre + (n - 1) * p);
    }

    // Return the answer
    return ans;
}

// Driver Code
int main()
{
    // Initialize the variables
    int n = 5, x = 2, p = 2, q = 3;

    // Function call
    cout << min_cost(n, x, p, q);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the minimum cost
// to reduce the integer N to 1
// by the given operations
static int min_cost(int n, int x,
                    int p, int q)
{

    // Check if x is 1
    if (x == 1)
    {

        // Print the answer
        System.out.println((n - 1) * p);
        return 0;
    }

    // Prestore the answer
    int ans = (n - 1) * p;
    int pre = 0;

    // Iterate till n exists
    while (n > 1)
    {

        // Divide N by x
        int tmp = n / x;

        if (tmp < 0)
            break;

        pre += (n - tmp * x) * p;

        // Reduce n by x
        n /= x;

        // Add the cost
        pre += q;

        // Update the answer
        ans = Math.min(ans,
                       pre + (n - 1) * p);
    }

    // Return the answer
    return ans;
}

// Driver code
public static void main(String[] args)
{

    // Initialize the variables
    int n = 5, x = 2, p = 2, q = 3;

    // Function call
    System.out.println(min_cost(n, x, p, q));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum cost
# to reduce the integer N to 1
# by the given operations
def min_cost(n, x, p, q):

  # Check if x is 1
  if (x == 1):

    # Print the answer
    print((n - 1) * p)
    return 0

  # Prestore the answer
  ans = (n - 1) * p
  pre = 0

  # Iterate till n exists
  while (n > 1):

    # Divide N by x
    tmp = n // x

    if (tmp < 0):
      break

    pre += (n - tmp * x) * p

    # Reduce n by x
    n //= x

    # Add the cost
    pre += q

    # Update the answer
    ans = min(ans, pre + (n - 1) * p)

  # Return the answer
  return ans

# Driver Code
if __name__ == '__main__':

  # Initialize the variables
  n = 5; x = 2;
  p = 2; q = 3;

  # Function call
  print(min_cost(n, x, p, q))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum cost
// to reduce the integer N to 1
// by the given operations
static int min_cost(int n, int x,
                    int p, int q)
{

    // Check if x is 1
    if (x == 1)
    {

        // Print the answer
        Console.WriteLine((n - 1) * p);
        return 0;
    }

    // Prestore the answer
    int ans = (n - 1) * p;
    int pre = 0;

    // Iterate till n exists
    while (n > 1)
    {

        // Divide N by x
        int tmp = n / x;

        if (tmp < 0)
            break;

        pre += (n - tmp * x) * p;

        // Reduce n by x
        n /= x;

        // Add the cost
        pre += q;

        // Update the answer
        ans = Math.Min(ans,
                       pre + (n - 1) * p);
    }

    // Return the answer
    return ans;
}

// Driver code
public static void Main(String[] args)
{

    // Initialize the variables
    int n = 5, x = 2, p = 2, q = 3;

    // Function call
    Console.WriteLine(min_cost(n, x, p, q));
}
}

// This code is contributed by princiraj1992
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the minimum cost
        // to reduce the integer N to 1
        // by the given operations
        function min_cost(n, x, p, q) {
            // Check if x is 1
            if (x == 1) {

                // Print the answer
                document.write((n - 1) * p + "<br>");
                return 0;
            }

            // Prestore the answer
            let ans = (n - 1) * p;
            let pre = 0;

            // Iterate till n exists
            while (n > 1) {

                // Divide N by x
                let tmp = Math.floor(n / x);

                if (tmp < 0)
                    break;

                pre += (n - tmp * x) * p;

                // Reduce n by x
                n = Math.floor(n / x)

                // Add the cost
                pre += q;

                // Update the answer
                ans = Math.min(ans,
                    pre + (n - 1) * p);
            }

            // Return the answer
            return ans;
        }

        // Driver Code

        // Initialize the variables
        let n = 5, x = 2, p = 2, q = 3;

        // Function call
        document.write(min_cost(n, x, p, q));

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
7
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(1)*