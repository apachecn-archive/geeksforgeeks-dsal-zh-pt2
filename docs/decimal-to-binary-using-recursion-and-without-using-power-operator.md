# 使用递归将十进制转换为二进制，不使用幂运算符

> 原文:[https://www . geesforgeks . org/十进制到二进制使用递归而不使用幂运算符/](https://www.geeksforgeeks.org/decimal-to-binary-using-recursion-and-without-using-power-operator/)

给定一个整数 **N** ，任务是转换并打印二进制等式；进入**号**。
**例:**

> **输入:** N = 13
> **输出:** 1101
> **输入:** N = 15
> **输出:** 1111

**逼近**编写一个递归函数，该函数接受一个参数 **N** 并用值 **N / 2** 作为新参数递归调用自身，并在调用后打印 **N % 2** 。基本条件是当 **N = 0** 时，只需打印 **0** 即可，此时退出功能。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Recursive function to convert n
// to its binary equivalent
void decimalToBinary(int n)
{
    // Base case
    if (n == 0) {
        cout << "0";
        return;
    }

    // Recursive call
    decimalToBinary(n / 2);
    cout << n % 2;
}

// Driver code
int main()
{
    int n = 13;

    decimalToBinary(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Recursive function to convert n
// to its binary equivalent
static void decimalToBinary(int n)
{
    // Base case
    if (n == 0)
    {
        System.out.print("0");
        return;
    }

    // Recursive call
    decimalToBinary(n / 2);
    System.out.print( n % 2);
}

// Driver code
public static void main (String[] args)
{
    int n = 13;

    decimalToBinary(n);
}
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Recursive function to convert n
# to its binary equivalent
def decimalToBinary(n) :

    # Base case
    if (n == 0) :
        print("0",end="");
        return;

    # Recursive call
    decimalToBinary(n // 2);
    print(n % 2,end="");

# Driver code
if __name__ == "__main__" :

    n = 13;
    decimalToBinary(n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Recursive function to convert n
    // to its binary equivalent
    static void decimalToBinary(int n)
    {

        // Base case
        if (n == 0)
        {
            Console.Write("0");
            return;
        }

        // Recursive call
        decimalToBinary(n / 2);
        Console.Write(n % 2);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 13;

        decimalToBinary(n);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    // Recursive function to convert n
    // to its binary equivalent
    function decimalToBinary(n) {
        // Base case
        if (n == 0) {
            document.write("0");
            return;
        }

        // Recursive call
        decimalToBinary(parseInt(n / 2));
        document.write(n % 2);
    }

    // Driver code

        var n = 13;

        decimalToBinary(n);

// This code contributed by gauravrajput1
</script>
```

**Output:** 

```
01101
```

**时间复杂度:**O(logN)
T3】辅助空间: O(logN)