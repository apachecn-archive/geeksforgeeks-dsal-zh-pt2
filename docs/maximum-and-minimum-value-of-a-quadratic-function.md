# 二次函数的最大值和最小值

> 原文:[https://www . geesforgeks . org/二次函数的最大值和最小值/](https://www.geeksforgeeks.org/maximum-and-minimum-value-of-a-quadratic-function/)

给定二次函数 **ax <sup>2</sup> + bx + c** 。当 x 对所有可能的实值都变化时，求函数的最大值和最小值。

**示例:**

```
Input: a = 1, b = -4, c = 4
Output:
Maxvalue = Infinity
Minvalue = 0
Quadratic function given is x2 -4x + 4
At x = 2, value of the function is equal to zero.

Input: a = -1, b = 3, c = -2
Output:
Maxvalue = 0.25
Minvalue = -Infinity
```

**进场:**

```
 Q(x)=ax2 + bx + c.
     =a(x + b/(2a))2      +     c-b2/(4a).
       first part             second part
```

该功能分为两部分。
第一部分是一个完美的平方函数。可能有两种情况:

1.  **情况 1:** 如果 a 的值为正。
    *   最大值将等于无穷大。
    *   当第一部分等于零时，函数的最小值就会出现，因为平方函数的最小值为零。
2.  **情况 2:** 如果 a 的值为负。
    *   最小值将等于-无穷大。
    *   既然 a 是负的，任务就是最大化负平方函数。同样，负平方函数的最大值将等于零，因为它对于 x 的任何其他值都是负值。

第二部分是给定二次函数的常数值，因此对于 x 的任何值都不能改变。因此，在两种情况下都会相加。因此，问题的答案是:

```
If a > 0,
    Maxvalue = Infinity
    Minvalue = c - b2 / (4a)
If a < 0,
    Maxvalue = c - b2 / (4a)
    Minvalue = -Infinity
```

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the Maximum and Minimum
// values of the quadratic function
void PrintMaxMinValue(double a, double b, double c)
{

    // Calculate the value of second part
    double secondPart = c * 1.0 - (b * b / (4.0 * a));

    // Print the values
    if (a > 0) {

        // Open upward parabola function
        cout << "Maxvalue = "
             << "Infinity\n";
        cout << "Minvalue = " << secondPart;
    }
    else if (a < 0) {

        // Open downward parabola function
        cout << "Maxvalue = " << secondPart << "\n";
        cout << "Minvalue = "
             << "-Infinity";
    }
    else {

        // If a=0 then it is not a quadratic function
        cout << "Not a quadratic function\n";
    }
}

// Driver code
int main()
{
    double a = -1, b = 3, c = -2;

    PrintMaxMinValue(a, b, c);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

    // Function to print the Maximum and Minimum
    // values of the quadratic function
    static void PrintMaxMinValue(double a, double b, double c)
    {

        // Calculate the value of second part
        double secondPart = c * 1.0 - (b * b / (4.0 * a));

        // Print the values
        if (a > 0)
        {

            // Open upward parabola function
            System.out.print("Maxvalue = "
                    + "Infinity\n");
            System.out.print("Minvalue = " + secondPart);
        }
        else if (a < 0)
        {

            // Open downward parabola function
            System.out.print("Maxvalue = " + secondPart + "\n");
            System.out.print("Minvalue = "
                    + "-Infinity");
        }
        else
        {

            // If a=0 then it is not a quadratic function
            System.out.print("Not a quadratic function\n");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        double a = -1, b = 3, c = -2;

        PrintMaxMinValue(a, b, c);
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to print the Maximum and Minimum
# values of the quadratic function
def PrintMaxMinValue(a, b, c) :

    # Calculate the value of second part
    secondPart = c * 1.0 - (b * b / (4.0 * a));

    # Print the values
    if (a > 0) :

        # Open upward parabola function
        print("Maxvalue =", "Infinity");
        print("Minvalue = ", secondPart);

    elif (a < 0) :

        # Open downward parabola function
        print("Maxvalue = ", secondPart);
        print("Minvalue =", "-Infinity");

    else :

        # If a=0 then it is not a quadratic function
        print("Not a quadratic function");

# Driver code
if __name__ == "__main__" :
    a = -1; b = 3; c = -2;

    PrintMaxMinValue(a, b, c);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to print the Maximum and Minimum
    // values of the quadratic function
    static void PrintMaxMinValue(double a, double b, double c)
    {

        // Calculate the value of second part
        double secondPart = c * 1.0 - (b * b / (4.0 * a));

        // Print the values
        if (a > 0)
        {

            // Open upward parabola function
            Console.Write("Maxvalue = "
                    + "Infinity\n");
            Console.Write("Minvalue = " + secondPart);
        }
        else if (a < 0)
        {

            // Open downward parabola function
            Console.Write("Maxvalue = " + secondPart + "\n");
            Console.Write("Minvalue = "
                    + "-Infinity");
        }
        else
        {

            // If a=0 then it is not a quadratic function
            Console.Write("Not a quadratic function\n");
        }
    }

    // Driver code
    static public void Main ()
    {
        double a = -1, b = 3, c = -2;
        PrintMaxMinValue(a, b, c);
    }
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to print the Maximum and Minimum
// values of the quadratic function
function PrintMaxMinValue(a, b, c)
{

    // Calculate the value of second part
    var secondPart = c * 1.0 -
                    (b * b / (4.0 * a));

    // Print the values
    if (a > 0)
    {

        // Open upward parabola function
        document.write("Maxvalue = " +
                       "Infinity" + "<br>");
        document.write("Minvalue = " +
                       secondPart);
    }
    else if (a < 0)
    {

        // Open downward parabola function
        document.write("Maxvalue = " +
                       secondPart + "<br>");
        document.write("Minvalue = " +
                       "-Infinity");
    }
    else
    {

        // If a=0 then it is not a quadratic function
        document.write("Not a quadratic function\n");
    }
}

// Driver Code
var a = -1, b = 3, c = -2;

PrintMaxMinValue(a, b, c);

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
Maxvalue = 0.25
Minvalue = -Infinity
```