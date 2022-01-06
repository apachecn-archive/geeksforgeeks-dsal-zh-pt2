# 从给定的有效括号序列中找到长度为 K 的有效括号序列

> 原文:[https://www . geeksforgeeks . org/find-a-valid-括号-长度序列-k-from-给定-valid-括号-序列/](https://www.geeksforgeeks.org/find-a-valid-parenthesis-sequence-of-length-k-from-a-given-valid-parenthesis-sequence/)

给定长度为 **N** 的有效括号序列的字符串 **S** 和偶数 **K** ，任务是找到长度为 **K** 的有效括号序列，它也是给定字符串的子序列。

**注意:**可以有多个有效序列，打印任意一个。

**示例:**

> **输入:** S =()())”，K = 4
> **输出:** ()()
> **解释:**
> 字符串“()()”是长度为 4 的子序列，是有效的括号序列。
> 
> **输入:** S =()((()))”，K = 6
> **输出:**()()
> **解释:**
> 字符串“()(())”是长度为 6 的子序列，是有效的括号序列。

**天真方法:**想法是[生成给定字符串的所有可能的长度子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)**K**，并打印任何具有有效括号序列的字符串。
***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(K)*

**高效方法:**上述方法可以使用[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)进行优化。其思想是遍历给定的字符串，当遇到左括号字符时，将它推到堆栈中，或者从中弹出一个字符。相应地，每次弹出一个字符时递增计数器。按照以下步骤解决问题:

1.  创建一个堆栈和布尔数组，初始化为**假**。
2.  遍历给定的字符串，如果遇到左括号，将该索引推入堆栈。
3.  否则，如果遇到右大括号:
    *   从堆栈中弹出顶部元素
    *   将计数器增加 **2**
    *   将弹出和当前索引标记为真。
4.  如果计数器超过 **K** ，终止。
5.  遍历后，从左到右将所有字符附加在一起，标记为 true。打印形成的结果字符串。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
#define ll long long
using namespace std;

// Function to find the subsequence
// of length K forming valid sequence
string findString(string s, int k)
{
    int n = s.length();

    // Stores the resultant string
    string ans = "";
    stack<int> st;

    // Check whether character at
    // index i is visited or not
    vector<bool> vis(n, false);
    int count = 0;

    // Traverse the string
    for (int i = 0; i < n; ++i) {

        // Push index of open bracket
        if (s[i] == '(') {
            st.push(i);
        }

        // Pop and mark visited
        if (count < k && s[i] == ')') {

            vis[st.top()] = 1;
            st.pop();
            vis[i] = true;

            // Increment count by 2
            count += 2;
        }
    }

    // Append the characters and create
    // the resultant string
    for (int i = 0; i < n; ++i) {

        if (vis[i] == true) {
            ans += s[i];
        }
    }

    // Return the resultant string
    return ans;
}

// Driver Code
int main()
{
    string s = "()()()";
    int K = 2;

    // Function Call
    cout << findString(s, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the subsequence
// of length K forming valid sequence
static String findString(String s, int k)
{
    int n = s.length();

    // Stores the resultant String
    String ans = " ";
    Stack<Integer> st = new Stack<>();

    // Check whether character at
    // index i is visited or not
    boolean []vis = new boolean[n];

    // Vector<boolean> vis(n, false);
    int count = 0;

    // Traverse the String
    for(int i = 0; i < n; ++i)
    {

        // Push index of open bracket
        if (s.charAt(i) == '(')
        {
            st.add(i);
        }

        // Pop and mark visited
        if (count < k && s.charAt(i) == ')')
        {
            vis[st.peek()] = true;
            st.pop();
            vis[i] = true;

            // Increment count by 2
            count += 2;
        }
    }

    // Append the characters and create
    // the resultant String
    for(int i = 0; i < n; ++i)
    {
        if (vis[i] == true)
        {
            ans += s.charAt(i);
        }
    }

    // Return the resultant String
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    String s = "()()()";
    int K = 2;

    // Function call
    System.out.print(findString(s, K));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the subsequence
# of length K forming valid sequence
def findString(s, k):

    n = len(s)

    # Stores the resultant string
    ans = ""
    st = []

    # Check whether character at
    # index i is visited or not
    vis = [False] * n
    count = 0

    # Traverse the string
    for i in range(n):

        # Push index of open bracket
        if (s[i] == '('):
            st.append(i)

        # Pop and mark visited
        if (count < k and s[i] == ')'):
            vis[st[-1]] = 1
            del st[-1]
            vis[i] = True

            # Increment count by 2
            count += 2

    # Append the characters and create
    # the resultant string
    for i in range(n):
        if (vis[i] == True):
            ans += s[i]

    # Return the resultant string
    return ans

# Driver Code
if __name__ == '__main__':

    s = "()()()"
    K = 2

    # Function call
    print(findString(s, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to find the
// subsequence of length
// K forming valid sequence
static String findString(String s,
                         int k)
{
  int n = s.Length;

  // Stores the resultant String
  String ans = " ";
  Stack<int> st = new Stack<int>();

  // Check whether character at
  // index i is visited or not
  bool []vis = new bool[n];

  // List<bool> vis(n, false);
  int count = 0;

  // Traverse the String
  for(int i = 0; i < n; ++i)
  {
    // Push index of open bracket
    if (s[i] == '(')
    {
      st.Push(i);
    }

    // Pop and mark visited
    if (count < k && s[i] == ')')
    {
      vis[st.Peek()] = true;
      st.Pop();
      vis[i] = true;

      // Increment count by 2
      count += 2;
    }
  }

  // Append the characters and create
  // the resultant String
  for(int i = 0; i < n; ++i)
  {
    if (vis[i] == true)
    {
      ans += s[i];
    }
  }

  // Return the resultant String
  return ans;
}

// Driver Code
public static void Main(String[] args)
{
  String s = "()()()";
  int K = 2;

  // Function call
  Console.Write(findString(s, K));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
      // JavaScript program for
      // the above approach

      // Function to find the
      // subsequence of length
      // K forming valid sequence
      function findString(s, k) {
        var n = s.length;

        // Stores the resultant String
        var ans = " ";
        var st = [];

        // Check whether character at
        // index i is visited or not
        var vis = new Array(n);

        // List<bool> vis(n, false);
        var count = 0;

        // Traverse the String
        for (var i = 0; i < n; ++i) {
          // Push index of open bracket
          if (s[i] === "(") {
            st.push(i);
          }

          // Pop and mark visited
          if (count < k && s[i] === ")") {
            vis[st[st.length - 1]] = true;
            st.pop();
            vis[i] = true;

            // Increment count by 2
            count += 2;
          }
        }

        // Append the characters and create
        // the resultant String
        for (var i = 0; i < n; ++i) {
          if (vis[i] === true) {
            ans += s[i];
          }
        }

        // Return the resultant String
        return ans;
      }

      // Driver Code
      var s = "()()()";
      var K = 2;

      // Function call
      document.write(findString(s, K));

</script>
```

**Output:** 

```
()
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)