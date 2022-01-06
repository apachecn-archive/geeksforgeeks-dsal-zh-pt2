# 没有相邻字符对的最长子串是相邻的英文字母

> 原文:[https://www . geesforgeks . org/无相邻字符对的最长子串英文字母/](https://www.geeksforgeeks.org/longest-substring-with-no-pair-of-adjacent-characters-are-adjacent-english-alphabets/)

给定一个由小写英文字母组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是从给定的字符串中找到最长的[子字符串](https://www.geeksforgeeks.org/substring-in-java/)，使得没有两个相邻的字符是相邻的英文字母。

**示例:**

> **输入:** S = "aabdml"
> **输出:**【bdm】
> **说明:**子串“bdm”是满足给定条件的最长子串。
> 
> **输入:**S =【ABC】
> **输出:**【a】
> **说明:**子串“a”、“b”、“c”满足给定条件。打印其中任何一个。

**方法:**按照以下步骤解决问题:

1.  初始化一个空字符串，比如 **T** ，在迭代过程中存储所有的临时子字符串。
2.  初始化另一个字符串，比如说**和**，按照给定的条件存储最长的子串，初始化一个变量，比如说 **len** ，存储最长的子串的长度。
3.  将字符串的第一个字符[追加到**和**中。](https://www.geeksforgeeks.org/how-to-find-the-first-and-last-character-of-a-string-in-java/)
4.  [在指标**【1，S.length()】范围内遍历字符串**](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)，并执行以下操作:
    *   如果相邻字符的 [ASCII 值](https://www.geeksforgeeks.org/program-print-ascii-value-character/)的绝对差值为 **1** ，则更新 **ans** 和最长字符串的长度，并将 **T** 设置为等于当前字符，以进行下一次迭代。
    *   否则，将当前字符追加到字符串 **T** 中。
5.  再次检查最长的子字符串，并相应地更新值。
6.  打印变量**和**中获得的最长子串。

下面是上述方法的实现:

## C++

```
// C++ program for
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the longest substring
// satisfying the given condition
void findSubstring(string S)
{
    // Stores all temporary substrings
    string T = "";

    // Stores the longest substring
    string ans = "";

    // Stores the length
    // of the substring T
    int l = 0;

    // Stores the first
    // character of string S
    T += S[0];

    // Traverse the string
    for (int i = 1; i < S.length(); i++) {

        // If the absolute difference is 1
        if (abs(S[i] - S[i - 1]) == 1) {

            // Update the length of
            // substring T
            l = T.length();

            // Update the longest substring
            if (l > ans.length()) {
                ans = T;
            }

            T = "";
            T += S[i];
        }

        // Otherwise, stores the current
        // character
        else {
            T += S[i];
        }
    }

    // Again checking for
    // longest substring
    // and update accordingly
    l = (int)T.length();

    if (l > (int)ans.length()) {
        ans = T;
    }

    // Print the longest substring
    cout << ans << endl;
}

// Driver Code
int main()
{
    // Given string
    string S = "aabdml";

    // Function call to find
    // the longest substring
    // satisfying given condition
    findSubstring(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

  // Function to find the longest substring
  // satisfying the given condition
  static void findSubstring(String S)
  {

    // Stores all temporary substrings
    String T = "";

    // Stores the longest substring
    String ans = "";

    // Stores the length
    // of the substring T
    int l = 0;

    // Stores the first
    // character of string S
    T += S.charAt(0);

    // Traverse the string
    for (int i = 1; i < S.length(); i++) {

      // If the absolute difference is 1
      if (Math.abs(S.charAt(i) - S.charAt(i - 1))
          == 1) {

        // Update the length of
        // substring T
        l = T.length();

        // Update the longest substring
        if (l > ans.length()) {
          ans = T;
        }

        T = "";
        T += S.charAt(i);
      }

      // Otherwise, stores the current
      // character
      else {
        T += S.charAt(i);
      }
    }

    // Again checking for
    // longest substring
    // and update accordingly
    l = T.length();
    if (l > ans.length()) {
      ans = T;
    }

    // Print the longest substring
    System.out.println(ans);
  }

  // Driver Code
  public static void main(String[] args)
  {

    // Given string
    String S = "aabdml";

    // Function call to find
    // the longest substring
    // satisfying given condition
    findSubstring(S);
  }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to find the longest substring
# satisfying the given condition
def findSubstring(S):

    # Stores all temporary substrings
    T = ""

    # Stores the longest substring
    ans = ""

    # Stores the length
    # of the subT
    l = 0

    # Stores the first
    # character of S
    T += S[0]

    # Traverse the string
    for i in range(1,len(S)):

        # If the absolute difference is 1
        if (abs(ord(S[i]) - ord(S[i - 1])) == 1):

            # Update the length of
            # subT
            l = len(T)

            # Update the longest substring
            if (l > len(ans)):
                ans = T
            T = ""
            T += S[i]

        # Otherwise, stores the current
        # character
        else:
            T += S[i]

    # Again checking for
    # longest substring
    # and update accordingly
    l = len(T)
    if (l > len(ans)):
        ans = T

    # Print the longest substring
    print (ans)

# Driver Code
if __name__ == '__main__':

    # Given string
    S = "aabdml"

    # Function call to find
    # the longest substring
    # satisfying given condition
    findSubstring(S)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

// Function to find the longest substring
// satisfying the given condition
static void findSubstring(string S)
{

    // Stores all temporary substrings
    string T = "";

    // Stores the longest substring
    string ans = "";

    // Stores the length
    // of the substring T
    int l = 0;

    // Stores the first
    // character of string S
    T += S[0];

    // Traverse the string
    for (int i = 1; i < S.Length; i++)
    {

        // If the absolute difference is 1
        if (Math.Abs(S[i] - S[i - 1]) == 1)
        {

            // Update the length of
            // substring T
            l = T.Length;

            // Update the longest substring
            if (l > ans.Length)
            {
                ans = T;
            }

            T = "";
            T += S[i];
        }

        // Otherwise, stores the current
        // character
        else
        {
            T += S[i];
        }
    }

    // Again checking for
    // longest substring
    // and update accordingly
    l = T.Length;
    if (l > ans.Length)
    {
        ans = T;
    }

    // Print the longest substring
    Console.Write(ans);
}

// Driver Code
public static void Main(String[] args)
{

    // Given string
    string S = "aabdml";

    // Function call to find
    // the longest substring
    // satisfying given condition
    findSubstring(S);
}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

      // JavaScript program for the above approach

      // Function to find the longest substring
      // satisfying the given condition
      function findSubstring(S) {
        // Stores all temporary substrings
        var T = "";

        // Stores the longest substring
        var ans = "";

        // Stores the length
        // of the substring T
        var l = 0;

        // Stores the first
        // character of string S
        T += S[0];

        // Traverse the string
        for (var i = 1; i < S.length; i++) {
          // If the absolute difference is 1
          if (Math.abs(S[i].charCodeAt(0) -
          S[i - 1].charCodeAt(0)) === 1)
          {
            // Update the length of
            // substring T
            l = T.length;

            // Update the longest substring
            if (l > ans.length) {
              ans = T;
            }

            T = "";
            T += S[i];
          }

          // Otherwise, stores the current
          // character
          else {
            T += S[i];
          }
        }

        // Again checking for
        // longest substring
        // and update accordingly
        l = T.length;
        if (l > ans.length) {
          ans = T;
        }

        // Print the longest substring
        document.write(ans);
      }

      // Driver Code
      // Given string
      var S = "aabdml";

      // Function call to find
      // the longest substring
      // satisfying given condition
      findSubstring(S);

</script>
```

**Output:** 

```
bdm
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)