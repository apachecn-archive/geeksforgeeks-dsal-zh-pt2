# 使用对数函数

求一个数的立方根

> 原文:[https://www . geesforgeks . org/find-cube-root-of-number-use-log-function/](https://www.geeksforgeeks.org/find-cube-root-of-a-number-using-log-function/)

给定编号 **N** ，任务是利用对数函数找到[立方根](https://www.geeksforgeeks.org/find-cubic-root-of-a-number/)。
**例:**

> **输入:** N = 8
> **输出:** 2.000000
> **输入:** N = 27
> **输出:** 3.000000

**方法:**为了解决上面提到的问题，我们将使用 log()函数，根据以下公式:

> 让 n 的立方根为 d .
> =>∛n = d
> =>n<sup>(1/3)</sup>= d
> 现在，在两边涂抹原木:
> 原木 <sub>3</sub> (N <sup>(1/3)</sup> ) =原木 <sub>3</sub> (d)
> = >原木 <sub>3</sub> (d) = 1/3 *原木 <sub>3</sub>

以下是上述问题的实现:

## C++

```
// C++ program to Find Cube root
// of a number using Logarithm

#include <bits/stdc++.h>

// Function to find the cube root
double cubeRoot(double n)
{
    // calculate the cube root
    double ans = pow(3, (1.0 / 3)
                            * (log(n) / log(3)));

    // Return the final answer
    return ans;
}

// Driver code
int main()
{
    double N = 8;

    printf("%.2lf ", cubeRoot(N));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Find Cube root
// of a number using Logarithm
class GFG{

// Function to find the cube root
static double cubeRoot(double n)
{

    // Calculate the cube root
    double ans = Math.pow(3, ((1.0 / 3) *
                              (Math.log(n) /
                               Math.log(3))));

    // Return the final answer
    return ans;
}

// Driver code
public static void main(String[] args)
{
    double N = 8;
    System.out.printf("%.2f", cubeRoot(N));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find cube root
# of a number using logarithm
import numpy as np

# Function to find the cube root
def cubeRoot(n):

    # Calculate the cube root
    ans = pow(3, (1.0 / 3) * (np.log(n) /
                              np.log(3)))

    # Return the final answer
    return ans

# Driver code
N = 8

print("%.2f" % cubeRoot(N))

# This code is contributed by PratikBasu
```

## C#

```
// C# program to find cube root
// of a number using logarithm
using System;

class GFG{

// Function to find the cube root
static double cubeRoot(double n)
{

    // Calculate the cube root
    double ans = Math.Pow(3, ((1.0 / 3) *
                              (Math.Log(n) /
                               Math.Log(3))));

    // Return the readonly answer
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    double N = 8;

    Console.Write("{0:F2}", cubeRoot(N));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
// javascript  program to Find Cube root
// of a number using Logarithm

// Function to find the cube root
function cubeRoot( n)
{

    // calculate the cube root
    let ans = Math.pow(3, (1.0 / 3)
                            * (Math.log(n) / Math.log(3)));

    // Return the final answer
    return ans;
}

// Driver code
let N = 8;
document.write( cubeRoot(N).toFixed(2));

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
2.00
```