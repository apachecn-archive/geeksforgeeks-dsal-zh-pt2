# 设置了第 0 位和第 n 位的数字的计数

> 原文:[https://www . geesforgeks . org/count-of-numbers-0th-bits-set/](https://www.geeksforgeeks.org/count-of-numbers-whose-0th-and-nth-bits-are-set/)

给定一个正整数 **N** ，任务是计算可以用 **N** 位表示的数字，并且设置其 **0 <sup>第</sup>T7】和 **N <sup>第</sup>T11】位。****

**示例:**

> **输入:** N = 2
> **输出:** 1
> 所有可能的 2 位整数为 00、01、10 和 11。
> 其中只有 11 位设置了 0 <sup>第</sup>和 N <sup>第</sup>位。
> **输入:** N = 4
> **输出:** 4

**方法:**在给定的 **N** 位中，只需要设置两个位，即 **0 <sup>第</sup>T7】位和 **N <sup>第</sup>T11】位。因此，将这 2 位设置为 1，剩下的**N–2**位可以是 **0** 或 **1** ，还有**2<sup>N–2</sup>**的方式。
以下是上述方法的实施:**** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of n-bit
// numbers whose 0th and nth bits are set
int countNum(int n)
{
    if (n == 1)
        return 1;
    int count = pow(2, n - 2);
    return count;
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
import java.io.*;

class GFG
{
    // Function to return the count of n-bit
    // numbers whose 0th and nth bits are set
    static int countNum(int n)
    {
        if (n == 1)
            return 1;

        int count = (int) Math.pow(2, n - 2);
        return count;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 3;
        System.out.println(countNum(n));
    }
}

// This code is contributed by ajit
```

## 计算机编程语言

```
# Python3 implementation of the approach

# Function to return the count of n-bit
# numbers whose 0th and nth bits are set
def countNum(n):
    if (n == 1):
        return 1
    count = pow(2, n - 2)
    return count

# Driver code

n = 3
print(countNum(n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the count of n-bit
    // numbers whose 0th and nth bits are set
    static int countNum(int n)
    {
        if (n == 1)
            return 1;

        int count = (int) Math.Pow(2, n - 2);
        return count;
    }

    // Driver code
    static public void Main ()
    {
        int n = 3;
        Console.WriteLine(countNum(n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the count of n-bit
// numbers whose 0th and nth bits are set
function countNum(n)
{
    if (n == 1)
        return 1;
    let count = Math.pow(2, n - 2);
    return count;
}

// Driver code
    let n = 3;
    document.write(countNum(n));

</script>
```

**Output:** 

```
2
```