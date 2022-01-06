# 最小化成本，以给定的增量使 X 和 Y 相等

> 原文:[https://www . geeksforgeeks . org/按给定增量最小化制造 x 和 y 的成本/](https://www.geeksforgeeks.org/minimize-cost-to-make-x-and-y-equal-by-given-increments/)

给定两个整数 **X** 和 **Y** ，任务是通过执行以下任意次数的操作使两个整数相等:

*   将 **X** 增加 **M** 倍。成本=**M–1**。
*   将 **Y** 增加 **N** 倍。成本=**N–1**。

**示例:**

> **输入:** X = 2，Y = 4
> **输出:** 1
> **说明:**
> 增加 X 2 倍。因此，X = 2 * 2 = 4。成本= 1。
> 很明显，X = Y .因此，总成本= 1。
> 
> **输入:** X = 4，Y = 6
> **输出:** 3
> **说明:**
> 增加 X 3 倍，X = 3 * 4 = 12。成本= 2。
> 将 Y 增加 2 倍，Y = 2 * 6 = 12。成本= 1。
> 很明显，X = Y .因此，总成本= 2 + 1 = 3。

**天真方法:**按照以下步骤解决问题:

1.  对于 **X** 的每个值，如果 **Y** 小于 **X** ，则增加 **Y** 并更新成本。
2.  如果 **X = Y** ，则打印总成本。
3.  如果 **X < Y** ，则增加 **X** 并更新成本。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to find minimum cost
// to make x and y equal
int minimumCost(int x, int y)
{
    int costx = 0, dup_x = x;

    while (true) {

        int costy = 0, dup_y = y;

        // Check if it possible
        // to make x == y
        while (dup_y != dup_x
               && dup_y < dup_x) {
            dup_y += y;
            costy++;
        }

        // Iif both are equal
        if (dup_x == dup_y)
            return costx + costy;

        // Otherwise
        else {

            // Increment cost of x
            // by 1 and dup_x by x
            dup_x += x;
            costx++;
        }
    }
}

// Driver Code
int main()
{
    int x = 5, y = 17;

    // Returns the required minimum cost
    cout << minimumCost(x, y) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to find minimum cost
// to make x and y equal
static int minimumCost(int x, int y)
{
    int costx = 0, dup_x = x;
    while (true)
    {
        int costy = 0, dup_y = y;

        // Check if it possible
        // to make x == y
        while (dup_y != dup_x
               && dup_y < dup_x)
        {
            dup_y += y;
            costy++;
        }

        // Iif both are equal
        if (dup_x == dup_y)
            return costx + costy;

        // Otherwise
        else {

            // Increment cost of x
            // by 1 and dup_x by x
            dup_x += x;
            costx++;
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    int x = 5, y = 17;

    // Returns the required minimum cost
    System.out.print(minimumCost(x, y) +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find minimum cost
# to make x and y equal
def minimumCost(x, y):

    costx, dup_x = 0, x

    while (True):
        costy, dup_y = 0, y

        # Check if it possible
        # to make x == y
        while (dup_y != dup_x and
               dup_y < dup_x):
            dup_y += y
            costy += 1

        # If both are equal
        if (dup_x == dup_y):
            return costx + costy

        # Otherwise
        else:

            # Increment cost of x
            # by 1 and dup_x by x
            dup_x += x
            costx += 1

# Driver Code
if __name__ == '__main__':

    x, y = 5, 17

    # Returns the required minimum cost
    print(minimumCost(x, y))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to find minimum cost
  // to make x and y equal
  static int minimumCost(int x, int y)
  {
    int costx = 0, dup_x = x;
    while (true)
    {
      int costy = 0, dup_y = y;

      // Check if it possible
      // to make x == y
      while (dup_y != dup_x
             && dup_y < dup_x)
      {
        dup_y += y;
        costy++;
      }

      // Iif both are equal
      if (dup_x == dup_y)
        return costx + costy;

      // Otherwise
      else {

        // Increment cost of x
        // by 1 and dup_x by x
        dup_x += x;
        costx++;
      }
    }
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int x = 5, y = 17;

    // Returns the required minimum cost
    Console.Write(minimumCost(x, y) +"\n");
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Function to find minimum cost
    // to make x and y equal
    function minimumCost(x, y)
    {
        var costx = 0, dup_x = x;
        while (true)
        {
            var costy = 0, dup_y = y;

            // Check if it possible
            // to make x == y
            while (dup_y != dup_x && dup_y < dup_x) {
                dup_y += y;
                costy++;
            }

            // Iif both are equal
            if (dup_x == dup_y)
                return costx + costy;

            // Otherwise
            else {

                // Increment cost of x
                // by 1 and dup_x by x
                dup_x += x;
                costx++;
            }
        }
    }

    // Driver Code
        var x = 5, y = 17;

        // Returns the required minimum cost
        document.write(minimumCost(x, y) + "\n");

// This code is contributed by Rajput-Ji
</script>
```

**Output:** 

```
20
```

***时间复杂度:**O((costx+costy)* Y)*
***辅助空间:** O(1)*

**高效方法:**这里的思路是使用 LCM 的[概念。制造 **X** 和 **Y** 的最低成本将等于它们的 LCM。但这还不够。减去 **X** 和 **Y** 的初始值，避免在计算答案时相加。
按照以下步骤解决问题:](https://www.geeksforgeeks.org/program-to-find-lcm-of-two-numbers/)

1.  [求 X 和 y 的 LCM](https://www.geeksforgeeks.org/program-to-find-lcm-of-two-numbers/)
2.  从 LCM 中减去 **X** 和 **Y** 的值。
3.  现在，将 LCM 除以 **X** 和 **Y** ，它们的值之和即为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to find gcd of x and y
int gcd(int x, int y)
{
    if (y == 0)
        return x;
    return gcd(y, x % y);
}

// Function to find lcm of x and y
int lcm(int x, int y)
{
    return (x * y) / gcd(x, y);
}

// Function to find minimum Cost
int minimumCost(int x, int y)
{
    int lcm_ = lcm(x, y);

    // Subtracted initial cost of x
    int costx = (lcm_ - x) / x;

    // Subtracted initial cost of y
    int costy = (lcm_ - y) / y;
    return costx + costy;
}

// Driver Code
int main()
{
    int x = 5, y = 17;

    // Returns the minimum cost required
    cout << minimumCost(x, y) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to find gcd of x and y
static int gcd(int x, int y)
{
    if (y == 0)
        return x;
    return gcd(y, x % y);
}

// Function to find lcm of x and y
static int lcm(int x, int y)
{
    return (x * y) / gcd(x, y);
}

// Function to find minimum Cost
static int minimumCost(int x, int y)
{
    int lcm_ = lcm(x, y);

    // Subtracted initial cost of x
    int costx = (lcm_ - x) / x;

    // Subtracted initial cost of y
    int costy = (lcm_ - y) / y;
    return costx + costy;
}

// Driver Code
public static void main(String[] args)
{
    int x = 5, y = 17;

    // Returns the minimum cost required
    System.out.print(minimumCost(x, y) +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find gcd of x and y
def gcd(x, y):

    if (y == 0):
        return x

    return gcd(y, x % y)

# Function to find lcm of x and y
def lcm(x, y):

    return (x * y) // gcd(x, y)

# Function to find minimum Cost
def minimumCost(x, y):

    lcm_ = lcm(x, y)

    # Subtracted initial cost of x
    costx = (lcm_ - x) // x

    # Subtracted initial cost of y
    costy = (lcm_ - y) // y

    return costx + costy

# Driver Code
if __name__ == "__main__":

    x = 5
    y = 17

    # Returns the minimum cost required
    print(minimumCost(x, y))

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Function to find gcd of x and y
static int gcd(int x, int y)
{
    if (y == 0)
        return x;
    return gcd(y, x % y);
}

// Function to find lcm of x and y
static int lcm(int x, int y)
{
    return (x * y) / gcd(x, y);
}

// Function to find minimum Cost
static int minimumCost(int x, int y)
{
    int lcm_ = lcm(x, y);

    // Subtracted initial cost of x
    int costx = (lcm_ - x) / x;

    // Subtracted initial cost of y
    int costy = (lcm_ - y) / y;
    return costx + costy;
}

// Driver Code
public static void Main(String[] args)
{
    int x = 5, y = 17;

    // Returns the minimum cost required
    Console.Write(minimumCost(x, y) +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Function to find gcd of x and y
    function gcd(x , y) {
        if (y == 0)
            return x;
        return gcd(y, x % y);
    }

    // Function to find lcm of x and y
    function lcm(x , y) {
        return (x * y) / gcd(x, y);
    }

    // Function to find minimum Cost
    function minimumCost(x , y) {
        var lcm_ = lcm(x, y);

        // Subtracted initial cost of x
        var costx = (lcm_ - x) / x;

        // Subtracted initial cost of y
        var costy = (lcm_ - y) / y;
        return costx + costy;
    }

    // Driver Code

        var x = 5, y = 17;

        // Returns the minimum cost required
        document.write(minimumCost(x, y) + "\n");

// This code contributed by gauravrajput1
</script>
```

**Output:** 

```
20
```

***时间复杂度:** O(log(min(x，y))*
***辅助空间:** O(1)*