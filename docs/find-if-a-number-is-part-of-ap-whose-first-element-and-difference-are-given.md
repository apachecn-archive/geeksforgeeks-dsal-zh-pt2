# 查找一个数是否是 AP 的一部分，AP 的第一个元素和差是给定的

> 原文:[https://www . geeksforgeeks . org/find-if-a-number-is-part-of-AP-first-element-and-difference-given/](https://www.geeksforgeeks.org/find-if-a-number-is-part-of-ap-whose-first-element-and-difference-are-given/)

给定三个非负整数 a、d 和 x。这里，a 是第一个元素，d 是一个 AP(算术级数)的差。我们需要找到 x 是否是给定 AP 的一部分。

**示例:**

```
Input : a = 1, d = 3, x = 7
Output : Yes
7 is part of given AP, 1 + 3 + 3 = 7

Input : a = 10, d = 0, x = 10
Output : Yes
```

首先，在 d = 0 的情况下，如果 a = x，我们应该输出 Yes，否则答案是 No，对于非零 d，如果 x 属于序列 x = a + n * d，其中 n 是非负整数，只有当(n–a)/d 是非负整数。

## C++

```
// C++ program to check if x exist
// or not in the given AP.
#include <bits/stdc++.h>
using namespace std;

// returns yes if exist else no.
bool isMember(int a, int d, int x)
{

    // If difference is 0, then x must
    // be same as a.
    if (d == 0)
        return (x == a);

    // Else difference between x and a
    // must be divisible by d.
    return ((x - a) % d == 0 && (x - a) / d >= 0);
}

// Driver code.
int main()
{
    int a = 1, x = 7, d = 3;
    if (isMember(a, d, x))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if x exist
// or not in the given AP.
class GFG {

    // returns yes if exist else no.
    static boolean isMember(int a, int d, int x)
    {

        // If difference is 0, then x must
        // be same as a.
        if (d == 0)
            return (x == a);

        // Else difference between x and a
        // must be divisible by d.
        return ((x - a) % d == 0 && (x - a) / d >= 0);
    }

    // Driver code.
    public static void main(String args[])
    {
        int a = 1, x = 7, d = 3;
        if (isMember(a, d, x))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by Nikita Tiwari
```

## 蟒蛇 3

```
# Python3 code to check if x exist
# or not in the given AP.

def isMember(a, d, x):

    # If difference is 0, then x
    # must be same as a.
    if d == 0:
        return x == a

    # Else difference between x
    # and a must be divisible by d.
    return ((x - a) % d == 0 and
        int((x - a) / d) >= 0)

# Driver code
a = 1
x = 7
d = 3

if isMember(a, d, x):
    print( "Yes")
else:
    print("No")

# This code is contributed by "Abhishek Sharma 44"
```

## C#

```
// C# program to check if x exist
// or not in the given AP.
using System;
class GFG {

    // returns yes if exist else no.
    static bool isMember(int a, int d, int x)
    {
        // If difference is 0, then x must
        // be same as a.
        if (d == 0)
            return (x == a);

        // Else difference between x and a
        // must be divisible by d.
        return ((x - a) % d == 0 && (x - a) / d >= 0);
    }

    // Driver code.
    public static void Main()
    {
        int a = 1, x = 7, d = 3;
        if (isMember(a, d, x))
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
// PHP program to check 
// if x exist or not in
// the given AP.

// returns yes if exist
// else no.
function isMember($a, $d, $x)
{

    // If difference is 0, then
    // x must be same as a
    if ($d == 0)
    return ($x == $a);

// Else difference between x
// and a must be divisible by d.
return (($x - $a) % $d == 0 &&
        ($x - $a) / $d >= 0);
}

// Driver code.
$a = 1; $x = 7; $d = 3;
if (isMember($a, $d, $x))
    echo "Yes";
else
    echo "No";

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>
    // Javascript program to check if x exist
    // or not in the given AP.

    // returns yes if exist else no.
    function isMember(a, d, x)
    {

        // If difference is 0, then x must
        // be same as a.
        if (d == 0)
            return (x == a);

        // Else difference between x and a
        // must be divisible by d.
        return ((x - a) % d == 0 && (x - a) / d >= 0);
    }

    let a = 1, x = 7, d = 3;
    if (isMember(a, d, x))
        document.write("Yes");
    else
        document.write("No");

    // This code is contributed by divyeshrabadiya07.
</script>
```

**输出:**

```
Yes
```