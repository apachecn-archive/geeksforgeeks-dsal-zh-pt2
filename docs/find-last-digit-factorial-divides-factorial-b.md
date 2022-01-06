# 求 A 的阶乘除以 B 的阶乘时的最后一位数字

> 原文:[https://www . geesforgeks . org/find-最后一位数字-阶乘-除法-阶乘-b/](https://www.geeksforgeeks.org/find-last-digit-factorial-divides-factorial-b/)

给我们两个数字 A 和 B，这样 B >= A。我们需要计算结果 F 的最后一个数字，这样 F = B！/A！其中 1 = A，B <= 10^18 (A and B are very large).
示例:

```
Input : A = 2, B = 4
Output : 2
Explanation : A! = 2 and B! = 24\. 
F = 24/2 = 12 --> last digit = 2

Input : 107 109
Output : 2
```

正如我们所知，阶乘函数以指数速率增长。即使是最大的数据类型
也不能容纳像 100 这样的数字的阶乘。要计算中等大数的阶乘，请参考[这个](https://www.geeksforgeeks.org/factorial-large-number/)。
这里给定的约束非常大。因此，计算两个阶乘，然后
对它们进行除法并计算最后一位数字实际上是一项不可能的任务。
因此，我们必须找到一种替代方法来解决我们的问题。众所周知，阶乘的最后一位总是属于集合{0，1，2，4，6}
方法如下:–
1)我们评估 B 和 A 之间的差异
2)如果(B–A)>= 5，那么答案总是 0
3)如果差异(B–A)<5，那么我们从(A+1)迭代到 B，相乘并存储它们。答案% 10 将是我们的答案。

## C++

```
// CPP program to find last digit of a number
// obtained by dividing factorial of a number
// with factorial of another number.
#include <iostream>
using namespace std;

// Function which computes the last digit
// of resultant of B!/A!
int computeLastDigit(long long int A, long long int B)
{

    int variable = 1;
    if (A == B) // If A = B, B! = A! and B!/A! = 1
        return 1;

    // If difference (B - A) >= 5, answer = 0
    else if ((B - A) >= 5)
        return 0;

    else {

        // If non of the conditions are true, we
        // iterate from  A+1 to B and multiply them.
        // We are only concerned for the last digit,
        // thus we take modulus of 10
        for (long long int i = A + 1; i <= B; i++)
            variable = (variable * (i % 10));

        return variable % 10;
    }
}

// driver function
int main()
{
    cout << computeLastDigit(2632, 2634);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find last digit of a number
// obtained by dividing factorial of a number
// with factorial of another number.
import java.io.*;

class GFG {

// Function which computes the last digit
// of resultant of B!/A!
static int computeLastDigit(long A, long B)
{

    int variable = 1;
    if (A == B) // If A = B, B! = A! and B!/A! = 1
        return 1;

    // If difference (B - A) >= 5, answer = 0
    else if ((B - A) >= 5)
        return 0;

    else {

        // If non of the conditions are true, we
        // iterate from A+1 to B and multiply them.
        // We are only concerned for the last digit,
        // thus we take modulus of 10
        for (long i = A + 1; i <= B; i++)
            variable = (int)(variable * (i % 10)) % 10;

        return variable % 10;
    }
}

// driver function
public static void main(String[] args)
{
    System.out.println(computeLastDigit(2632, 2634));
}
}

// This article is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python program to find
# last digit of a number
# obtained by dividing
# factorial of a number
# with factorial of another number.

# Function which computes
# the last digit
# of resultant of B!/A!
def computeLastDigit(A,B):

    variable = 1
    if (A == B): # If A = B, B! = A! and B!/A! = 1
        return 1

    # If difference (B - A) >= 5, answer = 0
    elif ((B - A) >= 5):
        return 0

    else:

        # If non of the conditions
        # are true, we
        # iterate from  A+1 to B
        # and multiply them.
        # We are only concerned
        # for the last digit,
        # thus we take modulus of 10
        for i in range(A + 1, B + 1):
            variable = (variable * (i % 10)) % 10

        return variable % 10

# driver function

print(computeLastDigit(2632, 2634))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to find last digit of
// a number obtained by dividing
// factorial of a number with
// factorial of another number.
using System;

class GFG {

// Function which computes the last
// digit of resultant of B!/A!
static int computeLastDigit(long A, long B)
{

    int variable = 1;
     // If A = B, B! = A!
     // and B!/A! = 1
     if (A == B)
        return 1;

    // If difference (B - A) >= 5,
    // answer = 0
    else if ((B - A) >= 5)
        return 0;

    else {

        // If non of the conditions are true, we
        // iterate from A+1 to B and multiply them.
        // We are only concerned for the last digit,
        // thus we take modulus of 10
        for (long i = A + 1; i <= B; i++)
            variable = (int)(variable *
                       (i % 10)) % 10;

        return variable % 10;
    }
}

// Driver Code
public static void Main()
{
    Console.WriteLine(computeLastDigit(2632, 2634));
}
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find last digit of a number
// obtained by dividing factorial of a number
// with factorial of another number.

// Function which computes the last
// digit of resultant of B!/A!
function computeLastDigit($A, $B)
{

    $variable = 1;

    // If A = B, B! = A!
    // and B!/A! = 1
    if ($A == $B)
        return 1;

    // If difference (B - A) >= 5,
    // answer = 0
    else if (($B - $A) >= 5)
        return 0;

    else
    {

        // If non of the conditions
        // are true, we iterate from
        // A+1 to B and multiply them.
        // We are only concerned for
        // the last digit, thus we
        // take modulus of 10
        for ($i = $A + 1; $i <= $B; $i++)
            $variable = ($variable * ($i % 10)) % 10;

        return $variable % 10;
    }
}

    // Driver Code
    echo computeLastDigit(2632, 2634);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// Javascript program to find last digit of a number
// obtained by dividing factorial of a number
// with factorial of another number.

// Function which computes the last digit
// of resultant of B!/A!
function computeLastDigit(A, B)
{

    let variable = 1;
    if (A == B) // If A = B, B! = A! and B!/A! = 1
        return 1;

    // If difference (B - A) >= 5, answer = 0
    else if ((B - A) >= 5)
        return 0;

    else {

        // If none of the conditions are true, we
        // iterate from A+1 to B and multiply them.
        // We are only concerned for the last digit,
        // thus we take modulus of 10
        for (let i = A + 1; i <= B; i++)
            variable = (variable * (i % 10)) % 10;

        return variable % 10;
    }
}

// driver function

    document.write(computeLastDigit(2632, 2634));

// This code is contributed by Surbhi Tyagi

</script>
```

输出:

```
2
```

时间复杂度:O(1)。

辅助空间:0(1)。
本文由**希瓦尼·米塔尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。