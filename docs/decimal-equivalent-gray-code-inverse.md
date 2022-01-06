# 格雷码及其逆码的十进制等价物

> 原文:[https://www . geesforgeks . org/decimal-等价物-格雷码-逆/](https://www.geeksforgeeks.org/decimal-equivalent-gray-code-inverse/)

给定一个十进制数 n，以十进制形式找出这个数的格雷码。

**示例:**

> 输入:7
> 输出:4
> **说明:** 7 以二进制形式表示为 111。111 的等价格雷码
> 是二进制形式的 100，其十进制等价为 4。
> 
> 输入:10
> 输出:15
> **说明:** 10 以二进制形式表示为 1010。1010 的等价格雷码
> 是二进制形式的 1111，其十进制等价为 15。

下表显示了二进制代码值到格雷码值的转换:

<figure class="table">

| 十进制值 | 二元等价物 | 格雷码等价物 | 格雷码等值的十进制值 |
| --- | --- | --- | --- |
| Zero | 000 | 000 | Zero |
| one | 001 | 001 | one |
| Two | 010 | 011 | three |
| three | 011 | 010 | Two |
| four | One hundred | One hundred and ten | six |
| five | One hundred and one | One hundred and eleven | seven |
| six | One hundred and ten | One hundred and one | five |
| seven | One hundred and eleven | One hundred | four |

**下面是将十进制代码值转换为格雷码值的方法。**
设 G(n)为二进制表示 n 的格雷码等价物，考虑一个数字 n 的比特和一个数字比特 G(n)。请注意，n 和 G(n)最左边的一组位位于同一位置。设这个位置为 I，它右边的位置为(i+1)、(i+2)等。如果 n 中的第(i + 1)位为 1，则 G(n)中的第(I+1)<sup>位为 0，反之亦然。第(i+2)位也是如此，等等。因此我们有 G (n) = n xor (n > > 1):</sup>

## C++

```
// CPP Program to convert given
// decimal number into decimal
// equivalent of its gray code form
#include <bits/stdc++.h>
using namespace std;

int grayCode(int n)
{
    /* Right Shift the number by 1
       taking xor with original number */
    return n ^ (n >> 1);
}

// Driver Code
int main()
{
    int n = 10;
    cout << grayCode(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to convert given
// decimal number into decimal
// equivalent of its gray code form
class GFG {

    static int grayCode(int n)
    {

        // Right Shift the number
        // by 1 taking xor with
        // original number
        return n ^ (n >> 1);
    }

    // Driver Code
    public static void main(String[] args)
    {

        int n = 10;

        System.out.println(grayCode(n));
    }
}

// This code is contributed by
// Smitha Dinesh Semwal
```

## 蟒蛇 3

```
# Python 3 Program to convert
# given decimal number into
# decimal equivalent of its
# gray code form

def grayCode(n):

    # Right Shift the number
    # by 1 taking xor with
    # original number
    return n ^ (n >> 1)

# Driver Code
n = 10
print(grayCode(n))

# This code is contributed
# by Smitha Dinesh Semwal
```

## C#

```
// C# Program to convert given
// decimal number into decimal
// equivalent of its gray code form
using System;

public class GFG {

    // Function for conversion
    public static int grayCode(int n)
    {

        // Right Shift the number
        // by 1 taking xor with
        // original number
        return n ^ (n >> 1);
    }

    // Driver Code
    static public void Main ()
    {
        int n = 10;

        Console.WriteLine(grayCode(n));
    }
}

// This code is contributed by Ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to convert given
// decimal number into decimal
// equivalent of its gray code form

function grayCode($n)
{
    /* Right Shift the number by 1
       taking xor with original
       number */
    return $n ^ ($n >> 1);
}

    // Driver Code
    $n = 10;
    echo grayCode($n) ;

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript Program to convert given
// decimal number into decimal
// equivalent of its gray code form

function grayCode(n)
{
    /* Right Shift the number by 1
       taking xor with original number */
    return n ^ (n >> 1);
}

// Driver Code
var n = 10;
document.write( grayCode(n) );

</script>
```

**Output:** 

```
15
```

**求逆格雷码**
给定一个十进制等价数 n 的格雷码。以十进制形式找到它的原始数字。

**示例:**

> 输入:4
> 输出:7
> 
> 输入:15
> 输出:10

**下面是将格雷码值转换为十进制码值的方法。**
我们将从较老的比特到较年轻的比特(即使最小的比特也有数字 1，最老的比特被编号为 k)。我们得到 n <sub>i</sub> 数 n 的比特和 g <sub>i</sub> 数 g 的比特之间的关系:

```
 nk = gk, 
 nk-1 = gk-1 xor nk = gk xor gk-1
 nk-2 = gk-2 xor nk-1 = gk xor gk-1 xor gk-2 
 nk-3 = gk-3 xor nk-2 = gk xor gk-1 xor gk-2 xor gk-3
 ... 
```

## C++

```
// CPP Program to convert given
// decimal number of gray code
// into its inverse in decimal form
#include <bits/stdc++.h>
using namespace std;

int inversegrayCode(int n)
{
    int inv = 0;

    // Taking xor until n becomes zero
    for (; n; n = n >> 1)
        inv ^= n;

    return inv;
}

// Driver Code
int main()
{
    int n = 15;
    cout << inversegrayCode(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to convert given
// decimal number of gray code
// into its inverse in decimal form
import java.io.*;

class GFG {

    // Function to convert given
    // decimal number of gray code
    // into its inverse in decimal form
    static int inversegrayCode(int n)
    {
        int inv = 0;

        // Taking xor until n becomes zero
        for ( ; n != 0 ; n = n >> 1)
            inv ^= n;

        return inv;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 15;
        System.out.println(inversegrayCode(n));
    }
}

// This code is contributed by Ajit.
```

## 蟒蛇 3

```
# Python3 Program to convert
# given decimal number of
# gray code into its inverse
# in decimal form

def inversegrayCode(n):
    inv = 0;

    # Taking xor until
    # n becomes zero
    while(n):
        inv = inv ^ n;
        n = n >> 1;
    return inv;

# Driver Code
n = 15;
print(inversegrayCode(n));

# This code is contributed
# by mits
```

## C#

```
// C# Program to convert given
// decimal number of gray code
// into its inverse in decimal form
using System;

class GFG {

    // Function to convert given
    // decimal number of gray code
    // into its inverse in decimal form
    static int inversegrayCode(int n)
    {
        int inv = 0;

        // Taking xor until n becomes zero
        for ( ; n != 0 ; n = n >> 1)
            inv ^= n;

        return inv;
    }

    // Driver code
    public static void Main ()
    {
        int n = 15;
        Console.Write(inversegrayCode(n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to convert given
// decimal number of gray code
// into its inverse in decimal form

function inversegrayCode( $n)
{
    $inv = 0;

    // Taking xor until
    // n becomes zero
    for (; $n; $n = $n >> 1)
        $inv ^= $n;

    return $inv;
}

    // Driver Code
    $n = 15;
    echo inversegrayCode($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript Program to convert given
// decimal number of gray code
// into its inverse in decimal form

function inversegrayCode(n)
{
    let inv = 0;

    // Taking xor until n becomes zero
    for (; n; n = n >> 1)
        inv ^= n;

    return inv;
}

// Driver Code
    let n = 15;
    document.write(inversegrayCode(n));

</script>
```

**Output:** 

```
10
```

</figure>