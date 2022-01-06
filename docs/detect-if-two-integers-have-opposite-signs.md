# 检测两个整数是否符号相反

> 原文:[https://www . geesforgeks . org/detect-if-two-integer-有相反的符号/](https://www.geeksforgeeks.org/detect-if-two-integers-have-opposite-signs/)

给定两个有符号整数，编写一个函数，如果给定整数的符号不同，则返回 true，否则返回 false。例如，函数应该返回 true -1 和+100，对于-100 和-200 应该返回 false。该函数不应使用任何算术运算符。
设给定的整数为 x 和 y，负数符号位为 1，正数符号位为 0。如果 x 和 y 的符号相反，则它们的异或符号位为 1。换句话说，x 和 y 的异或将是负数，如果 x 和 y 有相反的符号。下面的代码使用了这个逻辑。

## C++

```
// C++ Program to Detect
// if two integers have opposite signs.
#include<iostream>
using namespace std;

bool oppositeSigns(int x, int y)
{
    return ((x ^ y) < 0);
}

int main()
{
    int x = 100, y = -100;
    if (oppositeSigns(x, y) == true)
    cout << "Signs are opposite";
    else
    cout << "Signs are not opposite";
    return 0;
}

// this code is contributed by shivanisinghss2110
```

## C

```
// C++ Program to Detect 
// if two integers have opposite signs.
#include<stdbool.h>
#include<stdio.h>

bool oppositeSigns(int x, int y)
{
    return ((x ^ y) < 0);
}

int main()
{
    int x = 100, y = -100;
    if (oppositeSigns(x, y) == true)
       printf ("Signs are opposite");
    else
      printf ("Signs are not opposite");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to Detect 
// if two integers have opposite signs.

class GFG {

    static boolean oppositeSigns(int x, int y)
    {
        return ((x ^ y) < 0);
    }

    public static void main(String[] args)
    {
        int x = 100, y = -100;
        if (oppositeSigns(x, y) == true)
            System.out.println("Signs are opposite");
        else
            System.out.println("Signs are not opposite");
    }
}

// This code is contributed by prerna saini.
```

## 蟒蛇 3

```
# Python3 Program to Detect 
# if two integers have 
# opposite signs.
def oppositeSigns(x, y):
    return ((x ^ y) < 0);

x = 100
y = 1

if (oppositeSigns(x, y) == True):
    print ("Signs are opposite")
else:
    print ("Signs are not opposite")

# This article is contributed by Prerna Saini.
```

## C#

```
// C# Program to Detect 
// if two integers have 
// opposite signs.
using System;

class GFG {

    // Function to detect signs
    static bool oppositeSigns(int x, int y)
    {
        return ((x ^ y) < 0);
    }

    // Driver Code
    public static void Main()
    {
        int x = 100, y = -100;
        if (oppositeSigns(x, y) == true)
            Console.Write("Signs are opposite");
        else
            Console.Write("Signs are not opposite");
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to Detect if two
// integers have opposite signs.

function oppositeSigns($x, $y)
{
    return (($x ^ $y) < 0);
}

    // Driver Code
    $x = 100;
    $y = -100;
    if (oppositeSigns($x, $y) == true)
    echo ("Signs are opposite");
    else
    echo ("Signs are not opposite");

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>

// Javascript Program to Detect 
// if two integers have opposite signs.

function oppositeSigns(x, y)
    {
        return ((x ^ y) < 0);
    }

// Driver Code

    let x = 100, y = -100;
    if (oppositeSigns(x, y) == true)
         document.write("Signs are opposite");
    else
         document.write("Signs are not opposite");

</script>
```

**输出:**

```
Signs are opposite
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*

来源:[检测两个整数是否有相反的符号](http://graphics.stanford.edu/~seander/bithacks.html#DetectOppositeSigns)
我们也可以通过使用两个比较运算符来解决这个问题。请参见以下代码。

## 卡片打印处理机（Card Print Processor 的缩写）

```
bool oppositeSigns(int x, int y)
{
    return (x < 0)? (y >= 0): (y < 0);
}
```