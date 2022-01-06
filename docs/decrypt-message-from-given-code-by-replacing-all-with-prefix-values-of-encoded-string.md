# 通过用编码字符串的前缀值替换所有*从给定代码解密消息

> 原文:[https://www . geesforgeks . org/decrypt-message-from-给定代码-通过将所有代码替换为编码字符串的前缀值/](https://www.geeksforgeeks.org/decrypt-message-from-given-code-by-replacing-all-with-prefix-values-of-encoded-string/)

给定一个长度为 **N** 的字符串 **str** ，该字符串以编码形式带有**字母**和 ***** 。任务是找到生成它的 [**字符串**](https://www.geeksforgeeks.org/string-data-structure/) 。通过**将所有 ***** 替换为编码字符串的**前缀值**，可以从编码字符串中生成所需的字符串。**

**示例:**

> **输入:** str = ab*c*d
> **输出:**“ababcababcd”
> **说明:**第一次出现**“***”，前缀为“ab”。因此“*”被“ab”替换，结果字符串为**“ababc * d”**，下一个“ ***** ”的前缀为“ababc”。所以现在弦会从**“ababc * d”**变成**“ababc ababcd”。**
> 
> **输入:**str = " z * z * z "
> T3】输出: zzzzzzz

**进场:**解决方案基于[贪婪](http://www.geeksforgeeks.org/greedy-algorithms/)进场。按照下面提到的步骤解决问题:

*   考虑一个空字符串**结果**。
*   迭代给定的编码字符串。
    *   如果字符串中的当前字符是**而不是“***”，则**将当前字符添加到**结果**中。**
    *   否则，如果当前字符是“*”，**加上**将会产生**结果**字符串，直到现在**和它本身**一起形成。
*   返回结果。

下面是给定方法的实现。

## C++

```
// C++ code to implement above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return a string
// found from the coded string
string findstring(string str)
{
    // Declaring string to store result
    string result = "";

    // Loop to generate the original string
    for (int i = 0; str[i] != '\0'; i++) {
        // If current character in string
        // is '*' add result to itself
        if (str[i] == '*')
            result += result;

        // Else add current element only
        else
            result += str[i];
    }
    // Return the result
    return result;
}

// Driver code
int main()
{
    string str = "ab*c*d";
    cout << findstring(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement above approach
class GFG {

    // Function to return a string
    // found from the coded string
    static String findstring(String str)
    {

        // Declaring string to store result
        String result = "";

        // Loop to generate the original string
        for (int i = 0; i < str.length(); i++) {

            // If current character in string
            // is '*' add result to itself
            if (str.charAt(i) == '*')
                result += result;

            // Else add current element only
            else
                result += str.charAt(i);
        }

        // Return the result
        return result;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "ab*c*d";
        System.out.println(findstring(str));
    }
}

// This code is contributed by ukasp.
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to return a string
# found from the coded string
def findstring(str):

    # Declaring string to store result
    result = ""

    # Loop to generate the original string
    for i in range(len(str)):

        # If current character in string
        # is '*' add result to itself
        if (str[i] == '*'):
                result += result

        # Else add current element only
        else:
                result += str[i]
    # Return the result
    return result

# Driver code
str = "ab*c*d"
print(findstring(str))

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# code to implement above approach
using System;
class GFG
{

  // Function to return a string
  // found from the coded string
  static string findstring(string str)
  {

    // Declaring string to store result
    string result = "";

    // Loop to generate the original string
    for (int i = 0; i < str.Length; i++)
    {

      // If current character in string
      // is '*' add result to itself
      if (str[i] == '*')
        result += result;

      // Else add current element only
      else
        result += str[i];
    }

    // Return the result
    return result;
  }

  // Driver code
  public static void Main()
  {
    string str = "ab*c*d";
    Console.Write(findstring(str));

  }
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
   // JavaScript code for the above approach

   // Function to return a string
   // found from the coded string
   function findstring(str) {
     // Declaring string to store result
     let result = "";

     // Loop to generate the original string
     for (let i = 0; i < str.length; i++) {
       // If current character in string
       // is '*' add result to itself
       if (str[i] == '*')
         result += result;

       // Else add current element only
       else
         result += str[i];
     }
     // Return the result
     return result;
   }

   // Driver code

   let str = "ab*c*d";
   document.write(findstring(str));

 // This code is contributed by Potta Lokesh
 </script>
```

**Output**

```
ababcababcd
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)