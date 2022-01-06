# 有效检查 n 是否为 4 的倍数

> 原文:[https://www . geesforgeks . org/effective-check-what-n-multiple-4-not/](https://www.geeksforgeeks.org/efficiently-check-whether-n-multiple-4-not/)

给定一个数字 **n** 。问题是在不使用算术运算符的情况下，高效地检查 **n** 是否是 4 的倍数。
**例:**

```
Input : 16
Output : Yes

Input : 14
Output : No
```

**方法:**4 的倍数总是以 **00** 作为其二进制表示的最后两位数字。我们必须检查 **n** 的最后两位是否未置位。
**如何检查最后两位是否未置位。**
如果 n & 3 == 0，则最后两个位不置位，否则两个位或其中一个位置位。

## C++

```
// C++ implementation to efficiently check whether n
// is a multiple of 4 or not
#include <bits/stdc++.h>
using namespace std;

// function to check whether 'n' is
// a multiple of 4 or not
string isAMultipleOf4(int n)
{

    // if true, then 'n' is a multiple of 4
    if ((n & 3) == 0)
        return "Yes";

    // else 'n' is not a multiple of 4
    return "No";
}

// Driver program to test above
int main()
{
    int n = 16;
    cout << isAMultipleOf4(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to efficiently check
// whether n is a multiple of 4 or not

class GFG {
    // method to check whether 'n' is
    // a multiple of 4 or not
    static boolean isAMultipleOf4(int n)
    {
        // if true, then 'n' is a multiple of 4
        if ((n & 3) == 0)
            return true;

        // else 'n' is not a multiple of 4
        return false;
    }

    // Driver method
    public static void main(String[] args)
    {
        int n = 16;
        System.out.println(isAMultipleOf4(n) ? "Yes" : "No");
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation to
# efficiently check whether n
# is a multiple of 4 or not

# function to check whether 'n'
# is a multiple of 4 or not
def isAMultipleOf4(n):

    # if true, then 'n' is
    # a multiple of 4
    if ((n & 3) == 0):
        return "Yes"

    # else 'n' is not a
    # multiple of 4
    return "No"

# Driver Code
if __name__ == "__main__":

    n = 16
    print (isAMultipleOf4(n))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# implementation to efficiently check
// whether n is a multiple of 4 or not
using System;

class GFG {

    // method to check whether 'n' is
    // a multiple of 4 or not
    static bool isAMultipleOf4(int n)
    {
        // if true, then 'n' is a multiple of 4
        if ((n & 3) == 0)
            return true;

        // else 'n' is not a multiple of 4
        return false;
    }

    // Driver method
    public static void Main()
    {
        int n = 16;
        Console.WriteLine(isAMultipleOf4(n) ? "Yes" : "No");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to
// efficiently check whether n
// is a multiple of 4 or not

// function to check whether 'n' is
// a multiple of 4 or not
function isAMultipleOf4($n)
{

    // if true, then 'n'
    // is a multiple of 4
    if (($n & 3) == 0)
        return "Yes";

    // else 'n' is not
    // a multiple of 4
    return "No";
}

    // Driver Code
    $n = 16;
    echo isAMultipleOf4($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript implementation to efficiently check
// whether n is a multiple of 4 or not

    // method to check whether 'n' is
    // a multiple of 4 or not
    function isAMultipleOf4(n)
    {
        // if true, then 'n' is a multiple of 4
        if ((n & 3) == 0)
            return true;

        // else 'n' is not a multiple of 4
        return false;
    }

    // Driver method
    let n = 16;
    document.write(isAMultipleOf4(n) ? "Yes" : "No");

    //This code is contributed by rag2127

</script>
```

输出:

```
Yes
```

**能否推广上述解？**
同样的我们可以查一下其他 2 的幂。例如，如果 n & 7 是 0，数字 n 将是 8 的倍数。总的来说我们可以说。

```
// x must be a power of 2 for below
// logic to work
if (n & (x -1) == 0)
   n is a multiple of x
Else
   n is NOT a multiple of x
```

https://youtu.be/ke

-Mai2m6Cg
本文由**阿育什·尤赫里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。