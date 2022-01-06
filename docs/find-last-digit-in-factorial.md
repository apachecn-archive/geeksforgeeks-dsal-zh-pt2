# 寻找阶乘

中的最后一位数字

> 原文:[https://www.geeksforgeeks.org/find-last-digit-in-factorial/](https://www.geeksforgeeks.org/find-last-digit-in-factorial/)

给定一个数字 n，我们需要找到[阶乘](https://www.geeksforgeeks.org/program-for-factorial-of-a-number/) n 中的最后一位数字。

> 输入:n = 4
> 输出:4
> 4！= 4 * 3 * 2 * 1.= 24.24 的最后一位是 4。
> 
> 输入:n = 5
> 输出:5
> 5！= 5*4 * 3 * 2 * 1.= 120.120 的最后一位是 0。

一个**天真的解决方案**是先计算事实= n！，然后通过执行 fact % 10 返回结果的最后一位数字。这种解决方案效率很低，甚至对于稍大的 n 值也会导致整数溢出。

一个**有效解**是基于 5 之后的所有阶乘都有 0 作为最后一位数字的观察。

1!= 1
2！= 2
3！= 6
4！= 24
5！= 120
6！= 720
……..

## C++

```
// C++ program to find last digit in
// factorial n.
#include <iostream>
using namespace std;

int lastDigitFactorial(unsigned int n)
{
   // Explicitly handle all numbers
   // less than or equal to 4
   if (n == 0) return 1;
   else if (n <= 2) return n;
   else if (n == 3) return 6;
   else if (n == 4) return 4;

   // For all numbers greater than 4
   // the last digit is 0
   else return 0;
}

int main() {

    cout<<lastDigitFactorial(6);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find last 
// digit in factorial n.
import java.io.*;
import java.util.*;

class GFG {

static int lastDigitFactorial(int n)
{

    // Explicitly handle all numbers
    // less than or equal to 4
    if (n == 0) return 1;
    else if (n <= 2) return n;
    else if (n == 3) return 6;
    else if (n == 4) return 4;

    // For all numbers greater than
    // 4 the last digit is 0
    else return 0;
}

// Driver code
public static void main(String[] args)
{
    System.out.println(lastDigitFactorial(6));
}
}

// This code is contributed by coder001
```

## 蟒蛇 3

```
# Python3 program to find last digit in
# factorial n.

def lastDigitFactorial(n):

    # Explicitly handle all numbers
    # less than or equal to 4
    if (n == 0): return 1
    elif (n <= 2): return n
    elif (n == 3): return 6
    elif (n == 4): return 4

    # For all numbers greater than 4
    # the last digit is 0
    else: return 0

print(lastDigitFactorial(6))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to find last
// digit in factorial n.
using System;
class GFG{

static int lastDigitFactorial(int n)
{

    // Explicitly handle all numbers
    // less than or equal to 4
    if (n == 0) return 1;
    else if (n <= 2) return n;
    else if (n == 3) return 6;
    else if (n == 4) return 4;

    // For all numbers greater than
    // 4 the last digit is 0
    else return 0;
}

// Driver code
public static void Main(string[] args)
{
    Console.Write(lastDigitFactorial(6));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// JavaScript program to find last digit in
// factorial n.

function lastDigitFactorial(n)
{
    // Explicitly handle all numbers
    // less than or equal to 4
    if (n == 0) return 1;
    else if (n <= 2) return n;
    else if (n == 3) return 6;
    else if (n == 4) return 4;

    // For all numbers greater than 4
    // the last digit is 0
    else return 0;
}

    // Driver code 
    document.write(lastDigitFactorial(6));

// This code is contributed by Surbhi Tyagi

</script>
```

**Output:** 

```
0
```

时间复杂度:O(1)
辅助空间:O(1)

现在试试下面的问题

1) [阶乘](https://www.geeksforgeeks.org/last-non-zero-digit-factorial/)
中的最后一个非零数字 2) [阶乘](https://www.geeksforgeeks.org/count-trailing-zeroes-factorial-number/)中的计零
3) [阶乘](https://www.geeksforgeeks.org/first-digit-factorial-number/)中的第一个数字