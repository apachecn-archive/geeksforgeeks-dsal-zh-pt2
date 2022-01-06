# 奇数和偶数之和的差

> 原文:[https://www . geesforgeks . org/difference-sum-奇数-偶数/](https://www.geeksforgeeks.org/difference-sums-odd-even-digits/)

给定一个长整数，我们需要知道奇数和偶数之和的差是否为 0。索引从零开始(0 索引代表最左边的数字)。
示例:

```
Input : 1212112
Output : Yes
Explanation:-
the odd position element is 2+2+1=5
the even position element is 1+1+1+2=5
the difference is 5-5=0.so print yes.

Input :12345
Output : No
Explanation:-
the odd position element is 1+3+5=9
the even position element is 2+4=6
the difference is 9-6=3 not  equal
to zero. So print no.
```

**方法 1:** 逐个遍历数字，求两个和。如果两个和的差为 0，打印是，否则不打印
T3】方法 2 : 这可以使用 11 的[可除性轻松解决。只有当数能被 11 整除时，这个条件才成立。所以检查这个数是否能被 11 整除。](https://www.geeksforgeeks.org/check-large-number-divisible-11-not/) 

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to check if difference between sum of
// odd digits and sum of even digits is 0 or not
#include <bits/stdc++.h>
using namespace std;

bool isDiff0(long long int n)
{
    return (n % 11 == 0);
}

int main() {

    long int n = 1243
    if (isDiff0(n))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if difference between sum of
// odd digits and sum of even digits is 0 or not

import java.io.*;
import java.util.*;

class GFG
{
    public static boolean isDiff(int n)
    {
        return (n % 11 == 0);
    }
    public static void main (String[] args)
    {
        int n = 1243;
        if (isDiff(n))
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}
```

## 计算机编程语言

```
# Python program to check if difference between sum of
# odd digits and sum of even digits is 0 or not

def isDiff(n):
    return (n % 11 == 0)

# Driver code
n = 1243;
if (isDiff(n)):
    print("Yes")
else:
    print("No")

# Mohit Gupta_OMG <0_o>
```

## C#

```
// C# program to check if difference
// between sum of odd digits and sum
// of even digits is 0 or not
using System;

class GFG {

    public static bool isDiff(int n)
    {
        return (n % 11 == 0);
    }

    public static void Main ()
    {
        int n = 1243;

        if (isDiff(n))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if
// difference between sum of
// odd digits and sum of
// even digits is 0 or not

function isDiff0($n)
{
    return ($n % 11 == 0);
}

    // Driver Code
    $n = 1243;
    if (isDiff0($n))
        echo"Yes";
    else
        echo "No";

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>

// Javascript program to check if difference between sum of
// odd digits and sum of even digits is 0 or not

function isDiff0(n)
{
    return (n % 11 == 0);
}

    let n = 1243
    if (isDiff0(n))
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
Yes
```

本文由**贾斯帕尔·辛格**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。