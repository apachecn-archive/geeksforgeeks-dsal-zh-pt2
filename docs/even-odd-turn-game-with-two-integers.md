# 两个整数的偶奇回合游戏

> 原文:[https://www . geesforgeks . org/双数双数游戏/](https://www.geeksforgeeks.org/even-odd-turn-game-with-two-integers/)

给定三个正整数 X，Y 和 P，这里 P 表示匝数。每当转弯是奇数时，X 乘以 2，在每一个偶数的转弯中，Y 乘以 2。任务是在完成 P 转后，找出最大(X，Y)值÷最小(X，Y)值。
**例:**

```
Input : X = 1, Y = 2, P = 1
Output : 1
As turn is odd, X is multiplied by
2 and becomes 2\. Now, X is 2 and Y is also 2\. 
Therefore, 2 ÷ 2 is 1.

Input : X = 3, Y = 7, p = 2
Output : 2
Here we have 2 turns. In the 1st turn which is odd
X is multiplied by 2\. And the values are 6 and 7\. 
In the next turn which is even Y is multiplied by 2.
Now the final values are 6 and 14\. Therefore, 14 ÷ 6 is 2.
```

让我们玩上面的游戏 8 回合:

```
| i    | 0 | 1  | 2  | 3  | 4  | 5  | 6  | 7   | 8   |
|------|---|----|----|----|----|----|----|-----|-----|
| X(i) | X | 2X | 2X | 4X | 4X | 8X | 8X | 16X | 16X |
| Y(i) | Y | Y  | 2Y | 2Y | 4Y | 4Y | 8Y | 8Y  | 16Y |
```

这里我们可以很容易地发现一个模式:

```
if i is even, then X(i) = z * X and Y(i) = z * Y.
if i is odd, then X(i) = 2*z * X and Y(i) = z * Y.
```

这里 z 实际上是 2 的幂。所以，我们可以简单地说–

```
If P is even output will be max(X, Y) ÷ min(X, Y) 
else output will be max(2*X, Y) ÷ min(2*X, Y).
```

下面是实现:

## C++

```
// CPP program to find max(X, Y) / min(X, Y)
// after P turns
#include <bits/stdc++.h>
using namespace std;

int findValue(int X, int Y, int P)
{
    if (P % 2 == 0)
        return (max(X, Y) / min(X, Y));

    else
        return (max(2 * X, Y) / min(2 * X, Y));
}

// Driver code
int main()
{
    // 1st test case
    int X = 1, Y = 2, P = 1;
    cout << findValue(X, Y, P) << endl;

    // 2nd test case
    X = 3, Y = 7, P = 2;
    cout << findValue(X, Y, P) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find max(X, Y) / min(X, Y)
// after P turns
import java.util.*;

class Even_odd{
    public static int findValue(int X, int Y,
                                        int P)
    {
        if (P % 2 == 0)
            return (Math.max(X, Y) /
                            Math.min(X, Y));

        else
            return (Math.max(2 * X, Y) /
                            Math.min(2 * X, Y));
    }

    public static void main(String[] args)
    {
        // 1st test case
        int X = 1, Y = 2, P = 1;
        System.out.println(findValue(X, Y, P));

        // 2nd test case
        X = 3;
        Y = 7;
        P = 2;
        System.out.print(findValue(X, Y, P));
    }
}

//This code is contributed by rishabh_jain
```

## 蟒蛇 3

```
# Python3 code to find max(X, Y) / min(X, Y)
# after P turns

def findValue( X , Y , P ):
    if P % 2 == 0:
        return int(max(X, Y) / min(X, Y))

    else:
        return int(max(2 * X, Y) / min(2 * X, Y))

# Driver code
# 1st test case
X = 1
Y = 2
P = 1
print(findValue(X, Y, P))

# 2nd test case
X = 3
Y = 7
P = 2
print((findValue(X, Y, P)))

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to find max(X, Y) / min(X, Y)
// after P turns
using System;

class GFG
{
    public static int findValue(int X, int Y,
                                        int P)
    {
        if (P % 2 == 0)
            return (Math.Max(X, Y) /
                    Math.Min(X, Y));

        else
            return (Math.Max(2 * X, Y) /
                    Math.Min(2 * X, Y));
    }

    // Driver code
    public static void Main()
    {
        // 1st test case
        int X = 1, Y = 2, P = 1;
        Console.WriteLine(findValue(X, Y, P));

        // 2nd test case
        X = 3;
        Y = 7;
        P = 2;
        Console.WriteLine(findValue(X, Y, P));
    }
}

//This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// max(X, Y) / min(X, Y)
// after P turns

function findValue($X, $Y, $P)
{
    if ($P % 2 == 0)
        return (int)(max($X, $Y) /
                     min($X, $Y));

    else
        return (int)(max(2 * $X, $Y) /
                     min(2 * $X, $Y));
}

// Driver code

// 1st test case
$X = 1;
$Y = 2;
$P = 1;
echo findValue($X, $Y, $P), "\n";

// 2nd test case
$X = 3; $Y = 7; $P = 2;
echo findValue($X, $Y, $P), "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript program to find max(X, Y) / min(X, Y)
    // after P turns

    function findValue(X, Y, P)
    {
        if (P % 2 == 0)
            return parseInt((Math.max(X, Y) / Math.min(X, Y)), 10);

        else
            return parseInt((Math.max(2 * X, Y) / Math.min(2 * X, Y)), 10);
    }

    // 1st test case
    let X = 1, Y = 2, P = 1;
    document.write(findValue(X, Y, P) + "</br>");

    // 2nd test case
    X = 3, Y = 7, P = 2;
    document.write(findValue(X, Y, P));

    // This code is contributed by divyeshrabadiya07.
</script>
```

**输出:**

```
1
2
```

**时间复杂度:** O(1)