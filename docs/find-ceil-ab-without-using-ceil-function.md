# 不使用 ceil()功能查找 a/b 的 ceil

> 原文:[https://www . geesforgeks . org/find-CEI-ab-不使用-CEI-function/](https://www.geeksforgeeks.org/find-ceil-ab-without-using-ceil-function/)

给定 a 和 b，不使用天花板函数，求 a/b 的天花板值。
**例:**

```
Input : a = 5, b = 4 
Output : 2 
Explanation: a/b = ceil(5/4) = 2 

Input : a = 10, b = 2
Output : 5 
Explanation: a/b = ceil(10/2) = 5 
```

使用天花板函数可以解决这个问题，但是当整数作为参数传递时，天花板函数不起作用。因此，有以下两种方法来找到最高值。
**进场 1:**

> ceilival =**(a/b)+((a % b)！= 0)**

**a/b** 返回整数除数值， **((a % b)！= 0)** 是一个检查条件，如果 a/b 除法后还有余数，则返回 1，否则返回 0。整数除法值与校验值相加得到上限值。
以下是上述方法的示例:

## C++

```
// C++ program to find ceil(a/b)
// without using ceil() function
#include <cmath>
#include <iostream>
using namespace std;

// Driver function
int main()
{
    // taking input 1
    int a = 4;
    int b = 3;
    int val = (a / b) + ((a % b) != 0);
    cout << "The ceiling value of 4/3 is "
         << val << endl;

    // example of perfect division
    // taking input 2
    a = 6;
    b = 3;
    val = (a / b) + ((a % b) != 0);
    cout << "The ceiling value of 6/3 is "
         << val << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// ceil(a/b) without
// using ceil() function
import java.io.*;

class GFG
{
    // Driver Code
    public static void main(String args[])
    {
        // taking input 1
        int a = 4;
        int b = 3, val = 0;
        if((a % b) != 0)
            val = (a / b) +
                  (a % b);
        else
            val = (a / b);
        System.out.println("The ceiling " +
                       "value of 4/3 is " +
                                      val);
        // example of perfect
        // division taking input 2
        a = 6;
        b = 3;
        if((a % b) != 0)
            val = (a / b) + (a % b);
        else
            val = (a / b);
        System.out.println("The ceiling " +
                       "value of 6/3 is " +
                                      val);
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 蟒蛇 3

```
# Python3 program to find ceil(a/b)
# without using ceil() function
import math

# Driver Code

# taking input 1
a = 4;
b = 3;
val = (a / b) + ((a % b) != 0);
print("The ceiling value of 4/3 is",
                   math.floor(val));

# example of perfect division
# taking input 2
a = 6;
b = 3;
val = int((a / b) + ((a % b) != 0));
print("The ceiling value of 6/3 is", val);

# This code is contributed by mits
```

## C#

```
// C# program to find ceil(a/b)
// without using ceil() function
using System;

class GFG
{

    // Driver Code
    static void Main()
    {
        // taking input 1
        int a = 4;
        int b = 3, val = 0;
        if((a % b) != 0)
            val = (a / b) + (a % b);
        else
            val = (a / b);
        Console.WriteLine("The ceiling " +
                      "value of 4/3 is " +
                                     val);

        // example of perfect
        // division taking input 2
        a = 6;
        b = 3;
        if((a % b) != 0)
            val = (a / b) + (a % b);
        else
            val = (a / b);
        Console.WriteLine("The ceiling " +
                      "value of 6/3 is " +
                                     val);
    }
}
// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find ceil(a/b)
// without using ceil() function

// Driver function

    // taking input 1
    $a = 4;
    $b = 3;
    $val = ($a / $b) + (($a % $b) != 0);
    echo "The ceiling value of 4/3 is "
        , floor($val) ,"\n";

    // example of perfect division
    // taking input 2
    $a = 6;
    $b = 3;
    $val = ($a / $b) + (($a % $b) != 0);
    echo "The ceiling value of 6/3 is "
                               , $val ;

// This code is contributed by anuj_67.

?>
```

## java 描述语言

```
<script>
// javascript program to find
// ceil(a/b) without
// using ceil() function
    // Driver Code

        // taking input 1
        var a = 4;
        var b = 3, val = 0;
        if ((a % b) != 0)
            val = parseInt(a / b) + (a % b);
        else
            val = parseInt(a / b);
        document.write("The ceiling " + "value of 4/3 is " + val+"<br/>");

        // example of perfect
        // division taking input 2
        a = 6;
        b = 3;
        if ((a % b) != 0)
            val = parseInt(a / b) + (a % b);
        else
            val = parseInt(a / b);
        document.write("The ceiling " + "value of 6/3 is " + val);

// This code is contributed by gauravrajput1
</script>
```

**Output:** 

```
The ceiling value of 4/3 is 2
The ceiling value of 6/3 is 2
```

**进场 2:**

> ceilVal = (a+b-1) / b

用简单的数学方法，我们可以把分母加到分子上，然后减去 1，再除以分母，就可以得到最大值。
以下是上述方法的示例:

## C++

```
// C++ program to find ceil(a/b)
// without using ceil() function
#include <cmath>
#include <iostream>
using namespace std;

// Driver function
int main()
{
    // taking input 1
    int a = 4;
    int b = 3;
    int val = (a + b - 1) / b;
    cout << "The ceiling value of 4/3 is "
         << val << endl;

    // example of perfect division
    // taking input 2
    a = 6;
    b = 3;
    val = (a + b - 1) / b;
    cout << "The ceiling value of 6/3 is "
         << val << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find ceil(a/b)
// without using ceil() function

class GFG {

// Driver Code
public static void main(String args[])
{

    // taking input 1
    int a = 4;
    int b = 3;
    int val = (a + b - 1) / b;
    System.out.println("The ceiling value of 4/3 is "
                        + val);

    // example of perfect division
    // taking input 2
    a = 6;
    b = 3;
    val = (a + b - 1) / b;
    System.out.println("The ceiling value of 6/3 is "
                        + val );
}
}

// This code is contributed by Jaideep Pyne
```

## 蟒蛇 3

```
# Python3 program to find
# math.ceil(a/b) without
# using math.ceil() function
import math

# Driver Code
# taking input 1
a = 4;
b = 3;
val = (a + b - 1) / b;
print("The ceiling value of 4/3 is ",
                    math.floor(val));

# example of perfect division
# taking input 2
a = 6;
b = 3;
val = (a + b - 1) / b;
print("The ceiling value of 6/3 is ",
                    math.floor(val));

# This code is contributed by mits
```

## C#

```
// C# program to find ceil(a/b)
// without using ceil() function
using System;

class GFG {

    // Driver Code
    public static void Main()
    {

        // taking input 1
        int a = 4;
        int b = 3;
        int val = (a + b - 1) / b;
        Console.WriteLine("The ceiling"
          + " value of 4/3 is " + val);

        // example of perfect division
        // taking input 2
        a = 6;
        b = 3;
        val = (a + b - 1) / b;
        Console.WriteLine("The ceiling"
         + " value of 6/3 is " + val );
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find ceil(a/b)
// without using ceil() function

    // Driver function
    // taking input 1
    $a = 4;
    $b = 3;
    $val = ($a + $b - 1) /$b;
    echo "The ceiling value of 4/3 is "
        , floor($val) ,"\n";

    // example of perfect division
    // taking input 2
    $a = 6;
    $b = 3;
    $val = ($a + $b - 1) / $b;
    echo "The ceiling value of 6/3 is "
        ,floor($val) ;

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// javascript program to find ceil(a/b)
// without using ceil() function
    // Driver Code

        // taking input 1
        var a = 4;
        var b = 3;
        var val = (a + b - 1) / b;
        document.write("The ceiling value of 4/3 is " + val+"<br/>");

        // example of perfect division
        // taking input 2
        a = 6;
        b = 3;
        val = parseInt((a + b - 1) / b);
        document.write("The ceiling value of 6/3 is " + val);

// This code contributed by Rajput-Ji
</script>
```

**Output:** 

```
The ceiling value of 4/3 is 2
The ceiling value of 6/3 is 2
```