# 查找表达式是否有重复括号

> 原文:[https://www . geesforgeks . org/find-expression-replice-括号-not/](https://www.geeksforgeeks.org/find-expression-duplicate-parenthesis-not/)

给定一个平衡表达式，查找它是否包含重复的括号。如果同一个子表达式被多个括号包围，则一组括号是重复的。

**示例:**

```
Below expressions have duplicate parenthesis - 
((a+b)+((c+d)))
The subexpression "c+d" is surrounded by two
pairs of brackets.

(((a+(b)))+(c+d))
The subexpression "a+(b)" is surrounded by two 
pairs of brackets.

(((a+(b))+c+d))
The whole expression is surrounded by two 
pairs of brackets.

((a+(b))+(c+d))
(b) and ((a+(b)) is surrounded by two
pairs of brackets.

Below expressions don't have any duplicate parenthesis -
((a+b)+(c+d)) 
No subsexpression is surrounded by duplicate
brackets.
```

可以假设给定的表达式是有效的，并且不存在任何空格。

这个想法是使用堆栈。遍历给定的表达式，对于表达式中的每个字符，如果该字符是左括号“(”或任何运算符或操作数，则将其推到堆栈顶部。如果字符是右括号')'，则从堆栈中弹出字符，直到找到匹配的左括号'('，并使用计数器，该计数器的值为遇到的每个字符递增，直到找到左括号'('。如果在左括号和右括号对之间遇到的字符数(等于计数器的值)小于 1，则发现一对重复的括号，否则不会出现冗余的括号对。例如，((a+b))+c)在“a+b”周围有重复的括号。当遇到 a+b 后的第二个“)”时，堆栈包含”(()。由于栈顶是开括号，所以可以断定有重复的括号。

以下是上述想法的实现:

## C++

```
// C++ program to find duplicate parenthesis in a
// balanced expression
#include <bits/stdc++.h>
using namespace std;

// Function to find duplicate parenthesis in a
// balanced expression
bool findDuplicateparenthesis(string str)
{
    // create a stack of characters
    stack<char> Stack;

    // Iterate through the given expression
    for (char ch : str)
    {
        // if current character is close parenthesis ')'
        if (ch == ')')
        {
            // pop character from the stack
            char top = Stack.top();
            Stack.pop();

            // stores the number of characters between a
            // closing and opening parenthesis
            // if this count is less than or equal to 1
            // then the brackets are redundant else not
            int elementsInside = 0;
            while (top != '(')
            {
                elementsInside++;
                top = Stack.top();
                Stack.pop();
            }
            if(elementsInside < 1) {
                return 1;
            }
        }

        // push open parenthesis '(', operators and
        // operands to stack
        else
            Stack.push(ch);
    }

    // No duplicates found
    return false;
}

// Driver code
int main()
{
    // input balanced expression
    string str = "(((a+(b))+(c+d)))";

    if (findDuplicateparenthesis(str))
        cout << "Duplicate Found ";
    else
        cout << "No Duplicates Found ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Stack;

// Java program to find duplicate parenthesis in a
// balanced expression
public class GFG {

// Function to find duplicate parenthesis in a
// balanced expression
    static boolean findDuplicateparenthesis(String s) {
        // create a stack of characters
        Stack<Character> Stack = new Stack<>();

        // Iterate through the given expression
        char[] str = s.toCharArray();
        for (char ch : str) {
            // if current character is close parenthesis ')'
            if (ch == ')') {
                // pop character from the stack
                char top = Stack.peek();
                Stack.pop();

                // stores the number of characters between a
                // closing and opening parenthesis
                // if this count is less than or equal to 1
                // then the brackets are redundant else not
                int elementsInside = 0;
                while (top != '(') {
                    elementsInside++;
                    top = Stack.peek();
                    Stack.pop();
                }
                if (elementsInside < 1) {
                    return true;
                }
            } // push open parenthesis '(', operators and
            // operands to stack
            else {
                Stack.push(ch);
            }
        }

        // No duplicates found
        return false;
    }

// Driver code
public static void main(String[] args) {

        // input balanced expression
        String str = "(((a+(b))+(c+d)))";

        if (findDuplicateparenthesis(str)) {
            System.out.println("Duplicate Found ");
        } else {
            System.out.println("No Duplicates Found ");
        }

    }
}
```

## 蟒蛇 3

```
# Python3 program to find duplicate
# parenthesis in a balanced expression

# Function to find duplicate parenthesis
# in a balanced expression
def findDuplicateparenthesis(string):

    # create a stack of characters
    Stack = []

    # Iterate through the given expression
    for ch in string:

        # if current character is
        # close parenthesis ')'
        if ch == ')':

            # pop character from the stack
            top = Stack.pop()

            # stores the number of characters between
            # a closing and opening parenthesis
            # if this count is less than or equal to 1
            # then the brackets are redundant else not
            elementsInside = 0
            while top != '(':

                elementsInside += 1
                top = Stack.pop()

            if elementsInside < 1:
                return True

        # push open parenthesis '(', operators
        # and operands to stack
        else:
            Stack.append(ch)

    # No duplicates found
    return False

# Driver Code
if __name__ == "__main__":

    # input balanced expression
    string = "(((a+(b))+(c+d)))"

    if findDuplicateparenthesis(string) == True:
        print("Duplicate Found")
    else:
        print("No Duplicates Found")

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find duplicate parenthesis
// in a balanced expression
using System;
using System.Collections.Generic;

class GFG
{

// Function to find duplicate parenthesis 
// in a balanced expression
static Boolean findDuplicateparenthesis(String s)
{
    // create a stack of characters
    Stack<char> Stack = new Stack<char>();

    // Iterate through the given expression
    char[] str = s.ToCharArray();
    foreach (char ch in str)
    {
        // if current character is
        // close parenthesis ')'
        if (ch == ')')
        {
            // pop character from the stack
            char top = Stack.Peek();
            Stack.Pop();

            // stores the number of characters between
            // a closing and opening parenthesis
            // if this count is less than or equal to 1
            // then the brackets are redundant else not
            int elementsInside = 0;
            while (top != '(')
            {
                elementsInside++;
                top = Stack.Peek();
                Stack.Pop();
            }
            if (elementsInside < 1)
            {
                return true;
            }
        } 

        // push open parenthesis '(',
        // operators and operands to stack
        else
        {
            Stack.Push(ch);
        }
    }

    // No duplicates found
    return false;
}

// Driver code
public static void Main(String[] args)
{

    // input balanced expression
    String str = "(((a+(b))+(c+d)))";

    if (findDuplicateparenthesis(str))
    {
        Console.WriteLine("Duplicate Found ");
    }
    else
    {
        Console.WriteLine("No Duplicates Found ");
    }
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find duplicate
// parenthesis in a balanced expression

// Function to find duplicate parenthesis
// in a balanced expression
function findDuplicateparenthesis(s)
{

    // Create a stack of characters
    let Stack = [];

    // Iterate through the given expression
    let str = s.split("");
    for(let ch = 0; ch < str.length;ch++)
    {

        // If current character is close
        // parenthesis ')'
        if (str[ch] == ')')
        {

            // pop character from the stack
            let top = Stack.pop();

            // Stores the number of characters between a
            // closing and opening parenthesis
            // if this count is less than or equal to 1
            // then the brackets are redundant else not
            let elementsInside = 0;
            while (top != '(')
            {
                elementsInside++;
                top = Stack.pop();
            }
            if (elementsInside < 1)
            {
                return true;
            }
        }

        // push open parenthesis '(', operators
        // and operands to stack
        else
        {
            Stack.push(str[ch]);
        }
    }

    // No duplicates found
    return false;
}

// Driver code
let str = "(((a+(b))+(c+d)))";

// Input balanced expression
if (findDuplicateparenthesis(str))
{
    document.write("Duplicate Found ");
}
else
{
    document.write("No Duplicates Found ");
}

// This code is contributed by rag2127

</script>
```

**输出:**

```
Duplicate Found
```

**上述解的时间复杂度**为 O(n)。

**程序使用的辅助空间**为 O(n)。

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。