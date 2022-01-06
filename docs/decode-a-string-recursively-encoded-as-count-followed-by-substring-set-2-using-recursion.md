# 解码递归编码为计数后跟子串|集合 2 的字符串(使用递归)

> 原文:[https://www . geesforgeks . org/decode-a-string-recursive-encoded-as-count-后跟-substring-set-2-use-recursive/](https://www.geeksforgeeks.org/decode-a-string-recursively-encoded-as-count-followed-by-substring-set-2-using-recursion/)

给出了一个编码字符串**字符串**。字符串的编码模式如下。

> <count>[sub_str] == >子串‘sub _ str’出现计数次数。</count>

任务是解码这个字符串**字符串**。

**示例:**

> **输入:** str = "1[b]"
> **输出:** b
> **说明:**子串‘b’重复 1 次。
> 
> **输入:** str = "2[ab]"
> **输出:** abab
> **说明:**子串“ab”重复两次。
> 
> **输入:** str = "2[a2[b]]"
> **输出:**abbb
> **说明:**子串‘b’重复 2 次，加到‘a’上，形成子串‘abb’。
> 现在这个子串重复两次。所以最后一串是“abbabb”。

**迭代方式:**这个问题的 [**集-1**](https://www.geeksforgeeks.org/decode-string-recursively-encoded-count-followed-substring/) 中提到了迭代方式。

**递归方法:**在本文中，将使用 [**递归**](http://www.geeksforgeeks.org/recursion/) 和 [**堆栈**](https://www.geeksforgeeks.org/stack-data-structure/) 来解决问题。遵循下面提到的方法来解决问题

*   声明一个**堆栈**
*   逐个递归遍历给定字符串的每个字符。可能有 4 种情况:
    *   **情况 1:** 当前人物为 **'['**
        *   在这种情况下不需要做任何事情。继续下一个角色
    *   **情况二:**当前人物为**‘】’**
        *   从堆栈中弹出**顶部字符串温度**和**顶部整数 x**
        *   **重复**字符串温度，x 次
        *   如果堆栈中的下一个顶部元素是字符串，则将这个重复的字符串追加到顶部字符串
        *   否则将重复的字符串推入堆栈
    *   **情况 3:** 当前字符为**数字**
        *   如果原始字符串的前一个字符也是一个数字，则将该数字附加到堆栈顶部的数字上
        *   如果前一个字符是其他字符，将这个数字推入堆栈
    *   **情况 4:** 当前字符是一个**字母**
        *   如果原始字符串的前一个字符也是一个字母，则将这个字母附加到堆栈顶部的字符串中
        *   如果前一个字符是其他字符，将这个字母推入堆栈
*   最后，返回堆栈中的字符串并打印出来

下面是上述方法的实现。

## C++

```
// C++ code to implement above approach
#include <bits/stdc++.h>
using namespace std;

// Stack to store intermediate strings
stack<string> ans;
string res = "";

// Recusrsive function to decode
// the encoded string
void decode(string s, int i)
{ 
    if (i == s.length()) {
        res = ans.top();
        return;
    }

    // If the string character is '['
    if (s[i] == '[');

    // If the string character is ']'
    else if (s[i] == ']') { 
        string temp = ans.top();
        ans.pop();
        int x = stoi(ans.top());
        ans.pop();
        for (string j = temp; x > 1; x--)
            temp = temp + j;
        string temp1
            = ans.empty() == false ?
            ans.top() : "";

        if (!temp1.empty() &&
            !(temp1[0] - '0' < 10)) {
            ans.pop();
            temp1 = temp1 + temp;
            ans.push(temp1);
        }
        else {
            ans.push(temp);
        }
    }

    // If string character is a digit
    else if (s[i] - '0' < 10) {     
        string temp =
            ans.empty() == false ?
            ans.top() : "";

        if (!temp.empty() &&
            temp[0] - '0' < 10
            && s[i - 1] - '0' < 10) {
            ans.pop();
            temp = temp + s[i];
            ans.push(temp);
        }
        else {
            temp = s[i];
            ans.push(temp);
        }     
    }

    // If the string character is alphabet
    else if (s[i] - 'a' < 26) {     
        string temp =
            ans.empty() == false ?
            ans.top() : "";

        if (!temp.empty() &&
            temp[0] - 'a' >= 0
            && temp[0] - 'a' < 26) {
            ans.pop();
            temp = temp + s[i];
            ans.push(temp);
        }
        else {
            temp = s[i];
            ans.push(temp);
        }   
    }

    // Recursive call for next index
    decode(s, i + 1);
}

// Function to call the recursive function
string decodeString(string s)
{
    decode(s, 0);
    return res;
}

// Driver code
int main()
{
    string str = "2[a2[b]]";
    cout << decodeString(str) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement above approach
import java.util.*;
class GFG{

  // Stack to store intermediate Strings
  static Stack<String> ans = new Stack<String>();
  static String res = "";

  // Recusrsive function to decode
  // the encoded String
  static void decode(char[] s, int i)
  { 
    if (i == s.length) {
      res = ans.peek();
      return;
    }

    // If the String character is '['
    if (s[i] == '[');

    // If the String character is ']'
    else if (s[i] == ']') { 
      String temp = ans.peek();
      ans.pop();
      int x = Integer.valueOf(ans.peek());
      ans.pop();
      for (String j = temp; x > 1; x--)
        temp = temp + j;
      String temp1
        = ans.isEmpty() == false ?
        ans.peek() : "";

      if (!temp1.isEmpty() &&
          !(temp1.charAt(0) - '0' < 10)) {
        ans.pop();
        temp1 = temp1 + temp;
        ans.add(temp1);
      }
      else {
        ans.add(temp);
      }
    }

    // If String character is a digit
    else if (s[i] - '0' < 10) {     
      String temp =
        ans.isEmpty() == false ?
        ans.peek() : "";

      if (!temp.isEmpty() &&
          temp.charAt(0) - '0' < 10
          && s[i - 1] - '0' < 10) {
        ans.pop();
        temp = temp + s[i];
        ans.add(temp);
      }
      else {
        temp = String.valueOf(s[i]);
        ans.add(temp);
      }     
    }

    // If the String character is alphabet
    else if (s[i] - 'a' < 26) {     
      String temp =
        ans.isEmpty() == false ?
        ans.peek() : "";

      if (!temp.isEmpty() &&
          temp.charAt(0) - 'a' >= 0
          && temp.charAt(0) - 'a' < 26) {
        ans.pop();
        temp = temp + s[i];
        ans.add(temp);
      }
      else {
        temp = String.valueOf(s[i]);
        ans.add(temp);
      }   
    }

    // Recursive call for next index
    decode(s, i + 1);
  }

  // Function to call the recursive function
  static String decodeString(String s)
  {
    decode(s.toCharArray(), 0);
    return res;
  }

  // Driver code
  public static void main(String[] args)
  {
    String str = "2[a2[b]]";
    System.out.print(decodeString(str) +"\n");
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript code to implement above approach

// Stack to store intermediate strings
let ans = [];
let res = "";

// Recusrsive function to decode
// the encoded string
function decode(s, i)
{
    if (i == s.length)
    {
        res = ans[ans.length - 1];
        return;
    }

    // If the string character is '['
    if (s[i] == '[');

    // If the string character is ']'
    else if (s[i] == ']')
    {
        let temp = ans[ans.length - 1];
        ans.pop();
        let x = (ans[ans.length - 1]);
        ans.pop();
        for(let j = temp; x > 1; x--)
            temp = temp + j;
        let temp1 = ans.length != 0 ?
                ans[ans.length - 1] : "";

        if (!temp1.length == 0 &&
            !(temp1[0].charCodeAt(0) -
                   '0'.charCodeAt(0) < 10))
        {
            ans.pop();
            temp1 = temp1 + temp;
            ans.push(temp1);
        }
        else
        {
            ans.push(temp);
        }
    }

    // If string character is a digit
    else if (s[i].charCodeAt(0) -
              '0'.charCodeAt(0) < 10)
    {
        let temp = ans.length != 0 ?
               ans[ans.length - 1] : "";

        if (!temp.length == 0 &&
            temp[0].charCodeAt(0) -
                '0'.charCodeAt(0) < 10 &&
           s[i - 1].charCodeAt(0) -
                '0'.charCodeAt(0) < 10)
        {
            ans.pop();
            temp = temp + s[i];
            ans.push(temp);
        }
        else
        {
            temp = s[i];
            ans.push(temp);
        }
    }

    // If the string character is alphabet
    else if (s[i].charCodeAt(0) -
              'a'.charCodeAt(0) < 26)
    {
        let temp = ans.length != 0 ?
               ans[ans.length - 1] : "";

        if (!temp.length == 0 &&
            temp[0].charCodeAt(0) - 'a'.charCodeAt(0) >= 0 &&
            temp[0].charCodeAt(0) - 'a'.charCodeAt(0) < 26)
        {
            ans.pop();
            temp = temp + s[i];
            ans.push(temp);
        }
        else
        {
            temp = s[i];
            ans.push(temp);
        }
    }

    // Recursive call for next index
    decode(s, i + 1);
}

// Function to call the recursive function
function decodeString(s)
{
    decode(s, 0);
    return res;
}

// Driver code
let str = "2[a2[b]]";
document.write(decodeString(str) + '<br>');

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
abbabb
```

**时间复杂度:** O(N)其中 N 是解码字符串的长度
T3】辅助空间: O(N)