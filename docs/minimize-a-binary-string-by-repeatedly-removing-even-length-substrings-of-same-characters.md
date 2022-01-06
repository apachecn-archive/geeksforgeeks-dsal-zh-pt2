# 通过重复删除相同字符的偶数长度子串来最小化二进制字符串

> 原文:[https://www . geeksforgeeks . org/通过重复删除相同字符的偶数长度子字符串来最小化二进制字符串/](https://www.geeksforgeeks.org/minimize-a-binary-string-by-repeatedly-removing-even-length-substrings-of-same-characters/)

给定一个大小为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **字符串**，任务是通过多次从字符串中删除由 sam 字符组成的偶数长度子字符串，即仅 **0** s 或 **1** s，来最小化给定二进制字符串的长度。最后，打印修改后的字符串。

**示例:**

> **输入:**str = " 101001 "
> **输出:**【10】
> **说明:**字符串可以通过以下方式最小化:“101**00**1”—>10**11**“—>10”。
> 
> **输入:** str = "00110"
> **输出:**“0”
> **说明:**字符串可以通过以下方式最小化:“**00**110”—>”**11**0”—>0”。

**方法:**思路是用一个[栈](https://www.geeksforgeeks.org/stack-data-structure/)来解决问题。当[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)时，如果发现当前字符与堆栈的[顶部元素相同，](https://www.geeksforgeeks.org/stack-top-c-stl/)[从堆栈](https://www.geeksforgeeks.org/stack-pop-method-in-java/)中弹出该元素。遍历后，从下往上打印堆栈。按照以下步骤解决问题:

*   声明一个**栈**并将字符串 **串**的[第一个字符推入栈中。](https://www.geeksforgeeks.org/delete-first-character-of-a-string-in-javascript/)
*   [使用变量 **i.** 在指数**【1，N–1】**范围内遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/) **字符串**
    *   [如果堆栈为空](https://www.geeksforgeeks.org/stack-empty-method-in-java/)，则[将字符**str【I】**推入堆栈](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)。
    *   否则，检查 **str[i]** 是否等于堆栈顶部的[。](https://www.geeksforgeeks.org/stack-top-c-stl/)如果发现是真的，[从堆栈中弹出](https://www.geeksforgeeks.org/stack-pop-method-in-java/)。否则，将字符 **str[i]** 推给它。
*   完成以上步骤后，[自下而上打印堆栈](https://www.geeksforgeeks.org/print-stack-elements-from-bottom-to-top/)。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Recursive function to print stack
// elements from bottom to top without
// changing their order
void PrintStack(stack<char> s)
{
    // If stack is empty
    if (s.empty())
        return;

    char x = s.top();

    // Pop top element of the stack
    s.pop();

    // Recursively call the
    // function PrintStack
    PrintStack(s);

    // Print the stack element
    // from the bottom
    cout << x;

    // Push the same element onto the
    // stack to preserve the order
    s.push(x);
}

// Function to minimize binary string
// by removing substrings consisting
// of same character
void minString(string s)
{
    // Declare a stack of characters
    stack<char> Stack;

    // Push the first character of
    // the string into the stack
    Stack.push(s[0]);

    // Traverse the string s
    for (int i = 1; i < s.size(); i++) {

        // If Stack is empty
        if (Stack.empty()) {

            // Push current character
            // into the stack
            Stack.push(s[i]);
        }

        else {

            // Check if the current
            // character is same as
            // the top of the stack
            if (Stack.top() == s[i]) {

                // If true, pop the
                // top of the stack
                Stack.pop();
            }

            // Otherwise, push the
            // current element
            else {
                Stack.push(s[i]);
            }
        }
    }

    // Print stack from bottom to top
    PrintStack(Stack);
}

// Driver Code
int main()
{
    string str = "101001";
    minString(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Recursive function to print stack
// elements from bottom to top without
// changing their order
static void PrintStack(Stack<Character> s)
{
    // If stack is empty
    if (s.isEmpty())
        return;

    char x = s.peek();

    // Pop top element of the stack
    s.pop();

    // Recursively call the
    // function PrintStack
    PrintStack(s);

    // Print the stack element
    // from the bottom
    System.out.print(x);

    // Push the same element onto the
    // stack to preserve the order
    s.add(x);
}

// Function to minimize binary String
// by removing subStrings consisting
// of same character
static void minString(String s)
{
    // Declare a stack of characters
    Stack<Character> Stack = new Stack<Character>();

    // Push the first character of
    // the String into the stack
    Stack.add(s.charAt(0));

    // Traverse the String s
    for (int i = 1; i < s.length(); i++) {

        // If Stack is empty
        if (Stack.isEmpty()) {

            // Push current character
            // into the stack
            Stack.add(s.charAt(i));
        }

        else {

            // Check if the current
            // character is same as
            // the top of the stack
            if (Stack.peek() == s.charAt(i)) {

                // If true, pop the
                // top of the stack
                Stack.pop();
            }

            // Otherwise, push the
            // current element
            else {
                Stack.push(s.charAt(i));
            }
        }
    }

    // Print stack from bottom to top
    PrintStack(Stack);
}

// Driver Code
public static void main(String[] args)
{
    String str = "101001";
    minString(str);

}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Recursive function to print stack
# elements from bottom to top without
# changing their order
def PrintStack(s) :

    # If stack is empty
    if (len(s) == 0) :
        return;

    x = s[-1];

    # Pop top element of the stack
    s.pop();

    # Recursively call the
    # function PrintStack
    PrintStack(s);

    # Print the stack element
    # from the bottom
    print(x, end="");

    # Push the same element onto the
    # stack to preserve the order
    s.append(x);

# Function to minimize binary string
# by removing substrings consisting
# of same character
def minString(s) :

    # Declare a stack of characters
    Stack = [];

    # Push the first character of
    # the string into the stack
    Stack.append(s[0]);

    # Traverse the string s
    for i in range(1, len(s)) :

        # If Stack is empty
        if (len(Stack) == 0) :

            # Push current character
            # into the stack
            Stack.append(s[i]);

        else:

            # Check if the current
            # character is same as
            # the top of the stack
            if (Stack[-1] == s[i]) :

                # If true, pop the
                # top of the stack
                Stack.pop();

            # Otherwise, push the
            # current element
            else :
                Stack.append(s[i]);

    # Print stack from bottom to top
    PrintStack(Stack);

# Driver Code
if __name__ == "__main__" :

    string = "101001";
    minString(string);

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

// Recursive function to print stack
// elements from bottom to top without
// changing their order
static void PrintStack(Stack<char> s)
{
    // If stack is empty
    if (s.Count == 0)
        return;
    char x = s.Peek();

    // Pop top element of the stack
    s.Pop();

    // Recursively call the
    // function PrintStack
    PrintStack(s);

    // Print the stack element
    // from the bottom
    Console.Write((char)x);

    // Push the same element onto the
    // stack to preserve the order
    s.Push(x);
}

// Function to minimize binary String
// by removing subStrings consisting
// of same character
static void minString(String s)
{
    // Declare a stack of characters
    Stack<char> Stack = new Stack<char>();

    // Push the first character of
    // the String into the stack
    Stack.Push(s[0]);

    // Traverse the String s
    for (int i = 1; i < s.Length; i++)
    {

        // If Stack is empty
        if (Stack.Count == 0)
        {

            // Push current character
            // into the stack
            Stack.Push(s[i]);
        }

        else
        {

            // Check if the current
            // character is same as
            // the top of the stack
            if (Stack.Peek() == s[i])
            {

                // If true, pop the
                // top of the stack
                Stack.Pop();
            }

            // Otherwise, push the
            // current element
            else
            {
                Stack.Push(s[i]);
            }
        }
    }

    // Print stack from bottom to top
    PrintStack(Stack);
}

// Driver Code
public static void Main(String[] args)
{
    String str = "101001";
    minString(str);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// js program for the above approach

// Recursive function to print stack
// elements from bottom to top without
// changing their order
function PrintStack( s)
{
    // If stack is empty
    if (s.length == 0)
        return;

    let x = s[s.length-1];

    // Pop top element of the stack
    s.pop();

    // Recursively call the
    // function PrintStack
    PrintStack(s);

    // Print the stack element
    // from the bottom
    document.write(x);

    // Push the same element onto the
    // stack to preserve the order
    s.push(x);
}

// Function to minimize binary string
// by removing substrings consisting
// of same character
function minString( s)
{
    // Declare a stack of characters
    let Stack = [];

    // Push the first character of
    // the string into the stack
    Stack.push(s[0]);

    // Traverse the string s
    for (let i = 1; i < s.length; i++) {

        // If Stack is empty
        if (Stack.length==0) {

            // Push current character
            // into the stack
            Stack.push(s[i]);
        }

        else {

            // Check if the current
            // character is same as
            // the top of the stack
            if (Stack[Stack.length-1] == s[i]) {

                // If true, pop the
                // top of the stack
                Stack.pop();
            }

            // Otherwise, push the
            // current element
            else {
                Stack.push(s[i]);
            }
        }
    }

    // Print stack from bottom to top
    PrintStack(Stack);
}

// Driver Code
let str = "101001";
    minString(str);

</script>
```

**Output:** 

```
10
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)