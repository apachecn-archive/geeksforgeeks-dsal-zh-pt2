# 从(X，Y)

到达(1，1)所需的最小给定移动次数

> 原文:[https://www . geeksforgeeks . org/最小给定移动次数-需要到达-1-1-from-x-y/](https://www.geeksforgeeks.org/minimum-number-of-given-moves-required-to-reach-1-1-from-x-y/)

给定两个整数 **X** 和 **Y** ，任务是计算到达点 **(1，1)** 所需的最小移动次数，从点 **(1，1)** 开始，如果允许的移动来自任何一点，说 **(a，b)** 或者是**(a–b，b)** 或者是 **(a，b–a)。**

**示例:**

> **输入:** X = 3，Y = 1
> **输出:** 2
> **说明:**所需的招式顺序为(3，1) → (2，1) → (1，1)
> 
> **输入:** X = 2，Y = 2
> T3】输出: -1

**天真法:**解决问题最简单的方法就是不断地从较大的数中减去较小的数，直到它们变得相等。如果任何时刻 **X** 或 **Y** 小于 **1** ，打印 **-1** 。否则，将执行的减法次数打印为所需的最小操作次数。

***时间复杂度:** O(max(X，Y))*
***辅助空间:** O(1)*

**高效方法:**优化上述方法，思路是用模运算代替重复减法，类似于用[欧氏算法](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/)计算 [GCD](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/) 。按照以下步骤解决问题:

*   初始化一个变量，用 **0、**表示 **cnt** ，用于存储最小步数。
*   [迭代，当 **X** 和 **Y** 都为非零](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)时，执行以下操作:
    *   如果 **X > Y、**的值，则在 **cnt** 上加上 **X/Y** 。将 **X** 更新为 **X%Y**
    *   如果 **Y > X、**的值，则在 **cnt** 上加上 **Y/X** 。将 **Y** 更新为 **Y%X**
*   检查其中一个是否大于 **1** ，然后打印 **-1** 。
*   否则，将 **cnt** 的值减少 **1、**，因为多做了一步，使其中一个等于 **0** 。
*   打印 **cnt** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of steps
// required to convert (x, y) to (1, 1)
int minimumSteps(int x, int y)
{
    // Store the required result
    int cnt = 0;

    // Iterate while both x
    // and y are not equal to 0
    while (x != 0 && y != 0) {

        // If x is greater than y
        if (x > y) {

            // Update count and value of x
            cnt += x / y;
            x %= y;
        }

        // Otherwise
        else {

            // Update count and value of y
            cnt += y / x;
            y %= x;
        }
    }
    cnt--;

    // If both x and y > 1
    if (x > 1 || y > 1)
        cnt = -1;

    // Print the result
    cout << cnt;
}

// Driver Code
int main()
{
    // Given X and Y
    int x = 3, y = 1;
    minimumSteps(x, y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;

class GFG{

// Function to count the number of steps
// required to convert (x, y) to (1, 1)
static void minimumSteps(int x, int y)
{

    // Store the required result
    int cnt = 0;

    // Iterate while both x
    // and y are not equal to 0
    while (x != 0 && y != 0)
    {

        // If x is greater than y
        if (x > y)
        {

            // Update count and value of x
            cnt += x / y;
            x %= y;
        }

        // Otherwise
        else
        {

            // Update count and value of y
            cnt += y / x;
            y %= x;
        }
    }
    cnt--;

    // If both x and y > 1
    if (x > 1 || y > 1)
        cnt = -1;

    // Print the result
    System.out.println(cnt);
}

// Driver Code
public static void main (String[] args)
{

    // Given X and Y
    int x = 3, y = 1;

    minimumSteps(x, y);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of steps
# required to convert (x, y) to (1, 1)
def minimumSteps(x, y):

    # Store the required result
    cnt = 0

    # Iterate while both x
    # and y are not equal to 0
    while (x != 0 and y != 0):

        # If x is greater than y
        if (x > y):

            # Update count and value of x
            cnt += x / y
            x %= y

        # Otherwise
        else:

            # Update count and value of y
            cnt += y / x
            y %= x

    cnt -= 1

    # If both x and y > 1
    if (x > 1 or y > 1):
        cnt = -1

    # Print the result
    print(int(cnt))

# Driver Code
if __name__ == '__main__':

    # Given X and Y
    x = 3
    y = 1

    minimumSteps(x, y)

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count the number of steps
// required to convert (x, y) to (1, 1)
public static void minimumSteps(int x, int y)
{

    // Store the required result
    int cnt = 0;

    // Iterate while both x
    // and y are not equal to 0
    while (x != 0 && y != 0)
    {

        // If x is greater than y
        if (x > y)
        {

            // Update count and value of x
            cnt += x / y;
            x %= y;
        }

        // Otherwise
        else
        {

            // Update count and value of y
            cnt += y / x;
            y %= x;
        }
    }
    cnt--;

    // If both x and y > 1
    if (x > 1 || y > 1)
        cnt = -1;

    // Print the result
    Console.WriteLine(cnt);
}

// Driver Code
public static void Main()
{

    // Given X and Y
    int x = 3, y = 1;

    minimumSteps(x, y);
}
}

// This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the number of steps
// required to convert (x, y) to (1, 1)
function minimumSteps(x, y)
{
    // Store the required result
    var cnt = 0;

    // Iterate while both x
    // and y are not equal to 0
    while (x != 0 && y != 0) {

        // If x is greater than y
        if (x > y) {

            // Update count and value of x
            cnt += x / y;
            x %= y;
        }

        // Otherwise
        else {

            // Update count and value of y
            cnt += y / x;
            y %= x;
        }
    }
    cnt--;

    // If both x and y > 1
    if (x > 1 || y > 1)
        cnt = -1;

    // Print the result
    document.write( cnt);
}

// Driver Code
// Given X and Y
var x = 3, y = 1;
minimumSteps(x, y);

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(log(max(X，Y)))*
***辅助空间:** O(1)*