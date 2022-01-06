# 找出给定表达式的所有可能结果

> 原文:[https://www . geesforgeks . org/find-给定表达式的所有可能结果/](https://www.geeksforgeeks.org/find-all-possible-outcomes-of-a-given-expression/)

给定一个算术表达式，找出这个表达式的所有可能结果。通过在不同的地方放置括号来评估不同的结果。
我们可以假设给定表达式中的数字是个位数。
**例:**

```
Input:  1+3*2
Output: 8  7
Explanation
(1 + 3)*2     = 80
(1 + (3 * 2)) = 70

Input:  1*2+3*4
Output: 14 20 14 20 20
 (1*(2+(3*4))) =  14
 (1*((2+3)*4)) =  20 
 ((1*2)+(3*4)) =  14
 ((1*(2+3))*4) =  20
 ((1*2)+3)*4)  =  20
```

其思想是迭代给定表达式中的每个运算符。对于每个运算符，计算其左侧和右侧的所有可能值。对每对左侧和右侧值应用当前运算符，并将所有计算值添加到结果中。

```
1) Initialize result 'res' as empty.
2) Do following for every operator 'x'.
    a) Recursively evaluate all possible values on left of 'x'.
       Let the list of values be 'l'.  
    a) Recursively evaluate all possible values on right of 'x'.
       Let the list of values be 'r'.
    c) Loop through all values in list 'l'  
           loop through all values in list 'r'
               Apply current operator 'x' on current items of 
               'l' and 'r' and add the evaluated value to 'res'   
3) Return 'res'.
```

下面是上述算法的实现。

## C++

```
// C++ program to evaluate all possible values of
// a expression
#include<bits/stdc++.h>
using namespace std;

// Utility function to evaluate a simple expression
// with one operator only.
int eval(int a, char op, int b)
{
    if (op=='+')   return a+b;
    if (op=='-')   return a-b;
    if (op == '*') return a*b;
}

// This function evaluates all possible values and
// returns a list of evaluated values.
vector<int> evaluateAll(string expr, int low, int high)
{
    // To store result (all possible evaluations of
    // given expression 'expr')
    vector<int> res;

    // If there is only one character, it must
    // be a digit (or operand), return it.
    if (low == high)
    {
        res.push_back(expr[low] - '0');
        return res;
    }

    // If there are only three characters, middle
    // one must be operator and corner ones must be
    // operand
    if (low == (high-2))
    {
        int num = eval(expr[low]-'0', expr[low+1],
                       expr[low+2]-'0');

        res.push_back(num);
        return res;
    }

    // every i refers to an operator
    for (int i=low+1; i<=high; i+=2)
    {
        // l refers to all the possible values
        // in the left of operator 'expr[i]'
        vector<int> l = evaluateAll(expr, low, i-1);

        // r refers to all the possible values
        // in the right of operator 'expr[i]'
        vector<int> r = evaluateAll(expr, i+1, high);

        // Take above evaluated all possible
        // values in left side of 'i'
        for (int s1=0; s1<l.size(); s1++)
        {
            // Take above evaluated all possible
            // values in right side of 'i'
            for (int s2=0; s2<r.size(); s2++)
            {
                // Calculate value for every pair
                // and add the value to result.
                int val = eval(l[s1], expr[i], r[s2]);
                res.push_back(val);
            }
        }
    }
    return res;
}

// Driver program
int main()
{
    string expr = "1*2+3*4";
    int len = expr.length();
    vector<int> ans = evaluateAll(expr, 0, len-1);

    for (int i=0; i< ans.size(); i++)
        cout << ans[i] << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to evaluate all possible
// values of a expression
import java.util.*;

class GFG
{

    // Utility function to evaluate a simple expression
    // with one operator only.
    static int eval(int a, char op, int b)
    {
        if (op == '+')
        {
            return a + b;
        }
        if (op == '-')
        {
            return a - b;
        }
        if (op == '*')
        {
            return a * b;
        }
        return Integer.MAX_VALUE;
    }

    // This function evaluates all possible values and
    // returns a list of evaluated values.
    static Vector<Integer> evaluateAll(String expr,
                                    int low, int high)
    {
        // To store result (all possible evaluations of
        // given expression 'expr')
        Vector<Integer> res = new Vector<Integer>();

        // If there is only one character, it must
        // be a digit (or operand), return it.
        if (low == high)
        {
            res.add(expr.charAt(low) - '0');
            return res;
        }

        // If there are only three characters, middle
        // one must be operator and corner ones must be
        // operand
        if (low == (high - 2))
        {
            int num = eval(expr.charAt(low) - '0',
                         expr.charAt(low + 1),
                        expr.charAt(low + 2) - '0');

            res.add(num);
            return res;
        }

        // every i refers to an operator
        for (int i = low + 1; i <= high; i += 2)
        {

            // l refers to all the possible values
            // in the left of operator 'expr[i]'
            Vector<Integer> l = evaluateAll(expr, low, i - 1);

            // r refers to all the possible values
            // in the right of operator 'expr[i]'
            Vector<Integer> r = evaluateAll(expr, i + 1, high);

            // Take above evaluated all possible
            // values in left side of 'i'
            for (int s1 = 0; s1 < l.size(); s1++)
            {

                // Take above evaluated all possible
                // values in right side of 'i'
                for (int s2 = 0; s2 < r.size(); s2++)
                {

                    // Calculate value for every pair
                    // and add the value to result.
                    int val = eval(l.get(s1), expr.charAt(i), r.get(s2));
                    res.add(val);
                }
            }
        }
        return res;
    }

    // Driver program
    public static void main(String[] args)
    {
        String expr = "1*2+3*4";
        int len = expr.length();
        Vector<Integer> ans = evaluateAll(expr, 0, len - 1);

        for (int i = 0; i < ans.size(); i++)
        {
            System.out.println(ans.get(i));
        }
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to evaluate all
# possible values of a expression

# Utility function to evaluate a simple
# expression with one operator only.
def eval(a, op, b):

    if op == '+': return a + b
    if op == '-': return a - b
    if op == '*': return a * b

# This function evaluates all possible values
# and returns a list of evaluated values.
def evaluateAll(expr, low, high):

    # To store result (all possible
    # evaluations of given expression 'expr')
    res = []

    # If there is only one character,
    # it must be a digit (or operand),
    # return it.
    if low == high:

        res.append(int(expr[low]))
        return res

    # If there are only three characters,
    # middle one must be operator and 
    # corner ones must be operand
    if low == (high - 2):

        num = eval(int(expr[low]),
                       expr[low + 1],
                   int(expr[low + 2]))

        res.append(num)
        return res

    # every i refers to an operator
    for i in range(low + 1, high + 1, 2):

        # l refers to all the possible values
        # in the left of operator 'expr[i]'
        l = evaluateAll(expr, low, i - 1)

        # r refers to all the possible values
        # in the right of operator 'expr[i]'
        r = evaluateAll(expr, i + 1, high)

        # Take above evaluated all possible
        # values in left side of 'i'
        for s1 in range(0, len(l)):

            # Take above evaluated all possible
            # values in right side of 'i'
            for s2 in range(0, len(r)):

                # Calculate value for every pair
                # and add the value to result.
                val = eval(l[s1], expr[i], r[s2])
                res.append(val)

    return res

# Driver Code
if __name__ == "__main__":

    expr = "1*2+3*4"
    length = len(expr)
    ans = evaluateAll(expr, 0, length - 1)

    for i in range(0, len(ans)):
        print(ans[i])

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to evaluate all possible
// values of a expression
using System;
using System.Collections.Generic;

class GFG
{

    // Utility function to evaluate a simple expression
    // with one operator only.
    static int eval(int a, char op, int b)
    {
        if (op == '+')
        {
            return a + b;
        }
        if (op == '-')
        {
            return a - b;
        }
        if (op == '*')
        {
            return a * b;
        }
        return int.MaxValue;
    }

    // This function evaluates all possible values and
    // returns a list of evaluated values.
    static List<int> evaluateAll(String expr,
                                    int low, int high)
    {
        // To store result (all possible evaluations of
        // given expression 'expr')
        List<int> res = new List<int> ();

        // If there is only one character, it must
        // be a digit (or operand), return it.
        if (low == high)
        {
            res.Add(expr[low] - '0');
            return res;
        }

        // If there are only three characters, middle
        // one must be operator and corner ones must be
        // operand
        if (low == (high - 2))
        {
            int num = eval(expr[low] - '0',
                        expr[low + 1],
                        expr[low + 2] - '0');

            res.Add(num);
            return res;
        }

        // every i refers to an operator
        for (int i = low + 1; i <= high; i += 2)
        {

            // l refers to all the possible values
            // in the left of operator 'expr[i]'
            List<int> l = evaluateAll(expr, low, i - 1);

            // r refers to all the possible values
            // in the right of operator 'expr[i]'
            List<int> r = evaluateAll(expr, i + 1, high);

            // Take above evaluated all possible
            // values in left side of 'i'
            for (int s1 = 0; s1 < l.Count; s1++)
            {

                // Take above evaluated all possible
                // values in right side of 'i'
                for (int s2 = 0; s2 < r.Count; s2++)
                {

                    // Calculate value for every pair
                    // and add the value to result.
                    int val = eval(l[s1], expr[i], r[s2]);
                    res.Add(val);
                }
            }
        }
        return res;
    }

    // Driver code
    public static void Main()
    {
        String expr = "1*2+3*4";
        int len = expr.Length;
        List<int> ans = evaluateAll(expr, 0, len - 1);

        for (int i = 0; i < ans.Count; i++)
        {
            Console.WriteLine(ans[i]);
        }
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to evaluate all possible
// values of a expression

// Utility function to eval1uate a simple
// expression with one operator only.
function eval1($a, $op, $b)
{
    if ($op == '+') return $a + $b;
    if ($op == '-') return $a - $b;
    if ($op == '*') return $a * $b;
}

// This function eval1uates all possible values
// and returns a list of eval1uated values.
function eval1uateAll($expr, $low, $high)
{
    // To store result (all possible
    // evaluations of given expression 'expr')
    $res = array();

    // If there is only one character, it must
    // be a digit (or operand), return it.
    if ($low == $high)
    {
        array_push($res, ord($expr[$low]) -
                         ord('0'));
        return $res;
    }

    // If there are only three characters,
    // middle one must be operator and
    // corner ones must be operand
    if ($low == ($high - 2))
    {
        $num = eval1(ord($expr[$low]) -
                     ord('0'), $expr[$low + 1],
                     ord($expr[$low + 2]) -
                     ord('0'));

        array_push($res, $num);
        return $res;
    }

    // every i refers to an operator
    for ($i = $low + 1; $i <= $high; $i += 2)
    {
        // l refers to all the possible values
        // in the left of operator 'expr[i]'
        $l = eval1uateAll($expr, $low, $i - 1);

        // r refers to all the possible values
        // in the right of operator 'expr[i]'
        $r = eval1uateAll($expr, $i + 1, $high);

        // Take above eval1uated all possible
        // values in left side of 'i'
        for ($s1 = 0; $s1 < count($l); $s1++)
        {
            // Take above eval1uated all possible
            // values in right side of 'i'
            for ($s2 = 0; $s2 < count($r); $s2++)
            {
                // Calculate value for every pair
                // and add the value to result.
                $val = eval1($l[$s1],
                             $expr[$i], $r[$s2]);
                array_push($res, $val);
            }
        }
    }
    return $res;
}

// Driver Code
$expr = "1*2+3*4";
$len = strlen($expr);
$ans = eval1uateAll($expr, 0, $len - 1);

for ($i = 0; $i < count($ans); $i++)
    echo $ans[$i] . "\n";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to evaluate all possible
// values of a expression

// Utility function to evaluate a simple expression
    // with one operator only.
function eval(a,op,b)
{
    if (op == '+')
        {
            return a + b;
        }
        if (op == '-')
        {
            return a - b;
        }
        if (op == '*')
        {
            return a * b;
        }
        return Number.MAX_VALUE;
}

// This function evaluates all possible values and
    // returns a list of evaluated values.
function evaluateAll(expr,low,high)
{
    // To store result (all possible evaluations of
        // given expression 'expr')
        let res = [];

        // If there is only one character, it must
        // be a digit (or operand), return it.
        if (low == high)
        {
            res.push(expr[low] - '0');
            return res;
        }

        // If there are only three characters, middle
        // one must be operator and corner ones must be
        // operand
        if (low == (high - 2))
        {
            let num = eval(expr[low] - '0',
                         expr[low + 1],
                        expr[low + 2] - '0');

            res.push(num);
            return res;
        }

        // every i refers to an operator
        for (let i = low + 1; i <= high; i += 2)
        {

            // l refers to all the possible values
            // in the left of operator 'expr[i]'
            let l = evaluateAll(expr, low, i - 1);

            // r refers to all the possible values
            // in the right of operator 'expr[i]'
            let r = evaluateAll(expr, i + 1, high);

            // Take above evaluated all possible
            // values in left side of 'i'
            for (let s1 = 0; s1 < l.length; s1++)
            {

                // Take above evaluated all possible
                // values in right side of 'i'
                for (let s2 = 0; s2 < r.length; s2++)
                {

                    // Calculate value for every pair
                    // and add the value to result.
                    let val = eval(l[s1], expr[i], r[s2]);
                    res.push(val);
                }
            }
        }
        return res;
}

// Driver program
let  expr = "1*2+3*4";
let len = expr.length;
let ans = evaluateAll(expr, 0, len - 1);
for (let i = 0; i < ans.length; i++)
{
    document.write(ans[i]+"<br>");
}

// This code is contributed by rag2127
</script>
```

**输出:**

```
14
20
14
20
20
```

**练习:**扩展上述解决方案，使其也适用于多位数的数字。例如，像“100*30+20”这样的表达式(提示:我们可以创建一个整数数组来存储给定表达式的所有操作数和运算符)。
本文由[T4【Ekta Goel](https://www.linkedin.com/pub/ekta-goel/75/12a/3a6)供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。