# 计算一个数字的总位数

> 原文:[https://www.geeksforgeeks.org/count-total-bits-number/](https://www.geeksforgeeks.org/count-total-bits-number/)

给定一个正数 n，计算其中的总位数。
**例:**

```
Input : 13
Output : 4
Binary representation of 13 is 1101

Input  : 183
Output : 8

Input  : 4096
Output : 13
```

**方法 1(使用对数)**

对数 2(n)以 n 为底的对数，它是指数，2 被提升得到 n 个整数，我们在对数(n)时间内加 1 得到一个数的总位数。

## C++

```
// C++ program to find total bit in given number
#include <iostream>   
#include <cmath>

unsigned countBits(unsigned int number)
{   

    // log function in base 2
    // take only integer part
    return (int)log2(number)+1;
}

// Driven program   
int main()
{
    unsigned int num = 65;
    std::cout<<countBits(num)<<'\n';
    return 0;
}

// This code is contributed by thedev05.
```

## C

```
// C program to find total bit in given number
#include <stdio.h>     
#include <math.h>

unsigned countBits(unsigned int number)
{     
      // log function in base 2
      // take only integer part
      return (int)log2(number)+1;
}

// Driven program      
int main()
{
    unsigned int num = 65;
    printf("%d\n", countBits(num));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to
// find total bit
// in given number
import java.io.*;

class GFG
{
    static int countBits(int number)
    {

        // log function in base 2
        // take only integer part
        return (int)(Math.log(number) /
                     Math.log(2) + 1);
    }

    // Driver code
    public static void main (String[] args)
    {
        int num = 65;

        System.out.println(countBits(num));

    }
}

// This code is contributed by vij
```

## 蟒蛇 3

```
# Python3 program to find
# total bit in given number
import math
def countBits(number):

    # log function in base 2
    # take only integer part
    return int((math.log(number) /
                math.log(2)) + 1);

# Driver Code
num = 65;
print(countBits(num));

# This code is contributed by mits
```

## C#

```
// C# program to find total bit
// in given number
using System;

class GFG {

    static uint countBits(uint number)
    {    

        // log function in base 2
        // take only integer part
        return (uint)Math.Log(number , 2.0) + 1;
    }

    // Driver code
    public static void Main()
    {
        uint num = 65;

        Console.WriteLine(countBits(num));

    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find total
// bit in given number

function countBits($number)
{

    // log function in base 2
    // take only integer part
    return (int)(log($number) /
                   log(2)) + 1;
}

// Driver Code
$num = 65;
echo(countBits($num));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// JavaScript program to find total bit in given number

    function countBits(number) {      
      // log function in base 2 
      // take only integer part
      return Math.floor(Math.log2(number)+1);
    }

    // Driven program       

    let num = 65;
    document.write(countBits(num));

// This code is contributed by Surbhi Tyagi
</script>
```

**Output**

```
7

```

**方法 2(使用位遍历)**

## C

```
/* Function to get no of bits in binary
   representation of positive integer */
#include <stdio.h>        

unsigned int countBits(unsigned int n)
{
   unsigned int count = 0;
   while (n)
   {
        count++;
        n >>= 1;
    }
    return count;
}

/* Driver program*/
int main()
{
    int i = 65;
    printf("%d", countBits(i));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Function to get no of bits in binary
representation of positive integer */
class GFG {

    static int countBits(int n)
    {
        int count = 0;
        while (n != 0)
        {
            count++;
            n >>= 1;
        }

        return count;
    }

    /* Driver program*/
    public static void main(String[] arg)
    {
        int i = 65;
        System.out.print(countBits(i));
    }
}

// This code is contributed by Smitha.
```

## 蟒蛇 3

```
# Function to get no of bits
# in binary representation
# of positive integer

def countBits(n):

    count = 0
    while (n):
        count += 1
        n >>= 1

    return count

# Driver program
i = 65
print(countBits(i))

# This code is contributed
# by Smitha
```

## C#

```
/* Function to get no of bits
in binary representation of
positive integer */
using System;

class GFG
{
    static int countBits(int n)
    {
        int count = 0;
        while (n != 0)
        {
            count++;
            n >>= 1;
        }

        return count;
    }

    // Driver Code
    static public void Main ()
    {
        int i = 65;
        Console.Write(countBits(i));
    }
}

// This code is contributed
// by akt_mit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Code to get no of bits in binary
// representation of positive integer

// Function to get no of bits in binary
// representation of positive integer
function countBits($n)
{
    $count = 0;
    while ($n)
    {
        $count++;
        $n >>= 1;
    }
    return $count;
}

// Driver Code
$i = 65;
echo(countBits($i));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

/* Function to get no of bits
in binary representation of
positive integer */
function countBits(n)
{
    var count = 0;
    while (n != 0)
    {
        count++;
        n >>= 1;
    }

    return count;
}

// Driver Code
var i = 65;
document.write(countBits(i));

</script>
```

**Output**

```
7
```

**方法 3(使用从二进制到字符串的转换)**

## 蟒蛇 3

```
a = 65
b = 183

# Convert an integer to binary
a_bit = bin(a)[2::]
b_bit = bin(b)[2::]

# Convert the binary to string so that we can count the bits
str_a_bit = str(a_bit)
str_b_bit = str(b_bit)

print("Total bits :", len(str_a_bit))
print("Total bits :", len(str_b_bit))

# This code is contributed by harshit
```

**Output**

```
Total bits : 7
Total bits : 8

```

本文由**gyayayak Jain**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。