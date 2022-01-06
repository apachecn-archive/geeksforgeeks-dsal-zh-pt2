# 通过用*

替换前缀与其相同的子字符串，对给定字符串进行编码

> 原文:[https://www . geesforgeks . org/encode-给定字符串-通过用前缀替换子字符串-与自身相同-用/](https://www.geeksforgeeks.org/encode-given-string-by-replacing-substrings-with-prefix-same-as-itself-with/)

给定字符串**大小为 **N** 的字符串**，仅包含**小写英文字母**。任务是对字符串进行加密，使得前缀与其相同的子字符串被 ***** 替换。生成加密字符串。

**注意:**如果字符串可以多种方式加密，找到最小的加密字符串。

**示例:**

> **输入:** str = "ababcababcd"
> **输出:** ab*c*d
> **说明:**从第 5 个索引(基于 0 的索引)开始的子串**“ababc”**可以用“*****代替。于是弦就变成了**“ababcababcd”->“ababc * d”。**现在从第二个索引开始的子串**“ab”**又可以用“*”替换了。所以弦变成**“ab * c * d”**
> 
> **输入:** str = "zzzzzzz"
> **输出:** z*z*z
> **说明:**字符串可以用两种方式加密:“z*z*z”和“z**zzz”。在这两个“z*z*z”中，长度较小。

**方法:**生成最小加密字符串的一个简单解决方案是找到**最长的不重叠重复子串**，并首先加密该子串。要实现这一点，请使用以下步骤:

*   创建一个**栈**来存储加密的字符串。
*   声明两个指针 **(i & j)** 分别指向第一个索引和中间索引。
*   现在开始遍历字符串并重复循环，直到扫描完整个字符串。对于每个迭代，遵循下面提到的步骤:
    *   比较来自索引 **i** 和 **j** 的子串。
    *   如果两个子串**相等**，那么对这个子串重复相同的过程，并将剩余的串存储到堆栈中。
    *   否则将第二个指针 **( j )** 的值减 1。
*   现在**从堆栈中弹出**所有元素，并附加一个符号**“***，然后将其存储在输出字符串中。
*   返回加密字符串。

下面是上述方法的实现。

## C++

```
// C++ code to implement the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to generate the encrypted string
string compress(string str)
{
    // Stack to store encrypted string
    stack<string> st;

    // Variable to store length of string
    int N = str.length();

    // Variable to point 1st and middle index
    int i = 0, j = N / 2;

    // Repeat the loop until
    // the entire string is checked
    while (j > 0) {
        int mid = j;

        // Compare the substring
        // from index 0 to mid-1
        // with the rest of the substring
        // after mid.
        for (i = 0; i < mid && str[i] == str[j]; i++, j++)
            ;

        // If both substrings are equal
        // then repeat the same process
        // on this substring and store
        // the remaining string into stack
        if (i == mid) {
            st.push(str.substr(j, N - 1));

            // Update the value of
            // string 'str' with the
            // longest repeating substring
            str = str.substr(0, i);

            // Set the new string length to n
            N = mid;

            // Initialize the 2nd pointer
            // from the mid of new string
            j = N / 2;
        }

        // If both substrings are not equal
        // then decrement the 2nd pointer by 1
        else {
            j = mid - 1;
        }
    }

    // Pop all the elements from the stack
    // append a symbol '*' and store
    // in a output string
    while (!st.empty()) {
        str = str + "*" + st.top();
        st.pop();
    }

    return str;
}

// Driver code
int main()
{
    // Declare and initialize the string
    string str = "zzzzzzz";

    cout << compress(str) << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement the above approach

import java.util.*;

class GFG{

// Function to generate the encrypted String
static String compress(String str)
{
    // Stack to store encrypted String
    Stack<String> st = new Stack<String>();

    // Variable to store length of String
    int N = str.length();

    // Variable to point 1st and middle index
    int i = 0, j = N / 2;

    // Repeat the loop until
    // the entire String is checked
    while (j > 0) {
        int mid = j;

        // Compare the subString
        // from index 0 to mid-1
        // with the rest of the subString
        // after mid.
        for (i = 0; i < mid && str.charAt(i) == str.charAt(j); i++, j++)
            ;

        // If both subStrings are equal
        // then repeat the same process
        // on this subString and store
        // the remaining String into stack
        if (i == mid) {
            st.add(str.substring(j,  N));

            // Update the value of
            // String 'str' with the
            // longest repeating subString
            str = str.substring(0, i);

            // Set the new String length to n
            N = mid;

            // Initialize the 2nd pointer
            // from the mid of new String
            j = N / 2;
        }

        // If both subStrings are not equal
        // then decrement the 2nd pointer by 1
        else {
            j = mid - 1;
        }
    }

    // Pop all the elements from the stack
    // append a symbol '*' and store
    // in a output String
    while (!st.isEmpty()) {
        str = str + "*" + st.peek();
        st.pop();
    }

    return str;
}

// Driver code
public static void main(String[] args)
{
    // Declare and initialize the String
    String str = "zzzzzzz";

    System.out.print(compress(str)+ "\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to generate the encrypted string
def compress(str):

    # Stack to store encrypted string
    st = []

    # Variable to store length of string
    N = len(str)

    # Variable to point 1st and middle index
    i = 0
    j = (int)(N / 2)

    # Repeat the loop until
    # the entire string is checked
    while (j > 0):
        mid = j

        # Compare the substring
        # from index 0 to mid-1
        # with the rest of the substring
        # after mid.
        i=0
        while(str[i] == str[j] and i < mid):
            i += 1
            j += 1
        # If both substrings are equal
        # then repeat the same process
        # on this substring and store
        # the remaining string into stack
        if (i == mid):
            st.append(str[j:N])

            # Update the value of
            # string 'str' with the
            # longest repeating substring
            str = str[0:i]

            # Set the new string length to n
            N = mid

            # Initialize the 2nd pointer
            # from the mid of new string
            j = N // 2

        # If both substrings are not equal
        # then decrement the 2nd pointer by 1
        else:
            j = mid - 1

    # Pop all the elements from the stack
    # append a symbol '*' and store
    # in a output string
    while (len(st) != 0):
        str = str + '*' + st[len(st) - 1]
        st.pop()
    return str

# Driver code

# Declare and initialize the string
str = "zzzzzzz"
print(compress(str))

# This code is contributed by Saurabh jaiswal
```

## C#

```
// C# code to implement the above approach
using System;
using System.Collections.Generic;

public class GFG{

// Function to generate the encrypted String
static String compress(String str)
{
    // Stack to store encrypted String
    Stack<String> st = new Stack<String>();

    // Variable to store length of String
    int N = str.Length;

    // Variable to point 1st and middle index
    int i = 0, j = N / 2;

    // Repeat the loop until
    // the entire String is checked
    while (j > 0) {
        int mid = j;

        // Compare the subString
        // from index 0 to mid-1
        // with the rest of the subString
        // after mid.
        for (i = 0; i < mid && str[i] == str[j]; i++, j++)
            ;

        // If both subStrings are equal
        // then repeat the same process
        // on this subString and store
        // the remaining String into stack
        if (i == mid) {
            st.Push(str.Substring(j,  N-j));

            // Update the value of
            // String 'str' with the
            // longest repeating subString
            str = str.Substring(0, i);

            // Set the new String length to n
            N = mid;

            // Initialize the 2nd pointer
            // from the mid of new String
            j = N / 2;
        }

        // If both subStrings are not equal
        // then decrement the 2nd pointer by 1
        else {
            j = mid - 1;
        }
    }

    // Pop all the elements from the stack
    // append a symbol '*' and store
    // in a output String
    while (st.Count!=0) {
        str = str + "*" + st.Peek();
        st.Pop();
    }

    return str;
}

// Driver code
public static void Main(String[] args)
{
    // Declare and initialize the String
    String str = "zzzzzzz";

    Console.Write(compress(str)+ "\n");
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
  // JavaScript code for the above approach

  // Function to generate the encrypted string
  function compress(str) 
  {

    // Stack to store encrypted string
    let st = [];

    // Variable to store length of string
    let N = str.length;

    // Variable to point 1st and middle index
    let i = 0, j = Math.floor(N / 2);

    // Repeat the loop until
    // the entire string is checked
    while (j > 0) {
      let mid = j;

      // Compare the substring
      // from index 0 to mid-1
      // with the rest of the substring
      // after mid.
      for (i = 0; i < mid && str[i] == str[j]; i++, j++)
        ;

      // If both substrings are equal
      // then repeat the same process
      // on this substring and store
      // the remaining string into stack
      if (i == mid) {
        st.push(str.slice(j, N));

        // Update the value of
        // string 'str' with the
        // longest repeating substring
        str = str.slice(0, i);

        // Set the new string length to n
        N = mid;

        // Initialize the 2nd pointer
        // from the mid of new string
        j = Math.floor(N / 2);
      }

      // If both substrings are not equal
      // then decrement the 2nd pointer by 1
      else {
        j = mid - 1;
      }
    }

    // Pop all the elements from the stack
    // append a symbol '*' and store
    // in a output string
    while (st.length != 0) {
      str = str + '*' + st[st.length - 1];
      st.pop();
    }

    return str;
  }

  // Driver code

  // Declare and initialize the string
  let str = "zzzzzzz";

  document.write(compress(str) + '<br>');

// This code is contributed by Potta Lokesh
</script>
```

**Output**

```
z*z*z
```

**时间复杂度:** O(N. Log(N))
**辅助空间:** O(N)