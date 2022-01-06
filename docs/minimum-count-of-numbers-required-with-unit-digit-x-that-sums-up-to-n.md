# 合计为 N 的单位数字 X 所需的最小数量

> 原文:[https://www . geeksforgeeks . org/最小数字计数-需要单位数字-x-summary-to-n/](https://www.geeksforgeeks.org/minimum-count-of-numbers-required-with-unit-digit-x-that-sums-up-to-n/)

给定两个整数 **N** 和 **X** ，任务是找出和为 N 且单位数字为 X 的整数的最小个数，如果不存在这样的表示，则打印 **-1** 。
**举例:**

> **输入:** N = 38，X = 9
> **输出:** 2
> **说明:**
> 最小需要两个整数，单位数字为 X 表示为等于 38 的和。
> 38 = 19 + 19 或 38 = 29 + 9
> **输入:** N = 6，X = 4
> **输出:** -1
> **说明:**
> 没有
> 这样的表示

**进场:**
按照以下步骤解决问题:

*   获取 **N** 的**单位数字**，检查是否由单位数字为 x 的数字之和实现
*   如果可能，检查**是否 N** ？ ***X** *(需要将单位数字为 X 的数字相加得到总和的最小次数 **N** )* 。
*   如果满足上述条件，则打印需要添加单位数字 X 的数字的最小次数，以获得总和 **N** 。否则，打印-1。

以下是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate and return
// the minimum number of times a number
// with unit digit X needs to be added
// to get a sum N
int check(int unit_digit, int X)
{
    int times, digit;

    // Calculate the number of
    // additions required to get unit
    // digit of N
    for (int times = 1; times <= 10;
         times++) {
        digit = (X * times) % 10;
        if (digit == unit_digit)
            return times;
    }

    // If unit digit of N
    // cannot be obtained
    return -1;
}

// Function to return the minimum
// number required to represent N
int getNum(int N, int X)
{
    int unit_digit;

    // Stores unit digit of N
    unit_digit = N % 10;

    // Stores minimum addition
    // of X required to
    // obtain unit digit of N
    int times = check(unit_digit, X);

    // If unit digit of N
    // cannot be obtained
    if (times == -1)
        return times;

    // Otherwise
    else {

        // If N is greater than
        // or equal to (X*times)
        if (N >= (times * X))

            // Minimum count of numbers
            // that needed to represent N
            return times;

        // Representation not
        // possible
        else
            return -1;
    }
}

// Driver Code
int main()
{
    int N = 58, X = 7;
    cout << getNum(N, X) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
class GFG{

// Function to calculate and return
// the minimum number of times a number
// with unit digit X needs to be added
// to get a sum N
static int check(int unit_digit, int X)
{
    int times, digit;

    // Calculate the number of
    // additions required to get unit
    // digit of N
    for (times = 1; times <= 10;
                    times++)
    {
        digit = (X * times) % 10;
        if (digit == unit_digit)
            return times;
    }

    // If unit digit of N
    // cannot be obtained
    return -1;
}

// Function to return the minimum
// number required to represent N
static int getNum(int N, int X)
{
    int unit_digit;

    // Stores unit digit of N
    unit_digit = N % 10;

    // Stores minimum addition
    // of X required to
    // obtain unit digit of N
    int times = check(unit_digit, X);

    // If unit digit of N
    // cannot be obtained
    if (times == -1)
        return times;

    // Otherwise
    else
    {

        // If N is greater than
        // or equal to (X*times)
        if (N >= (times * X))

            // Minimum count of numbers
            // that needed to represent N
            return times;

        // Representation not
        // possible
        else
            return -1;
    }
}

// Driver Code
public static void main(String []args)
{
    int N = 58, X = 7;
    System.out.println( getNum(N, X));
}
}

// This code is contributed by Ritik Bansal
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to calculate and return
# the minimum number of times a number
# with unit digit X needs to be added
# to get a sum N
def check(unit_digit, X):

    # Calculate the number of additions
    # required to get unit digit of N
    for times in range(1, 11):
        digit = (X * times) % 10
        if (digit == unit_digit):
            return times

    # If unit digit of N
    # cannot be obtained
    return -1

# Function to return the minimum
# number required to represent N
def getNum(N, X):

    # Stores unit digit of N
    unit_digit = N % 10

    # Stores minimum addition
    # of X required to
    # obtain unit digit of N
    times = check(unit_digit, X)

    # If unit digit of N
    # cannot be obtained
    if (times == -1):
        return times

    # Otherwise
    else:

        # If N is greater than
        # or equal to (X*times)
        if (N >= (times * X)):

            # Minimum count of numbers
            # that needed to represent N
            return times

        # Representation not
        # possible
        else:
            return -1

# Driver Code
N = 58
X = 7

print(getNum(N, X))

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG{

// Function to calculate and return
// the minimum number of times a number
// with unit digit X needs to be added
// to get a sum N
static int check(int unit_digit, int X)
{
    int times, digit;

    // Calculate the number of
    // additions required to get unit
    // digit of N
    for (times = 1; times <= 10;
                    times++)
    {
        digit = (X * times) % 10;
        if (digit == unit_digit)
            return times;
    }

    // If unit digit of N
    // cannot be obtained
    return -1;
}

// Function to return the minimum
// number required to represent N
static int getNum(int N, int X)
{
    int unit_digit;

    // Stores unit digit of N
    unit_digit = N % 10;

    // Stores minimum addition
    // of X required to
    // obtain unit digit of N
    int times = check(unit_digit, X);

    // If unit digit of N
    // cannot be obtained
    if (times == -1)
        return times;

    // Otherwise
    else
    {

        // If N is greater than
        // or equal to (X*times)
        if (N >= (times * X))

            // Minimum count of numbers
            // that needed to represent N
            return times;

        // Representation not
        // possible
        else
            return -1;
    }
}

// Driver Code
public static void Main()
{
    int N = 58, X = 7;
    Console.Write(getNum(N, X));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript program implementation
// of the approach

// Function to calculate and return
// the minimum number of times a number
// with unit digit X needs to be added
// to get a sum N
function check(unit_digit, X)
{
    let times, digit;

    // Calculate the number of
    // additions required to get unit
    // digit of N
    for (times = 1; times <= 10;
                    times++)
    {
        digit = (X * times) % 10;
        if (digit == unit_digit)
            return times;
    }

    // If unit digit of N
    // cannot be obtained
    return -1;
}

// Function to return the minimum
// number required to represent N
function getNum(N, X)
{
    let unit_digit;

    // Stores unit digit of N
    unit_digit = N % 10;

    // Stores minimum addition
    // of X required to
    // obtain unit digit of N
    let times = check(unit_digit, X);

    // If unit digit of N
    // cannot be obtained
    if (times == -1)
        return times;

    // Otherwise
    else
    {

        // If N is greater than
        // or equal to (X*times)
        if (N >= (times * X))

            // Minimum count of numbers
            // that needed to represent N
            return times;

        // Representation not
        // possible
        else
            return -1;
    }
}

// Driver Code

    let N = 58, X = 7;
    document.write( getNum(N, X));

   // This code is contributed by splevel62.
</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(1)*
***辅助空间:** O(1)*