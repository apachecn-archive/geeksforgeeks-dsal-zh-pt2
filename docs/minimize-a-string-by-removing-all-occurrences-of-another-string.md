# 通过移除另一个字符串的所有出现来最小化一个字符串

> 原文:[https://www . geeksforgeeks . org/通过删除另一个字符串的所有出现次数来最小化一个字符串/](https://www.geeksforgeeks.org/minimize-a-string-by-removing-all-occurrences-of-another-string/)

给定两个长度分别为 **N** 和**M****、**的字符串 **S1** 和 **S2** ，由小写字母组成，任务是通过从字符串 **S1** 中移除字符串 **S2** 的所有出现，找到 **S1** 可以减少的最小长度。

**示例:**

> **输入:**S1 =“fffoxoxfxo”，S2 =“fox”；
> **输出:** 3
> **解释:**
> 通过从索引 2 开始移除“fox”，字符串修改为“ffoxoxfxo”。
> 通过从索引 1 开始移除“fox”，字符串修改为“foxfxo”。
> 通过从索引 0 开始移除“fox”，字符串修改为“fxo”。
> 因此，去除所有 S2 事件后，字符串 S1 的最小长度为 3。
> 
> **输入:**S1 =“ABCD”，S2 =“pqr”
> T3】输出: 4

**方法:**解决这个问题的思路是使用[栈数据结构](https://www.geeksforgeeks.org/stack-data-structure/)。按照以下步骤解决给定的问题:

*   初始化一个堆栈，在其中存储字符串 **S1** 的字符。
*   [遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)**【S1】**并执行以下操作:
    *   [推送堆栈中的当前字符。](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)
    *   如果栈的[大小至少为**M**，则检查栈](https://www.geeksforgeeks.org/stack-size-method-in-java-with-example/)的[顶 **M** 字符是否构成字符串 **S2** 。如果发现是真的，那么删除那些字符。](https://www.geeksforgeeks.org/stack-top-c-stl/)
*   完成上述步骤后，堆叠的剩余[尺寸为所需的最小长度。](https://www.geeksforgeeks.org/stack-empty-and-stack-size-in-c-stl/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>

using namespace std;

// Function to find the minimum length
// to which string str can be reduced to
// by removing all occurrences of string K
int minLength(string str, int N,
              string K, int M)
{

    // Initialize stack of characters
    stack<char> stackOfChar;

    for (int i = 0; i < N; i++) {

        // Push character into the stack
        stackOfChar.push(str[i]);

        // If stack size >= K.size()
        if (stackOfChar.size() >= M) {

            // Create empty string to
            // store characters of stack
            string l = "";

            // Traverse the string K in reverse
            for (int j = M - 1; j >= 0; j--) {

                // If any of the characters
                // differ, it means that K
                // is not present in the stack
                if (K[j] != stackOfChar.top()) {

                    // Push the elements
                    // back into the stack
                    int f = 0;
                    while (f != l.size()) {

                        stackOfChar.push(l[f]);
                        f++;
                    }

                    break;
                }

                // Store the string
                else {

                    l = stackOfChar.top()
                        + l;

                    // Remove top element
                    stackOfChar.pop();
                }
            }
        }
    }

    // Size of stack gives the
    // minimized length of str
    return stackOfChar.size();
}

// Driver Code
int main()
{
    string S1 = "fffoxoxoxfxo";
    string S2 = "fox";

    int N = S1.length();
    int M = S2.length();

    // Function Call
    cout << minLength(S1, N, S2, M);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to find the minimum length
// to which String str can be reduced to
// by removing all occurrences of String K
static int minLength(String str, int N,
              String K, int M)
{

    // Initialize stack of characters
    Stack<Character> stackOfChar = new Stack<Character>();

    for (int i = 0; i < N; i++)
    {

        // Push character into the stack
        stackOfChar.add(str.charAt(i));

        // If stack size >= K.size()
        if (stackOfChar.size() >= M)
        {

            // Create empty String to
            // store characters of stack
            String l = "";

            // Traverse the String K in reverse
            for (int j = M - 1; j >= 0; j--)
            {

                // If any of the characters
                // differ, it means that K
                // is not present in the stack
                if (K.charAt(j) != stackOfChar.peek())
                {

                    // Push the elements
                    // back into the stack
                    int f = 0;
                    while (f != l.length())
                    {
                        stackOfChar.add(l.charAt(f));
                        f++;
                    }

                    break;
                }

                // Store the String
                else
                {
                    l = stackOfChar.peek()
                        + l;

                    // Remove top element
                    stackOfChar.pop();
                }
            }
        }
    }

    // Size of stack gives the
    // minimized length of str
    return stackOfChar.size();
}

// Driver Code
public static void main(String[] args)
{
    String S1 = "fffoxoxoxfxo";
    String S2 = "fox";

    int N = S1.length();
    int M = S2.length();

    // Function Call
    System.out.print(minLength(S1, N, S2, M));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum length
# to which string str can be reduced to
# by removing all occurrences of string K
def minLength(Str, N, K, M) :

    # Initialize stack of characters
    stackOfChar = []

    for i in range(N) :

        # Push character into the stack
        stackOfChar.append(Str[i])

        # If stack size >= K.size()
        if (len(stackOfChar) >= M) :

            # Create empty string to
            # store characters of stack
            l = ""

            # Traverse the string K in reverse
            for j in range(M - 1, -1, -1) :

                # If any of the characters
                # differ, it means that K
                # is not present in the stack
                if (K[j] != stackOfChar[-1]) :

                    # Push the elements
                    # back into the stack
                    f = 0
                    while (f != len(l)) :
                        stackOfChar.append(l[f])
                        f += 1

                    break

                # Store the string
                else :
                    l = stackOfChar[-1] + l

                    # Remove top element
                    stackOfChar.pop()

    # Size of stack gives the
    # minimized length of str
    return len(stackOfChar)

# Driver code 
S1 = "fffoxoxoxfxo"
S2 = "fox"

N = len(S1)
M = len(S2)

# Function Call
print(minLength(S1, N, S2, M))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

// Function to find the minimum length
// to which String str can be reduced to
// by removing all occurrences of String K
static int minLength(String str, int N,
              String K, int M)
{

    // Initialize stack of characters
    Stack<char> stackOfChar = new Stack<char>();
    for (int i = 0; i < N; i++)
    {

        // Push character into the stack
        stackOfChar.Push(str[i]);

        // If stack size >= K.Count
        if (stackOfChar.Count >= M)
        {

            // Create empty String to
            // store characters of stack
            String l = "";

            // Traverse the String K in reverse
            for (int j = M - 1; j >= 0; j--)
            {

                // If any of the characters
                // differ, it means that K
                // is not present in the stack
                if (K[j] != stackOfChar.Peek())
                {

                    // Push the elements
                    // back into the stack
                    int f = 0;
                    while (f != l.Length)
                    {
                        stackOfChar.Push(l[f]);
                        f++;
                    }
                    break;
                }

                // Store the String
                else
                {
                    l = stackOfChar.Peek()
                        + l;

                    // Remove top element
                    stackOfChar.Pop();
                }
            }
        }
    }

    // Size of stack gives the
    // minimized length of str
    return stackOfChar.Count;
}

// Driver Code
public static void Main(String[] args)
{
    String S1 = "fffoxoxoxfxo";
    String S2 = "fox";

    int N = S1.Length;
    int M = S2.Length;

    // Function Call
    Console.Write(minLength(S1, N, S2, M));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the minimum length
// to which string str can be reduced to
// by removing all occurrences of string K
function minLength(str, N, K, M)
{

    // Initialize stack of characters
    var stackOfChar = [];

    for (var i = 0; i < N; i++) {

        // Push character into the stack
        stackOfChar.push(str[i]);

        // If stack size >= K.size()
        if (stackOfChar.length >= M) {

            // Create empty string to
            // store characters of stack
            var l = "";

            // Traverse the string K in reverse
            for (var j = M - 1; j >= 0; j--) {

                // If any of the characters
                // differ, it means that K
                // is not present in the stack
                if (K[j] != stackOfChar[stackOfChar.length-1]) {

                    // Push the elements
                    // back into the stack
                    var f = 0;
                    while (f != l.length) {

                        stackOfChar.push(l[f]);
                        f++;
                    }

                    break;
                }

                // Store the string
                else {

                    l = stackOfChar[stackOfChar.length-1]
                        + l;

                    // Remove top element
                    stackOfChar.pop();
                }
            }
        }
    }

    // Size of stack gives the
    // minimized length of str
    return stackOfChar.length;
}

// Driver Code
var S1 = "fffoxoxoxfxo";
var S2 = "fox";
var N = S1.length;
var M = S2.length;

// Function Call
document.write( minLength(S1, N, S2, M));

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(N)*