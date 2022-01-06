# 使用递归计算设定位数

> 原文:[https://www . geesforgeks . org/count-set-bits-of-number-use-recursion/](https://www.geeksforgeeks.org/count-set-bits-of-number-using-recursion/)

给定一个数字 n，任务是使用递归找到其二进制表示中的集合位数。

**示例:**

> **输入:** 21
> **输出:** 3
> 21 用二进制表示表示为 10101
> 
> **输入:** 16
> **输出:** 1
> 16 用二进制表示表示为 10000

**进场:**

1.  首先，检查号码的 LSB。
2.  如果 LSB 是 1，那么我们把 1 加到我们的答案上，然后把这个数除以 2。
3.  如果 LSB 是 0，我们将 0 加到答案中，然后将数字除以 2。
4.  然后我们递归地遵循步骤(1)，直到数字大于 0。

下面是上述方法的实现:

## C++

```
// CPP program to find number
// of set bist in a number
#include <bits/stdc++.h>
using namespace std;

// Recursive function to find
// number of set bist in a number
int CountSetBits(int n)
{
    // Base condition
    if (n == 0)
        return 0;

    // If Least significant bit is set
    if((n & 1) == 1)
        return 1 + CountSetBits(n >> 1);

    // If Least significant bit is not set
    else
        return CountSetBits(n >> 1);
}

// Driver code
int main()
{
    int n = 21;

    // Function call
    cout << CountSetBits(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number
// of set bist in a number
class GFG
{
    // Recursive function to find
    // number of set bist in a number
    static int CountSetBits(int n)
    {
        // Base condition
        if (n == 0)
            return 0;

        // If Least significant bit is set
        if((n & 1) == 1)
            return 1 + CountSetBits(n >> 1);

        // If Least significant bit is not set
        else
            return CountSetBits(n >> 1);
    }

    // Driver code
    public static void main (String [] args)
    {
        int n = 21;

        // Function call
        System.out.println(CountSetBits(n));
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 program to find number
# of set bist in a number

# Recursive function to find
# number of set bist in a number
def CountSetBits(n):

    # Base condition
    if (n == 0):
        return 0;

    # If Least significant bit is set
    if((n & 1) == 1):
        return 1 + CountSetBits(n >> 1);

    # If Least significant bit is not set
    else:
        return CountSetBits(n >> 1);

# Driver code
if __name__ == '__main__':
    n = 21;

    # Function call
    print(CountSetBits(n));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to find number
// of set bist in a number
using System;

class GFG
{
    // Recursive function to find
    // number of set bist in a number
    static int CountSetBits(int n)
    {
        // Base condition
        if (n == 0)
            return 0;

        // If Least significant bit is set
        if((n & 1) == 1)
            return 1 + CountSetBits(n >> 1);

        // If Least significant bit is not set
        else
            return CountSetBits(n >> 1);
    }

    // Driver code
    public static void Main ()
    {
        int n = 21;

        // Function call
        Console.WriteLine(CountSetBits(n));
    }
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>

// Javascript program to find number
// of set bist in a number

// Recursive function to find
// number of set bist in a number
function CountSetBits(n)
{

    // Base condition
    if (n == 0)
        return 0;

    // If Least significant bit is set
    if ((n & 1) == 1)
        return 1 + CountSetBits(n >> 1);

    // If Least significant bit is not set
    else
        return CountSetBits(n >> 1);
}

// Driver code
var n = 21;

// Function call
document.write(CountSetBits(n));

// This code is contributed by Amit Katiyar

</script>
```

**Output:** 

```
3
```

时间复杂度:0(对数 n)

辅助空间:0(对数)