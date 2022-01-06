# 表情评价

> 原文:[https://www.geeksforgeeks.org/expression-evaluation/](https://www.geeksforgeeks.org/expression-evaluation/)

计算由字符串表示的表达式。表达式可以包含圆括号，您可以假设圆括号匹配良好。为简单起见，您可以假设只允许+、-、*和/二进制操作。算术表达式可以用三种形式之一编写:
*中缀符号:*运算符写在它们操作的操作数之间，例如 3 + 4。
*前缀符号:*运算符写在操作数之前，例如+ 3 4
*后缀符号:*运算符写在操作数之后。
由于需要额外的工作来决定优先级，中缀表达式对计算机来说更难评估。中缀符号是人类编写和识别表达式的方式，通常也是程序的输入。考虑到它们更难评估，它们通常会转换为其余两种形式之一。将中缀符号转换为后缀符号的一个非常著名的算法是埃德加·迪克斯特拉的[调车场算法](http://en.wikipedia.org/wiki/Shunting-yard_algorithm)。该算法将一个中缀表达式作为输入，并生成一个将该表达式转换为后缀表示法的队列。可以修改相同的算法，使其输出表达式的计算结果，而不是队列。诀窍是使用两个堆栈而不是一个，一个用于操作数，一个用于运算符。该算法在 http://www.cis.upenn.edu/ matuszek/cit 594-2002/Assignments/5-expressions . htm 上得到了简洁的描述，并在此进行了复制。(注意简洁的功劳归于所述页面的作者)

```
1\. While there are still tokens to be read in,
   1.1 Get the next token.
   1.2 If the token is:
       1.2.1 A number: push it onto the value stack.
       1.2.2 A variable: get its value, and push onto the value stack.
       1.2.3 A left parenthesis: push it onto the operator stack.
       1.2.4 A right parenthesis:
         1 While the thing on top of the operator stack is not a 
           left parenthesis,
             1 Pop the operator from the operator stack.
             2 Pop the value stack twice, getting two operands.
             3 Apply the operator to the operands, in the correct order.
             4 Push the result onto the value stack.
         2 Pop the left parenthesis from the operator stack, and discard it.
       1.2.5 An operator (call it thisOp):
         1 While the operator stack is not empty, and the top thing on the
           operator stack has the same or greater precedence as thisOp,
           1 Pop the operator from the operator stack.
           2 Pop the value stack twice, getting two operands.
           3 Apply the operator to the operands, in the correct order.
           4 Push the result onto the value stack.
         2 Push thisOp onto the operator stack.
2\. While the operator stack is not empty,
    1 Pop the operator from the operator stack.
    2 Pop the value stack twice, getting two operands.
    3 Apply the operator to the operands, in the correct order.
    4 Push the result onto the value stack.
3\. At this point the operator stack should be empty, and the value
   stack should have only one value in it, which is the final result.
```

应该清楚的是，该算法以线性时间运行——每个数字或运算符仅被推入堆栈一次，并从堆栈中弹出一次。另见[http://www2.lawrence.edu/fast/GREGGJ/CMSC270/Infix.html](http://www2.lawrence.edu/fast/GREGGJ/CMSC270/Infix.html)
T3】http://faculty.cs.niu.edu/~hutchins/csci241/eval.htm。
以下是上述算法的实现:

## C++

```
// CPP program to evaluate a given
// expression where tokens are
// separated by space.
#include <bits/stdc++.h>
using namespace std;

// Function to find precedence of
// operators.
int precedence(char op){
    if(op == '+'||op == '-')
    return 1;
    if(op == '*'||op == '/')
    return 2;
    return 0;
}

// Function to perform arithmetic operations.
int applyOp(int a, int b, char op){
    switch(op){
        case '+': return a + b;
        case '-': return a - b;
        case '*': return a * b;
        case '/': return a / b;
    }
}

// Function that returns value of
// expression after evaluation.
int evaluate(string tokens){
    int i;

    // stack to store integer values.
    stack <int> values;

    // stack to store operators.
    stack <char> ops;

    for(i = 0; i < tokens.length(); i++){

        // Current token is a whitespace,
        // skip it.
        if(tokens[i] == ' ')
            continue;

        // Current token is an opening
        // brace, push it to 'ops'
        else if(tokens[i] == '('){
            ops.push(tokens[i]);
        }

        // Current token is a number, push
        // it to stack for numbers.
        else if(isdigit(tokens[i])){
            int val = 0;

            // There may be more than one
            // digits in number.
            while(i < tokens.length() &&
                        isdigit(tokens[i]))
            {
                val = (val*10) + (tokens[i]-'0');
                i++;
            }

            values.push(val);

            // right now the i points to
            // the character next to the digit,
            // since the for loop also increases
            // the i, we would skip one
            //  token position; we need to
            // decrease the value of i by 1 to
            // correct the offset.
              i--;
        }

        // Closing brace encountered, solve
        // entire brace.
        else if(tokens[i] == ')')
        {
            while(!ops.empty() && ops.top() != '(')
            {
                int val2 = values.top();
                values.pop();

                int val1 = values.top();
                values.pop();

                char op = ops.top();
                ops.pop();

                values.push(applyOp(val1, val2, op));
            }

            // pop opening brace.
            if(!ops.empty())
               ops.pop();
        }

        // Current token is an operator.
        else
        {
            // While top of 'ops' has same or greater
            // precedence to current token, which
            // is an operator. Apply operator on top
            // of 'ops' to top two elements in values stack.
            while(!ops.empty() && precedence(ops.top())
                                >= precedence(tokens[i])){
                int val2 = values.top();
                values.pop();

                int val1 = values.top();
                values.pop();

                char op = ops.top();
                ops.pop();

                values.push(applyOp(val1, val2, op));
            }

            // Push current token to 'ops'.
            ops.push(tokens[i]);
        }
    }

    // Entire expression has been parsed at this
    // point, apply remaining ops to remaining
    // values.
    while(!ops.empty()){
        int val2 = values.top();
        values.pop();

        int val1 = values.top();
        values.pop();

        char op = ops.top();
        ops.pop();

        values.push(applyOp(val1, val2, op));
    }

    // Top of 'values' contains result, return it.
    return values.top();
}

int main() {
    cout << evaluate("10 + 2 * 6") << "\n";
    cout << evaluate("100 * 2 + 12") << "\n";
    cout << evaluate("100 * ( 2 + 12 )") << "\n";
    cout << evaluate("100 * ( 2 + 12 ) / 14");
    return 0;
}

// This code is contributed by Nikhil jindal.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* A Java program to evaluate a
   given expression where tokens
   are separated by space.
*/
import java.util.Stack;

public class EvaluateString
{
    public static int evaluate(String expression)
    {
        char[] tokens = expression.toCharArray();

         // Stack for numbers: 'values'
        Stack<Integer> values = new
                              Stack<Integer>();

        // Stack for Operators: 'ops'
        Stack<Character> ops = new
                              Stack<Character>();

        for (int i = 0; i < tokens.length; i++)
        {

            // Current token is a
            // whitespace, skip it
            if (tokens[i] == ' ')
                continue;

            // Current token is a number,
            // push it to stack for numbers
            if (tokens[i] >= '0' &&
                 tokens[i] <= '9')
            {
                StringBuffer sbuf = new
                            StringBuffer();

                // There may be more than one
                // digits in number
                while (i < tokens.length &&
                        tokens[i] >= '0' &&
                          tokens[i] <= '9')
                    sbuf.append(tokens[i++]);
                values.push(Integer.parseInt(sbuf.
                                      toString()));

                // right now the i points to
                // the character next to the digit,
                // since the for loop also increases
                // the i, we would skip one
                //  token position; we need to
                // decrease the value of i by 1 to
                // correct the offset.
                  i--;
            }

            // Current token is an opening brace,
            // push it to 'ops'
            else if (tokens[i] == '(')
                ops.push(tokens[i]);

            // Closing brace encountered,
            // solve entire brace
            else if (tokens[i] == ')')
            {
                while (ops.peek() != '(')
                  values.push(applyOp(ops.pop(),
                                   values.pop(),
                                 values.pop()));
                ops.pop();
            }

            // Current token is an operator.
            else if (tokens[i] == '+' ||
                     tokens[i] == '-' ||
                     tokens[i] == '*' ||
                        tokens[i] == '/')
            {
                // While top of 'ops' has same
                // or greater precedence to current
                // token, which is an operator.
                // Apply operator on top of 'ops'
                // to top two elements in values stack
                while (!ops.empty() &&
                       hasPrecedence(tokens[i],
                                    ops.peek()))
                  values.push(applyOp(ops.pop(),
                                   values.pop(),
                                 values.pop()));

                // Push current token to 'ops'.
                ops.push(tokens[i]);
            }
        }

        // Entire expression has been
        // parsed at this point, apply remaining
        // ops to remaining values
        while (!ops.empty())
            values.push(applyOp(ops.pop(),
                             values.pop(),
                           values.pop()));

        // Top of 'values' contains
        // result, return it
        return values.pop();
    }

    // Returns true if 'op2' has higher
    // or same precedence as 'op1',
    // otherwise returns false.
    public static boolean hasPrecedence(
                           char op1, char op2)
    {
        if (op2 == '(' || op2 == ')')
            return false;
        if ((op1 == '*' || op1 == '/') &&
            (op2 == '+' || op2 == '-'))
            return false;
        else
            return true;
    }

    // A utility method to apply an
    // operator 'op' on operands 'a'
    // and 'b'. Return the result.
    public static int applyOp(char op,
                           int b, int a)
    {
        switch (op)
        {
        case '+':
            return a + b;
        case '-':
            return a - b;
        case '*':
            return a * b;
        case '/':
            if (b == 0)
                throw new
                UnsupportedOperationException(
                      "Cannot divide by zero");
            return a / b;
        }
        return 0;
    }

    // Driver method to test above methods
    public static void main(String[] args)
    {
        System.out.println(EvaluateString.
                        evaluate("10 + 2 * 6"));
        System.out.println(EvaluateString.
                      evaluate("100 * 2 + 12"));
        System.out.println(EvaluateString.
                   evaluate("100 * ( 2 + 12 )"));
        System.out.println(EvaluateString.
             evaluate("100 * ( 2 + 12 ) / 14"));
    }
}
```

## 蟒蛇 3

```
# Python3 program to evaluate a given
# expression where tokens are
# separated by space.

# Function to find precedence
# of operators.
def precedence(op):

    if op == '+' or op == '-':
        return 1
    if op == '*' or op == '/':
        return 2
    return 0

# Function to perform arithmetic
# operations.
def applyOp(a, b, op):

    if op == '+': return a + b
    if op == '-': return a - b
    if op == '*': return a * b
    if op == '/': return a // b

# Function that returns value of
# expression after evaluation.
def evaluate(tokens):

    # stack to store integer values.
    values = []

    # stack to store operators.
    ops = []
    i = 0

    while i < len(tokens):

        # Current token is a whitespace,
        # skip it.
        if tokens[i] == ' ':
            i += 1
            continue

        # Current token is an opening
        # brace, push it to 'ops'
        elif tokens[i] == '(':
            ops.append(tokens[i])

        # Current token is a number, push
        # it to stack for numbers.
        elif tokens[i].isdigit():
            val = 0

            # There may be more than one
            # digits in the number.
            while (i < len(tokens) and
                tokens[i].isdigit()):

                val = (val * 10) + int(tokens[i])
                i += 1

            values.append(val)

            # right now the i points to
            # the character next to the digit,
            # since the for loop also increases
            # the i, we would skip one
            #  token position; we need to
            # decrease the value of i by 1 to
            # correct the offset.
              i-=1

        # Closing brace encountered,
        # solve entire brace.
        elif tokens[i] == ')':

            while len(ops) != 0 and ops[-1] != '(':

                val2 = values.pop()
                val1 = values.pop()
                op = ops.pop()

                values.append(applyOp(val1, val2, op))

            # pop opening brace.
            ops.pop()

        # Current token is an operator.
        else:

            # While top of 'ops' has same or
            # greater precedence to current
            # token, which is an operator.
            # Apply operator on top of 'ops'
            # to top two elements in values stack.
            while (len(ops) != 0 and
                precedence(ops[-1]) >=
                   precedence(tokens[i])):

                val2 = values.pop()
                val1 = values.pop()
                op = ops.pop()

                values.append(applyOp(val1, val2, op))

            # Push current token to 'ops'.
            ops.append(tokens[i])

        i += 1

    # Entire expression has been parsed
    # at this point, apply remaining ops
    # to remaining values.
    while len(ops) != 0:

        val2 = values.pop()
        val1 = values.pop()
        op = ops.pop()

        values.append(applyOp(val1, val2, op))

    # Top of 'values' contains result,
    # return it.
    return values[-1]

# Driver Code
if __name__ == "__main__":

    print(evaluate("10 + 2 * 6"))
    print(evaluate("100 * 2 + 12"))
    print(evaluate("100 * ( 2 + 12 )"))
    print(evaluate("100 * ( 2 + 12 ) / 14"))

# This code is contributed
# by Rituraj Jain
```

## C#

```
/* A C# program to evaluate a given
   expression where tokens
   are separated by space.
*/
using System;
using System.Collections.Generic;
using System.Text;

public class EvaluateString
{
    public static int evaluate(string expression)
    {
        char[] tokens = expression.ToCharArray();

         // Stack for numbers: 'values'
        Stack<int> values = new Stack<int>();

        // Stack for Operators: 'ops'
        Stack<char> ops = new Stack<char>();

        for (int i = 0; i < tokens.Length; i++)
        {
             // Current token is a whitespace, skip it
            if (tokens[i] == ' ')
            {
                continue;
            }

            // Current token is a number,
            // push it to stack for numbers
            if (tokens[i] >= '0' && tokens[i] <= '9')
            {
                StringBuilder sbuf = new StringBuilder();

                // There may be more than
                // one digits in number
                while (i < tokens.Length &&
                        tokens[i] >= '0' &&
                            tokens[i] <= '9')
                {
                    sbuf.Append(tokens[i++]);
                }
                values.Push(int.Parse(sbuf.ToString()));

                // Right now the i points to
                // the character next to the digit,
                // since the for loop also increases
                // the i, we would skip one
                //  token position; we need to
                // decrease the value of i by 1 to
                // correct the offset.
                  i--;
            }

            // Current token is an opening
            // brace, push it to 'ops'
            else if (tokens[i] == '(')
            {
                ops.Push(tokens[i]);
            }

            // Closing brace encountered,
            // solve entire brace
            else if (tokens[i] == ')')
            {
                while (ops.Peek() != '(')
                {
                  values.Push(applyOp(ops.Pop(),
                                   values.Pop(),
                                  values.Pop()));
                }
                ops.Pop();
            }

            // Current token is an operator.
            else if (tokens[i] == '+' ||
                     tokens[i] == '-' ||
                     tokens[i] == '*' ||
                     tokens[i] == '/')
            {

                // While top of 'ops' has same
                // or greater precedence to current
                // token, which is an operator.
                // Apply operator on top of 'ops'
                // to top two elements in values stack
                while (ops.Count > 0 &&
                         hasPrecedence(tokens[i],
                                     ops.Peek()))
                {
                  values.Push(applyOp(ops.Pop(),
                                   values.Pop(),
                                 values.Pop()));
                }

                // Push current token to 'ops'.
                ops.Push(tokens[i]);
            }
        }

        // Entire expression has been
        // parsed at this point, apply remaining
        // ops to remaining values
        while (ops.Count > 0)
        {
            values.Push(applyOp(ops.Pop(),
                             values.Pop(),
                            values.Pop()));
        }

        // Top of 'values' contains
        // result, return it
        return values.Pop();
    }

    // Returns true if 'op2' has
    // higher or same precedence as 'op1',
    // otherwise returns false.
    public static bool hasPrecedence(char op1,
                                     char op2)
    {
        if (op2 == '(' || op2 == ')')
        {
            return false;
        }
        if ((op1 == '*' || op1 == '/') &&
               (op2 == '+' || op2 == '-'))
        {
            return false;
        }
        else
        {
            return true;
        }
    }

    // A utility method to apply an
    // operator 'op' on operands 'a' 
    // and 'b'. Return the result.
    public static int applyOp(char op,
                            int b, int a)
    {
        switch (op)
        {
        case '+':
            return a + b;
        case '-':
            return a - b;
        case '*':
            return a * b;
        case '/':
            if (b == 0)
            {
                throw new
                System.NotSupportedException(
                       "Cannot divide by zero");
            }
            return a / b;
        }
        return 0;
    }

    // Driver method to test above methods
    public static void Main(string[] args)
    {
        Console.WriteLine(EvaluateString.
                     evaluate("10 + 2 * 6"));
        Console.WriteLine(EvaluateString.
                     evaluate("100 * 2 + 12"));
        Console.WriteLine(EvaluateString.
                   evaluate("100 * ( 2 + 12 )"));
        Console.WriteLine(EvaluateString.
               evaluate("100 * ( 2 + 12 ) / 14"));
    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
    /* A Javascript program to evaluate a given
       expression where tokens
       are separated by space.
    */

    function evaluate(expression)
    {
        let tokens = expression.split('');

         // Stack for numbers: 'values'
        let values = [];

        // Stack for Operators: 'ops'
        let ops = [];

        for (let i = 0; i < tokens.length; i++)
        {
             // Current token is a whitespace, skip it
            if (tokens[i] == ' ')
            {
                continue;
            }

            // Current token is a number,
            // push it to stack for numbers
            if (tokens[i] >= '0' && tokens[i] <= '9')
            {
                let sbuf = "";

                // There may be more than
                // one digits in number
                while (i < tokens.length &&
                        tokens[i] >= '0' &&
                            tokens[i] <= '9')
                {
                    sbuf = sbuf + tokens[i++];
                }
                values.push(parseInt(sbuf, 10));

                // Right now the i points to
                // the character next to the digit,
                // since the for loop also increases
                // the i, we would skip one
                //  token position; we need to
                // decrease the value of i by 1 to
                // correct the offset.
                  i--;
            }

            // Current token is an opening
            // brace, push it to 'ops'
            else if (tokens[i] == '(')
            {
                ops.push(tokens[i]);
            }

            // Closing brace encountered,
            // solve entire brace
            else if (tokens[i] == ')')
            {
                while (ops[ops.length - 1] != '(')
                {
                  values.push(applyOp(ops.pop(),
                                   values.pop(),
                                  values.pop()));
                }
                ops.pop();
            }

            // Current token is an operator.
            else if (tokens[i] == '+' ||
                     tokens[i] == '-' ||
                     tokens[i] == '*' ||
                     tokens[i] == '/')
            {

                // While top of 'ops' has same
                // or greater precedence to current
                // token, which is an operator.
                // Apply operator on top of 'ops'
                // to top two elements in values stack
                while (ops.length > 0 &&
                         hasPrecedence(tokens[i],
                                     ops[ops.length - 1]))
                {
                  values.push(applyOp(ops.pop(),
                                   values.pop(),
                                 values.pop()));
                }

                // Push current token to 'ops'.
                ops.push(tokens[i]);
            }
        }

        // Entire expression has been
        // parsed at this point, apply remaining
        // ops to remaining values
        while (ops.length > 0)
        {
            values.push(applyOp(ops.pop(),
                             values.pop(),
                            values.pop()));
        }

        // Top of 'values' contains
        // result, return it
        return values.pop();
    }

    // Returns true if 'op2' has
    // higher or same precedence as 'op1',
    // otherwise returns false.
    function hasPrecedence(op1, op2)
    {
        if (op2 == '(' || op2 == ')')
        {
            return false;
        }
        if ((op1 == '*' || op1 == '/') &&
               (op2 == '+' || op2 == '-'))
        {
            return false;
        }
        else
        {
            return true;
        }
    }

    // A utility method to apply an
    // operator 'op' on operands 'a'
    // and 'b'. Return the result.
    function applyOp(op, b, a)
    {
        switch (op)
        {
        case '+':
            return a + b;
        case '-':
            return a - b;
        case '*':
            return a * b;
        case '/':
            if (b == 0)
            {
                document.write("Cannot divide by zero");
            }
            return parseInt(a / b, 10);
        }
        return 0;
    }

    document.write(evaluate("10 + 2 * 6") + "</br>");
    document.write(evaluate("100 * 2 + 12") + "</br>");
    document.write(evaluate("100 * ( 2 + 12 )") + "</br>");
    document.write(evaluate("100 * ( 2 + 12 ) / 14") + "</br>");

// This code is contributed by decode2207.
</script>
```

**输出:**

```
22
212
1400
100
```

**时间复杂度:**O(n)
T3】空间复杂度: O(n)
更多测试用例的样本运行见[本](http://ideone.com/NEYfnD)。
本文由 **Ciphe** 整理。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论