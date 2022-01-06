# 使两个给定整数相等所需的 2、3 或 5 的除法最小化

> 原文:[https://www . geesforgeks . org/minimum-division-by-2-3 或-5-required-make-two-给定整数-equal/](https://www.geeksforgeeks.org/minimize-divisions-by-2-3-or-5-required-to-make-two-given-integers-equal/)

给定两个整数 **X** 和 **Y** ，任务是通过将 **X** 或 **Y** 除以 **2** 、 **3** 或 **5** 中的最小次数，使 **X** 和 **Y** 相等。如果两个整数可以相等，则打印**-1”**。

**示例:**

> **输入:** X = 15，Y = 20
> **输出:** 3
> **解释:**
> **运算 1:** 将 X(= 15)减少到 15/3 即 X = 15/3 = 5。
> **操作 2:** 将 Y(= 20)减少到 20/2，即 Y = 20/2 = 10。
> **操作 3:** 将 Y(= 20)减少到 10/2，即 Y = 10/2 = 5。
> 上述操作后，X 和 Y 相等，即 5。
> 因此，所需操作的计数为 3。
> 
> **输入:** X = 6，Y = 6
> T3】输出: 0

**进场:**给定的问题可以解决[贪婪的](https://www.geeksforgeeks.org/greedy-algorithms/)。这个想法是将给定的整数简化为它们的 [GCD](https://www.geeksforgeeks.org/stdgcd-c-inbuilt-function-finding-gcd/) ，以使它们相等。按照以下步骤解决问题:

*   求 **X** 和**Y**T7】的[最大公约数( **GCD** ，用它们的 **GCD** 除 **X** 和 **Y** 。](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)
*   初始化一个变量，比如说**计数**，来存储需要的除法数。
*   迭代直到 **X** 不等于 **Y** ，执行以下步骤:
    *   如果 **X** 的值大于 **Y** ，则交换 **X** 和 **Y** 。
    *   如果**较大的数**(即 **Y** )可被 **2** 、 **3** 或 **5** 整除，则除以该数。将**计数**增加 **1** 。否则，如果无法使两个数相等，则打印**-1”**、[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   完成上述步骤后，如果两个数可以相等，则打印**计数**的值作为使 **X** 和 **Y** 相等所需的最小除法数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate
// GCD of two numbers
int gcd(int a, int b)
{
    // Base Case
    if (b == 0) {
        return a;
    }

    // Calculate GCD recursively
    return gcd(b, a % b);
}

// Function to count the minimum
// number of divisions required
// to make X and Y equal
void minimumOperations(int X, int Y)
{
    // Calculate GCD of X and Y
    int GCD = gcd(X, Y);

    // Divide X and Y by their GCD
    X = X / GCD;
    Y = Y / GCD;

    // Stores the number of divisions
    int count = 0;

    // Iterate until X != Y
    while (X != Y) {

        // Maintain the order X <= Y
        if (Y > X) {
            swap(X, Y);
        }

        // If X is divisible by 2,
        // then divide X by 2
        if (X % 2 == 0) {
            X = X / 2;
        }

        // If X is divisible by 3,
        // then divide X by 3
        else if (X % 3 == 0) {
            X = X / 3;
        }

        // If X is divisible by 5,
        // then divide X by 5
        else if (X % 5 == 0) {
            X = X / 5;
        }

        // If X is not divisible by
        // 2, 3, or 5, then print -1
        else {
            cout << "-1";
            return;
        }

        // Increment count by 1
        count++;
    }

    // Print the value of count as the
    // minimum number of operations
    cout << count;
}

// Driver Code
int main()
{
    int X = 15, Y = 20;
    minimumOperations(X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to calculate
// GCD of two numbers
static int gcd(int a, int b)
{

    // Base Case
    if (b == 0)
    {
        return a;
    }

    // Calculate GCD recursively
    return gcd(b, a % b);
}

// Function to count the minimum
// number of divisions required
// to make X and Y equal
static void minimumOperations(int X, int Y)
{

    // Calculate GCD of X and Y
    int GCD = gcd(X, Y);

    // Divide X and Y by their GCD
    X = X / GCD;
    Y = Y / GCD;

    // Stores the number of divisions
    int count = 0;

    // Iterate until X != Y
    while (X != Y)
    {

        // Maintain the order X <= Y
        if (Y > X)
        {
            int t = X;
            X = Y;
            Y = t;
        }

        // If X is divisible by 2,
        // then divide X by 2
        if (X % 2 == 0)
        {
            X = X / 2;
        }

        // If X is divisible by 3,
        // then divide X by 3
        else if (X % 3 == 0)
        {
            X = X / 3;
        }

        // If X is divisible by 5,
        // then divide X by 5
        else if (X % 5 == 0)
        {
            X = X / 5;
        }

        // If X is not divisible by
        // 2, 3, or 5, then print -1
        else
        {
            System.out.print("-1");
            return;
        }

        // Increment count by 1
        count += 1;
    }

    // Print the value of count as the
    // minimum number of operations
    System.out.println(count);
}

// Driver Code
static public void main(String args[])
{
    int X = 15, Y = 20;

    minimumOperations(X, Y);
}
}

// This code is contributed by ipg2016107
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate
# GCD of two numbers
def gcd(a, b):

    # Base Case
    if (b == 0):
        return a

    # Calculate GCD recursively
    return gcd(b, a % b)

# Function to count the minimum
# number of divisions required
# to make X and Y equal
def minimumOperations(X, Y):

    # Calculate GCD of X and Y
    GCD = gcd(X, Y)

    # Divide X and Y by their GCD
    X = X // GCD
    Y = Y // GCD

    # Stores the number of divisions
    count = 0

    # Iterate until X != Y
    while (X != Y):

        # Maintain the order X <= Y
        if (Y > X):
            X, Y = Y, X

        # If X is divisible by 2,
        # then divide X by 2
        if (X % 2 == 0):
            X = X // 2

        # If X is divisible by 3,
        # then divide X by 3
        elif (X % 3 == 0):
            X = X // 3

        # If X is divisible by 5,
        # then divide X by 5
        elif (X % 5 == 0):
            X = X // 5

        # If X is not divisible by
        # 2, 3, or 5, then pr-1
        else:
            print("-1")
            return

        # Increment count by 1
        count += 1

    # Print the value of count as the
    # minimum number of operations
    print (count)

# Driver Code
if __name__ == '__main__':

    X, Y = 15, 20

    minimumOperations(X, Y)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

// Function to calculate
// GCD of two numbers
static int gcd(int a, int b)
{

    // Base Case
    if (b == 0) {
        return a;
    }

    // Calculate GCD recursively
    return gcd(b, a % b);
}

// Function to count the minimum
// number of divisions required
// to make X and Y equal
static void minimumOperations(int X, int Y)
{

    // Calculate GCD of X and Y
    int GCD = gcd(X, Y);

    // Divide X and Y by their GCD
    X = X / GCD;
    Y = Y / GCD;

    // Stores the number of divisions
    int count = 0;

    // Iterate until X != Y
    while (X != Y) {

        // Maintain the order X <= Y
        if (Y > X) {
            int t = X;
            X = Y;
            Y = t;
        }

        // If X is divisible by 2,
        // then divide X by 2
        if (X % 2 == 0) {
            X = X / 2;
        }

        // If X is divisible by 3,
        // then divide X by 3
        else if (X % 3 == 0) {
            X = X / 3;
        }

        // If X is divisible by 5,
        // then divide X by 5
        else if (X % 5 == 0) {
            X = X / 5;
        }

        // If X is not divisible by
        // 2, 3, or 5, then print -1
        else {
            Console.WriteLine("-1");
            return;
        }

        // Increment count by 1
        count++;
    }

    // Print the value of count as the
    // minimum number of operations
    Console.WriteLine(count);
}

// Driver Code
static public void Main()
{
    int X = 15, Y = 20;
    minimumOperations(X, Y);
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

    // Function to calculate
    // GCD of two numbers
    function gcd(a , b) {

        // Base Case
        if (b == 0) {
            return a;
        }

        // Calculate GCD recursively
        return gcd(b, a % b);
    }

    // Function to count the minimum
    // number of divisions required
    // to make X and Y equal
    function minimumOperations(X , Y) {

        // Calculate GCD of X and Y
        var GCD = gcd(X, Y);

        // Divide X and Y by their GCD
        X = X / GCD;
        Y = Y / GCD;

        // Stores the number of divisions
        var count = 0;

        // Iterate until X != Y
        while (X != Y) {

            // Maintain the order X <= Y
            if (Y > X) {
                var t = X;
                X = Y;
                Y = t;
            }

            // If X is divisible by 2,
            // then divide X by 2
            if (X % 2 == 0) {
                X = X / 2;
            }

            // If X is divisible by 3,
            // then divide X by 3
            else if (X % 3 == 0) {
                X = X / 3;
            }

            // If X is divisible by 5,
            // then divide X by 5
            else if (X % 5 == 0) {
                X = X / 5;
            }

            // If X is not divisible by
            // 2, 3, or 5, then print -1
            else {
                document.write("-1");
                return;
            }

            // Increment count by 1
            count += 1;
        }

        // Print the value of count as the
        // minimum number of operations
        document.write(count);
    }

    // Driver Code
        var X = 15, Y = 20;

        minimumOperations(X, Y);

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(log(max(X，Y)))*
***辅助空间:** O(1)*