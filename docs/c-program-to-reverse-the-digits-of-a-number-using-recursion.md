# 使用递归反转数字的程序

> 原文:[https://www . geesforgeks . org/c-program-to-reverse-the-digits-of-a-number-in-recursion/](https://www.geeksforgeeks.org/c-program-to-reverse-the-digits-of-a-number-using-recursion/)

给定一个整数 **N** ，任务是[使用](https://www.geeksforgeeks.org/write-a-program-to-reverse-digits-of-a-number/)[递归](https://www.geeksforgeeks.org/recursion/)反转给定整数的位数。

**示例:**

> **输入:** N = 123
> **输出:** 321
> **说明:**
> 给定数字的倒数为 321。
> 
> **输入:** N = 12532
> **输出:** 23521
> **说明:**
> 给定数字的倒数为 23521。

**方法:**按照以下步骤解决问题:

*   递归迭代 **N** 的每个数字。
*   如果通过的 **N** 当前值小于 **10** ，则返回 **N** 。

> if(num < 10)
> 返回 N；

*   否则，每次递归调用后(*除基本情况*)，返回递归函数进行下一次迭代:

> 反向返回(N/10) + ((N%10)*(功率(10)，(地板(log10(abs(N))))))
> 
> 其中， **floor(log10(abs(x)))** 给出了 x
> **((x%10)*(pow(10)，(floor(log10(ABS(x)))))))))**将提取的单位位置数字 **(x%10)** 放置到所需位置

下面是上述方法的实现:

## C

```
// C program for the above approach

#include <math.h>
#include <stdio.h>
#include <stdlib.h>

// Function to reverse the digits of
// the given integer
int reverse(int N)
{
    return ((N <= 9))
               ? N
               : reverse(N / 10)
                     + ((N % 10)
                        * (pow(10,
                               (floor(log10(
                                   abs(N)))))));
}

// Utility function to reverse the
// digits of the given integer
void reverseUtil(int N)
{
    // Stores reversed integer
    int result = reverse(N);

    // Print reversed integer
    printf("%d", result);
}

// Driver Code
int main()
{
    // Given integer N
    int N = 123;

    // Function Call
    reverseUtil(N);

    return 0;
}
```

**Output:**

```
321

```

***时间复杂度:**O(log<sub>10</sub>N)*
***辅助空间:** O(1)*