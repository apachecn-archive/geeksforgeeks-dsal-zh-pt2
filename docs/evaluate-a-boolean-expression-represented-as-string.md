# 计算表示为字符串的布尔表达式

> 原文:[https://www . geesforgeks . org/evaluate-a-boolean-expression-presented-as-string/](https://www.geeksforgeeks.org/evaluate-a-boolean-expression-represented-as-string/)

给定一个仅由 0、1、A、B、C 组成的字符串，其中
A = AND
B = OR
C = XOR
计算该字符串的值，假设没有优先顺序，并且从左到右进行计算。
限制条件——绳子的长度是奇数。它将始终是一个有效的字符串。
示例，1AA0 将不作为输入给出。

**示例:**

```
Input : 1A0B1
Output : 1
1 AND 0 OR 1 = 1

Input : 1C1B1B0A0
Output : 0
```

来源:微软 2017 年在线实习

其思想是通过在每次迭代后跳转一个字符来遍历所有操作数。对于当前操作数 str[i]，检查 str[i+1]和 str[i+2]的值，从而决定当前子表达式的值。

## C++

```
// C++ program to evaluate value of an expression.
#include <bits/stdc++.h>

using namespace std;

int evaluateBoolExpr(string s)
{
    int n = s.length();

    // Traverse all operands by jumping
    // a character after every iteration.
    for (int i = 0; i < n; i += 2) {

        // If operator next to current operand
        // is AND.
        if (s[i + 1] == 'A') {
            if (s[i + 2] == '0'|| s[i] == '0')
                s[i + 2] = '0';
            else
                s[i + 2] = '1';
        }

        // If operator next to current operand
        // is OR.
        else if (s[i + 1] == 'B') {
            if (s[i + 2] == '1'|| s[i] == '1')
                s[i + 2] = '1';
            else
                s[i + 2] = '0';
        }

        // If operator next to current operand
        // is XOR (Assuming a valid input)
        else {
            if (s[i + 2] == s[i])
                s[i + 2] = '0';
            else
                s[i + 2] = '1';
        }
    }
    return s[n - 1] -'0';
}

// Driver code
int main()
{
    string s = "1C1B1B0A0";
    cout << evaluateBoolExpr(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to evaluate value of an expression.
public class Evaluate_BoolExp {

    // Evaluates boolean expression
    // and returns the result
    static int evaluateBoolExpr(StringBuffer s)
    {
        int n = s.length();

        // Traverse all operands by jumping
        // a character after every iteration.
        for (int i = 0; i < n; i += 2) {

            // If operator next to current operand
            // is AND.
            if( i + 1 < n && i + 2 < n)
            {
                if (s.charAt(i + 1) == 'A') {
                    if (s.charAt(i + 2) == '0' ||
                            s.charAt(i) == 0)
                        s.setCharAt(i + 2, '0');
                    else
                        s.setCharAt(i + 2, '1');
                }

                // If operator next to current operand
                // is OR.
                else if ((i + 1) < n &&
                           s.charAt(i + 1 ) == 'B') {
                    if (s.charAt(i + 2) == '1' ||
                          s.charAt(i) == '1')
                        s.setCharAt(i + 2, '1');
                    else
                        s.setCharAt(i + 2, '0');
                }

                // If operator next to current operand
                // is XOR (Assuming a valid input)
                else {
                    if (s.charAt(i + 2) == s.charAt(i))
                        s.setCharAt(i + 2, '0');
                    else
                        s.setCharAt(i + 2 ,'1');
                }
            }
        }
        return s.charAt(n - 1) - '0';
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "1C1B1B0A0";
        StringBuffer sb = new StringBuffer(s);
        System.out.println(evaluateBoolExpr(sb));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 program to evaluate value
# of an expression.
import math as mt

def evaluateBoolExpr(s):

    n = len(s)

    # Traverse all operands by jumping
    # a character after every iteration.
    for i in range(0, n - 2, 2):

        # If operator next to current
        # operand is AND.'''
        if (s[i + 1] == "A"):

            if (s[i + 2] == "0" or s[i] == "0"):
                s[i + 2] = "0"
            else:
                s[i + 2] = "1"

        # If operator next to current
        # operand is OR.
        elif (s[i + 1] == "B"):
            if (s[i + 2] == "1" or s[i] == "1"):
                s[i + 2] = "1"
            else:
                s[i + 2] = "0"

        # If operator next to current operand
        # is XOR (Assuming a valid input)
        else:
            if (s[i + 2] == s[i]):
                s[i + 2] = "0"
            else:
                s[i + 2] = "1"

    return ord(s[n - 1]) - ord("0")

# Driver code
s = "1C1B1B0A0"
string=[s[i] for i in range(len(s))]
print(evaluateBoolExpr(string))

# This code is contributed
# by mohit kumar 29
```

## C#

```
// C# program to evaluate value
// of an expression.
using System;
using System.Text;

class GFG
{

// Evaluates boolean expression
// and returns the result
public static int evaluateBoolExpr(StringBuilder s)
{
    int n = s.Length;

    // Traverse all operands by jumping
    // a character after every iteration.
    for (int i = 0; i < n; i += 2)
    {

        // If operator next to current
        // operand is AND.
        if (i + 1 < n && i + 2 < n)
        {
            if (s[i + 1] == 'A')
            {
                if (s[i + 2] == '0' || s[i] == 0)
                {
                    s[i + 2] = '0';
                }
                else
                {
                    s[i + 2] = '1';
                }
            }

            // If operator next to current
            // operand is OR.
            else if ((i + 1) < n && s[i + 1] == 'B')
            {
                if (s[i + 2] == '1' || s[i] == '1')
                {
                    s[i + 2] = '1';
                }
                else
                {
                    s[i + 2] = '0';
                }
            }

            // If operator next to current operand
            // is XOR (Assuming a valid input)
            else
            {
                if (s[i + 2] == s[i])
                {
                    s[i + 2] = '0';
                }
                else
                {
                    s[i + 2] = '1';
                }
            }
        }
    }
    return s[n - 1] - '0';
}

// Driver code
public static void Main(string[] args)
{
    string s = "1C1B1B0A0";
    StringBuilder sb = new StringBuilder(s);
    Console.WriteLine(evaluateBoolExpr(sb));
}
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to evaluate value
// of an expression.

function evaluateBoolExpr($s)
{
    $n = strlen($s);

    // Traverse all operands by jumping
    // a character after every iteration.
    for ($i = 0; $i < $n; $i += 2)
    {

        // If operator next to current operand
        // is AND.
        if (($i + 1) < $n  && $s[$i + 1] == 'A')
        {
            if ($s[$i + 2] == '0'|| $s[$i] == '0')
                $s[$i + 2] = '0';
            else
                $s[$i + 2] = '1';
        }

        // If operator next to current operand
        // is OR.
        else if (($i + 1) < $n  && $s[$i + 1] == 'B')
        {
            if ($s[$i + 2] == '1'|| $s[$i] == '1')
                $s[$i + 2] = '1';
            else
                $s[$i + 2] = '0';
        }

        // If operator next to current operand
        // is XOR (Assuming a valid input)
        else
        {
            if (($i + 2) < $n  && $s[$i + 2] == $s[$i])
                $s[$i + 2] = '0';
            else
                $s[$i + 2] = '1';
        }
    }
    return $s[$n - 1] -'0';
}

// Driver code
$s = "1C1B1B0A0";
echo evaluateBoolExpr($s);

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>

// Javascript program to evaluate
// value of an expression.

// Evaluates boolean expression
// and returns the result
function evaluateBoolExpr(s)
{
    let n = s.length;

    // Traverse all operands by jumping
    // a character after every iteration.
    for(let i = 0; i < n; i += 2)
    {

        // If operator next to current
        // operand is AND.
        if (i + 1 < n && i + 2 < n)
        {
            if (s[i + 1] == 'A')
            {
                if (s[i + 2] == '0' ||
                    s[i] == 0)
                {
                    s[i + 2] = '0';
                }
                else
                {
                    s[i + 2] = '1';
                }
            }

            // If operator next to current
            // operand is OR.
            else if ((i + 1) < n && s[i + 1] == 'B')
            {
                if (s[i + 2] == '1' || s[i] == '1')
                {
                    s[i + 2] = '1';
                }
                else
                {
                    s[i + 2] = '0';
                }
            }

            // If operator next to current operand
            // is XOR (Assuming a valid input)
            else
            {
                if (s[i + 2] == s[i])
                {
                    s[i + 2] = '0';
                }
                else
                {
                    s[i + 2] = '1';
                }
            }
        }
    }
    return (s[n - 1].charCodeAt() -
                 '0'.charCodeAt());
}

// Driver code
let s = "1C1B1B0A0";
let sb = s.split('');

document.write(evaluateBoolExpr(sb) + "</br>");

// This code is contributed by rameshtravel07

</script>
```

**输出:**

```
0
```

本文由 **Ayushi Jain** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。