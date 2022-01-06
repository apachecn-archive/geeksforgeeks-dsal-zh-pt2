# 使表达式平衡所需的最小括号反转次数|设置–2

> 原文:[https://www . geeksforgeeks . org/最小括号反转数-需要制作表达式-平衡集-2/](https://www.geeksforgeeks.org/minimum-number-of-bracket-reversals-needed-to-make-an-expression-balanced-set-2/)

给定的表达式只有“}”和“{ 0 }”。表达式可能不平衡。任务是找到最小数量的括号反转，使表达式平衡。
**例:**

```
Input : exp = "}{"
Output : 2
We need to change '}' to '{' and '{' to
'}' so that the expression becomes balanced, 
the balanced expression is '{}'

Input : exp = "}{{}}{{{"
Output : 3
The balanced expression is "{{{}}{}}"
```

在[之前的帖子](https://www.geeksforgeeks.org/minimum-number-of-bracket-reversals-needed-to-make-an-expression-balanced/)中讨论的解决方案需要 O(n)个额外空间。这个问题可以用常数空间来解决。
想法是用两个变量*打开*和*关闭*，其中，*打开*代表不平衡开括号的数量，*关闭*代表不平衡关括号的数量。
遍历字符串，如果当前字符是左括号增量*打开*。如果当前字符是右括号，则检查是否有不平衡的左括号(*打开* > 0)。如果是，则减少*打开*，否则增加*关闭*，因为该支架不平衡。
以下是上述办法的实施:

## C++

```
// C++ program to find minimum number of
// reversals required to balance an expression
#include <bits/stdc++.h>
using namespace std;

// Returns count of minimum reversals for making
// expr balanced. Returns -1 if expr cannot be
// balanced.
int countMinReversals(string expr)
{
    int len = expr.length();

    // length of expression must be even to make
    // it balanced by using reversals.
    if (len % 2)
        return -1;

    // To store number of reversals required.
    int ans = 0;

    int i;

    // To store number of unbalanced opening brackets.
    int open = 0;

    // To store number of unbalanced closing brackets.
    int close = 0;

    for (i = 0; i < len; i++) {

        // If current bracket is open then increment
        // open count.
        if (expr[i] == '{')
            open++;

        // If current bracket is close, check if it
        // balances opening bracket. If yes then
        // decrement count of unbalanced opening
        // bracket else increment count of
        // closing bracket.
        else {
            if (!open)
                close++;
            else
                open--;
        }
    }

    ans = (close / 2) + (open / 2);

    // For the case: "}{" or when one closing and
    // one opening bracket remains for pairing, then
    // both need to be reversed.
    close %= 2;
    open %= 2;
    if (close)
        ans += 2;

    return ans;
}

// Driver Code
int main()
{
    string expr = "}}{{";

    cout << countMinReversals(expr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum number of
// reversals required to balance an expression
class GFG
{

// Returns count of minimum reversals for making
// expr balanced. Returns -1 if expr cannot be
// balanced.
static int countMinReversals(String expr)
{
    int len = expr.length();

    // length of expression must be even to make
    // it balanced by using reversals.
    if (len % 2 != 0)
        return -1;

    // To store number of reversals required.
    int ans = 0;

    int i;

    // To store number of unbalanced opening brackets.
    int open = 0;

    // To store number of unbalanced closing brackets.
    int close = 0;

    for (i = 0; i < len; i++)
    {

        // If current bracket is open then increment
        // open count.
        if (expr.charAt(i) == '{')
            open++;

        // If current bracket is close, check if it
        // balances opening bracket. If yes then
        // decrement count of unbalanced opening
        // bracket else increment count of
        // closing bracket.
        else
        {
            if (open == 0)
                close++;
            else
                open--;
        }
    }

    ans = (close / 2) + (open / 2);

    // For the case: "}{" or when one closing and
    // one opening bracket remains for pairing, then
    // both need to be reversed.
    close %= 2;
    open %= 2;
    if (close != 0)
        ans += 2;

    return ans;
}

// Driver Code
public static void main(String args[])
{
    String expr = "}}{{";

    System.out.println(countMinReversals(expr));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find minimum number of
# reversals required to balance an expression

# Returns count of minimum reversals for
# making expr balanced. Returns -1 if
# expr cannot be balanced.
def countMinReversals(expr):

    length = len(expr)

    # length of expression must be even to
    # make it balanced by using reversals.
    if length % 2:
        return -1

    # To store number of reversals required.
    ans = 0

    # To store number of unbalanced
    # opening brackets.
    open = 0

    # To store number of unbalanced
    # closing brackets.
    close = 0

    for i in range(0, length):

        # If current bracket is open
        # then increment open count.
        if expr[i] == "":
            open += 1

        # If current bracket is close, check if it
        # balances opening bracket. If yes then
        # decrement count of unbalanced opening
        # bracket else increment count of
        # closing bracket.
        else:
            if not open:
                close += 1
            else:
                open -= 1

    ans = (close // 2) + (open // 2)

    # For the case: "" or when one closing
    # and one opening bracket remains for
    # pairing, then both need to be reversed.
    close %= 2
    open %= 2

    if close > 0:
        ans += 2

    return ans

# Driver Code
if __name__ == "__main__":

    expr = "}}{{"
    print(countMinReversals(expr))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find minimum number of
// reversals required to balance an expression
using System;

class GFG
{

// Returns count of minimum reversals for making
// expr balanced. Returns -1 if expr cannot be
// balanced.
static int countMinReversals(String expr)
{
    int len = expr.Length;

    // length of expression must be even to make
    // it balanced by using reversals.
    if (len % 2 != 0)
        return -1;

    // To store number of reversals required.
    int ans = 0;

    int i;

    // To store number of unbalanced opening brackets.
    int open = 0;

    // To store number of unbalanced closing brackets.
    int close = 0;

    for (i = 0; i < len; i++)
    {

        // If current bracket is open then increment
        // open count.
        if (expr[i] == '{')
            open++;

        // If current bracket is close, check if it
        // balances opening bracket. If yes then
        // decrement count of unbalanced opening
        // bracket else increment count of
        // closing bracket.
        else
        {
            if (open == 0)
                close++;
            else
                open--;
        }
    }

    ans = (close / 2) + (open / 2);

    // For the case: "}{" or when one closing and
    // one opening bracket remains for pairing, then
    // both need to be reversed.
    close %= 2;
    open %= 2;
    if (close != 0)
        ans += 2;

    return ans;
}

// Driver Code
public static void Main(String []args)
{
    String expr = "}}{{";

    Console.WriteLine(countMinReversals(expr));
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to find minimum number of
// reversals required to balance an expression

// Returns count of minimum reversals for making
// expr balanced. Returns -1 if expr cannot be
// balanced.
function countMinReversals(expr)
{
    var len = expr.length;

    // length of expression must be even to make
    // it balanced by using reversals.
    if (len % 2)
        return -1;

    // To store number of reversals required.
    var ans = 0;

    var i;

    // To store number of unbalanced opening brackets.
    var open = 0;

    // To store number of unbalanced closing brackets.
    var close = 0;

    for (i = 0; i < len; i++) {

        // If current bracket is open then increment
        // open count.
        if (expr[i] == '{')
            open++;

        // If current bracket is close, check if it
        // balances opening bracket. If yes then
        // decrement count of unbalanced opening
        // bracket else increment count of
        // closing bracket.
        else {
            if (!open)
                close++;
            else
                open--;
        }
    }

    ans = (close / 2) + (open / 2);

    // For the case: "}{" or when one closing and
    // one opening bracket remains for pairing, then
    // both need to be reversed.
    close %= 2;
    open %= 2;
    if (close)
        ans += 2;

    return ans;
}

// Driver Code
var expr = "}}{{";
document.write( countMinReversals(expr));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N)，其中 N 为字符串的长度。
**辅助空间:** O(1)