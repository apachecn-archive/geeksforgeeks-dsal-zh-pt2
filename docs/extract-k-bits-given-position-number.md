# 从一个数字的给定位置提取“k”位。

> 原文:[https://www . geesforgeks . org/extract-k-bits-给定位置-编号/](https://www.geeksforgeeks.org/extract-k-bits-given-position-number/)

如何从数字中给定的位置“p”提取“k”位？

示例:

```
Input : number = 171
             k = 5 
             p = 2
Output : The extracted number is 21
171 is represented as 0101011 in binary,
so, you should get only 10101 i.e. 21.

Input : number = 72
            k = 5 
            p = 1
Output : The extracted number is 8
72 is represented as 1001000 in binary,
so, you should get only 01000 i.e 8.

```

1)由 p-1 表示的右移位数。
2)用修改后的数字对 k 组位进行逐位“与”运算。我们可以通过做(1<<k)–1 得到 k 组位。

## C++

```
// C++ program to extract k bits from a given
// position.
#include <bits/stdc++.h>
using namespace std;

// Function to extract k bits from p position
// and returns the extracted value as integer
int bitExtracted(int number, int k, int p)
{
    return (((1 << k) - 1) & (number >> (p - 1)));
}

// Driver code
int main()
{
    int number = 171, k = 5, p = 2;
    cout << "The extracted number is " <<
            bitExtracted(number, k, p);

    return 0;
}

// This code is contributed by importantly
```

## C

```
// C program to extract k bits from a given
// position.
#include <stdio.h>

// Function to extract k bits from p position
// and returns the extracted value as integer
int bitExtracted(int number, int k, int p)
{
    return (((1 << k) - 1) & (number >> (p - 1)));
}

// Driver code
int main()
{
    int number = 171, k = 5, p = 2;
    printf("The extracted number is %d",
               bitExtracted(number, k, p));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to extract k bits from a given
// position.

class GFG {

    // Function to extract k bits from p position
    // and returns the extracted value as integer
    static int bitExtracted(int number, int k, int p)
    {
        return (((1 << k) - 1) & (number >> (p - 1)));
    }

    // Driver code
    public static void main (String[] args) {
        int number = 171, k = 5, p = 2;
        System.out.println("The extracted number is "+
               bitExtracted(number, k, p));
    }
}
```

## 计算机编程语言

```
# Python program to extract k bits from a given
# position.

# Function to extract k bits from p position
# and returns the extracted value as integer
def bitExtracted(number, k, p):  
    return ( ((1 << k) - 1)  &  (number >> (p-1) ) );

# number is from where 'k' bits are extracted
# from p position
number = 171
k = 5
p = 2
print "The extracted number is ", bitExtracted(number, k, p)
```

## C#

```
// C# program to extract k bits from a given
// position.
using System;

class GFG {

    // Function to extract k bits from p position
    // and returns the extracted value as integer
    static int bitExtracted(int number, int k, int p)
    {
        return (((1 << k) - 1) & (number >> (p - 1)));
    }

    // Driver code
    public static void Main()
    {
        int number = 171, k = 5, p = 2;

        Console.WriteLine("The extracted number is "
                      + bitExtracted(number, k, p));
    }
}

//This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP program to extract
// k bits from a given
// position.

// Function to extract k
// bits from p position
// and returns the extracted
// value as integer
function bitExtracted($number, $k, $p)
{
    return (((1 << $k) - 1) &
           ($number >> ($p - 1)));
}

    // Driver Code
    $number = 171; $k = 5; $p = 2;
    echo "The extracted number is ",
          bitExtracted($number, $k, $p);

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>
// JavaScript program to extract k bits from a given
// position.

// Function to extract k bits from p position
// and returns the extracted value as integer
function bitExtracted(number, k, p)
{
    return (((1 << k) - 1) & (number >> (p - 1)));
}

// Driver code

    let number = 171, k = 5, p = 2;
    document.write("The extracted number is ",
            bitExtracted(number, k, p));

// This code is contributed by Manoj.
</script>
```

**输出:**

```
The extracted number is 21
```

本文由 **Ujjwal Aryal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。