# 找出是否有可能制作一个包含给定数量的“0”、“1”、“01”和“10”的二进制字符串作为子序列

> 原文:[https://www . geeksforgeeks . org/find-如果可能的话-制作一个二进制字符串，其中包含给定的 0-1-01 和-10 的数字作为子序列/](https://www.geeksforgeeks.org/find-if-it-is-possible-to-make-a-binary-string-which-contanins-given-number-of-0-1-01-and-10-as-sub-sequences/)

给定四个整数 **l** 、 **m** 、 **x** 和 **y** 。任务是检查是否有可能将由**l 0s**、**m 1s**、**x“01”**和**y“10”**组成的二进制字符串作为其中的子序列。
**举例:**

> **输入:** l = 3，m = 2，x = 4，y = 2
> **输出:**是
> 可能的字符串为“00110”。它包含 3 个 0、2 个 1、
> 4 个“01”子序列和 2 个“10”子序列。
> **输入:** l = 3，m = 2，x = 4，y = 3
> **输出:**否
> 不存在这样的二进制字符串。

**方法:**可能的字符串总是形式为 **00…11…00…** 。首先是一些零，然后是所有的 1，然后是剩余的零。
假设 **l1** 是 1 之前的零的数量， **l2** 是 1 之后的零的数量，那么等式为:

1.  **l1 + l2 = l** (零的总数)。
2.  **l1 * m = x** (子序列“01”的数量)。
3.  **m * L2 = y**(10 个子序列数)。

从以上三个方程，我们得到 **x + y = l * m** 。如果这个等式对于给定值失败，那么字符串是不可能的，否则打印**是**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if it is possible to
// make a binary string consisting of l 0's, m 1's,
// x "01" sub-sequences and y "10" sub-sequences
bool isPossible(int l, int m, int x, int y)
{
    if (l * m == x + y)
        return true;

    return false;
}

// Driver code
int main()
{
    int l = 3, m = 2, x = 4, y = 2;

    if (isPossible(l, m, x, y))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class sol
{

// Function that returns true if it is possible to
// make a binary string consisting of l 0's, m 1's,
// x "01" sub-sequences and y "10" sub-sequences
static boolean isPossible(int l, int m, int x, int y)
{
    if (l * m == x + y)
        return true;

    return false;
}

// Driver code
public static void main(String args[])
{
    int l = 3, m = 2, x = 4, y = 2;

    if (isPossible(l, m, x, y))
        System.out.print("Yes");
    else
        System.out.print("No");

}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if it is possible to
# make a binary string consisting of l 0's, m 1's,
# x "01" sub-sequences and y "10" sub-sequences
def isPossible(l, m, x, y) :

    if (l * m == x + y) :
        return True;

    return False;

# Driver code
if __name__ == "__main__" :

    l = 3; m = 2; x = 4; y = 2;

    if (isPossible(l, m, x, y)) :
        print("Yes");
    else :
        print("No");

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class sol
{

// Function that returns true if it is possible to
// make a binary string consisting of l 0's, m 1's,
// x "01" sub-sequences and y "10" sub-sequences
static Boolean isPossible(int l, int m, int x, int y)
{
    if (l * m == x + y)
        return true;

    return false;
}

// Driver code
public static void Main(String []args)
{
    int l = 3, m = 2, x = 4, y = 2;

    if (isPossible(l, m, x, y))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by Arnab Kundu
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if it is possible to
// make a binary string consisting of l 0's, m 1's,
// x "01" sub-sequences and y "10" sub-sequences
function isPossible(l, m, x, y)
{
    if (l * m == x + y)
        return true;

    return false;
}

// Driver code
    let l = 3, m = 2, x = 4, y = 2;

    if (isPossible(l, m, x, y))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
Yes
```