# 仅包含辅音的字符串的最长子序列

> 原文:[https://www . geeksforgeeks . org/仅包含辅音的最长子序列/](https://www.geeksforgeeks.org/longest-subsequence-of-a-string-containing-only-consonants/)

给定一个只包含英文字母的字符串，任务是打印只包含[辅音](https://en.wikipedia.org/wiki/Consonant)的最长子序列。
**例:**

> **输入:** str = "geeksforgeeks"
> **输出:** gksfrgks
> 包含辅音的最长子序列将是给定字符串中所有辅音的字符串。
> 这里用字符串“gksfrgks”给出。
> **输入:** str = "HelloWorld"
> **输出:**hllworld

**进场:**

*   首先，我们将遍历给定的字符串。
*   我们将包括在遍历答案串时遇到的所有辅音。
*   一旦遇到了整个初始字符串，我们就有了最长的子序列，其中只包含辅音。

以下是上述方法的实现:

## C++

```
// C++ program to find the longest subsequence
// which contain all consonants
#include <bits/stdc++.h>

using namespace std;

// Returns true if x is consonants.
bool isConsonants(char x)
{
    // Function to check whether a character is
    // consonants or not
    x = tolower(x);
    return !(x == 'a' || x == 'e' || x == 'i'
                      || x == 'o' || x == 'u');
}

// Function to find the longest subsequence
// which contain all consonants
string longestConsonantsSubsequence(string str)
{
    string answer = "";
    int n = str.size();

    for (int i = 0; i < n; i++) {
        if (isConsonants(str[i])) {
            answer += str[i];
        }
    }

    return answer;
}

// Driver code
int main()
{
    string str = "geeksforgeeks";

    // Function call
    cout << longestConsonantsSubsequence(str) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the longest subsequence
// which contain all consonants
class GFG{

// Returns true if x is consonants.
static boolean isConsonants(char x)
{

    // Function to check whether a character
    // is consonants or not
    x = Character.toLowerCase(x);
    return !(x == 'a' || x == 'e' ||
             x == 'i' || x == 'o' ||
             x == 'u');
}

// Function to find the longest subsequence
// which contain all consonants
static String longestConsonantsSubsequence(String str)
{
    String answer = "";
    int n = str.length();

    for (int i = 0; i < n; i++)
    {
        if (isConsonants(str.charAt(i)))
        {
            answer += str.charAt(i);
        }
    }
    return answer;
}

// Driver code
public static void main(String[] args)
{
    String str = "geeksforgeeks";

    // Function call
    System.out.print(longestConsonantsSubsequence(str) + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to find the longest subsequence
# which contain all consonants

# Returns true if x is consonants.
def isComsomamts(x):

    x = x.lower()
    return not (x == 'a' or x == 'e' or
                x == 'i' or x == 'o' or
                x == 'u')

# Function to find the longest subsequence
# which contain all consonants
def longestConsonantsSubsequence(s):

    answer = ''
    n = len(s)

    for i in range(n):
        if isComsomamts(s[i]):
            answer += s[i]

    return answer

# Driver code
s = 'geeksforgeeks'

# Function call
print(longestConsonantsSubsequence(s))

# This code is contributed by rutvik_56
```

## C#

```
// C# program to find the longest subsequence
// which contain all consonants
using System;

class GFG{

// Returns true if x is consonants.
static bool isConsonants(char x)
{

    // Function to check whether a 
    // character is consonants or not
    x = Char.ToLower(x);
    return !(x == 'a' || x == 'e' ||
             x == 'i' || x == 'o' ||
             x == 'u');
}

// Function to find the longest subsequence
// which contain all consonants
static string longestConsonantsSubsequence(string str)
{
    string answer = "";
    int n = str.Length;

    for(int i = 0; i < n; i++)
    {
       if (isConsonants(str[i]))
       {
           answer += str[i];
       }
    }
    return answer;
}

// Driver code
static void Main()
{
    string str = "geeksforgeeks";

    // Function call
    Console.Write(longestConsonantsSubsequence(str) + "\n");
}
}

// This code is contributed by divyeshrabadiya07   
```

## java 描述语言

```
<script>
      // JavaScript program to find the longest subsequence
      // which contain all consonants
      // Returns true if x is consonants.
      function isConsonants(x) {
        // Function to check whether a
        // character is consonants or not
        x = x.toLowerCase();
        return !(x === "a" || x === "e" || x === "i" || x === "o" || x === "u");
      }

      // Function to find the longest subsequence
      // which contain all consonants
      function longestConsonantsSubsequence(str) {
        var answer = "";
        var n = str.length;

        for (var i = 0; i < n; i++) {
          if (isConsonants(str[i])) {
            answer += str[i];
          }
        }
        return answer;
      }

      // Driver code
      var str = "geeksforgeeks";

      // Function call
      document.write(longestConsonantsSubsequence(str) + "<br>");

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
gksfrgks
```