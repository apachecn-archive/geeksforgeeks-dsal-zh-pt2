# 平衡表达式所需的最小括号反转次数

> 原文:[https://www . geeksforgeeks . org/最小括号反转数-需要进行表达式平衡/](https://www.geeksforgeeks.org/minimum-number-of-bracket-reversals-needed-to-make-an-expression-balanced/)

给定的表达式只有“}”和“{ 0 }”。表达式可能不平衡。找到最小数量的括号反转，使表达式平衡。
**例:**

```
Input:  exp = "}{"
Output: 2
We need to change '}' to '{' and '{' to
'}' so that the expression becomes balanced, 
the balanced expression is '{}'

Input:  exp = "{{{"
Output: Can't be made balanced using reversals

Input:  exp = "{{{{"
Output: 2 

Input:  exp = "{{{{}}"
Output: 1 

Input:  exp = "}{{}}{{{"
Output: 3
```

一个简单的观察是，只有当括号总数为偶数(必须有相等数量的' { '和' }')
时，字符串才能平衡**天真的解决方案**是考虑每个括号，并通过两种情况递归地计算反转次数(I)保持括号不变(ii)反转括号。如果我们得到一个平衡的表达式，如果到达这里的步数小于目前为止的最小值，我们就更新结果。这个解的时间复杂度为 O(2 <sup>n</sup> )。

一个**高效解**可以在 O(n)时间内解决这个问题。这个想法是首先删除所有平衡的表达部分。例如，通过删除突出显示的部分，将“}**{ { }**{ { {”转换为“} { { }”。如果我们仔细看一下，我们可以注意到，在去掉平衡部分之后，我们总是以{ }…} { { }形式的表达式结束，该表达式包含 0 个或更多数量的右括号，后跟 0 个或更多数量的左括号。
一个表达式需要多少次最小反转..}{{..{" ?。设 m 为结束括号的总数，n 为开始括号的数量。我们需要⌈m/2⌉ + ⌈n/2⌉逆转。例如}}}}{{需要 2+1 次反转。
以下是上述想法的实现:

## C++14

```
// C++ program to find minimum number of
// reversals required to balance an expression
#include<bits/stdc++.h>
using namespace std;

// Returns count of minimum reversals for making
// expr balanced. Returns -1 if expr cannot be
// balanced.
int countMinReversals(string expr)
{
    int len = expr.length();

    // length of expression must be even to make
    // it balanced by using reversals.
    if (len%2)
       return -1;

    // After this loop, stack contains unbalanced
    // part of expression, i.e., expression of the
    // form "}}..}{{..{"
    stack<char> s;
    for (int i=0; i<len; i++)
    {
        if (expr[i]=='}' && !s.empty())
        {
            if (s.top()=='{')
                s.pop();
            else
                s.push(expr[i]);
        }
        else
            s.push(expr[i]);
    }

    // Length of the reduced expression
    // red_len = (m+n)
    int red_len = s.size();

    // count opening brackets at the end of
    // stack
    int n = 0;
    while (!s.empty() && s.top() == '{')
    {
        s.pop();
        n++;
    }

    // return ceil(m/2) + ceil(n/2) which is
    // actually equal to (m+n)/2 + n%2 when
    // m+n is even.
    return (red_len/2 + n%2);
}

// Driver program to test above function
int main()
{
   string expr = "}}{{";
   cout << countMinReversals(expr);
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java Code to count minimum reversal for
//making an expression balanced.

import java.util.Stack;

public class GFG
{

    // Method count minimum reversal for
    //making an expression balanced.
    //Returns -1 if expression cannot be balanced
    static int countMinReversals(String expr)
    {
        int len = expr.length();

        // length of expression must be even to make
        // it balanced by using reversals.
        if (len%2 != 0)
        return -1;

        // After this loop, stack contains unbalanced
        // part of expression, i.e., expression of the
        // form "}}..}{{..{"
        Stack<Character> s=new Stack<>();

        for (int i=0; i<len; i++)
        {
            char c = expr.charAt(i);
            if (c =='}' && !s.empty())
            {
                if (s.peek()=='{')
                    s.pop();
                else
                    s.push(c);
            }
            else
                s.push(c);
        }

        // Length of the reduced expression
        // red_len = (m+n)
        int red_len = s.size();

        // count opening brackets at the end of
        // stack
        int n = 0;
        while (!s.empty() && s.peek() == '{')
        {
            s.pop();
            n++;
        }

        // return ceil(m/2) + ceil(n/2) which is
        // actually equal to (m+n)/2 + n%2 when
        // m+n is even.
        return (red_len/2 + n%2);
    }

    // Driver method
    public static void main(String[] args)
    {
        String expr = "}}{{";

        System.out.println(countMinReversals(expr));
    }

}
//This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 program to find minimum number of
# reversals required to balance an expression

# Returns count of minimum reversals
# for making expr balanced. Returns -1
# if expr cannot be balanced.
def countMinReversals(expr):

    lenn = len(expr)

    # length of expression must be even
    # to make it balanced by using reversals.
    if (lenn % 2) :
        return -1

    # After this loop, stack contains
    # unbalanced part of expression, 
    # i.e., expression of the form "...."
    s = []
    for i in range(lenn):
        if (expr[i] =='' and len(s)):

            if (s[0] == '') :
                s.pop(0)
            else:
                s.insert(0, expr[i])
        else:
            s.insert(0, expr[i])

    # Length of the reduced expression
    # red_len = (m+n)
    red_len = len(s)

    # count opening brackets at the
    # end of stack
    n = 0
    while (len(s)and s[0] == '') :
            s.pop(0)
            n += 1

    # return ceil(m/2) + ceil(n/2) which
    # is actually equal to (m+n)/2 + n%2
    # when m+n is even.
    return (red_len // 2 + n % 2)

# Driver Code
if __name__ == '__main__':

    expr = "}}{{"
    print(countMinReversals(expr.strip()))

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# Code to count minimum reversal for
// making an expression balanced.
using System;
using System.Collections.Generic;

class GFG
{

// Method count minimum reversal for
// making an expression balanced.
// Returns -1 if expression cannot be balanced
public static int countMinReversals(string expr)
{
    int len = expr.Length;

    // length of expression must be
    // even to make it balanced by
    // using reversals.
    if (len % 2 != 0)
    {
        return -1;
    }

    // After this loop, stack contains
    // unbalanced part of expression,
    // i.e., expression of the form "}}..}{{..{"
    Stack<char> s = new Stack<char>();

    for (int i = 0; i < len; i++)
    {
        char c = expr[i];
        if (c == '}' && s.Count > 0)
        {
            if (s.Peek() == '{')
            {
                s.Pop();
            }
            else
            {
                s.Push(c);
            }
        }
        else
        {
            s.Push(c);
        }
    }

    // Length of the reduced expression
    // red_len = (m+n)
    int red_len = s.Count;

    // count opening brackets at
    // the end of stack
    int n = 0;
    while (s.Count > 0 && s.Peek() == '{')
    {
        s.Pop();
        n++;
    }

    // return ceil(m/2) + ceil(n/2) which is
    // actually equal to (m+n)/2 + n%2 when
    // m+n is even.
    return (red_len / 2 + n % 2);
}

// Driver Code
public static void Main(string[] args)
{
    string expr = "}}{{";

    Console.WriteLine(countMinReversals(expr));
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

        // JavaScript program to find minimum number of
        // reversals required to balance an expression

        // Returns count of minimum reversals for making
        // expr balanced. Returns -1 if expr cannot be
        // balanced.
        function countMinReversals(expr) {
            let len = expr.length;

            // Expressions of odd lengths
            // cannot be balanced
            if (len % 2)
                return -1;

            // After this loop, stack contains unbalanced
            // part of expression, i.e., expression of the
            // form "}}..}{{..{"
            var s = new Array();
            for (let i = 0; i < len; i++) {
                if (expr[i] == '}' && !s.length == 0) {
                    if (s[s.length - 1] == '{')
                        s.pop();
                    else
                        s.push(expr[i]);
                }
                else
                    s.push(expr[i]);
            }

            // Length of the reduced expression
            // red_len = (m+n)
            let red_len = s.length;

            // count opening brackets at the end of
            // stack
            let n = 0;
            while (!s.length == 0 && s[s.length - 1] == '{') {
                s.pop();
                n++;
            }

            // return ceil(m/2) + ceil(n/2) which is
            // actually equal to (m+n)/2 + n%2 when
            // m+n is even.
            return (red_len / 2 + n % 2);
        }

        // Driver program to test above function

        let expr = "}}{{";
        document.write(countMinReversals(expr));

</script>
```

**Output**

```
2
```