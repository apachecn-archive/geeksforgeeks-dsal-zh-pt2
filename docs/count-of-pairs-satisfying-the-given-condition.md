# 满足给定条件的配对数

> 原文:[https://www . geesforgeks . org/满足给定条件的配对计数/](https://www.geeksforgeeks.org/count-of-pairs-satisfying-the-given-condition/)

给定两个整数 **A** 和 **B** ，任务是计算对的数量 **(a，b)** ，使得 **1 ≤ a ≤ A，1 ≤ b ≤ B** 并且等式 **(a * b) + a + b = concat(a，b)** 为真，其中 **conc(a，b)** 是 A 和 B 的串联(例如，conc(12，23)= 11)**注意**中 **a** 和 **b** 不应包含任何前导零。

**示例:**

> **输入:** A = 1，B = 12
> **输出:** 1
> 只有一对(1，9)满足公式((1 * 9) + 1 + 9 = 19)
> 
> **输入:** A = 2，B = 8
> **输出:** 0
> 不存在满足方程的任何一对。

**逼近:**可以观察到，只有当整数 **≤ b** 的位数只包含 **9** 时，上述 **(a * b + a + b = conc(a，b))** 才会满足。简单计算只包含 **9** 的位数(≤ b)，乘以整数 **a** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number of
// pairs satisfying the equation
int countPair(int a, int b)
{
    // Converting integer b to string
    // by using to_string function
    string s = to_string(b);

    // Loop to check if all the digits
    // of b are 9 or not
    int i;
    for (i = 0; i < s.length(); i++) {

        // If '9' doesn't appear
        // then break the loop
        if (s[i] != '9')
            break;
    }

    int result;

    // If all the digits of b contain 9
    // then multiply a with string length
    // else multiply a with string length - 1
    if (i == s.length())
        result = a * s.length();
    else
        result = a * (s.length() - 1);

    // Return the number of pairs
    return result;
}

// Driver code
int main()
{
    int a = 5, b = 101;

    cout << countPair(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the number of
// pairs satisfying the equation
static int countPair(int a, int b)
{
    // Converting integer b to String
    // by using to_String function
    String s = String.valueOf(b);

    // Loop to check if all the digits
    // of b are 9 or not
    int i;
    for (i = 0; i < s.length(); i++)
    {

        // If '9' doesn't appear
        // then break the loop
        if (s.charAt(i) != '9')
            break;
    }

    int result;

    // If all the digits of b contain 9
    // then multiply a with String length
    // else multiply a with String length - 1
    if (i == s.length())
        result = a * s.length();
    else
        result = a * (s.length() - 1);

    // Return the number of pairs
    return result;
}

// Driver code
public static void main(String[] args)
{
    int a = 5, b = 101;

    System.out.print(countPair(a, b));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the number of
# pairs satisfying the equation
def countPair(a, b):

    # Converting integer b to string
    # by using to_function
    s = str(b)

    # Loop to check if all the digits
    # of b are 9 or not
    i = 0
    while i < (len(s)):

        # If '9' doesn't appear
        # then break the loop
        if (s[i] != '9'):
            break
        i += 1

    result = 0

    # If all the digits of b contain 9
    # then multiply a with length
    # else multiply a with length - 1
    if (i == len(s)):
        result = a * len(s)
    else:
        result = a * (len(s) - 1)

    # Return the number of pairs
    return result

# Driver code
a = 5
b = 101

print(countPair(a, b))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the number of
// pairs satisfying the equation
static int countPair(int a, int b)
{
    // Converting integer b to String
    // by using to_String function
    String s = String.Join("", b);

    // Loop to check if all the digits
    // of b are 9 or not
    int i;
    for (i = 0; i < s.Length; i++)
    {

        // If '9' doesn't appear
        // then break the loop
        if (s[i] != '9')
            break;
    }

    int result;

    // If all the digits of b contain 9
    // then multiply a with String length
    // else multiply a with String length - 1
    if (i == s.Length)
        result = a * s.Length;
    else
        result = a * (s.Length - 1);

    // Return the number of pairs
    return result;
}

// Driver code
public static void Main(String[] args)
{
    int a = 5, b = 101;

    Console.Write(countPair(a, b));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the number of
// pairs satisfying the equation
function countPair(a, b)
{

    // Converting integer b to string
    // by using to_string function
    var s = (b.toString());

    // Loop to check if all the digits
    // of b are 9 or not
    var i;
    for(i = 0; i < s.length; i++)
    {

        // If '9' doesn't appear
        // then break the loop
        if (s[i] != '9')
            break;
    }

    var result;

    // If all the digits of b contain 9
    // then multiply a with string length
    // else multiply a with string length - 1
    if (i == s.length)
        result = a * s.length;
    else
        result = a * (s.length - 1);

    // Return the number of pairs
    return result;
}

// Driver code
var a = 5, b = 101;
document.write(countPair(a, b));

// This code is contributed by rutvik_56

</script>
```

**Output:** 

```
10
```