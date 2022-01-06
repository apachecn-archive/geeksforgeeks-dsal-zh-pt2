# 最大化重复从管柱 S 上移除管柱 P 或其反向物的成本

> 原文:[https://www . geeksforgeeks . org/重复移除字符串的最大成本-p 或其反向-从字符串中-s/](https://www.geeksforgeeks.org/maximize-cost-of-repeated-removal-of-string-p-or-its-reverse-from-the-string-s/)

给定两个正整数 **X** 和 **Y** 以及两个长度分别为 **N** 和 **2** 的[数字字符串](https://www.geeksforgeeks.org/splitting-numeric-string/) **S** 和 **P** ，任务是在

**示例:**

> **输入:**S =“12333444”，X = 5，Y = 4，P =“34”
> **输出:** 15
> **说明:**
> 下面是去除子串得到最大代价的操作:
> 
> *   从字符串 S 中删除字符串**“**34”，因此字符串 S 修改为“123344”。成本= 5。
> *   从字符串 S 中删除字符串**“**34”，因此字符串 S 修改为“1234”。成本= 5。
> *   从字符串 S 中删除字符串**“**34”，因此字符串 S 修改为“12”。成本= 5。
> 
> 因此，总成本为 5 + 5 + 5 = 15。
> 
> **输入:**S =“12121221”，X = 7，Y = 10，P =“12”
> T3】输出: 37

**方法:**给定的问题可以使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)和[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)来解决。按照以下步骤解决问题:

*   初始化一个变量，比如说**和**为 **0** 来存储移除给定子串的最大成本。
*   初始化一个[栈](https://www.geeksforgeeks.org/stack-data-structure-introduction-program/)，用来决定是去掉弦 **P** 还是反弦 **P** 。
*   [遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，并执行以下步骤:
    *   如果当前字符和[顶字符](https://www.geeksforgeeks.org/stack-top-c-stl/)分别不等于**P【1】**和**P【0】**或者如果[栈](https://www.geeksforgeeks.org/stack-data-structure-introduction-program/)为空，则[将当前字符推入**栈**](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/) 。
    *   否则，移除[堆栈的顶部元素](https://www.geeksforgeeks.org/stack-data-structure-introduction-program/)，并将值**和**增加 **X** 。
*   同样，通过将 **Y** 添加到成本中，可以从任何字符串中删除字符串 **P** 的反向。
*   现在如果 **X** 大于 **Y** ，那么在之前去掉 **P** ，去掉 **P** 的反相会给出更大的值。否则，先去掉图案 **P** 的反面。
*   完成上述步骤后，打印**和**的值作为总最大成本。

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Initialize amount
int ans[1] = {0};

// Function to remove reverse of P first
void rp(string str, int x, int y, bool flag, char p, char r)
{

  // Initialize empty stack
  stack<char>stk;

  // Iterate through each char in string
  for(int i = 0; i < str.length(); i++)
  {
    // Remove reverse of P
    if (str[i]== p) {
      if (stk.size() > 0 && stk.top() == r)
      {
        ans[0] += y;

        // Pop the element from
        // the stack
        stk.pop();
      }
      else
      {
        stk.push(str[i]);
      }
    }
    else
    {
      stk.push(str[i]);
    }
    // Remove P, if needed
    ans[0]+=1;
    if (flag)
    {
      string s = "";
      stack<char> s1 ;
      while (s1.size() > 0) {
        s += s1.top();
        s1.pop();
      }
      pr(s, x, y, false, p, r);
    }
  }
}

// Function to remove the string P first
void pr(string str, int x, int y, bool flag, char p, char r) {

  // Initialize empty stack
  stack<int>stk;

  // Iterate through each char
  // in string
  for(int i = 0; i < str.length(); i++) {

    // Remove the string P
    if (str[i]== r) {
      if (stk.size() > 0 && stk.top() == p) {
        ans[0] += x;
        stk.pop();
      }
      // If no such pair exists just
      // push the chars to stack
      else {
        stk.push(str[i]);
      }
    }
    else {
      stk.push(str[i]);
    }
    ans[0] += 1;

    // Remove reverse of P, if needed
    if (flag) {
      string s = "";
      stack<char>s1;
      while (s1.size() > 0) {
        s = s + s1.top();
        s1.pop();
      }
      rp(s, x, y, false, p, r);
    }
  }
}

// Function to find the appropriate answer
int solve(string str, int x, int y, char p, char r) {

  // Remove P then reverse of P
  if (x > y)
    pr(str, x, y, true, p, r);

  // Remove reverse of P then P
  else
    rp(str, x, y, true, p, r);

  // Return the result
  return ans[0]-1;
}

// Driver Code
int main() {

  // Given string S
  string S = "12333444";

  // Given X and Y
  int x = 5;
  int y = 4;

  // Given P
  String P = "34";

  // Function Call
  cout<<solve(S, x, y, P[0], P[1]<<endl;
              return 0;
              }
              // This code is contributed by dwivediyash
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class Main
{

    // Initialize amount
    static int[] ans = {0};

    // Function to remove the string P first
    static void pr(String str, int x, int y, boolean flag, char p, char r) {

        // Initialize empty stack
        Stack<Character> stack = new Stack<Character>();

        // Iterate through each char
        // in string
        for(int i = 0; i < str.length(); i++) {

            // Remove the string P
            if (str.charAt(i) == r) {
                if (stack.size() > 0 && stack.peek() == p) {
                    ans[0] += x;
                    stack.pop();
                }
                // If no such pair exists just
                // push the chars to stack
                else {
                    stack.push(str.charAt(i));
                }
            }
            else {
                stack.push(str.charAt(i));
            }
            ans[0] += 1;

            // Remove reverse of P, if needed
            if (flag) {
                String s = "";
                Stack<Character> s1 = stack;
                while (s1.size() > 0) {
                    s = s + s1.peek();
                    s1.pop();
                }
                rp(s, x, y, false, p, r);
            }
        }
    }

    // Function to remove reverse of P first
    static void rp(String str, int x, int y, boolean flag, char p, char r)
    {
        // Initialize empty stack
        Stack<Character> stack = new Stack<Character>();

        // Iterate through each char in string
        for(int i = 0; i < str.length(); i++)
        {
            // Remove reverse of P
            if (str.charAt(i) == p) {
                if (stack.size() > 0 && stack.peek() == r)
                {
                    ans[0] += y;

                    // Pop the element from
                    // the stack
                    stack.pop();
                }
                else
                {
                    stack.push(str.charAt(i));
                }
            }
            else
            {
                stack.push(str.charAt(i));
            }
            // Remove P, if needed
            ans[0]+=1;
            if (flag)
            {
                String s = "";
                Stack<Character> s1 = stack;
                while (s1.size() > 0) {
                    s = s + s1.peek();
                    s1.pop();
                }
                pr(s, x, y, false, p, r);
            }
        }
    }

    // Function to find the appropriate answer
    static int solve(String str, int x, int y, char p, char r) {

        // Remove P then reverse of P
        if (x > y)
            pr(str, x, y, true, p, r);

        // Remove reverse of P then P
        else
            rp(str, x, y, true, p, r);

        // Return the result
        return ans[0]-1;
    }

  // Driver code
    public static void main(String[] args)
    {

        // Given string S
        String S = "12333444";

        // Given X and Y
        int x = 5;
        int y = 4;

        // Given P
        String P = "34";

        // Function Call
        System.out.print(solve(S, x, y, P.charAt(0), P.charAt(1)));
    }
}

// This code is contributed by mukesh07.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to remove reverse of P first
def rp(string, x, y, ans, flag, p, r):

    # Initialize empty stack
    stack = []

    # Iterate through each char in string
    for char in string:       

        # Remove reverse of P
        if char == p:
            if stack and stack[-1] == r:
                ans[0] += y

                # Pop the element from
                # the stack
                stack.pop()
            else:
                stack.append(char)
        else:
            stack.append(char)

    # Remove P, if needed
    if flag:
        pr("".join(stack), x, y, ans, False, p, r)

# Function to remove the string P first
def pr(string, x, y, ans, flag, p, r):

    # Initialize empty stack
    stack = []

    # Iterate through each char
    # in string
    for char in string:

      # Remove the string P
        if char == r:

            if stack and stack[-1] == p:
                ans[0] += x
                stack.pop()

            # If no such pair exists just
            # push the chars to stack
            else:
                stack.append(char)

        else:
            stack.append(char)

        # Remove reverse of P, if needed
        if flag:
            rp("".join(stack), x, y, ans, False, p, r)

# Function to find the appropriate answer
def solve(string, x, y, p, r):

    # Initialize amount
    ans = [0]

    # Remove P then reverse of P
    if x > y:
        pr(string, x, y, ans, True, p, r)

    # Remove reverse of P then P
    else:
        rp(string, x, y, ans, True, p, r)

    # Return the result
    return ans[0]

# Driver Code

# Given string S
S = "12333444"

# Given X and Y
x = 5
y = 4

# Given P
P = "34"

# Function Call
print(solve(S, x, y, P[0], P[1]))
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
class GFG {

    // Initialize amount
    static int[] ans = {0};

    // Function to remove the string P first
    static void pr(string str, int x, int y, bool flag, char p, char r) {

        // Initialize empty stack
        Stack stack = new Stack();

        // Iterate through each char
        // in string
        foreach(char c in str) {

            // Remove the string P
            if (c == r) {
                if (stack.Count > 0 && (char)stack.Peek() == p) {
                    ans[0] += x;
                    stack.Pop();
                }
                // If no such pair exists just
                // push the chars to stack
                else {
                    stack.Push(c);
                }
            }
            else {
                stack.Push(c);
            }
            ans[0]+=1;
            // Remove reverse of P, if needed
            if (flag) {
                string s = "";
                Stack s1 = stack;
                while (s1.Count > 0) {
                    s = s + (char)s1.Peek();
                    s1.Pop();
                }
                rp(s, x, y, false, p, r);
            }
        }
    }

    // Function to remove reverse of P first
    static void rp(string str, int x, int y, bool flag, char p, char r)
    {
        // Initialize empty stack
        Stack stack = new Stack();

        // Iterate through each char in string
        foreach(char c in str)
        {
            // Remove reverse of P
            if (c == p) {
                if (stack.Count > 0 && (char)stack.Peek() == r)
                {
                    ans[0] += y;

                    // Pop the element from
                    // the stack
                    stack.Pop();
                }
                else
                {
                    stack.Push(c);
                }
            }
            else
            {
                stack.Push(c);
            }
            // Remove P, if needed
            ans[0]+=1;
            if (flag)
            {
                string s = "";
                Stack s1 = stack;
                while (s1.Count > 0) {
                    s = s + (char)s1.Peek();
                    s1.Pop();
                }
                pr(s, x, y, false, p, r);
            }
        }
    }

    // Function to find the appropriate answer
    static int solve(string str, int x, int y, char p, char r) {

        // Remove P then reverse of P
        if (x > y)
            pr(str, x, y, true, p, r);

        // Remove reverse of P then P
        else
            rp(str, x, y, true, p, r);

        // Return the result
        return ans[0]-1;
    }

    static void Main()
    {

        // Given string S
        string S = "12333444";

        // Given X and Y
        int x = 5;
        int y = 4;

        // Given P
        string P = "34";

        // Function Call
        Console.Write(solve(S, x, y, P[0], P[1]));
    }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to remove reverse of P first
function rp(string, x, y, ans, flag, p, r) {

    // Initialize empty stack
    let stack = []

    // Iterate through each char in string
    for (let char of string) {

        // Remove reverse of P
        if (char == p) {
            if (stack && stack[stack.length - 1] == r) {
                ans[0] += y

                // Pop the element from
                // the stack
                stack.pop()
            }
            else
                stack.push(char)
        }
        else
            stack.push(char)
        // Remove P, if needed

        if (flag) {
            pr(stack.join(""), x, y, ans, false, p, r)
        }
    }
}

// Function to remove the string P first
function pr(string, x, y, ans, flag, p, r) {

    // Initialize empty stack
    let stack = []

    // Iterate through each char
    // in string
    for (let char of string) {

        // Remove the string P
        if (char == r) {

            if (stack && stack[stack.length - 1] == p) {
                ans[0] += x
                stack.pop()
            }
            // If no such pair exists just
            // push the chars to stack
            else {
                stack.push(char)
            }
        }
        else {
            stack.push(char)
        }

        // Remove reverse of P, if needed
        if (flag) {
            rp(stack.join(""), x, y, ans, false, p, r)
        }
    }
}

// Function to find the appropriate answer
function solve(string, x, y, p, r) {

    // Initialize amount
    let ans = [0]

    // Remove P then reverse of P
    if (x > y)
        pr(string, x, y, ans, true, p, r)

    // Remove reverse of P then P
    else
        rp(string, x, y, ans, true, p, r)

    // Return the result
    return ans[0]
}

// Driver Code

// Given string S
let S = "12333444"

// Given X and Y
let x = 5
let y = 4

// Given P
let P = "34"

// Function Call
document.write(solve(S, x, y, P[0], P[1]))

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
15
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)