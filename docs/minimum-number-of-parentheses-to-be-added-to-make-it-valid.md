# 使其有效的最小括号数

> 原文:[https://www . geesforgeks . org/要使其有效的最小括号数/](https://www.geeksforgeeks.org/minimum-number-of-parentheses-to-be-added-to-make-it-valid/)

给定一串括号“(”或“)”其中，![0\leq len(S)\leq 1000  ](img/6c8850f9fe082c9e57e22593f401751a.png "Rendered by QuickLaTeX.com")。任务是找到最小数量的括号'('或')'(在任何位置)我们必须添加，以使结果括号字符串有效。
**例:**

```
Input: str = "())"
Output: 1
One '(' is required at beginning.

Input: str = "((("
Output: 3
Three ')' is required at end.
```

**方法:**我们跟踪字符串的平衡情况，即“(‘减’的数量)”。如果字符串的余额为 0，并且每个前缀都有非负余额，则该字符串有效。
现在，考虑 s 的每个前缀的平衡。如果它是负的(比如，-1)，我们必须在开头添加一个'('括号。还有，如果 S 的余额是正数(比如+P)，我们必须在末尾加 P 倍')'括号。
**以下是上述方法的实施:**

## C++

```
// C++ Program to find minimum number of '(' or ')'
// must be added to make Parentheses string valid.
#include <bits/stdc++.h>
using namespace std;

// Function to return required minimum number
int minParentheses(string p)
{

    // maintain balance of string
    int bal = 0;
    int ans = 0;

    for (int i = 0; i < p.length(); ++i) {

        bal += p[i] == '(' ? 1 : -1;

        // It is guaranteed bal >= -1
        if (bal == -1) {
            ans += 1;
            bal += 1;
        }
    }

    return bal + ans;
}

// Driver code
int main()
{

    string p = "())";

    // Function to print required answer
    cout << minParentheses(p);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find minimum number of '(' or ')'
// must be added to make Parentheses string valid.

public class GFG {

    // Function to return required minimum number
    static int minParentheses(String p)
    {

        // maintain balance of string
        int bal = 0;
        int ans = 0;

        for (int i = 0; i < p.length(); ++i) {

            bal += p.charAt(i) == '(' ? 1 : -1;

            // It is guaranteed bal >= -1
            if (bal == -1) {
                ans += 1;
                bal += 1;
            }
        }

        return bal + ans;
    }

    public static void main(String args[])
    {
        String p = "())";

        // Function to print required answer
        System.out.println(minParentheses(p));

    }
    // This code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python3 Program to find
# minimum number of '(' or ')'
# must be added to make Parentheses
# string valid.

# Function to return required
# minimum number
def minParentheses(p):

    # maintain balance of string
    bal=0
    ans=0
    for i in range(0,len(p)):
        if(p[i]=='('):
            bal+=1
        else:
            bal+=-1

        # It is guaranteed bal >= -1
        if(bal==-1):
            ans+=1
            bal+=1
    return bal+ans

# Driver code
if __name__=='__main__':
    p = "())"

# Function to print required answer
    print(minParentheses(p))

# this code is contributed by
# sahilshelangia
```

## C#

```
// C# Program to find minimum number
// of '(' or ')' must be added to
// make Parentheses string valid.
using System;

class GFG
{
// Function to return required
// minimum number
static int minParentheses(string p)
{

    // maintain balance of string
    int bal = 0;
    int ans = 0;

    for (int i = 0; i < p.Length; ++i)
    {

        bal += p[i] == '(' ? 1 : -1;

        // It is guaranteed bal >= -1
        if (bal == -1)
        {
            ans += 1;
            bal += 1;
        }
    }

    return bal + ans;
}

// Driver code
public static void Main()
{
    string p = "())";

    // Function to print required answer
    Console.WriteLine(minParentheses(p));
}
}

// This code is contributed
// by Kirti_Mangal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find minimum number of
// '(' or ')' must be added to make
// Parentheses string valid.

// Function to return required minimum number
function minParentheses($p)
{

    // maintain balance of string
    $bal = 0;
    $ans = 0;

    for ($i = 0; $i < strlen($p); ++$i)
    {
        if ($p[$i] == '(' )
            $bal += 1 ;
        else
            $bal += -1;

        // It is guaranteed bal >= -1
        if ($bal == -1)
        {
            $ans += 1;
            $bal += 1;
        }
    }

    return $bal + $ans;
}

// Driver code
$p = "())";

// Function to print required answer
echo minParentheses($p);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript Program to find minimum number of '(' or ')'
// must be added to make Parentheses string valid.

// Function to return required minimum number
function minParentheses( p)
{

    // maintain balance of string
    var bal = 0;
    var ans = 0;

    for (var i = 0; i < p.length; ++i) {

        bal += p[i] == '(' ? 1 : -1;

        // It is guaranteed bal >= -1
        if (bal == -1) {
            ans += 1;
            bal += 1;
        }
    }

    return bal + ans;
}

var p = "())";

// Function to print required answer
document.write( minParentheses(p));

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(N)，其中 N 为 s 的长度
T3】空间复杂度: O(1)。