# 若存在有限解，求线性丢番图方程的初始积分解

> 原文:[https://www . geesforgeks . org/find-初始-积分-线性丢番图方程解-如果-有限-解-存在/](https://www.geeksforgeeks.org/find-initial-integral-solution-of-linear-diophantine-equation-if-finite-solution-exists/)

给定三个整数 **a** 、 **b** 和 **c** ，表示形式为: **ax + by = c** 的线性方程。任务是在存在有限解的情况下找到给定方程的初始积分解。

> 一个[线性丢番图方程(LDE)](https://math.libretexts.org/Courses/Mount_Royal_University/MATH_2150%3A_Higher_Arithmetic/5%3A_Diophantine_Equations/5.1%3A_Linear_Diophantine_Equations) 是一个具有 2 个或更多整数未知数的方程，并且每个整数未知数至多为 1 度。二元线性丢番图方程取 ax+by=c 的形式，其中 x，y 为整数变量，a，b，c 为整数常数。x 和 y 是未知变量。

**例:**

> **输入:** a = 4，b = 18，c = 10
> **输出:** x = -20，y = 5
> 
> **解释:** (-20)*4 + (5)*18 = 10
> 
> **输入:** a = 9，b = 12，c = 5
> **输出:**不存在解

**进场:**

1.  首先，检查 **a** 和是否非零。
2.  如果两者都为零并且 **c** 非零，则不存在解。如果 **c** 也为零，则无限解存在。
3.  对于给定的 **a** 和 **b** ，使用[扩展欧氏算法](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/)计算 x <sub>1</sub> 、y <sub>1</sub> 和 *gcd* 的值。
4.  现在，对于现有 gcd 的一个解决方案(a，b)应该是 **c** 的倍数。
5.  如下计算方程的解:

```
x = x1 * ( c / gcd )
y = y1 * ( c / gcd )
```

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to implement the extended
// euclid algorithm
int gcd_extend(int a, int b,
               int& x, int& y)
{
    // Base Case
    if (b == 0) {
        x = 1;
        y = 0;
        return a;
    }

    // Recursively find the gcd
    else {
        int g = gcd_extend(b,
                           a % b, x, y);
        int x1 = x, y1 = y;
        x = y1;
        y = x1 - (a / b) * y1;
        return g;
    }
}

// Function to print the solutions of
// the given equations ax + by = c
void print_solution(int a, int b, int c)
{
    int x, y;
    if (a == 0 && b == 0) {

        // Condition for infinite solutions
        if (c == 0) {
            cout
                << "Infinite Solutions Exist"
                << endl;
        }

        // Condition for no solutions exist
        else {
            cout
                << "No Solution exists"
                << endl;
        }
    }
    int gcd = gcd_extend(a, b, x, y);

    // Condition for no solutions exist
    if (c % gcd != 0) {
        cout
            << "No Solution exists"
            << endl;
    }
    else {

        // Print the solution
        cout << "x = " << x * (c / gcd)
             << ", y = " << y * (c / gcd)
             << endl;
    }
}

// Driver Code
int main(void)
{
    int a, b, c;

    // Given coefficients
    a = 4;
    b = 18;
    c = 10;

    // Function Call
    print_solution(a, b, c);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

static int x, y;

// Function to implement the extended
// euclid algorithm
static int gcd_extend(int a, int b)
{

    // Base Case
    if (b == 0)
    {
        x = 1;
        y = 0;
        return a;
    }

    // Recursively find the gcd
    else
    {
        int g = gcd_extend(b, a % b);
        int x1 = x, y1 = y;
        x = y1;
        y = x1 - (a / b) * y1;
        return g;
    }
}

// Function to print the solutions of
// the given equations ax + by = c
static void print_solution(int a, int b, int c)
{
    if (a == 0 && b == 0)
    {

        // Condition for infinite solutions
        if (c == 0)
        {
            System.out.print("Infinite Solutions " +
                             "Exist" + "\n");
        }

        // Condition for no solutions exist
        else
        {
            System.out.print("No Solution exists" +
                             "\n");
        }
    }
    int gcd = gcd_extend(a, b);

    // Condition for no solutions exist
    if (c % gcd != 0)
    {
        System.out.print("No Solution exists" + "\n");
    }
    else
    {

        // Print the solution
        System.out.print("x = " + x * (c / gcd) +
                       ", y = " + y * (c / gcd) + "\n");
    }
}

// Driver Code
public static void main(String[] args)
{
    int a, b, c;

    // Given coefficients
    a = 4;
    b = 18;
    c = 10;

    // Function Call
    print_solution(a, b, c);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

x, y = 0, 0

# Function to implement the extended
# euclid algorithm
def gcd_extend(a, b):
    global x, y

    # Base Case
    if (b == 0):
        x = 1
        y = 0
        return a

    # Recursively find the gcd
    else:
        g = gcd_extend(b, a % b)
        x1, y1 = x, y
        x = y1
        y = x1 - math.floor(a / b) * y1
        return g

# Function to print the solutions of
# the given equations ax + by = c
def print_solution(a, b, c):
    if (a == 0 and b == 0):

        # Condition for infinite solutions
        if (c == 0):
            print("Infinite Solutions Exist")

        # Condition for no solutions exist
        else :
            print("No Solution exists")
    gcd = gcd_extend(a, b)

    # Condition for no solutions exist
    if (c % gcd != 0):
        print("No Solution exists")
    else:
        # Print the solution
        print("x = ", int(x * (c / gcd)), ", y = ", int(y * (c / gcd)), sep = "")

# Given coefficients
a = 4
b = 18
c = 10

# Function Call
print_solution(a, b, c)

# This code is contributed by decode2207.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static int x, y;

// Function to implement the extended
// euclid algorithm
static int gcd_extend(int a, int b)
{

    // Base Case
    if (b == 0)
    {
        x = 1;
        y = 0;
        return a;
    }

    // Recursively find the gcd
    else
    {
        int g = gcd_extend(b, a % b);
        int x1 = x, y1 = y;
        x = y1;
        y = x1 - (a / b) * y1;
        return g;
    }
}

// Function to print the solutions of
// the given equations ax + by = c
static void print_solution(int a, int b, int c)
{
    if (a == 0 && b == 0)
    {

        // Condition for infinite solutions
        if (c == 0)
        {
            Console.Write("Infinite Solutions " +
                          "Exist" + "\n");
        }

        // Condition for no solutions exist
        else
        {
            Console.Write("No Solution exists" +
                          "\n");
        }
    }
    int gcd = gcd_extend(a, b);

    // Condition for no solutions exist
    if (c % gcd != 0)
    {
        Console.Write("No Solution exists" + "\n");
    }
    else
    {

        // Print the solution
        Console.Write("x = " + x * (c / gcd) +
                    ", y = " + y * (c / gcd) + "\n");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int a, b, c;

    // Given coefficients
    a = 4;
    b = 18;
    c = 10;

    // Function call
    print_solution(a, b, c);
}
}

// This code contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript program for the above approach

let x, y;

// Function to implement the extended
// euclid algorithm
function gcd_extend(a, b)
{

    // Base Case
    if (b == 0)
    {
        x = 1;
        y = 0;
        return a;
    }

    // Recursively find the gcd
    else
    {
        let g = gcd_extend(b, a % b);
        let x1 = x, y1 = y;
        x = y1;
        y = x1 - Math.floor(a / b) * y1;
        return g;
    }
}

// Function to print the solutions of
// the given equations ax + by = c
function print_solution(a, b, c)
{
    if (a == 0 && b == 0)
    {

        // Condition for infinite solutions
        if (c == 0)
        {
            document.write("Infinite Solutions " +
                             "Exist" + "\n");
        }

        // Condition for no solutions exist
        else
        {
            document.write("No Solution exists" +
                             "\n");
        }
    }
    let gcd = gcd_extend(a, b);

    // Condition for no solutions exist
    if (c % gcd != 0)
    {
        document.write("No Solution exists" + "\n");
    }
    else
    {

        // Print the solution
        document.write("x = " + x * (c / gcd) +
                       ", y = " + y * (c / gcd) + "<br/>");
    }
}

// Driver Code

   let a, b, c;

    // Given coefficients
    a = 4;
    b = 18;
    c = 10;

    // Function Call
    print_solution(a, b, c);

</script>
```

**Output:** 

```
x = -20, y = 5
```

**时间复杂度:** *O(log(max(A，B)))* ，其中 A 和 B 是给定线性方程中 x 和 y 的系数。
**辅助空间:** *O(1)*