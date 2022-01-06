# 可以在机器上计算阶乘的整数的最大值

> 原文:[https://www . geesforgeks . org/最大值-整数-阶乘-可计算-机器/](https://www.geeksforgeeks.org/maximum-value-integer-factorial-can-calculated-machine/)

假设阶乘是用 long long int 这样的基本数据类型存储的，那么程序可以找到一个可以在机器上计算阶乘的整数的最大值。

这个想法是基于这样一个事实，即在大多数机器中，当我们越过整数极限时，值变成负的。

## C

```
// C program to find maximum value of
// an integer for which factorial can
// be calculated on your system
#include <stdio.h>

int findMaxValue()
{
    int res = 2;
    long long int fact = 2;
    while (1)
    {
        // when fact crosses its size,
        // it gives negative value
        if (fact < 0)
            break;
        res++;
        fact = fact * res;
    }
    return res - 1;
}

// Driver Code
int main()
{
    printf ("Maximum value of integer : %d\n",
                                 findMaxValue());
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum value of
// an integer for which factorial can be
// calculated on your system
import java.io.*;
import java.util.*;

class GFG
{
    public static int findMaxValue()
    {
        int res = 2;
        long fact = 2;
        while (true)
        {
            // when fact crosses its size,
            // it gives negative value
            if (fact < 0)
                break;
            res++;
            fact = fact * res;
        }
        return res - 1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        System.out.println("Maximum value of"+
                                 " integer " +
                              findMaxValue());
    }
}
```

## 蟒蛇 3

```
# Python3 program to find maximum value of
# an integer for which factorial can be
# calculated on your system
import sys
def findMaxValue():

    res = 2;
    fact = 2;
    while (True):

        # when fact crosses its size
        # it gives negative value
        if (fact < 0 or fact > sys.maxsize):
            break;
        res += 1;
        fact = fact * res;
    return res - 1;

# Driver Code
if __name__ == '__main__':

    print("Maximum value of integer:",
                      findMaxValue());

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to find maximum value of
// an integer for which factorial can
// be calculated on your system
using System;

class GFG
{
    public static int findMaxValue()
    {
        int res = 2;
        long fact = 2;
        while (true)
        {
            // when fact crosses its size,
            // it gives negative value
            if (fact < 0)
                break;
            res++;
            fact = fact * res;
        }
        return res - 1;
    }

    // Driver Code
    public static void Main()
    {
        Console.Write("Maximum value of"+
                            " integer " +
                         findMaxValue());
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum
// value of an integer for which
// factorial can be calculated
// on your system
function findMaxValue()
{
    $res = 2;
    $fact = 2;
    $pos = -1;
    while (true)
    {
        // when fact crosses its size,
        // it gives negative value
        $mystring = $fact;
        $pos = strpos($mystring, 'E');

        if ($pos > 0)
            break;
        $res++;
        $fact = $fact * $res;
    }
    return $res - 1;
}

// Driver Code
echo "Maximum value of".
           " integer " .
         findMaxValue();

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// Javascript program to find maximum
// value of an integer for which factorial
// can be calculated on your system
function findMaxValue()
{
    let res = 2;
    let fact = 2;

    while (true)
    {

        // When fact crosses its size,
        // it gives negative value
        if (fact < 0 || fact > 9223372036854775807)
            break;

        res++;
        fact = fact * res;
    }
    return res - 1;
}

// Driver Code
document.write("Maximum value of"+
               " integer " + findMaxValue());

// This code is contributed by rag2127

</script>
```

**输出:**

```
Maximum value of integer : 20
```

本文由**普拉莫德·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。