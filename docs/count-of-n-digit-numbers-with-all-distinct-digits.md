# 所有不同数字的 N 位数计数

> 原文:[https://www . geesforgeks . org/n 位数字计数加全异数字/](https://www.geeksforgeeks.org/count-of-n-digit-numbers-with-all-distinct-digits/)

给定一个整数 **N** ，任务是找到所有不同数字的 **N 位**数字的计数。
**例:**

> **输入:** N = 1
> **输出:** 9
> 1、2、3、4、5、6、7、8 和 9 是 1 位数的数字
> ，所有数字都不同。
> **输入:** N = 3
> **输出:** 648

**方法:**如果 **N > 10** 即至少有一个数字将重复，因此对于这种情况，答案将是 **0** 否则对于 **N = 1，2，3，…，9** 的值，一个系列将形成为 **9，81，648，4536，27216，136080，544320，…** 其【T10/(10–N)！。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the factorial of n
int factorial(int n)
{
    if (n == 0)
        return 1;
    return n * factorial(n - 1);
}

// Function to return the count
// of n-digit numbers with
// all distinct digits
int countNum(int n)
{
    if (n > 10)
        return 0;
    return (9 * factorial(9)
            / factorial(10 - n));
}

// Driver code
int main()
{
    int n = 3;

    cout << countNum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the factorial of n
    static int factorial(int n)
    {
        if (n == 0)
            return 1;
        return n * factorial(n - 1);
    }

    // Function to return the count
    // of n-digit numbers with
    // all distinct digits
    static int countNum(int n)
    {
        if (n > 10)
            return 0;
        return (9 * factorial(9) /
                    factorial(10 - n));
    }

    // Driver code
    public static void main(String []args)
    {
        int n = 3;
        System.out.println(countNum(n));
    }
}

// This code is contributed by Srathore
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the factorial of n
def factorial(n) :

    if (n == 0) :
        return 1;
    return n * factorial(n - 1);

# Function to return the count
# of n-digit numbers with
# all distinct digits
def countNum(n) :
    if (n > 10) :
        return 0;

    return (9 * factorial(9) //
                factorial(10 - n));

# Driver code
if __name__ == "__main__" :

    n = 3;

    print(countNum(n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the factorial of n
    static int factorial(int n)
    {
        if (n == 0)
            return 1;
        return n * factorial(n - 1);
    }

    // Function to return the count
    // of n-digit numbers with
    // all distinct digits
    static int countNum(int n)
    {
        if (n > 10)
            return 0;
        return (9 * factorial(9) /
                    factorial(10 - n));
    }

    // Driver code
    public static void Main(String []args)
    {
        int n = 3;
        Console.WriteLine(countNum(n));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the factorial of n
function factorial(n)
{
    if (n == 0)
        return 1;
    return n * factorial(n - 1);
}

// Function to return the count
// of n-digit numbers with
// all distinct digits
function countNum(n)
{
    if (n > 10)
        return 0;
    return (9 * factorial(9)
            / factorial(10 - n));
}

// Driver code
var n = 3;
document.write(countNum(n));

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
648
```

**时间复杂度:** O(n)