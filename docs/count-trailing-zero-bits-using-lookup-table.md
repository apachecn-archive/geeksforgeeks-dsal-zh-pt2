# 使用查找表

对尾随零位进行计数

> 原文:[https://www . geesforgeks . org/count-trading-zero-bits-use-lookup-table/](https://www.geeksforgeeks.org/count-trailing-zero-bits-using-lookup-table/)

给定一个整数，计算尾随零的数量。例如，对于 n = 12，其二进制表示为 1100，尾随零位数为 2。

**示例:**

```
Input : 8
Output : 3
Binary of 8 is 1000, so there are three
trailing zero bits.

Input : 18
Output : 1
Binary of 18 is 10010, so there is one
trailing zero bit.
```

一个简单的解决方案是从最低有效位开始遍历位，并在位为 0 时增加计数。

## C++

```
// Simple C++ code for counting trailing zeros
// in binary representation of a number
#include<bits/stdc++.h>
using namespace std;

int countTrailingZero(int x)
{
  int count = 0;
  while ((x & 1) == 0)
  {
      x = x >> 1;
      count++;
  }
  return count;
}

// Driver Code
int main()
{
    cout << countTrailingZero(11) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Simple Java code for counting
// trailing zeros in binary
// representation of a number
import java.io.*;

class GFG
{
    public static int countTrailingZero(int x)
    {
        int count = 0;

        while ((x & 1) == 0)
        {
            x = x >> 1;
            count++;
        }
        return count;
    }

    // Driver Code
    public static void main (String[] args)
    {

        System.out.println(countTrailingZero(11));
    }
}

// This code is contributed by ajit
```

## 蟒蛇 3

```
# Python 3 code for counting trailing zeros
# in binary representation of a number
def countTrailingZero(x):
    count = 0
    while ((x & 1) == 0):
        x = x >> 1
        count += 1

    return count

# Driver Code
if __name__ == '__main__':
    print(countTrailingZero(11))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// Simple C# code for counting
// trailing zeros in binary
// representation of a number
using System;

class GFG
{
    public static int countTrailingZero(int x)
    {
        int count = 0;

        while ((x & 1) == 0)
        {
            x = x >> 1;
            count++;
        }
        return count;
    }

    // Driver Code
    static public void Main ()
    {
        Console.WriteLine(countTrailingZero(11));
    }
}

// This code is contributed by aj_36
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Simple PHP code for counting trailing zeros
// in binary representation of a number

function countTrailingZero($x)
{
    $count = 0;
    while (($x & 1) == 0)
    {
        $x = $x >> 1;
        $count++;
    }
    return $count;
}

    // Driver Code
    echo countTrailingZero(11),"\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Simple Javascript code for counting trailing zeros
// in binary representation of a number

 function countTrailingZero(x)
    {
        let count = 0;

        while ((x & 1) == 0)
        {
            x = x >> 1;
            count++;
        }
        return count;
    }

// Driver Code

    document.write(countTrailingZero(11));

</script>
```

**输出:**

```
0
```

**时间复杂度:**O(Log n)

**查找表解决方案**基于以下概念:

1.  该解决方案假设负数以 [2 的补码](https://www.geeksforgeeks.org/efficient-method-2s-complement-binary-string/)形式存储，这对于大多数设备都是正确的。如果数字以 2 的补码形式表示，那么(x&-x【x 和负 x 的按位 and】产生一个只有最后一个设定位的数字。
2.  一旦我们得到一个只有一个位集的数字，我们就可以使用查找表找到它的位置。它利用了前 32 位位置值相对于 37 是质数的事实，因此用 37 执行模数除法会给出从 0 到 36 的唯一数字。然后，可以使用小的查找表将这些数字映射到零的数量。

## C++

```
// C++ code for counting trailing zeros
// in binary representation of a number
#include<bits/stdc++.h>
using namespace std;

int countTrailingZero(int x)
{
     // Map a bit value mod 37 to its position
     static const int lookup[] = {32, 0, 1,
     26, 2, 23, 27, 0, 3, 16, 24, 30, 28, 11,
     0, 13, 4, 7, 17, 0, 25, 22, 31, 15, 29,
     10, 12, 6, 0, 21, 14, 9, 5, 20, 8, 19,
     18};

     // Only difference between (x and -x) is
     // the value of signed magnitude(leftmostbit)
     // negative numbers signed bit is 1
     return lookup[(-x & x) % 37];
}

// Driver Code
int main()
{
    cout << countTrailingZero(48) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for counting
// trailing zeros in binary
// representation of a number
import java.io.*;

class GFG
{
static int countTrailingZero(int x)
{

    // Map a bit value mod
    // 37 to its position
    int lookup[] = {32, 0, 1, 26, 2, 23, 
                    27, 0, 3, 16, 24, 30,
                    28, 11, 0, 13, 4, 7,
                    17, 0, 25, 22, 31, 15,
                    29, 10, 12, 6, 0, 21,
                    14, 9, 5, 20, 8, 19, 18};

    // Only difference between
    // (x and -x) is the value
    // of signed magnitude
    // (leftmostbit) negative
    // numbers signed bit is 1
    return lookup[(-x & x) % 37];
}

// Driver Code
public static void main (String[] args)
{
    System.out.println(countTrailingZero(48));
}
}

// This code is contributed
// by ajit
```

## 蟒蛇 3

```
# Python3 code for counting trailing zeros
# in binary representation of a number

def countTrailingZero(x):

    # Map a bit value mod 37 to its position
    lookup = [32, 0, 1, 26, 2, 23, 27, 0,
              3, 16, 24, 30, 28, 11, 0, 13,
              4, 7, 17, 0, 25, 22, 31, 15,
              29, 10, 12, 6, 0, 21, 14, 9,
              5, 20, 8, 19, 18]

    # Only difference between (x and -x) is
    # the value of signed magnitude(leftmostbit)
    # negative numbers signed bit is 1
    return lookup[(-x & x) % 37]

# Driver Code
if __name__ == "__main__":

    print(countTrailingZero(48))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# code for counting
// trailing zeros in binary
// representation of a number
using System;

class GFG
{
static int countTrailingZero(int x)
{

    // Map a bit value mod
    // 37 to its position
    int []lookup = {32, 0, 1, 26, 2, 23,
                    27, 0, 3, 16, 24, 30,
                    28, 11, 0, 13, 4, 7,
                    17, 0, 25, 22, 31, 15,
                    29, 10, 12, 6, 0, 21,
                    14, 9, 5, 20, 8, 19, 18};

    // Only difference between
    // (x and -x) is the value
    // of signed magnitude
    // (leftmostbit) negative
    // numbers signed bit is 1
    return lookup[(-x & x) % 37];
}

// Driver Code
static public void Main ()
{
    Console.WriteLine(countTrailingZero(48));
}
}

// This code is contributed
// by m_kit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code for counting
// trailing zeros in binary
// representation of a number

function countTrailingZero($x)
{
    // Map a bit value mod
    // 37 to its position
    $lookup = array (32, 0, 1, 26, 2, 23,
                     27, 0, 3, 16, 24, 30,
                     28, 11, 0, 13, 4, 7,
                     17, 0, 25, 22, 31, 15,
                     29, 10, 12, 6, 0, 21,
                     14, 9, 5, 20, 8, 19, 18);

    // Only difference between
    // (x and -x) is the value
    // of signed magnitude
    // (leftmostbit) negative
    // numbers signed bit is 1
    return $lookup[(-$x &
                     $x) % 37];
}

// Driver Code
echo countTrailingZero(48), "\n";

// This code is contributed
// by akt_mit
?>
```

## java 描述语言

```
<script>

// Javascript code for counting
// trailing zeros in binary
// representation of a number
function countTrailingZero(x)
{

    // Map a bit value mod
    // 37 to its position
    let lookup = [ 32, 0, 1, 26, 2, 23,
                   27, 0, 3, 16, 24, 30,
                   28, 11, 0, 13, 4, 7,
                   17, 0, 25, 22, 31, 15,
                   29, 10, 12, 6, 0, 21,
                   14, 9, 5, 20, 8, 19, 18 ];

    // Only difference between
    // (x and -x) is the value
    // of signed magnitude
    // (leftmostbit) negative
    // numbers signed bit is 1
    return lookup[(-x & x) % 37];
}

// Driver code
document.write(countTrailingZero(48));

// This code is contributed by divyesh072019

</script>
```

**输出:**

```
4
```

**时间复杂度:** O(1)
**来源:**
[https://graphics.stanford.edu/~seander/bithacks.html](https://graphics.stanford.edu/~seander/bithacks.html)

本文由 **Sumit Sudhakar(Sam)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。