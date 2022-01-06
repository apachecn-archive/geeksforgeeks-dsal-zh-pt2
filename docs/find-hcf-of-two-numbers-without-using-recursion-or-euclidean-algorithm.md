# 不用递归或欧几里德算法求两个数的 HCF

> 原文:[https://www . geesforgeks . org/find-hcf-of-two-numbers-of-not-use-recursion-or-euclidean-algorithm/](https://www.geeksforgeeks.org/find-hcf-of-two-numbers-without-using-recursion-or-euclidean-algorithm/)

给定两个整数 **x** 和 **y** ，任务是在不使用递归或欧几里得方法的情况下找到数字的 HCF。

**示例:**

> **输入:** x = 16，y = 32
> T3】输出: 16
> 
> **输入:** x = 12，y = 15
> **输出:** 3

**逼近:**两个数的 HCF 是能除两个数的最大数。如果两个数字中较小的一个可以除以较大的数字，那么 HCF 就是较小的数字。否则从(smaller)到 1 开始，检查当前元素是否将两个数字分开。如果是，那么它就是所需的 HCF。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the HCF of x and y
int getHCF(int x, int y)
{

    // Minimum of the two numbers
    int minimum = min(x, y);

    // If both the numbers are divisible
    // by the minimum of these two then
    // the HCF is equal to the minimum
    if (x % minimum == 0 && y % minimum == 0)
        return minimum;

    // Highest number between 2 and minimum/2
    // which can divide both the numbers
    // is the required HCF
    for (int i = minimum / 2; i >= 2; i--) {

        // If both the numbers
        // are divisible by i
        if (x % i == 0 && y % i == 0)
            return i;
    }

    // 1 divides every number
    return 1;
}

// Driver code
int main()
{
    int x = 16, y = 32;
    cout << getHCF(x, y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the HCF of x and y
static int getHCF(int x, int y)
{

    // Minimum of the two numbers
    int minimum = Math.min(x, y);

    // If both the numbers are divisible
    // by the minimum of these two then
    // the HCF is equal to the minimum
    if (x % minimum == 0 && y % minimum == 0)
        return minimum;

    // Highest number between 2 and minimum/2
    // which can divide both the numbers
    // is the required HCF
    for (int i = minimum / 2; i >= 2; i--)
    {

        // If both the numbers
        // are divisible by i
        if (x % i == 0 && y % i == 0)
            return i;
    }

    // 1 divides every number
    return 1;
}

// Driver code
public static void main(String[] args)
{
    int x = 16, y = 32;
    System.out.println(getHCF(x, y));
}
}

// This code is contributed by Code_Mech.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the HCF of x and y
def getHCF(x, y):

    # Minimum of the two numbers
    minimum = min(x, y)

    # If both the numbers are divisible
    # by the minimum of these two then
    # the HCF is equal to the minimum
    if (x % minimum == 0 and y % minimum == 0):
        return minimum

    # Highest number between 2 and minimum/2
    # which can divide both the numbers
    # is the required HCF
    for i in range(minimum // 2, 1, -1):

        # If both the numbers are divisible by i
        if (x % i == 0 and y % i == 0):
            return i

    # 1 divides every number
    return 1

# Driver code
x, y = 16, 32
print(getHCF(x, y))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the HCF of x and y
static int getHCF(int x, int y)
{

    // Minimum of the two numbers
    int minimum = Math.Min(x, y);

    // If both the numbers are divisible
    // by the minimum of these two then
    // the HCF is equal to the minimum
    if (x % minimum == 0 && y % minimum == 0)
        return minimum;

    // Highest number between 2 and minimum/2
    // which can divide both the numbers
    // is the required HCF
    for (int i = minimum / 2; i >= 2; i--)
    {

        // If both the numbers
        // are divisible by i
        if (x % i == 0 && y % i == 0)
            return i;
    }

    // 1 divides every number
    return 1;
}

// Driver code
static void Main()
{
    int x = 16, y = 32;
    Console.WriteLine(getHCF(x, y));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the HCF of x and y
function getHCF($x, $y)
{

    // Minimum of the two numbers
    $minimum = min($x, $y);

    // If both the numbers are divisible
    // by the minimum of these two then
    // the HCF is equal to the minimum
    if ($x % $minimum == 0 &&
        $y % $minimum == 0)
        return $minimum;

    // Highest number between 2 and minimum/2
    // which can divide both the numbers
    // is the required HCF
    for ($i = $minimum / 2; $i >= 2; $i--)
    {

        // If both the numbers
        // are divisible by i
        if ($x % $i == 0 &&
            $y % $i == 0)
            return $i;
    }

    // 1 divides every number
    return 1;
}

// Driver code
$x = 16; $y = 32;
echo(getHCF($x, $y));

// This code is contributed
// by Code_Mech.
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the HCF of x and y
function getHCF(x, y)
{

    // Minimum of the two numbers
    var minimum = Math.min(x, y);

    // If both the numbers are divisible
    // by the minimum of these two then
    // the HCF is equal to the minimum
    if (x % minimum == 0 && y % minimum == 0)
        return minimum;

    // Highest number between 2 and minimum/2
    // which can divide both the numbers
    // is the required HCF
    for(var i = minimum / 2; i >= 2; i--)
    {

        // If both the numbers
        // are divisible by i
        if (x % i == 0 && y % i == 0)
            return i;
    }

    // 1 divides every number
    return 1;
}

// Driver code
var x = 16, y = 32;

document.write(getHCF(x, y));

// This code is contributed by noob2000

</script>
```

**Output:** 

```
16
```