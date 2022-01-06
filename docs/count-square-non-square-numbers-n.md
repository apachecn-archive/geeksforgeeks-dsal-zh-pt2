# 计数 n 前的平方数和非平方数

> 原文:[https://www . geesforgeks . org/count-square-non-square-numbers-n/](https://www.geeksforgeeks.org/count-square-non-square-numbers-n/)

给定一个数 n，我们需要计算小于或等于 n 的平方数
**例:**

```
Input : n = 5
Output : Square Number : 2
         Non-square numbers : 3
Explanation : Square numbers are 1 and 4.
Non square numbers are 2, 3 and 5.

Input : n = 10
Output : Square Number : 3
         Non-square numbers : 7
Explanation : Square numbers are 1, 4 and 9.
Non square numbers are 2, 3, 5, 6, 7, 8 and 10.
```

一个**简单的解决方案**是遍历从 1 到 n 的所有数字，并且对于每个数字检查 n 是否是完美平方。
一个**高效解决方案**基于以下公式。
**大于 0 且小于或等于 n 的平方数**的计数为 floor(sqrt(n))或 **⌊√(n)⌋**
非平方数的计数=**n–⌊√(n)⌋**

## C++

```
// CPP program to count squares and
// non-squares before a number.
#include <bits/stdc++.h>
using namespace std;

void countSquaresNonSquares(int n)
{
    int sc = floor(sqrt(n));
    cout << "Count of squares "
         << sc << endl;
    cout << "Count of non-squares "
         << n - sc << endl;
}

// Driver Code
int main()
{
    int n = 10;
    countSquaresNonSquares(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count squares and
// non-squares before a number.
import java.io.*;
import java.math.*;

class GFG
{
    static void countSquaresNonSquares(int n)
    {
        int sc = (int)(Math.floor(Math.sqrt(n)));
        System.out.println("Count of" +
                     " squares " + sc);
        System.out.println("Count of" +
                      " non-squares " +
                            (n - sc) );
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 10;
        countSquaresNonSquares(n);
    }
}

// This code is contributed
// by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python 3 program to count
# squares and non-squares
# before a number.
import math

def countSquaresNonSquares(n) :
    sc = (math.floor(math.sqrt(n)))
    print("Count of squares ", sc)
    print("Count of non-squares ", (n - sc) )

# Driver code
n = 10
countSquaresNonSquares(n)

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// C# program to count squares and
// non-squares before a number.
using System;

class GFG
{
static void countSquaresNonSquares(int n)
{
    int sc = (int)Math.Sqrt(n);
    Console.WriteLine( "Count of " +
                        "squares " +
                               sc) ;
    Console.WriteLine("Count of " +
                   "non-squares " +
                         (n - sc));
}

    // Driver Code
    static public void Main ()
    {
    int n = 10;
    countSquaresNonSquares(n);
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count
// squares and non-squares
// before a number.

// function to count squares
// and non-squares before a
// number
function countSquaresNonSquares($n)
{
    $sc = floor(sqrt($n));
    echo("Count of squares " .
                  $sc . "\n");
    echo("Count of non-squares " .
                      ($n - $sc));
}

// Driver code
$n = 10;
countSquaresNonSquares($n);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to count squares and
// non-squares before a number.

function countSquaresNonSquares(n)
{
    let sc = Math.floor(Math.sqrt(n));
    document.write("Count of squares "
        + sc + "<br>");
    document.write("Count of non-squares "
        + (n - sc) + "<br>");
}

// Driver Code

    let n = 10;
    countSquaresNonSquares(n);

//This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
Count of squares 3
Count of non-squares 7
```