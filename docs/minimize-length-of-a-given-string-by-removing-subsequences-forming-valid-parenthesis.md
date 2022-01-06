# 通过移除形成有效括号的子序列来最小化给定字符串的长度

> 原文:[https://www . geesforgeks . org/通过移除子序列来最小化给定字符串的长度-形成-有效-括号/](https://www.geeksforgeeks.org/minimize-length-of-a-given-string-by-removing-subsequences-forming-valid-parenthesis/)

给定一个由字符**“(”、“)”、“[”、“]”、“{”、“}”**组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是从字符串中移除所有平衡的括号子序列并打印剩余的字符。

**示例:**

> **输入:**S =**“((){()({ })”
> **输出:**”({“
> **)解释:****
> 
> 1.  **S[1]和 S[2]形成一个规则的括号序列。因此，从字符串中移除它们。S = "({()({})"**
> 2.  **S[2]和 S[3]是规则的括号序列。因此，从字符串中移除它们。s =({({ })"**
> 3.  **字符串[2…4]是常规的括号序列。因此，从字符串中移除它们。S = "({ "**
> 
> **剩余字符串不包含任何常规括号序列。因此，打印所有剩余字符。**
> 
>  ****输入:**S = {[}])(
> T3】输出:)(”**

****方法:**思路是用[栈数据结构](https://www.geeksforgeeks.org/stack-data-structure/)来解决这个问题。按照以下步骤解决问题:**

*   **初始化三个[栈](https://www.geeksforgeeks.org/stack-data-structure/)，比如 **A** 、 **B** 和 **C** ，用于存储每种类型的括号。**
*   **初始化一个布尔数组，比如 **vis[]** ，标记已经访问过的字符。**
*   **在堆栈 **A** 中存储字符**(**)的索引。同样，堆叠 **B** 和 **C** 存储字符串中 **'{'** 和 **'['** 的位置。**
*   **[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **字符串**的字符，并执行以下操作:

    *   如果当前字符是' **)** ':
        *   如果[栈 **A** 不为空](https://www.geeksforgeeks.org/stack-empty-and-stack-size-in-c-stl/)，则将字符串中的当前字符和**vis【A . top()】**标记为**假**。
        *   [弹出](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)叠加的[顶元素**一**。](https://www.geeksforgeeks.org/stack-top-c-stl/)
    *   如果当前字符是“**}”:**
        *   如果堆栈 **B** 不为空，则将字符串中的当前字符和**vis【B . top()】**标记为 **false** 。
        *   弹出栈顶元素 **B** 。
    *   如果当前字符是 **']':**
        *   如果堆栈 **C** 不为空，则将字符串中的当前字符和**vis【C . top()】**标记为 **false。**
        *   弹出栈顶元素 **C** 。** 
*   **完成所有操作后，在**vis【】**数组中打印索引标记为 **true** 的字符串的字符。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to remove all possible valid
// bracket subsequences
void removeValidBracketSequences(string& str,
                                 int N)
{

    // Stores indexes of '(' in
    // valid subsequences
    stack<int> A;

    // Stores indexes of '{' in
    // valid subsequences
    stack<int> B;

    // Stores indexes of '[' in
    // valid subsequences
    stack<int> C;

    // vis[i]: Check if character at
    // i-th index is removed or not
    bool vis[N];

    // Mark vis[i] as not removed
    memset(vis, true, sizeof(vis));

    // Iterate over the characters of string
    for (int i = 0; i < N; i++) {

        // If current character is '('
        if (str[i] == '(') {
            A.push(i);
        }

        // If current character is '{'
        else if (str[i] == '{') {
            B.push(i);
        }

        // If current character is '['
        else if (str[i] == '[') {
            C.push(i);
        }

        // If current character is ')' and
        // top element of A is '('
        else if (str[i] == ')' && !A.empty()) {

            // Mark the top element
            // of A as removed
            vis[A.top()] = false;
            A.pop();

            // Mark current character
            // as removed
            vis[i] = false;
        }

        // If current character is '}' and
        // top element of B is '{'
        else if (str[i] == '}' && !B.empty()) {

            // Mark the top element
            // of B as removed
            vis[B.top()] = false;
            B.pop();

            // Mark current character
            // as removed
            vis[i] = false;
        }

        // If current character is ']' and
        // top element of B is '['
        else if (str[i] == ']' && !C.empty()) {

            // Mark the top element
            // of C as removed
            vis[C.top()] = false;
            C.pop();

            // Mark current character
            // as removed
            vis[i] = false;
        }
    }

    // Print the remaining characters
    // which is not removed from S
    for (int i = 0; i < N; ++i) {

        if (vis[i])
            cout << str[i];
    }
}

// Driver Code
int main()
{
    // Given string
    string str = "((){()({})";

    // Size of the string
    int N = str.length();

    // Function Call
    removeValidBracketSequences(str, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program of the above approach
import java.util.*;
public class GFG
{

  // Function to remove all possible valid
  // bracket subsequences
  static void removeValidBracketSequences(String str, int N)
  {

    // Stores indexes of '(' in
    // valid subsequences
    Vector<Integer> A = new Vector<Integer>(); 

    // Stores indexes of '{' in
    // valid subsequences
    Vector<Integer> B = new Vector<Integer>();

    // Stores indexes of '[' in
    // valid subsequences
    Vector<Integer> C = new Vector<Integer>();

    // vis[i]: Check if character at
    // i-th index is removed or not
    boolean[] vis = new boolean[N];

    // Mark vis[i] as not removed
    for(int i = 0; i < N; i++)
    {
      vis[i] = true;
    }

    // Iterate over the characters of string
    for (int i = 0; i < N; i++) {

      // If current character is '('
      if (str.charAt(i) == '(') {
        A.add(i);
      }

      // If current character is '{'
      else if (str.charAt(i) == '{') {
        B.add(i);
      }

      // If current character is '['
      else if (str.charAt(i) == '[') {
        C.add(i);
      }

      // If current character is ')' and
      // top element of A is '('
      else if (str.charAt(i) == ')' && (A.size() > 0)) {

        // Mark the top element
        // of A as removed
        vis[A.get(A.size() - 1)] = false;
        A.remove(A.size() - 1);

        // Mark current character
        // as removed
        vis[i] = false;
      }

      // If current character is '}' and
      // top element of B is '{'
      else if (str.charAt(i) == '}' && (B.size() > 0)) {

        // Mark the top element
        // of B as removed
        vis[B.get(B.size() - 1)] = false;
        B.remove(B.size() - 1);

        // Mark current character
        // as removed
        vis[i] = false;
      }

      // If current character is ']' and
      // top element of B is '['
      else if (str.charAt(i) == ']' && (C.size() > 0)) {

        // Mark the top element
        // of C as removed
        vis[C.get(C.size() - 1)] = false;
        C.remove(C.size() - 1);

        // Mark current character
        // as removed
        vis[i] = false;
      }
    }

    // Print the remaining characters
    // which is not removed from S
    for (int i = 0; i < N; ++i)
    {
      if (vis[i])
        System.out.print(str.charAt(i));
    }
  }

  // Driver code
  public static void main(String[] args)
  {

    // Given string
    String str = "((){()({})";

    // Size of the string
    int N = str.length();

    // Function Call
    removeValidBracketSequences(str, N);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## **蟒蛇 3**

```
# Python3 program of the above approach

# Function to remove all possible valid
# bracket subsequences
def removeValidBracketSequences(str, N):

    # Stores indexes of '(' in
    # valid subsequences
    A = []

    # Stores indexes of '{' in
    # valid subsequences
    B = []

    # Stores indexes of '[' in
    # valid subsequences
    C = []

    # vis[i]: Check if character at
    # i-th index is removed or not
    vis = [True for i in range(N)]

    # Iterate over the characters of string
    for i in range(N):

        # If current character is '('
        if (str[i] == '('):
            A.append(i)

        # If current character is '{'
        elif (str[i] == '{'):
            B.append(i)

        # If current character is '['
        elif (str[i] == '['):
            C.append(i)

        # If current character is ')' and
        # top element of A is '('
        elif(str[i] == ')' and len(A) != 0):

            # Mark the top element
            # of A as removed
            vis[A[-1]] = False
            A.pop()

            # Mark current character
            # as removed
            vis[i] = False

        # If current character is '}' and
        # top element of B is '{'
        elif (str[i] == '}' and len(B) != 0):

            # Mark the top element
            # of B as removed
            vis[B[-1]] = False
            B.pop()

            # Mark current character
            # as removed
            vis[i] = False

        # If current character is ']' and
        # top element of B is '['
        elif(str[i] == ']' and len(C) != 0):

            # Mark the top element
            # of C as removed
            vis[C[-1]] = False
            C.pop()

            # Mark current character
            # as removed
            vis[i] = False

    # Print the remaining characters
    # which is not removed from S
    for i in range(N):
        if (vis[i]):
            print(str[i], end = '')

# Driver Code
if __name__=='__main__':

    # Given string
    str = "((){()({})"

    # Size of the string
    N = len(str)

    # Function Call
    removeValidBracketSequences(str, N)

# This code is contributed by rutvik_56
```

## **C#**

```
// C# program of the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to remove all possible valid
    // bracket subsequences
    static void removeValidBracketSequences(string str, int N)
    {

        // Stores indexes of '(' in
        // valid subsequences
        List<int> A = new List<int>();

        // Stores indexes of '{' in
        // valid subsequences
        List<int> B = new List<int>();

        // Stores indexes of '[' in
        // valid subsequences
        List<int> C = new List<int>();

        // vis[i]: Check if character at
        // i-th index is removed or not
        bool[] vis = new bool[N];

        // Mark vis[i] as not removed
        for(int i = 0; i < N; i++)
        {
            vis[i] = true;
        }

        // Iterate over the characters of string
        for (int i = 0; i < N; i++) {

            // If current character is '('
            if (str[i] == '(') {
                A.Add(i);
            }

            // If current character is '{'
            else if (str[i] == '{') {
                B.Add(i);
            }

            // If current character is '['
            else if (str[i] == '[') {
                C.Add(i);
            }

            // If current character is ')' and
            // top element of A is '('
            else if (str[i] == ')' && (A.Count > 0)) {

                // Mark the top element
                // of A as removed
                vis[A[A.Count - 1]] = false;
                A.RemoveAt(A.Count - 1);

                // Mark current character
                // as removed
                vis[i] = false;
            }

            // If current character is '}' and
            // top element of B is '{'
            else if (str[i] == '}' && (B.Count > 0)) {

                // Mark the top element
                // of B as removed
                vis[B[B.Count - 1]] = false;
                B.RemoveAt(B.Count - 1);

                // Mark current character
                // as removed
                vis[i] = false;
            }

            // If current character is ']' and
            // top element of B is '['
            else if (str[i] == ']' && (C.Count > 0)) {

                // Mark the top element
                // of C as removed
                vis[C[C.Count - 1]] = false;
                C.RemoveAt(C.Count - 1);

                // Mark current character
                // as removed
                vis[i] = false;
            }
        }

        // Print the remaining characters
        // which is not removed from S
        for (int i = 0; i < N; ++i) {

            if (vis[i])
                Console.Write(str[i]);
        }
    }

  // Driver code
  static void Main()
  {

    // Given string
    string str = "((){()({})";

    // Size of the string
    int N = str.Length;

    // Function Call
    removeValidBracketSequences(str, N);
  }
}

// This code is contributed by divyesh072019.
```

## **java 描述语言**

```
<script>
    // Javascript program of the above approach

    // Function to remove all possible valid
    // bracket subsequences
    function removeValidBracketSequences(str, N)
    {

        // Stores indexes of '(' in
        // valid subsequences
        let A = [];

        // Stores indexes of '{' in
        // valid subsequences
        let B = [];

        // Stores indexes of '[' in
        // valid subsequences
        let C = [];

        // vis[i]: Check if character at
        // i-th index is removed or not
        let vis = new Array(N);

        // Mark vis[i] as not removed
        for(let i = 0; i < N; i++)
        {
            vis[i] = true;
        }

        // Iterate over the characters of string
        for (let i = 0; i < N; i++) {

            // If current character is '('
            if (str[i] == '(') {
                A.push(i);
            }

            // If current character is '{'
            else if (str[i] == '{') {
                B.push(i);
            }

            // If current character is '['
            else if (str[i] == '[') {
                C.push(i);
            }

            // If current character is ')' and
            // top element of A is '('
            else if (str[i] == ')' && (A.length > 0)) {

                // Mark the top element
                // of A as removed
                vis[A[A.length - 1]] = false;
                A.pop();

                // Mark current character
                // as removed
                vis[i] = false;
            }

            // If current character is '}' and
            // top element of B is '{'
            else if (str[i] == '}' && (B.length > 0)) {

                // Mark the top element
                // of B as removed
                vis[B[B.length - 1]] = false;
                B.pop();

                // Mark current character
                // as removed
                vis[i] = false;
            }

            // If current character is ']' and
            // top element of B is '['
            else if (str[i] == ']' && (C.length > 0)) {

                // Mark the top element
                // of C as removed
                vis[C[C.length - 1]] = false;
                C.pop();

                // Mark current character
                // as removed
                vis[i] = false;
            }
        }

        // Print the remaining characters
        // which is not removed from S
        for (let i = 0; i < N; ++i) {

            if (vis[i])
                document.write(str[i]);
        }
    }

    // Given string
    let str = "((){()({})";

    // Size of the string
    let N = str.length;

    // Function Call
    removeValidBracketSequences(str, N);

  // This code is contributed by suresh07
</script>
```

****Output:** 

```
({
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(N)**