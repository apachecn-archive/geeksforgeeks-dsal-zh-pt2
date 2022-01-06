# 两个数字相加可能达到的最大 GCD 值

> 原文:[https://www . geeksforgeeks . org/两个数字的最大 gcd-通过向它们添加相同的值来实现/](https://www.geeksforgeeks.org/maximum-gcd-of-two-numbers-possible-by-adding-same-value-to-them/)

给定两个数字 **A** 和 **B** ，任务是通过将数字 **X** 加到 **A** 和 **B** 上，找到最大 [**最大公约数(GCD)**](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 。

***例***

> **输入:** A = 1，B = 5
> **输出:** 4
> **说明:**加 X = 15，得到的数字是 A = 16，B = 20。因此，A、B 的 GCD 为 4。
> 
> **输入:** A = 2，B = 23
> T3】输出: 21

**方法:**利用[欧氏 GCD 算法](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/)的性质，可以非常优化的方式解决这个问题。按照以下步骤解决问题:

*   **如果 a > b: GCD(a，b)= GCD(a–b，b)** 。因此， **GCD(a，b)= GCD(a–b，b** )。
*   关于将 **x** 加到 **A，B，gcd(a + x，b + x)= gcd(A–B，B+x)。**可见**(a–b)**保持不变。
*   可以有把握地说，这些数字的 GCD 永远不会超过**(a–b)**。因为 **(b + x)** 可以通过增加 **x** 的可能值而成为**(a–b)**的倍数。
*   因此，可以得出结论，GCD 保持**(a–b)。**

下面是上述方法的实现。

## C++

```
// C++ implementation of above approach.
#include <iostream>
using namespace std;

// Function to calculate maximum
// gcd of two numbers possible by
// adding same value to both a and b
void maxGcd(int a, int b)
{
    cout << abs(a - b);
}

// Driver Code
int main()
{
    // Given Input
    int a = 2231;
    int b = 343;

    maxGcd(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach.
import java.io.*;

class GFG
{

  // Function to calculate maximum
  // gcd of two numbers possible by
  // adding same value to both a and b
  static void maxGcd(int a, int b)
  {
    System.out.println(Math.abs(a - b));
  }

  // Driver Code
  public static void main (String[] args)
  {

    // Given Input
    int a = 2231;
    int b = 343;

    maxGcd(a, b);

  }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate maximum
# gcd of two numbers possible by
# adding same value to both a and b
def maxGcd(a, b):

    print(abs(a - b))

# Driver code

# Given Input
a = 2231
b = 343

maxGcd(a, b)

# This code is contributed by Parth Manchanda
```

## C#

```
// C# program for the above approach
using System;

class GFG{

 // Function to calculate maximum
  // gcd of two numbers possible by
  // adding same value to both a and b
  static void maxGcd(int a, int b)
  {
    Console.Write(Math.Abs(a - b));
  }

// Driver Code
static public void Main ()
{

     // Given Input
    int a = 2231;
    int b = 343;

    maxGcd(a, b);
}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>
       // JavaScript Program for the above approach

       // Function to calculate maximum
       // gcd of two numbers possible by
       // adding same value to both a and b
       function maxGcd(a, b) {
           document.write(Math.abs(a - b));
       }

       // Driver Code

       // Given Input
       let a = 2231;
       let b = 343;

       maxGcd(a, b);

   // This code is contributed by Potta Lokesh
   </script>
```

**Output:** 

```
1888
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)