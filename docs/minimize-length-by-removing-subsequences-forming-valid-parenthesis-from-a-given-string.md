# 通过从给定字符串中移除形成有效括号的子序列来最小化长度

> 原文:[https://www . geesforgeks . org/通过从给定字符串中移除子序列来最小化长度-形成-有效-括号/](https://www.geeksforgeeks.org/minimize-length-by-removing-subsequences-forming-valid-parenthesis-from-a-given-string/)

给定由**'('，')'、'['** '和 **']'** 组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是通过移除有效括号的子序列来找到字符串中剩余字符的最小数量。

**示例:**

> **输入:** S = "[]])(["
> **输出:** 4
> **解释:**
> 移除子序列{ str[0]，str[1] }将 S 修改为"])(["。
> 因此，要求输出为 4。
> 
> **输入:**S =([)(])”
> **输出:** 0
> **解释:**
> 移除子序列{ str[0]，str[2] }将 S 修改为“[(])”。
> 删除子序列{ str[0]，str[2] }将 S 修改为“()”。
> 删除子序列{ str[0]，str[1] }将 S 修改为" "。
> 因此，要求输出为 0。

**方法:**使用[栈](https://www.geeksforgeeks.org/stack-data-structure/)可以解决问题。按照以下步骤解决问题:

*   想法是在两个独立的堆栈中处理圆括号“**”()“**”和括号“**”[]“**”。
*   初始化两个变量，比如**舍入**和**平方计数**，分别存储 **'()'** 和 **'[]'** 的有效括号中左括号的计数。
*   迭代给定字符串的每个字符，并使用两个不同的堆栈计算 **'()'** 和 **'[]'** 的有效括号长度。
*   最后，打印**(N–2 *(四舍五入+平方数))**的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum count of remaining
// characters left into the string by removing
// the valid subsequences
void deleteSubseq(string s)
{

    // Length of the string
    int N = s.size();

    // Stores opening parenthesis
    // '(' of the given string
    stack<char> roundStk;

    // Stores square parenthesis
    // '[' of the given string
    stack<char> squareStk;

    // Stores count of opening parenthesis '('
    // in valid subsequences
    int roundCount = 0;

    // Stores count of opening parenthesis '['
    // in valid subsequences
    int squareCount = 0;

    // Iterate over each
    // characters of S
    for (int i = 0; i < N; i++)
    {

        // If current character is '['
        if (s[i] == '[')
        {

            // insert into stack
            squareStk.push(s[i]);
        }

        // If i is equal to ']'
        else if (s[i] == ']')
        {

            // If stack is not empty and
            // top element of stack is '['
            if (squareStk.size() != 0
                && squareStk.top() == '[')
            {

                // Remove top element from stack
                squareStk.pop();

                // Update squareCount
                squareCount += 1;
            }
        }

        // If current character is '('
        else if (s[i] == '(')
        {

            // Insert into stack
            roundStk.push(s[i]);
        }

        // If i is equal to ')'
        else
        {

            // If stack is not empty and
            // top element of stack is '('
            if (roundStk.size() != 0
                && squareStk.top() == '(')
            {

                // Remove top element from stack
                squareStk.pop();

                // Update roundCount
                roundCount += 1;
            }
        }
    }

    // Print the minimum number of remaining
    // characters left into S
    cout << (N - (2 * squareCount + 2 * roundCount));
}

// Driver code
int main()
{

    // input string
    string s = "[]])([";

    // function call
    deleteSubseq(s);
}

// This code is contributed by gauravrajput1
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

// Java program for the above approach
import java.io.*;
import java.util.Stack;
class GFG
{

  // Function to find the minimum count of remaining
  // characters left into the string by removing
  // the valid subsequences
  public static void deleteSubseq(String s)
  {

    // Length of the string
    int N = s.length();

    // Stores opening parenthesis
    // '(' of the given string
    Stack<Character> roundStk = new Stack<>();

    // Stores square parenthesis
    // '[' of the given string
    Stack<Character> squareStk = new Stack<>();

    // Stores count of opening parenthesis '('
    // in valid subsequences
    int roundCount = 0;

    // Stores count of opening parenthesis '['
    // in valid subsequences
    int squareCount = 0;

    // Iterate over each
    // characters of S
    for (int i = 0; i < N; i++)
    {

      // If current character is '['
      if (s.charAt(i) == '[')
      {

        // insert into stack
        squareStk.push(s.charAt(i));
      }

      // If i is equal to ']'
      else if (s.charAt(i) == ']')
      {

        // If stack is not empty and
        // top element of stack is '['
        if (squareStk.size() != 0
            && squareStk.peek() == '[')
        {

          // Remove top element from stack
          squareStk.pop();

          // Update squareCount
          squareCount += 1;
        }
      }

      // If current character is '('
      else if (s.charAt(i) == '(')
      {

        // Insert into stack
        roundStk.push(s.charAt(i));
      }

      // If i is equal to ')'
      else
      {

        // If stack is not empty and
        // top element of stack is '('
        if (roundStk.size() != 0
            && squareStk.peek() == '(')
        {

          // Remove top element from stack
          squareStk.pop();

          // Update roundCount
          roundCount += 1;
        }
      }
    }

    // Print the minimum number of remaining
    // characters left into S
    System.out.println(
      N - (2 * squareCount + 2 * roundCount));
  }

  // Driver code
  public static void main(String[] args)
  {

    // input string
    String s = "[]])([";

    // function call
    deleteSubseq(s);
  }
}

// This code is contributed by aditya7409
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the minimum count of remaining
# characters left into the string by removing
# the valid subsequences
def deleteSubseq(S):

    # Length of the string
    N = len(S)

    # Stores opening parenthesis
    # '(' of the given string
    roundStk = []

    # Stores square parenthesis
    # '[' of the given string
    squareStk = []

    # Stores count of opening parenthesis '('
    # in valid subsequences
    roundCount = 0

    # Stores count of opening parenthesis '['
    # in valid subsequences
    squareCount = 0

    # Iterate over each
    # characters of S
    for i in S:

        # If current character is '['
        if i == '[':

            # Insert into stack
            squareStk.append(i)

        # If i is equal to ']'
        elif i == ']':

            # If stack is not empty and
            # top element of stack is '['
            if squareStk and squareStk[-1] == '[':

                # Remove top element from stack
                squareStk.pop()

                # Update squareCount
                squareCount += 1

        # If current character is '('
        elif i == '(':

            # Insert into stack
            roundStk.append(i)
        else:

            # If stack is not empty and
            # top element of stack is '('
            if roundStk and roundStk[-1] == '(':

                # Remove top element from stack
                roundStk.pop()

                # Update roundCount
                roundCount += 1

    # Print the minimum number of remaining
    # characters left into S
    print(N - (2 * squareCount + 2 * roundCount))

# Driver Code
if __name__ == '__main__':

    # Given string
    S = '[]])(['

    # Function Call
    deleteSubseq(S)
```

## C#

```
/*package whatever //do not write package name here */

// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

  // Function to find the minimum count of remaining
  // characters left into the string by removing
  // the valid subsequences
  public static void deleteSubseq(String s)
  {

    // Length of the string
    int N = s.Length;

    // Stores opening parenthesis
    // '(' of the given string
    Stack<char> roundStk = new Stack<char>();

    // Stores square parenthesis
    // '[' of the given string
    Stack<char> squareStk = new Stack<char>();

    // Stores count of opening parenthesis '('
    // in valid subsequences
    int roundCount = 0;

    // Stores count of opening parenthesis '['
    // in valid subsequences
    int squareCount = 0;

    // Iterate over each
    // characters of S
    for (int i = 0; i < N; i++)
    {

      // If current character is '['
      if (s[i] == '[')
      {

        // insert into stack
        squareStk.Push(s[i]);
      }

      // If i is equal to ']'
      else if (s[i] == ']')
      {

        // If stack is not empty and
        // top element of stack is '['
        if (squareStk.Count != 0
            && squareStk.Peek() == '[')
        {

          // Remove top element from stack
          squareStk.Pop();

          // Update squareCount
          squareCount += 1;
        }
      }

      // If current character is '('
      else if (s[i] == '(')
      {

        // Insert into stack
        roundStk.Push(s[i]);
      }

      // If i is equal to ')'
      else
      {

        // If stack is not empty and
        // top element of stack is '('
        if (roundStk.Count != 0
            && squareStk.Peek() == '(')
        {

          // Remove top element from stack
          squareStk.Pop();

          // Update roundCount
          roundCount += 1;
        }
      }
    }

    // Print the minimum number of remaining
    // characters left into S
    Console.WriteLine(
      N - (2 * squareCount + 2 * roundCount));
  }

  // Driver code
  public static void Main(String[] args)
  {

    // input string
    String s = "[]])([";

    // function call
    deleteSubseq(s);
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the minimum count of remaining
// characters left into the string by removing
// the valid subsequences
function deleteSubseq(s)
{

    // Length of the string
    var N = s.length;

    // Stores opening parenthesis
    // '(' of the given string
    var roundStk = [];

    // Stores square parenthesis
    // '[' of the given string
    var squareStk = [];

    // Stores count of opening parenthesis '('
    // in valid subsequences
    var roundCount = 0;

    // Stores count of opening parenthesis '['
    // in valid subsequences
    var squareCount = 0;

    // Iterate over each
    // characters of S
    for (var i = 0; i < N; i++)
    {

        // If current character is '['
        if (s[i] == '[')
        {

            // insert into stack
            squareStk.push(s[i]);
        }

        // If i is equal to ']'
        else if (s[i] == ']')
        {

            // If stack is not empty and
            // top element of stack is '['
            if (squareStk.length != 0
                && squareStk[squareStk.length-1] == '[')
            {

                // Remove top element from stack
                squareStk.pop();

                // Update squareCount
                squareCount += 1;
            }
        }

        // If current character is '('
        else if (s[i] == '(')
        {

            // Insert into stack
            roundStk.push(s[i]);
        }

        // If i is equal to ')'
        else
        {

            // If stack is not empty and
            // top element of stack is '('
            if (roundStk.length != 0
                && squareStk[squareStk.length-1] == '(')
            {

                // Remove top element from stack
                squareStk.pop();

                // Update roundCount
                roundCount += 1;
            }
        }
    }

    // Print the minimum number of remaining
    // characters left into S
    document.write(N - (2 * squareCount + 2 * roundCount));
}

// Driver code

// input string
var s = "[]])([";

// function call
deleteSubseq(s);

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)