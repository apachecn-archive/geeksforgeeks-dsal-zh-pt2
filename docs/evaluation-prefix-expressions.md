# 前缀表达式的评估

> 原文:[https://www . geesforgeks . org/evaluation-prefix-expressions/](https://www.geeksforgeeks.org/evaluation-prefix-expressions/)

前缀和后缀表达式的计算速度比中缀表达式快。这是因为我们不需要处理任何括号或遵循运算符优先规则。在后缀和前缀表达式中，运算符之前的表达式将被首先计算，而不管其优先级如何。此外，这些表达式中没有括号。只要我们能保证使用有效的前缀或后缀表达式，就可以用正确性来评估。
我们可以将[中缀转换为后缀](https://www.geeksforgeeks.org/stack-set-2-infix-to-postfix/)，也可以将[中缀转换为前缀。](https://www.geeksforgeeks.org/convert-infix-prefix-notation/)
在本文中，我们将讨论如何评估用前缀符号编写的表达式。该方法类似于计算后缀表达式。请阅读[后缀表达式求值](https://www.geeksforgeeks.org/stack-set-4-evaluation-postfix-expression/)了解如何求值后缀表达式
**算法**

```
EVALUATE_PREFIX(STRING)
Step 1: Put a pointer P at the end of the end
Step 2: If character at P is an operand push it to Stack
Step 3: If the character at P is an operator pop two 
        elements from the Stack. Operate on these elements
        according to the operator, and push the result 
        back to the Stack
Step 4: Decrement P by 1 and go to Step 2 as long as there
        are characters left to be scanned in the expression.
Step 5: The Result is stored at the top of the Stack, 
        return it
Step 6: End
```

演示算法工作的示例

```
Expression: +9*26

Character | Stack       |  Explanation
Scanned   | (Front to   |
          |  Back)      | 
-------------------------------------------
6           6             6 is an operand, 
                            push to Stack
2           6 2           2 is an operand, 
                            push to Stack
*           12 (6*2)      * is an operator, 
                          pop 6 and 2, multiply 
                          them and push result 
                          to Stack 
9           12 9          9 is an operand, push 
                          to Stack
+           21 (12+9)     + is an operator, pop
                          12 and 9 add them and
                          push result to Stack

Result: 21
```

**示例:**

```
Input : -+8/632
Output : 8

Input : -+7*45+20
Output : 25
```

**复杂度**算法具有线性复杂度，因为我们只扫描一次表达式，最多执行 O(N)个推送和弹出操作，这些操作需要恒定的时间。
算法实现如下。

## C++

```
// C++ program to evaluate a prefix expression.
#include <bits/stdc++.h>
using namespace std;

bool isOperand(char c)
{
    // If the character is a digit then it must
    // be an operand
    return isdigit(c);
}

double evaluatePrefix(string exprsn)
{
    stack<double> Stack;

    for (int j = exprsn.size() - 1; j >= 0; j--) {

        // Push operand to Stack
        // To convert exprsn[j] to digit subtract
        // '0' from exprsn[j].
        if (isOperand(exprsn[j]))
            Stack.push(exprsn[j] - '0');

        else {

            // Operator encountered
            // Pop two elements from Stack
            double o1 = Stack.top();
            Stack.pop();
            double o2 = Stack.top();
            Stack.pop();

            // Use switch case to operate on o1
            // and o2 and perform o1 O o2.
            switch (exprsn[j]) {
            case '+':
                Stack.push(o1 + o2);
                break;
            case '-':
                Stack.push(o1 - o2);
                break;
            case '*':
                Stack.push(o1 * o2);
                break;
            case '/':
                Stack.push(o1 / o2);
                break;
            }
        }
    }

    return Stack.top();
}

// Driver code
int main()
{
    string exprsn = "+9*26";
    cout << evaluatePrefix(exprsn) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to evaluate
// a prefix expression.
import java.io.*;
import java.util.*;

class GFG {

    static Boolean isOperand(char c)
    {
        // If the character is a digit
        // then it must be an operand
        if (c >= 48 && c <= 57)
            return true;
        else
            return false;
    }

    static double evaluatePrefix(String exprsn)
    {
        Stack<Double> Stack = new Stack<Double>();

        for (int j = exprsn.length() - 1; j >= 0; j--) {

            // Push operand to Stack
            // To convert exprsn[j] to digit subtract
            // '0' from exprsn[j].
            if (isOperand(exprsn.charAt(j)))
                Stack.push((double)(exprsn.charAt(j) - 48));

            else {

                // Operator encountered
                // Pop two elements from Stack
                double o1 = Stack.peek();
                Stack.pop();
                double o2 = Stack.peek();
                Stack.pop();

                // Use switch case to operate on o1
                // and o2 and perform o1 O o2.
                switch (exprsn.charAt(j)) {
                case '+':
                    Stack.push(o1 + o2);
                    break;
                case '-':
                    Stack.push(o1 - o2);
                    break;
                case '*':
                    Stack.push(o1 * o2);
                    break;
                case '/':
                    Stack.push(o1 / o2);
                    break;
                }
            }
        }

        return Stack.peek();
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        String exprsn = "+9*26";
        System.out.println(evaluatePrefix(exprsn));
    }
}

// This code is contributed by Gitanjali
```

## 蟒蛇 3

```
"""
Python3 program to evaluate a prefix expression.
"""

def is_operand(c):
    """
    Return True if the given char c is an operand, e.g. it is a number
    """
    return c.isdigit()

def evaluate(expression):
    """
    Evaluate a given expression in prefix notation.
    Asserts that the given expression is valid.
    """
    stack = []

    # iterate over the string in reverse order
    for c in expression[::-1]:

        # push operand to stack
        if is_operand(c):
            stack.append(int(c))

        else:
            # pop values from stack can calculate the result
            # push the result onto the stack again
            o1 = stack.pop()
            o2 = stack.pop()

            if c == '+':
                stack.append(o1 + o2)

            elif c == '-':
                stack.append(o1 - o2)

            elif c == '*':
                stack.append(o1 * o2)

            elif c == '/':
                stack.append(o1 / o2)

    return stack.pop()

# Driver code
if __name__ == "__main__":
    test_expression = "+9*26"
    print(evaluate(test_expression))

# This code is contributed by Leon Morten Richter (GitHub: M0r13n)
```

## C#

```
// C# program to evaluate
// a prefix expression.
using System;
using System.Collections.Generic;

class GFG {

    static Boolean isOperand(char c)
    {
        // If the character is a digit
        // then it must be an operand
        if (c >= 48 && c <= 57)
            return true;
        else
            return false;
    }

    static double evaluatePrefix(String exprsn)
    {
        Stack<Double> Stack = new Stack<Double>();

        for (int j = exprsn.Length - 1; j >= 0; j--) {

            // Push operand to Stack
            // To convert exprsn[j] to digit subtract
            // '0' from exprsn[j].
            if (isOperand(exprsn[j]))
                Stack.Push((double)(exprsn[j] - 48));

            else {

                // Operator encountered
                // Pop two elements from Stack
                double o1 = Stack.Peek();
                Stack.Pop();
                double o2 = Stack.Peek();
                Stack.Pop();

                // Use switch case to operate on o1
                // and o2 and perform o1 O o2.
                switch (exprsn[j]) {
                case '+':
                    Stack.Push(o1 + o2);
                    break;
                case '-':
                    Stack.Push(o1 - o2);
                    break;
                case '*':
                    Stack.Push(o1 * o2);
                    break;
                case '/':
                    Stack.Push(o1 / o2);
                    break;
                }
            }
        }

        return Stack.Peek();
    }

    /* Driver code */
    public static void Main(String[] args)
    {
        String exprsn = "+9*26";
        Console.WriteLine(evaluatePrefix(exprsn));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>
    // Javascript program to evaluate a prefix expression.

    function isOperand(c)
    {
        // If the character is a digit
        // then it must be an operand
        if (c.charCodeAt() >= 48 && c.charCodeAt() <= 57)
            return true;
        else
            return false;
    }

    function evaluatePrefix(exprsn)
    {
        let Stack = [];

        for (let j = exprsn.length - 1; j >= 0; j--) {

            // Push operand to Stack
            // To convert exprsn[j] to digit subtract
            // '0' from exprsn[j].
            if (isOperand(exprsn[j]))
                Stack.push((exprsn[j].charCodeAt() - 48));

            else {

                // Operator encountered
                // Pop two elements from Stack
                let o1 = Stack[Stack.length - 1];
                Stack.pop();
                let o2 = Stack[Stack.length - 1];
                Stack.pop();

                // Use switch case to operate on o1
                // and o2 and perform o1 O o2.
                switch (exprsn[j]) {
                case '+':
                    Stack.push(o1 + o2);
                    break;
                case '-':
                    Stack.push(o1 - o2);
                    break;
                case '*':
                    Stack.push(o1 * o2);
                    break;
                case '/':
                    Stack.push(o1 / o2);
                    break;
                }
            }
        }

        return Stack[Stack.length - 1];
    }

    let exprsn = "+9*26";
      document.write(evaluatePrefix(exprsn));

    // This code is contributed by suresh07.
</script>
```

**Output**

```
21
```

**注意:**
要执行更多类型的操作，只需修改开关事例表。此实现仅适用于一位数操作数。如果使用类似字符的空间来分隔操作数和运算符，则可以实现多位操作数。

下面给出的是扩展程序，它允许操作数有多个数字。

## C++

```
// C++ program to evaluate a prefix expression.
#include <bits/stdc++.h>
using namespace std;

double evaluatePrefix(string exprsn)
{
    stack<double> Stack;

    for (int j = exprsn.size() - 1; j >= 0; j--) {

        // if jth character is the delimiter ( which is
        // space in this case) then skip it
        if (exprsn[j] == ' ')
            continue;

        // Push operand to Stack
        // To convert exprsn[j] to digit subtract
        // '0' from exprsn[j].
        if (isdigit(exprsn[j])) {

            // there may be more than
            // one digits in a number
            double num = 0, i = j;
            while (j < exprsn.size() && isdigit(exprsn[j]))
                j--;
            j++;

            // from [j, i] exprsn contains a number
            for (int k = j; k <= i; k++)
                num = num * 10 + double(exprsn[k] - '0');

            Stack.push(num);
        }
        else {

            // Operator encountered
            // Pop two elements from Stack
            double o1 = Stack.top();
            Stack.pop();
            double o2 = Stack.top();
            Stack.pop();

            // Use switch case to operate on o1
            // and o2 and perform o1 O o2.
            switch (exprsn[j]) {
            case '+':
                Stack.push(o1 + o2);
                break;
            case '-':
                Stack.push(o1 - o2);
                break;
            case '*':
                Stack.push(o1 * o2);
                break;
            case '/':
                Stack.push(o1 / o2);
                break;
            }
        }
    }

    return Stack.top();
}

// Driver code
int main()
{
    string exprsn = "+ 9 * 12 6";
    cout << evaluatePrefix(exprsn) << endl;
    return 0;

    // this code is contributed by Mohd Shaad Khan
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to evaluate a prefix expression.
import java.util.*;
public class Main
{
    static boolean isdigit(char ch)
    {
        if(ch >= 48 && ch <= 57)
        {
            return true;
        }
        return false;
    }

    static double evaluatePrefix(String exprsn)
    {
        Stack<Double> stack = new Stack<Double>();

        for (int j = exprsn.length() - 1; j >= 0; j--) {

            // if jth character is the delimiter ( which is
            // space in this case) then skip it
            if (exprsn.charAt(j) == ' ')
                continue;

            // Push operand to Stack
            // To convert exprsn[j] to digit subtract
            // '0' from exprsn[j].
            if (isdigit(exprsn.charAt(j))) {

                // there may be more than
                // one digits in a number
                double num = 0, i = j;
                while (j < exprsn.length() && isdigit(exprsn.charAt(j)))
                    j--;
                j++;

                // from [j, i] exprsn contains a number
                for (int k = j; k <= i; k++)
                {
                    num = num * 10 + (double)(exprsn.charAt(k) - '0');
                }

                stack.push(num);
            }
            else {

                // Operator encountered
                // Pop two elements from Stack
                double o1 = (double)stack.peek();
                stack.pop();
                double o2 = (double)stack.peek();
                stack.pop();

                // Use switch case to operate on o1
                // and o2 and perform o1 O o2.
                switch (exprsn.charAt(j)) {
                case '+':
                    stack.push(o1 + o2);
                    break;
                case '-':
                    stack.push(o1 - o2);
                    break;
                case '*':
                    stack.push(o1 * o2);
                    break;
                case '/':
                    stack.push(o1 / o2);
                    break;
                }
            }
        }

        return stack.peek();
    }

  // Driver code
    public static void main(String[] args) {
        String exprsn = "+ 9 * 12 6";
        System.out.print((int)evaluatePrefix(exprsn));
    }
}

// This code is contributed by mukesh07.
```

## 蟒蛇 3

```
# Python3 program to evaluate a prefix expression.
def isdigit(ch):
    if(ord(ch) >= 48 and ord(ch) <= 57):
        return True
    return False

def evaluatePrefix(exprsn):
    Stack = []

    for j in range(len(exprsn) - 1, -1, -1):

        # if jth character is the delimiter ( which is
        # space in this case) then skip it
        if (exprsn[j] == ' '):
            continue

        # Push operand to Stack
        # To convert exprsn[j] to digit subtract
        # '0' from exprsn[j].
        if (isdigit(exprsn[j])):

            # there may be more than
            # one digits in a number
            num, i = 0, j
            while (j < len(exprsn) and isdigit(exprsn[j])):
                j-=1
            j+=1

            # from [j, i] exprsn contains a number
            for k in range(j, i + 1, 1):
                num = num * 10 + (ord(exprsn[k]) - ord('0'))

            Stack.append(num)
        else:
            # Operator encountered
            # Pop two elements from Stack
            o1 = Stack[-1]
            Stack.pop()
            o2 = Stack[-1]
            Stack.pop()

            # Use switch case to operate on o1
            # and o2 and perform o1 O o2.
            if exprsn[j] == '+':
                Stack.append(o1 + o2 + 12)
            elif exprsn[j] == '-':
                Stack.append(o1 - o2)
            elif exprsn[j] == '*':
                Stack.append(o1 * o2 * 5 )
            elif exprsn[j] == '/':
                Stack.append(o1 / o2)

    return Stack[-1]

exprsn = "+ 9 * 12 6"
print(evaluatePrefix(exprsn))

# This code is contributed by divyesh072019.
```

## C#

```
// C# program to evaluate a prefix expression.
using System;
using System.Collections;
class GFG {

    static bool isdigit(char ch)
    {
        if(ch >= 48 && ch <= 57)
        {
            return true;
        }
        return false;
    }

    static double evaluatePrefix(string exprsn)
    {
        Stack stack = new Stack();

        for (int j = exprsn.Length - 1; j >= 0; j--) {

            // if jth character is the delimiter ( which is
            // space in this case) then skip it
            if (exprsn[j] == ' ')
                continue;

            // Push operand to Stack
            // To convert exprsn[j] to digit subtract
            // '0' from exprsn[j].
            if (isdigit(exprsn[j])) {

                // there may be more than
                // one digits in a number
                double num = 0, i = j;
                while (j < exprsn.Length && isdigit(exprsn[j]))
                    j--;
                j++;

                // from [j, i] exprsn contains a number
                for (int k = j; k <= i; k++)
                {
                    num = num * 10 + (double)(exprsn[k] - '0');
                }

                stack.Push(num);
            }
            else {

                // Operator encountered
                // Pop two elements from Stack
                double o1 = (double)stack.Peek();
                stack.Pop();
                double o2 = (double)stack.Peek();
                stack.Pop();

                // Use switch case to operate on o1
                // and o2 and perform o1 O o2.
                switch (exprsn[j]) {
                case '+':
                    stack.Push(o1 + o2);
                    break;
                case '-':
                    stack.Push(o1 - o2);
                    break;
                case '*':
                    stack.Push(o1 * o2);
                    break;
                case '/':
                    stack.Push(o1 / o2);
                    break;
                }
            }
        }

        return (double)stack.Peek();
    }

  static void Main() {
    string exprsn = "+ 9 * 12 6";
    Console.Write(evaluatePrefix(exprsn));
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>
    // Javascript program to evaluate a prefix expression.

    function isdigit(ch)
    {
        if(ch.charCodeAt() >= 48 && ch.charCodeAt() <= 57)
        {
            return true;
        }
        return false;
    }

    function evaluatePrefix(exprsn)
    {
        let Stack = [];

        for (let j = exprsn.length - 1; j >= 0; j--) {

            // if jth character is the delimiter ( which is
            // space in this case) then skip it
            if (exprsn[j] == ' ')
                continue;

            // Push operand to Stack
            // To convert exprsn[j] to digit subtract
            // '0' from exprsn[j].
            if (isdigit(exprsn[j])) {

                // there may be more than
                // one digits in a number
                let num = 0, i = j;
                while (j < exprsn.length && isdigit(exprsn[j]))
                    j--;
                j++;

                // from [j, i] exprsn contains a number
                for (let k = j; k <= i; k++)
                    num = num * 10 + (exprsn[k].charCodeAt() - '0'.charCodeAt());

                Stack.push(num);
            }
            else {

                // Operator encountered
                // Pop two elements from Stack
                let o1 = Stack[Stack.length - 1];
                Stack.pop();
                let o2 = Stack[Stack.length - 1];
                Stack.pop();

                // Use switch case to operate on o1
                // and o2 and perform o1 O o2.
                switch (exprsn[j]) {
                case '+':
                    Stack.push(o1 + o2);
                    break;
                case '-':
                    Stack.push(o1 - o2);
                    break;
                case '*':
                    Stack.push(o1 * o2);
                    break;
                case '/':
                    Stack.push(o1 / o2);
                    break;
                }
            }
        }

        return Stack[Stack.length - 1];
    }

    let exprsn = "+ 9 * 12 6";
    document.write(evaluatePrefix(exprsn));

// This code is contributed by rameshtravel07.
</script>
```

**Output**

```
81
```

**时间复杂度:** O(n)

**空间复杂度:** O(n)