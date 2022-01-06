# 表达式是否包含冗余括号

> 原文:[https://www . geesforgeks . org/expression-contains-redundancy-方括号-not/](https://www.geeksforgeeks.org/expression-contains-redundant-bracket-not/)

给定一串平衡表达式，查找它是否包含多余的括号。如果同一个子表达式被不必要的或多个括号包围，则一组括号是多余的。如果多余，则打印“是”，否则打印“否”。
**注意:**表达式可能包含“ **+** ”、“ ***** ”、“**–**”和“ **/** ”运算符。给定的表达式为**有效**，并且不存在**白色**空格。
**例:**

```
Input: 
((a+b))
(a+(b)/c)
(a+b*(c-d))
Output: 
Yes
Yes
No

Explanation:
1\. ((a+b)) can reduced to (a+b), this Redundant
2\. (a+(b)/c) can reduced to (a+b/c) because b is
surrounded by () which is redundant.
3\. (a+b*(c-d)) doesn't have any redundant or multiple
brackets.
```

想法是使用堆栈，这在[这篇](https://www.geeksforgeeks.org/find-expression-duplicate-parenthesis-not/)文章中讨论。对于表达式的任何子表达式，如果我们能够选择由()包围的表达式的任何子表达式，那么我们再次留下()作为字符串的一部分，我们有多余的大括号。
我们遍历给定的表达式，对于表达式中的每个字符，如果该字符是左括号“(”或任何运算符或操作数，我们会将其推入堆栈。如果字符是右括号')'，则从堆栈中弹出字符，直到找到匹配的左括号'('。
现在对于冗余，弹出时会出现两种情况-

1.  如果立即弹出碰到一个左括号“(”，那么我们发现了一个重复的括号。例如，**((a+b))+c)**在 **a+b** 周围有重复的括号。当我们到达第二个)a+b 之后，我们有“**”((**)在堆栈中。由于堆栈顶部是一个左括号，我们得出结论，有重复的括号。

2.  如果立即弹出没有命中任何操作数(“*”、“+”、“/”、“-”)，则表明存在表达式包围的不需要的括号。例如， **(a)+b** 在 **a** 周围包含不需要的 **()** ，因此是多余的。

## C++

```
/* C++ Program to check whether valid
 expression is redundant or not*/
#include <bits/stdc++.h>
using namespace std;

// Function to check redundant brackets in a
// balanced expression
bool checkRedundancy(string& str)
{
    // create a stack of characters
    stack<char> st;

    // Iterate through the given expression
    for (auto& ch : str) {

        // if current character is close parenthesis ')'
        if (ch == ')') {
            char top = st.top();
            st.pop();

            // If immediate pop have open parenthesis '('
            // duplicate brackets found
            bool flag = true;

            while (!st.empty() and top != '(') {

                // Check for operators in expression
                if (top == '+' || top == '-' ||
                    top == '*' || top == '/')
                    flag = false;

                // Fetch top element of stack
                top = st.top();
                st.pop();
            }

            // If operators not found
            if (flag == true)
                return true;
        }

        else
            st.push(ch); // push open parenthesis '(',
                  // operators and operands to stack
    }
    return false;
}

// Function to check redundant brackets
void findRedundant(string& str)
{
    bool ans = checkRedundancy(str);
    if (ans == true)
        cout << "Yes\n";
    else
        cout << "No\n";
}

// Driver code
int main()
{
    string str = "((a+b))";
    findRedundant(str);

    str = "(a+(b)/c)";
    findRedundant(str);

    str = "(a+b*(c-d))";
    findRedundant(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java Program to check whether valid
expression is redundant or not*/
import java.util.Stack;
public class GFG {
// Function to check redundant brackets in a
// balanced expression

    static boolean checkRedundancy(String s) {
        // create a stack of characters
        Stack<Character> st = new Stack<>();
        char[] str = s.toCharArray();
        // Iterate through the given expression
        for (char ch : str) {

            // if current character is close parenthesis ')'
            if (ch == ')') {
                char top = st.peek();
                st.pop();

                // If immediate pop have open parenthesis '('
                // duplicate brackets found
                boolean flag = true;

                while (top != '(') {

                    // Check for operators in expression
                    if (top == '+' || top == '-'
                            || top == '*' || top == '/') {
                        flag = false;
                    }

                    // Fetch top element of stack
                    top = st.peek();
                    st.pop();
                }

                // If operators not found
                if (flag == true) {
                    return true;
                }
            } else {
                st.push(ch); // push open parenthesis '(',
            }                // operators and operands to stack
        }
        return false;
    }

// Function to check redundant brackets
    static void findRedundant(String str) {
        boolean ans = checkRedundancy(str);
        if (ans == true) {
            System.out.println("Yes");
        } else {
            System.out.println("No");
        }
    }

// Driver code
    public static void main(String[] args) {
        String str = "((a+b))";
        findRedundant(str);

        str = "(a+(b)/c)";
        findRedundant(str);

        str = "(a+b*(c-d))";
        findRedundant(str);
    }
}
```

## 蟒蛇 3

```
# Python3 Program to check whether valid
# expression is redundant or not

# Function to check redundant brackets
# in a balanced expression
def checkRedundancy(Str):

    # create a stack of characters
    st = []

    # Iterate through the given expression
    for ch in Str:

        # if current character is close
        # parenthesis ')'
        if (ch == ')'):
            top = st[-1]
            st.pop()

            # If immediate pop have open parenthesis
            # '(' duplicate brackets found
            flag = True

            while (top != '('):

                # Check for operators in expression
                if (top == '+' or top == '-' or
                    top == '*' or top == '/'):
                    flag = False

                # Fetch top element of stack
                top = st[-1]
                st.pop()

            # If operators not found
            if (flag == True):
                return True

        else:
            st.append(ch) # append open parenthesis '(',
                          # operators and operands to stack
    return False

# Function to check redundant brackets
def findRedundant(Str):
    ans = checkRedundancy(Str)
    if (ans == True):
        print("Yes")
    else:
        print("No")

# Driver code
if __name__ == '__main__':
    Str = "((a+b))"
    findRedundant(Str)

    Str = "(a+(b)/c)"
    findRedundant(Str)

    Str = "(a+b*(c-d))"
    findRedundant(Str)

# This code is contributed by PranchalK
```

## C#

```
/* C# Program to check whether valid
expression is redundant or not*/
using System;
using System.Collections.Generic;

class GFG
{
    // Function to check redundant brackets in a
    // balanced expression
    static bool checkRedundancy(String s)
    {
        // create a stack of characters
        Stack<char> st = new Stack<char>();
        char[] str = s.ToCharArray();

        // Iterate through the given expression
        foreach (char ch in str)
        {

            // if current character is close parenthesis ')'
            if (ch == ')')
            {
                char top = st.Peek();
                st.Pop();

                // If immediate pop have open parenthesis '('
                // duplicate brackets found
                bool flag = true;

                while (top != '(')
                {

                    // Check for operators in expression
                    if (top == '+' || top == '-'
                            || top == '*' || top == '/')
                    {
                        flag = false;
                    }

                    // Fetch top element of stack
                    top = st.Peek();
                    st.Pop();
                }

                // If operators not found
                if (flag == true)
                {
                    return true;
                }
            }
            else
            {
                st.Push(ch); // push open parenthesis '(',
            }         // operators and operands to stack
        }
        return false;
    }

    // Function to check redundant brackets
    static void findRedundant(String str)
    {
        bool ans = checkRedundancy(str);
        if (ans == true)
        {
            Console.WriteLine("Yes");
        }
        else
        {
            Console.WriteLine("No");
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "((a+b))";
        findRedundant(str);

        str = "(a+(b)/c)";
        findRedundant(str);

        str = "(a+b*(c-d))";
        findRedundant(str);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

/* JavaScript Program to check whether valid
 expression is redundant or not*/

// Function to check redundant brackets in a
// balanced expression
function checkRedundancy(str)
{
    // create a stack of characters
    var st = [];
    var ans = false;
    // Iterate through the given expression
    str.split('').forEach(ch => {

        // if current character is close parenthesis ')'
        if (ch == ')') {
            var top = st[st.length-1];
            st.pop();

            // If immediate pop have open parenthesis '('
            // duplicate brackets found
            var flag = true;

            while (st.length!=0 && top != '(') {

                // Check for operators in expression
                if (top == '+' || top == '-' ||
                    top == '*' || top == '/')
                    flag = false;

                // Fetch top element of stack
                top = st[st.length-1];
                st.pop();
            }

            // If operators not found
            if (flag == true)
                ans = true;
        }

        else
            st.push(ch); // push open parenthesis '(',
                  // operators and operands to stack
    });
    return ans;
}

// Function to check redundant brackets
function findRedundant(str)
{
    var ans = checkRedundancy(str);
    if (ans == true)
        document.write( "Yes<br>");
    else
        document.write( "No<br>");
}

// Driver code

var str = "((a+b))";
findRedundant(str);

str = "(a+(b)/c)";
findRedundant(str);

str = "(a+b*(c-d))";
findRedundant(str);

</script>
```

**Output**

```
Yes
Yes
No

```