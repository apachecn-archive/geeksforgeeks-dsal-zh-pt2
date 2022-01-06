# 无前导零的 N 位二进制数的计数

> 原文:[https://www . geeksforgeeks . org/无前导零的 n 位二进制数计数/](https://www.geeksforgeeks.org/count-of-n-bit-binary-numbers-without-leading-zeros/)

给定一个整数 **N** ，任务是找到没有前导零的 N 位二进制数的计数。
**例:**

> **输入:** N = 2
> **输出:** 2
> 10 和 11 是唯一可能的二进制数。
> **输入:** N = 4
> **输出:** 8

**方法:**由于数字不能有前导零，所以最左边的位必须设置为 **1** 。现在对于其余的**N–1**位，有两种选择，它们可以设置为 **0** 或 **1** 。因此，可能数量的计数将是**2<sup>N–1</sup>**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of possible numbers
int count(int n)
{
    return pow(2, n - 1);
}

// Driver code
int main()
{
    int n = 4;

    cout << count(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the count
    // of possible numbers
    static int count(int n)
    {
        return (int)Math.pow(2, n - 1);
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 4;

        System.out.println(count(n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of possible numbers
def count(n):
    return pow(2, n - 1)

# Driver code
n = 4

print(count(n))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to return the count
    // of possible numbers
    static int count(int n)
    {
        return (int)Math.Pow(2, n - 1);
    }

    // Driver code
    public static void Main (String[] args)
    {
        int n = 4;

        Console.WriteLine(count(n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the count
// of possible numbers
function count(n)
{
    return Math.pow(2, n - 1);
}

// Driver code
var n = 4;
document.write(count(n));

</script>
```

**Output:** 

```
8
```