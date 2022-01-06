# 计算数字位数的程序

> 原文:[https://www . geesforgeks . org/c-程序对数字进行计数/](https://www.geeksforgeeks.org/c-program-to-count-the-digits-of-a-number/)

给定一个数字 **N** ，编写一个 C 程序，求出数字 **N** 的位数。

**示例:**

> **输入:** N = 12345
> **输出:** 5
> **说明:**
> 12345 中的位数= 5。
> 
> **输入:** N = 23451452
> **输出:** 8
> **说明:**
> 23451452 中的位数= 8。

**方法:**一个数字的位数可以通过几个步骤高效地找到:

1.  用 10 除数字的最后一位。
2.  将数字的**计数**增加 **1** 。
3.  继续重复步骤 1 和 2，直到 **N** 的值变为 **0** 。在这种情况下，在要计数的数字中将不再有剩余的数字

## C

```
// C Program to find count of
// digits in a number

#include <stdio.h>

// Find the count of digits
int findCount(int n)
{
    int count = 0;

    // Remove last digit from number
    // till number is 0
    while (n != 0) {

  //Increment count
        count++;
        n /= 10;
    }

    // return the count of digit
    return count;
}

// Driver program
int main()
{
    int n = 98562;
    printf("Count of digits in %d = %d\n",
 n, findCount(n));
    return 0;
}
```

**Output:**

```
Count of digits in 98562 = 5

```

***时间复杂度:** O(D)* ，其中 D 为数字 n 中的位数
***辅助空间复杂度:** O(1)*