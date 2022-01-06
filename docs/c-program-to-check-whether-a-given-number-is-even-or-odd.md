# C 程序检查给定的数字是偶数还是奇数

> 原文:[https://www . geesforgeks . org/c-program-to-check-给定的数字是偶数还是奇数/](https://www.geeksforgeeks.org/c-program-to-check-whether-a-given-number-is-even-or-odd/)

给定一个整数 **N** ，任务是检查给定的数字 **N** 是偶数还是奇数。如果发现是偶数，则打印**“偶数”**。否则，打印**“奇数”**。

**示例:**

> **输入:**N = 2
> T3】输出:偶数
> 
> **输入:**N = 5
> T3】输出:奇数

**方法 1:** 最简单的方法是检查给定数 **N** 除以 **2** 得到的余数是 **0** 还是 **1** 。如果余数为 **0** ，则打印**“偶数”**。否则，打印**“奇数”**。

下面是上述方法的实现:

## C

```
// C program for the above approach
#include <stdio.h>

// Function to check if a
// number is even or odd
void checkEvenOdd(int N)
{
    // Find remainder
    int r = N % 2;

    // Condition for even
    if (r == 0) {
        printf("Even");
    }

    // Otherwise
    else {
        printf("Odd");
    }
}

// Driver Code
int main()
{
    // Given number N
    int N = 101;

    // Function Call
    checkEvenOdd(N);

    return 0;
}
```

**Output:**

```
Odd

```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)

**方法 2:** 另一种方法是使用[逐位运算符](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。其思想是检查给定数字 **N** 的最后一位是否为 **1** 。检查最后一位是否为 **1** 求 **(N & 1)** 的值。如果结果为 **1** ，则打印**“奇数”**。否则，打印**“偶数”**。

下图为 **N** = 5:

> N = 5。
> 5 的二进制表示为 00000101
> 1 的二进制表示为 00000001
> ———————————————————
> 按位“与”的值为 000000001
> 
> 既然结果是 1。所以 **N = 5** 这个数字是奇数。

下面是上述方法的实现:

## C

```
// C program for the above approach

#include <stdio.h>

// Function to check if a
// number is even or odd
void checkEvenOdd(int N)
{
    // If N & 1 is true
    if (N & 1) {
        printf("Odd");
    }

    // Otherwise
    else {
        printf("Even");
    }
}

// Driver Code
int main()
{
    // Given number N
    int N = 101;

    // Function Call
    checkEvenOdd(N);

    return 0;
}
```

**Output:**

```
Odd

```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)

**方法三:**思路是将一个整型变量 **var** 初始化为 **1** ，从 **1** 变为 **0** ，反之亦然，交替 **N** 次。如果在 **N** 次操作后 var 等于 **1** ，则打印“偶数”。否则，打印**“奇数”**。

下面是上述方法的实现:

## C

```
// C program for the above approach
#include <stdio.h>

// Function to check a number is
// even or odd
void checkEvenOdd(int N)
{
    // Initialise a variable var
    int var = 1;

    // Iterate till N
    for (int i = 1; i <= N; i++) {

        // Subtract var from 1
        var = 1 - var;
    }

    // Condition for even
    if (var == 1) {
        printf("Even");
    }

    // Otherwise
    else {
        printf("Odd");
    }
}

// Driver Code
int main()
{
    // Given number N
    int N = 101;

    // Function Call
    checkEvenOdd(N);

    return 0;
}
```

**Output:**

```
Odd

```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)