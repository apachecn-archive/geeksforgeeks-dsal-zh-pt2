# 判断给定的数字是否出现在无限序列中

> 原文:[https://www . geesforgeks . org/find-如果给定的数字存在于无限序列中，则不存在/](https://www.geeksforgeeks.org/find-if-the-given-number-is-present-in-the-infinite-sequence-or-not/)

给定三个整数 **A** 、 **B** 和 **C** 。在无限序列中， **A** 是**的第一个数字**， **C** 是**的共同区别**(S<sub>I</sub>–S<sub>I–1</sub>= C)。任务是检查编号 **B** 是否会出现在序列中。
**例:**

> **输入:** A = 1，B = 7，C = 3
> **输出:**是
> 顺序为 1，4，7，10，…
> **输入:** A = 1，B = -4，C = 5
> **输出:**否

**进场:**有两种情况:

1.  当 **C = 0** 时，如果 **A = B** 则打印**是**,否则打印**否**,因为序列只包含数字 **A**
2.  当 **C > 0** 时，对于任意非负整数 **k** 必须满足方程 **B = A + k * C** ，即**(B–A)/C**必须是非负整数。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if
// the sequence will contain B
bool doesContainB(int a, int b, int c)
{
    if (a == b)
        return true;

    if ((b - a) * c > 0 && (b - a) % c == 0)
        return true;

    return false;
}

// Driver code
int main()
{
    int a = 1, b = 7, c = 3;

    if (doesContainB(a, b, c))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function that returns true if
    // the sequence will contain B
    static boolean doesContainB(int a, int b, int c)
    {
        if (a == b)
        {
            return true;
        }

        if ((b - a) * c > 0 && (b - a) % c == 0)
        {
            return true;
        }

        return false;
    }

    // Driver code
    public static void main(String[] args)
    {
        int a = 1, b = 7, c = 3;

        if (doesContainB(a, b, c))
        {
            System.out.println("Yes");
        }
        else
        {
            System.out.println("No");
        }
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if
# the sequence will contain B
def doesContainB(a, b, c):
    if (a == b):
        return True

    if ((b - a) * c > 0 and (b - a) % c == 0):
        return True

    return False

# Driver code
if __name__ == '__main__':
    a, b, c = 1, 7, 3

    if (doesContainB(a, b, c)):
        print("Yes")
    else:
        print("No")

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns true if
    // the sequence will contain B
    static bool doesContainB(int a, int b, int c)
    {
        if (a == b)
        {
            return true;
        }

        if ((b - a) * c > 0 && (b - a) % c == 0)
        {
            return true;
        }

        return false;
    }

    // Driver code
    public static void Main()
    {
        int a = 1, b = 7, c = 3;

        if (doesContainB(a, b, c))
        {
            Console.WriteLine("Yes");
        }
        else
        {
            Console.WriteLine("No");
        }
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true if
// the sequence will contain B
function doesContainB($a, $b, $c)
{
    if ($a == $b)
        return true;

    if (($b - $a) * $c > 0 &&
        ($b - $a) % $c == 0)
        return true;

    return false;
}

// Driver code
$a = 1; $b = 7; $c = 3;

if (doesContainB($a, $b, $c))
    echo "Yes";
else
    echo "No";

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// javascript program for the above approach

    // Function that returns true if
    // the sequence will contain B
    function doesContainB(a, b, c)
    {
        if (a == b)
        {
            return true;
        }

        if ((b - a) * c > 0 && (b - a) % c == 0)
        {
            return true;
        }

        return false;
    }

// Driver Code

    let a = 1, b = 7, c = 3;

        if (doesContainB(a, b, c))
        {
            document.write("Yes");
        }
        else
        {
            document.write("No");
        }

</script>
```

**Output:** 

```
Yes
```