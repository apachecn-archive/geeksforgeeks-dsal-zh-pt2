# 最小数字，数字只有 4 和 7，给定总和

> 原文:[https://www . geesforgeks . org/最小数字-数字-4-7-给定-总和/](https://www.geeksforgeeks.org/minimum-number-digits-4-7-given-sum/)

幸运数字是正整数，其十进制表示只包含幸运数字 4 和 7。
哪个最小幸运数字的位数之和等于 n。

示例:

```
Input : sum = 11
Output : 47
Sum of digits in 47 is 11 and 47
is the smallest number with given sum.

Input :  sum = 10
Output : -1    
```

该方法基于以下事实:

1.  因为数字只有 4 和 7，所以给定的数字和可以写成 **a*4 + b*7 =和**，其中 a 和 b 分别是表示 4 和 7 个数的正整数(大于或等于 0)。
2.  因为我们需要找到最小数，结果总是先有所有 4，再有所有 7，即 44…477…7。

我们基本上需要找到‘a’和‘b’的值。我们使用以下事实找到这些值:

1.  如果和是 4 的倍数，那么结果就都是 4。
2.  如果和是 7 的倍数，那么结果就是 7。
3.  如果和不是 4 或 7 的倍数，那么我们可以减去其中的一个，直到和变成其他的倍数。

## C++

```
// C++ program to find smallest number
// with given sum of digits.
#include <bits/stdc++.h>
using namespace std;

// Prints minimum number with given digit
// sum and only allowed digits as 4 and 7.
void findMin(int sum)
{
    int a = 0, b = 0;
    while (sum > 0)
    {
        // Cases where all remaining digits
        // are 4 or 7 (Remaining sum of digits
        // should be multiple of 4 or 7)
        if (sum % 7 == 0)
        {
            b++;
            sum -= 7;
        }
        else if (sum % 4 == 0)
        {
            a++;
            sum -= 4;
        }

        // If both 4s and 7s are there
        // in digit sum, we subtract a 4.
        else
        {
            a++;
            sum -= 4;
        }
    }

    if (sum < 0)
    {
        printf("-1n");
        return;
    }

    for (int i=0; i<a; i++)
        printf("4");

    for (int i=0; i<b; i++)
        printf("7");

    printf("n");
}

// Driver code
int main()
{
    findMin(15);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find smallest number
// with given sum of digits.
import java.io.*;

class GFG {

    // Prints minimum number with given digit
    // sum and only allowed digits as 4 and 7.
    static void findMin(int sum)
    {
        int a = 0, b = 0;
        while (sum > 0)
        {
            // Cases where all remaining digits
            // are 4 or 7 (Remaining sum of digits
            // should be multiple of 4 or 7)
            if (sum % 7 == 0)
            {
                b++;
                sum -= 7;
            }
            else if (sum % 4 == 0)
            {
                a++;
                sum -= 4;
            }

            // If both 4s and 7s are there
            // in digit sum, we subtract a 4.
            else
            {
                a++;
                sum -= 4;
            }
        }

        if (sum < 0)
        {
            System.out.print("-1n");
            return;
        }

        for (int i = 0; i < a; i++)
            System.out.print("4");

        for (int i = 0; i < b; i++)
            System.out.print("7");

        System.out.println();
    }

    // Driver code
    public static void main(String args[])
                            throws IOException
    {
        findMin(15);
    }
}

/* This code is contributed by Nikita tiwari.*/
```

## 计算机编程语言

```
# Python program to find smallest number
# with given sum of digits.

# Prints minimum number with given digit
# sum and only allowed digits as 4 and 7.
def findMin(s):
    a, b = 0, 0
    while (s > 0):

        # Cases where all remaining digits
        # are 4 or 7 (Remaining sum of digits
        # should be multiple of 4 or 7)
        if (s % 7 == 0):
            b += 1
            s -= 7
        elif (s % 4 == 0):
            a += 1
            s -= 4

        # If both 4s and 7s are there
        # in digit sum, we subtract a 4.
        else:
            a += 1
            s -= 4

    string = ""
    if (s < 0):
        string = "-1"
        return string

    string += "4" * a
    string += "7" * b

    return string

# Driver code
print findMin(15)

# This code is contributed by Sachin Bisht
```

## C#

```
// C# program to find smallest number
// with given sum of digits.
using System;

class GFG {

    // Prints minimum number with given digit
    // sum and only allowed digits as 4 and 7.
    static void findMin(int sum)
    {
        int a = 0, b = 0;
        while (sum > 0)
        {

            // Cases where all remaining digits
            // are 4 or 7 (Remaining sum of digits
            // should be multiple of 4 or 7)
            if (sum % 7 == 0)
            {
                b++;
                sum -= 7;
            }
            else if (sum % 4 == 0)
            {
                a++;
                sum -= 4;
            }

            // If both 4s and 7s are there
            // in digit sum, we subtract a 4.
            else
            {
                a++;
                sum -= 4;
            }
        }

        if (sum < 0)
        {
            Console.Write("-1n");
            return;
        }

        for (int i = 0; i < a; i++)
            Console.Write("4");

        for (int i = 0; i < b; i++)
            Console.Write("7");

        Console.WriteLine();
    }

    // Driver code
    public static void Main()
    {
        findMin(15);
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find smallest number
// with given sum of digits.

// Prints minimum number with given digit
// sum and only allowed digits as 4 and 7.
function findMin($sum)
{
    $a = 0;
    $b = 0;
    while ($sum > 0)
    {

        // Cases where all remaining digits
        // are 4 or 7 (Remaining sum of digits
        // should be multiple of 4 or 7)
        if ($sum % 7 == 0)
        {
            $b++;
            $sum -= 7;
        }
        else if ($sum % 4 == 0)
        {
            $a++;
            $sum -= 4;
        }

        // If both 4s and 7s are there
        // in digit sum, we subtract a 4.
        else
        {
            $a++;
            $sum -= 4;
        }
    }

    if ($sum < 0)
    {
        echo("-1n");
        return;
    }

    for ($i = 0; $i < $a; $i++)
        echo("4");

    for ($i = 0; $i < $b; $i++)
        echo("7");

    echo("\n");
}

    // Driver code
    findMin(15);

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>

// Javascript program to find smallest number
// with given sum of digits.

// Prints minimum number with given digit
// sum and only allowed digits as 4 and 7.
function findMin(sum)
{
    var a = 0, b = 0;

    while (sum > 0)
    {

        // Cases where all remaining digits
        // are 4 or 7 (Remaining sum of digits
        // should be multiple of 4 or 7)
        if (sum % 7 == 0)
        {
            b++;
            sum -= 7;
        }
        else if (sum % 4 == 0)
        {
            a++;
            sum -= 4;
        }

        // If both 4s and 7s are there
        // in digit sum, we subtract a 4.
        else
        {
            a++;
            sum -= 4;
        }
    }

    if (sum < 0)
    {
        document.write("-1n");
        return;
    }

    for(i = 0; i < a; i++)
        document.write("4");

    for(i = 0; i < b; i++)
        document.write("7");

    document.write();
}

// Driver code
findMin(15);

// This code is contributed by todaysgaurav

</script>
```

输出:

```
447
```

**时间复杂度:** O(和)。

本文由 **Amit** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。