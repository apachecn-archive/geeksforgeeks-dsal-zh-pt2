# 和为 X，积为 Y 的最小序列的长度

> 原文:[https://www . geesforgeks . org/最小序列长度-有-和-x-和-积-y/](https://www.geeksforgeeks.org/length-of-smallest-sequence-having-sum-x-and-product-y/)

给定两个整数 **X** 和 **Y** ，任务是找出由具有和 **X** 和积 **Y** 的正整数组成的最小序列的长度。如果无法生成这样的序列，请打印-1。

**示例:**

> **输入:** X = 5，Y = 5
> **输出:** 1
> **解释:**
> 具有和 5 与积 5 的最小可能序列是{5}。因此，需要的答案是序列的长度(= 1)。
> 
> **输入:** X = 9，Y = 8
> **输出:** 2
> **解释:**
> 最小可能的序列是{1，8}，和 X (= 1 + 8 = 9)与乘积 Y(= 1 * 8 = 8)。

**方法:**思路是在**【1，地板(x/e)】**范围内实施[二分搜索法](https://www.geeksforgeeks.org/binary-search/)解决所需尺寸的给定问题，其中 **e** 为[欧拉常数](https://en.wikipedia.org/wiki/E_(mathematical_constant))。

*   将两个变量**低**和**高**分别初始化为 **1** 和**楼层(x/e)** 。
*   如果 **X** 等于 **Y** ，那么序列的最大尺寸始终可以是 **1** 。所以，打印出来。
*   否则，迭代至**高**与**低**之差超过 1，每次计算**中**。
*   根据每一步的边界条件，重新设置**高**和**低**的值，最后打印**高**的最终值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

#define ll long long
#define pb push_back

// Function for checking valid or not
double temp(int n, int x)
{
    return pow(x * 1.0 / n, n);
}

// Function for checking boundary
// of binary search
bool check(int n, int y, int x)
{
    double v = temp(n, x);
    return (v >= y);
}

// Function to calculate the
// minimum sequence size
// using binary search
void find(int x, int y)
{
    // Initialize high and low
    int high = (int)floor(x / exp(1.0));
    int low = 1;

    // Base case
    if (x == y)
        cout << 1 << endl;

    // Print -1 if a sequence
    // cannot be generated
    else if (!check(high, y, x))
        cout << -1 << endl;

    // Otherwise
    else {

        // Iterate until difference
        // between high and low exceeds 1
        while (high - low > 1) {

            // Calculate mid
            int mid
                = (high + low) / 2;

            // Reset values of high
            // and low accordingly
            if (check(mid, y, x))
                high = mid;
            else
                low = mid;
        }

        // Print the answer
        cout << high << endl;
    }
}

// Driver Code
int main()
{

    int x = 9, y = 8;

    // Function call
    find(x, y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function for checking valid or not
static double temp(int n, int x)
{
    return Math.pow(x * 1.0 / n, n);
}

// Function for checking boundary
// of binary search
static boolean check(int n, int y, int x)
{
    double v = temp(n, x);
    return (v >= y);
}

// Function to calculate the
// minimum sequence size
// using binary search
static void find(int x, int y)
{

    // Initialize high and low
    int high = (int)Math.floor(x /
                    Math.exp(1.0));
    int low = 1;

    // Base case
    if (x == y)
        System.out.print(1 + "\n");

    // Print -1 if a sequence
    // cannot be generated
    else if (!check(high, y, x))
        System.out.print(-1 + "\n");

    // Otherwise
    else
    {

        // Iterate until difference
        // between high and low exceeds 1
        while (high - low > 1)
        {

            // Calculate mid
            int mid = (high + low) / 2;

            // Reset values of high
            // and low accordingly
            if (check(mid, y, x))
                high = mid;
            else
                low = mid;
        }

        // Print the answer
        System.out.print(high + "\n");
    }
}

// Driver Code
public static void main(String[] args)
{
    int x = 9, y = 8;

    // Function call
    find(x, y);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import floor, exp

# Function for checking valid or not
def temp(n, x):

    return pow(x * 1 / n, n)

# Function for checking boundary
# of binary search
def check(n, y, x):

    v = temp(n, x)
    return (v >= y)

# Function to calculate the
# minimum sequence size
# using binary search
def find(x, y):

    # Initialize high and low
    high = floor(x / exp(1.0))
    low = 1

    # Base case
    if (x == y):
        print(1)

    # Print -1 if a sequence
    # cannot be generated
    elif (not check(high, y, x)):
        print(-1)

    # Otherwise
    else:

        # Iterate until difference
        # between high and low exceeds 1
        while (high - low > 1):

            # Calculate mid
            mid = (high + low) // 2

            # Reset values of high
            # and low accordingly
            if (check(mid, y, x)):
                high = mid
            else:
                low = mid

        # Print the answer
        print(high)

# Driver Code
if __name__ == '__main__':

    x = 9
    y = 8

    # Function call
    find(x, y)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function for checking
// valid or not
static double temp(int n,
                   int x)
{
  return Math.Pow(x * 1.0 / n, n);
}

// Function for checking
// boundary of binary search
static bool check(int n,
                  int y, int x)
{
  double v = temp(n, x);
  return (v >= y);
}

// Function to calculate the
// minimum sequence size
// using binary search
static void find(int x, int y)
{
  // Initialize high and low
  int high = (int)Math.Floor(x /
                  Math.Exp(1.0));
  int low = 1;

  // Base case
  if (x == y)
    Console.Write(1 + "\n");

  // Print -1 if a sequence
  // cannot be generated
  else if (!check(high, y, x))
    Console.Write(-1 + "\n");

  // Otherwise
  else
  {
    // Iterate until difference
    // between high and low exceeds 1
    while (high - low > 1)
    {
      // Calculate mid
      int mid = (high + low) / 2;

      // Reset values of high
      // and low accordingly
      if (check(mid, y, x))
        high = mid;
      else
        low = mid;
    }

    // Print the answer
    Console.Write(high + "\n");
  }
}

// Driver Code
public static void Main(String[] args)
{
  int x = 9, y = 8;

  // Function call
  find(x, y);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function for checking valid or not
function temp(n, x)
{
    return Math.pow((x * 1.0) / n, n);
}

// Function for checking boundary
// of binary search
function check(n, y, x)
{
    var v = temp(n, x);
    return v >= y;
}

// Function to calculate the
// minimum sequence size
// using binary search
function find(x, y)
{

    // Initialize high and low
    var high = parseInt(Math.floor(x /
                        Math.exp(1.0)));
    var low = 1;

    // Base case
    if (x == y)
        document.write(1 + "<br>");

    // Print -1 if a sequence
    // cannot be generated
    else if (!check(high, y, x))
        document.write(-1 + "<br>");

    // Otherwise
    else
    {

        // Iterate until difference
        // between high and low exceeds 1
        while (high - low > 1)
        {

            // Calculate mid
            var mid = (high + low) / 2;

            // Reset values of high
            // and low accordingly
            if (check(mid, y, x))
                high = mid;
            else
                low = mid;
        }

        // Print the answer
        document.write(high + "<br>");
    }
}

// Driver Code
var x = 9,
y = 8;

// Function call
find(x, y);

// This code is contributed by rdtank

</script>
```

**Output**

```
2
```

**时间复杂度:**O(log<sub>2</sub>(X/e)
**辅助空间:** O(1)