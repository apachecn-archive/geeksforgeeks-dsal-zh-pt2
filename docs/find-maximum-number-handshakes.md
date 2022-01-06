# 求最大握手次数

> 原文:[https://www . geesforgeks . org/find-最大数量-握手/](https://www.geeksforgeeks.org/find-maximum-number-handshakes/)

一个房间里有 **N** 个人。找到可能的最大握手次数。鉴于任何两个人只握一次手。

**示例:**

```
Input : N = 2
Output : 1.
There are only 2 persons in the room. 1 handshake take place.

Input : N = 10
Output : 45.
```

为了最大限度地握手，每个人都应该和房间里的其他人握手。对于第一个人，会有 N-1 次握手。对于第二个人，将有 N-1 个人可用，但他已经与第一个人握手。所以会有 N-2 次握手等等。
所以，握手总次数= N-1 + N-2 +…。+ 1 + 0，相当于((N-1)*N)/2
(使用前 N 个自然数之和的公式)。

下面是这个问题的实现。

## C++

```
// C++ program to find maximum number of
// handshakes.
#include<bits/stdc++.h>
using namespace std;

// Calculating the maximum number of handshake
// using derived formula.
int maxHandshake(int n)
{
  return (n * (n - 1))/ 2;
}

// Driver Code
int main()
{
  int n = 10;
  cout << maxHandshake(n) <<endl;

  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum number of
// handshakes.

class GFG
{
    // Calculating the maximum number of
    // handshake using derived formula.
    static int maxHandshake(int n)
    {
        return (n * (n - 1)) / 2;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 10;
        System.out.println( maxHandshake(n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find maximum
# number of handshakes.

# Calculating the maximum number
# of handshake using derived formula.
def maxHandshake(n):

    return int((n * (n - 1)) / 2)

# Driver Code
n = 10
print(maxHandshake(n))

# This code is contributed by Smitha Dinesh Semwal.
```

## C#

```
// C# program to find maximum number of
// handshakes.
using System;

class GFG
{
    // Calculating the maximum number of
    // handshake using derived formula.
    static int maxHandshake(int n)
    {
        return (n * (n - 1)) / 2;
    }

    // Driver code
    public static void Main ()
    {
        int n = 10;
        Console.Write( maxHandshake(n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to
// find maximum number
// of handshakes.

// Calculating the maximum
// number of handshake
// using derived formula.
function maxHandshake($n)
{
    return ($n * ($n - 1))/ 2;
}

// Driver Code
$n = 10;
echo maxHandshake($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find maximum
// number of handshakes.

// Calculating the maximum number of
// handshake using derived formula.
function maxHandshake(n)
{
    return (n * (n - 1)) / 2;
}

// Driver Code
let n = 10;

document.write( maxHandshake(n));

// This code is contributed by souravghosh0416 

</script>
```

**输出:**

```
45
```

**时间复杂度:** O(1)

本文由[**Anuj Chauhan(Anuj 0503)**](https://web.facebook.com/anuj0503)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。