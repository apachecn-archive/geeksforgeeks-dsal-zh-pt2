# 仅包含一次所有不同字符的字典序最大子序列

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的包含所有不同字符的最大子序列-仅一次/](https://www.geeksforgeeks.org/lexicographically-largest-subsequence-containing-all-distinct-characters-only-once/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是找到[字典上最大的子序列](https://www.geeksforgeeks.org/lexicographically-largest-sub-sequence-of-the-given-string/)，该子序列可以使用给定字符串中的所有不同字符只形成一次。

**示例:**

> **输入:**S = ababc
> T3】输出: bac
> **解释:**
> 包含 S 中所有字符恰好一次的所有可能的子序列为{“ABC”、“BAC”}。所有子序列中词汇顺序最大的是“bac”。
> 
> **输入:**S = " zydsbacab "
> T3】输出: zydscab

**方法:**给定的问题可以使用 [**栈**](https://www.geeksforgeeks.org/stack-data-structure/) 来解决。其思想是[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)，并将这些字符以字典上最大的顺序存储在堆栈中，从而生成结果字符串。按照以下步骤解决给定的问题:

*   [将字符串](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/) **S** 的所有字符的频率存储在一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)中，比如**count【】**。
*   初始化一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，比如说**访问了【】**，该数组存储堆栈中是否存在任何字符。
*   [使用变量 **i** 遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，并执行以下步骤:
    *   通过 **1** 减少**计数【】**中字符**S【I】**的频率。
    *   现在，如果该角色已经出现在堆栈中，则[继续下一次迭代](https://www.geeksforgeeks.org/continue-statement-cpp/)。
    *   否则，检查当前字符是否大于堆栈中的顶部字符，顶部字符的频率是否大于 **0** ，然后继续从堆栈中弹出[顶部元素。](https://www.geeksforgeeks.org/stack-top-c-stl/)
    *   完成上述步骤后，在数组**中添加当前字符并标记为已访问【】**。
*   完成上述步骤后，使用堆栈中的字符生成字符串，并打印其反面，以获得[字典顺序上最大的子序列](https://www.geeksforgeeks.org/lexicographically-largest-sub-sequence-of-the-given-string/)。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the lexicographically
// largest subsequence consisting of all
// distinct characters of S only once
string lexicoMaxSubsequence(string s, int n)
{
    stack<char> st;

    // Stores if any alphabet is present
    // in the current stack
    vector<int> visited(26, 0), cnt(26, 0);

    // Findthe number of occurences of
    // the character s[i]
    for (int i = 0; i < n; i++) {
        cnt[s[i] - 'a']++;
    }
    for (int i = 0; i < n; i++) {

        // Decrease the character count
        // in remaining string
        cnt[s[i] - 'a']--;

        // If character is already present
        // in the stack
        if (visited[s[i] - 'a']) {
            continue;
        }

        // if current character is greater
        // than last character in stack
        // then pop the top character
        while (!st.empty() && st.top() < s[i]
               && cnt[st.top() - 'a'] != 0) {
            visited[st.top() - 'a'] = 0;
            st.pop();
        }

        // Push the current character
        st.push(s[i]);
        visited[s[i] - 'a'] = 1;
    }

    // Stores the resultant string
    string s1;

    // Generate the string
    while (!st.empty()) {
        s1 = st.top() + s1;
        st.pop();
    }

    // Return the resultant string
    return s1;
}

// Driver Code
int main()
{
    string S = "ababc";
    int N = S.length();
    cout << lexicoMaxSubsequence(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;

class GFG {
    // Function to find the lexicographically
    // largest subsequence consisting of all
    // distinct characters of S only once
    static String lexicoMaxSubsequence(String s, int n)
    {
        Stack<Character> st = new Stack<Character>();

        // Stores if any alphabet is present
        // in the current stack
        int[] visited = new int[26];
        int[] cnt = new int[26];
        for (int i = 0; i < 26; i++) {
            visited[i] = 0;
            cnt[i] = 0;
        }

        // Findthe number of occurences of
        // the character s[i]
        for (int i = 0; i < n; i++) {
            cnt[s.charAt(i) - 'a']++;
        }
        for (int i = 0; i < n; i++) {

            // Decrease the character count
            // in remaining string
            cnt[s.charAt(i) - 'a']--;

            // If character is already present
            // in the stack
            if (visited[s.charAt(i) - 'a'] > 0) {
                continue;
            }

            // if current character is greater
            // than last character in stack
            // then pop the top character
            while (!st.empty() && st.peek() < s.charAt(i)
                   && cnt[st.peek() - 'a'] != 0) {
                visited[st.peek() - 'a'] = 0;
                st.pop();
            }

            // Push the current character
            st.push(s.charAt(i));
            visited[s.charAt(i) - 'a'] = 1;
        }

        // Stores the resultant string
        String s1 = "";

        // Generate the string
        while (!st.empty()) {
            s1 = st.peek() + s1;
            st.pop();
        }

        // Return the resultant string
        return s1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String S = "ababc";
        int N = S.length();
        System.out.println(lexicoMaxSubsequence(S, N));
    }
}

// This code is contributed by maddler.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the lexicographically
# largest subsequence consisting of all
# distinct characters of S only once
def lexicoMaxSubsequence(s, n):
    st = []

    # Stores if any alphabet is present
    # in the current stack
    visited = [0]*(26)
    cnt = [0]*(26)
    for i in range(26):
        visited[i] = 0
        cnt[i] = 0

    # Findthe number of occurences of
    # the character s[i]
    for i in range(n):
        cnt[ord(s[i]) - ord('a')]+=1
    for i in range(n):
        # Decrease the character count
        # in remaining string
        cnt[ord(s[i]) - ord('a')]-=1

        # If character is already present
        # in the stack
        if (visited[ord(s[i]) - ord('a')] > 0):
            continue

        # if current character is greater
        # than last character in stack
        # then pop the top character
        while (len(st) > 0 and ord(st[-1]) < ord(s[i]) and cnt[ord(st[-1]) - ord('a')] != 0):
            visited[ord(st[-1]) - ord('a')] = 0
            st.pop()

        # Push the current character
        st.append(s[i])
        visited[ord(s[i]) - ord('a')] = 1

    # Stores the resultant string
    s1 = ""

    # Generate the string
    while (len(st) > 0):
        s1 = st[-1] + s1
        st.pop()

    # Return the resultant string
    return s1

S = "ababc"
N = len(S)
print(lexicoMaxSubsequence(S, N))

# This code is contributed by decode2207.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to find the lexicographically
    // largest subsequence consisting of all
    // distinct characters of S only once
    static string lexicoMaxSubsequence(string s, int n)
    {
        Stack<char> st = new Stack<char>();

        // Stores if any alphabet is present
        // in the current stack
        int[] visited = new int[26];
        int[] cnt = new int[26];
        for (int i = 0; i < 26; i++) {
            visited[i] = 0;
            cnt[i] = 0;
        }

        // Findthe number of occurences of
        // the character s[i]
        for (int i = 0; i < n; i++) {
            cnt[s[i] - 'a']++;
        }
        for (int i = 0; i < n; i++) {

            // Decrease the character count
            // in remaining string
            cnt[s[i] - 'a']--;

            // If character is already present
            // in the stack
            if (visited[s[i] - 'a'] > 0) {
                continue;
            }

            // if current character is greater
            // than last character in stack
            // then pop the top character
            while (st.Count > 0 && st.Peek() < s[i]
                   && cnt[st.Peek() - 'a'] != 0) {
                visited[st.Peek() - 'a'] = 0;
                st.Pop();
            }

            // Push the current character
            st.Push(s[i]);
            visited[s[i] - 'a'] = 1;
        }

        // Stores the resultant string
        string s1 = "";

        // Generate the string
        while (st.Count > 0) {
            s1 = st.Peek() + s1;
            st.Pop();
        }

        // Return the resultant string
        return s1;
    }

  static void Main() {
    string S = "ababc";
    int N = S.Length;
    Console.Write(lexicoMaxSubsequence(S, N));
  }
}

// This code is contributed by suresh07.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to find the lexicographically
    // largest subsequence consisting of all
    // distinct characters of S only once
    function lexicoMaxSubsequence(s, n)
    {
        let st = [];

        // Stores if any alphabet is present
        // in the current stack
        let visited = new Array(26);
        let cnt = new Array(26);
        for (let i = 0; i < 26; i++) {
            visited[i] = 0;
            cnt[i] = 0;
        }

        // Findthe number of occurences of
        // the character s[i]
        for (let i = 0; i < n; i++) {
            cnt[s[i].charCodeAt() - 'a'.charCodeAt()]++;
        }
        for (let i = 0; i < n; i++) {

            // Decrease the character count
            // in remaining string
            cnt[s[i].charCodeAt() - 'a'.charCodeAt()]--;

            // If character is already present
            // in the stack
            if (visited[s[i].charCodeAt() - 'a'.charCodeAt()] > 0) {
                continue;
            }

            // if current character is greater
            // than last character in stack
            // then pop the top character
            while (st.length > 0 && st[st.length - 1].charCodeAt() < s[i].charCodeAt()
                   && cnt[st[st.length - 1].charCodeAt() - 'a'.charCodeAt()] != 0) {
                visited[st[st.length - 1].charCodeAt() - 'a'.charCodeAt()] = 0;
                st.pop();
            }

            // Push the current character
            st.push(s[i]);
            visited[s[i].charCodeAt() - 'a'.charCodeAt()] = 1;
        }

        // Stores the resultant string
        let s1 = "";

        // Generate the string
        while (st.length > 0) {
            s1 = st[st.length - 1] + s1;
            st.pop();
        }

        // Return the resultant string
        return s1;
    }

    let S = "ababc";
    let N = S.length;
    document.write(lexicoMaxSubsequence(S, N));

    // This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
bac
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)