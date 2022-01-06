# 通过精确替换一个字符

，使字符串在词典上最小且不重复

> 原文:[https://www . geesforgeks . org/make-the-string-按字典顺序排列-最小-非回文-通过替换恰好一个字符/](https://www.geeksforgeeks.org/make-the-string-lexicographically-smallest-non-palindromic-by-replacing-exactly-one-character/)

给定一个仅包含小写字母的回文字符串 **str** ，任务是通过恰好替换一个字符来打印字典上最小的字符串，这样该字符串就不是回文了。
**例:**

> **输入:**str = " abcba "
> **输出:**【aaccba】
> **解释:**
> 字典上最小的非回文串可能是“aaccba”，这里我们把第二个字母‘b’换成了‘a’，使之成为非回文。
> **输入:** str = "a"
> **输出:** -1
> **解释:**
> 单个字符始终是回文，因此我们无法替换该值。因此输出为-1。

**方法:**为了解决上面提到的问题，我们将**只检查字符串**的一半，并将所有不是“a”的字符替换为字符“a”本身。问题的边缘情况是，如果只有一个字符，我们将返回一个空字符串。否则，如果所有字符都相同，那么我们将用字符“b”替换最后一个字符。
以下是上述方法的实施:

## C++

```
// C++ program to make the string
// lexicographically smallest non
// palindromic string by replacing
// exactly one character

#include <bits/stdc++.h>
using namespace std;

// Function to find the required string
string findStr(string S)
{
    // length of the string
    int n = S.size();

    // Iterate till half of the string
    for (int i = 0; i < n / 2; ++i) {

        // replacing a non 'a' char with 'a'
        if (S[i] != 'a') {
            S[i] = 'a';

            return S;
        }
    }

    // Check if there is no 'a' in string
    // we replace last char of string by 'b'
    S[n - 1] = 'b';

    // If the input is a single character
    return n < 2 ? " -1 " : S;
}

// Driver code
int main()
{
    string str = "a";
    cout << findStr(str) << endl;

    string str1 = "abccba";
    cout << findStr(str1) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to make the string
// lexicographically smallest non
// palindromic string by replacing
// exactly one character
import java.util.*;
class GFG {

// Function to find the required string
static String findStr(String S)
{
    StringBuilder sb = new StringBuilder(S);

    // length of the string
    int n = sb.length();

    // Iterate till half of the string
    for (int i = 0; i < n / 2; ++i)
    {

        // replacing a non 'a' char with 'a'
        if (sb.charAt(i) != 'a')
        {
            sb.setCharAt(i, 'a');

            return sb.toString();
        }
    }

    // Check if there is no 'a' in string
    // we replace last char of string by 'b'
    sb.setCharAt(n - 1, 'b');

    // If the input is a single character
    return n < 2 ? " -1 " : sb.toString();
}

// Driver code
public static void main(String[] args)
{
    String str = "a";
    System.out.println(findStr(str));

    String str1 = "abccba";
    System.out.println(findStr(str1));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to make the string
# lexicographically smallest non
# palindromic string by replacing
# exactly one character

# Function to find the required string
def findStr(S):

    S = list(S)

    # Length of the string
    n = len(S)

    # Iterate till half of the string
    for i in range(0, n // 2):

        # Replacing a non 'a' char with 'a'
        if S[i] != 'a':
            S[i] = 'a'
            return (''.join(S))

    # Check if there is no 'a' in string
    # we replace last char of string by 'b'
    S[n - 1] = 'b'

    # If the input is a single character
    if n < 2:
        return '-1'
    else:
        return (''.join(S))

# Driver Code
if __name__=='__main__':

    str1 = 'a'
    print(findStr(str1))

    str2 = 'abccba'
    print(findStr(str2))

# This code is contributed by rutvik_56
```

## C#

```
// C# program to make the string
// lexicographically smallest non
// palindromic string by replacing
// exactly one character
using System;

class GFG{

// Function to find the required string
static String findStr(char []S)
{

    // Length of the string
    int n = S.Length;

    // Iterate till half of the string
    for(int i = 0; i < n / 2; ++i)
    {

       // Replacing a non 'a' char with 'a'
       if (S[i] != 'a')
       {
           S[i] = 'a';
           return new String(S);
       }
    }

    // Check if there is no 'a' in string
    // we replace last char of string by 'b'
    S[n - 1] = 'b';

    // If the input is a single character
    return n < 2 ? " -1 " : new String(S);
}

// Driver code
public static void Main(String[] args)
{
    String str = "a";
    Console.WriteLine(findStr(str.ToCharArray()));

    String str1 = "abccba";
    Console.WriteLine(findStr(str1.ToCharArray()));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to make the string
// lexicographically smallest non
// palindromic string by replacing
// exactly one character

// Function to find the required string
function findStr(S)
{
    // length of the string
    var n = S.length;

    // Iterate till half of the string
    for (var i = 0; i < n / 2; ++i) {

        // replacing a non 'a' char with 'a'
        if (S[i] != 'a') {
            S[i] = 'a';

            return S.join("");;
        }
    }

    // Check if there is no 'a' in string
    // we replace last char of string by 'b'
    S[n - 1] = 'b';

    // If the input is a single character
    return n < 2 ? " -1 " : S.join("");;
}

// Driver code

var str = "a";
document.write( findStr(Array.from(str)) + "<br>");
var str1 = "abccba";
document.write( findStr(Array.from(str1)));

</script>
```

**Output:** 

```
-1 
aaccba
```

***时间复杂度:**O(N)*T4】