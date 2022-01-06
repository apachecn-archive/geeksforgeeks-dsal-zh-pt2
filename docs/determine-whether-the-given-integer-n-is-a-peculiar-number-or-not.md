# 判断给定的整数 N 是否为特殊数

> 原文:[https://www . geesforgeks . org/declare-给定整数 n 是否是一个特殊的数字/](https://www.geeksforgeeks.org/determine-whether-the-given-integer-n-is-a-peculiar-number-or-not/)

给定一个整数 N，我们的任务是确定整数 N 是否为**特殊数。**如果是，则打印“是”，否则输出“否”。
特殊数字是数字位数总和的三倍。
**示例:**

> **输入:** N = 27
> **输出:**是
> **说明:**
> 27 的数字和是 9，3 * 9 = 27 等于 N，因此输出为是。
> **输入:** N = 36
> **输出:**否
> **说明:**
> 36 的数字和为 9，3 * 9 = 27，不等于 N，因此输出为编号

**方法:**
要解决上面提到的问题，我们首先要**求一个数字 N 的位数之和**，然后检查这个数字的位数之和乘以 3 是否真的是数字 N 本身。如果是，则打印是，否则输出否
以下是上述方法的实现:

## C++

```
// C++ implementation to check if the
// number is peculiar

#include <bits/stdc++.h>
using namespace std;

// Function to find sum of digits
// of a number
int sumDig(int n)
{
    int s = 0;

    while (n != 0) {
        s = s + (n % 10);

        n = n / 10;
    }

    return s;
}

// Function to check if the
// number is peculiar
bool Pec(int n)
{
    // Store a duplicate of n
    int dup = n;

    int dig = sumDig(n);

    if (dig * 3 == dup)
        return true;

    else
        return false;
}

// Driver code
int main()
{
    int n = 36;

    if (Pec(n) == true)
        cout << "Yes" << endl;

    else
        cout << "No" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check if the
// number is peculiar
import java.io.*;

class GFG{

// Function to find sum of digits
// of a number
static int sumDig(int n)
{
    int s = 0;

    while (n != 0)
    {
        s = s + (n % 10);
        n = n / 10;
    }
    return s;
}

// Function to check if number is peculiar
static boolean Pec(int n)
{

    // Store a duplicate of n
    int dup = n;
    int dig = sumDig(n);

    if (dig * 3 == dup)
        return true;
    else
        return false;
}

// Driver code
public static void main (String[] args)
{
    int n = 36;

    if (Pec(n) == true)
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by shubhamsingh10
```

## 蟒蛇 3

```
# Python3 implementation to check if the
# number is peculiar

# Function to get sum of digits
# of a number
def sumDig(n):

    s = 0
    while (n != 0):
        s = s + int(n % 10)
        n = int(n / 10)

    return s

# Function to check if the 
# number is peculiar    
def Pec(n):

    dup = n
    dig = sumDig(n)

    if(dig * 3 == dup):
        return "Yes"
    else :
        return "No"

# Driver code
n = 36

if Pec(n) == True:
    print("Yes")
else:
    print("No")

# This code is contributed by grand_master
```

## C#

```
// C# implementation to check if the
// number is peculiar
using System;

class GFG{

// Function to find sum of digits
// of a number
static int sumDig(int n)
{
    int s = 0;

    while (n != 0)
    {
        s = s + (n % 10);
        n = n / 10;
    }
    return s;
}

// Function to check if the number is peculiar
static bool Pec(int n)
{

    // Store a duplicate of n
    int dup = n;
    int dig = sumDig(n);

    if (dig * 3 == dup)
        return true;
    else
        return false;
}

// Driver code
public static void Main()
{
    int n = 36;

    if (Pec(n) == true)
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Akanksha_Rai
```

## java 描述语言

```
<script>

// Javascript implementation to check if the
// number is peculiar

// Function to find sum of digits
// of a number
function sumDig(n)
{
    var s = 0;

    while (n != 0) {
        s = s + (n % 10);

        n = parseInt(n / 10);
    }

    return s;
}

// Function to check if the
// number is peculiar
function Pec(n)
{
    // Store a duplicate of n
    var dup = n;

    var dig = sumDig(n);

    if (dig * 3 == dup)
        return true;

    else
        return false;
}

// Driver code
var n = 36;
if (Pec(n) == true)
    document.write( "Yes");
else
    document.write( "No" );

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
No
```