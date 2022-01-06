# 字典式中间字符串

> 原文:[https://www . geeksforgeeks . org/词典-中字符串/](https://www.geeksforgeeks.org/lexicographically-middle-string/)

给定两条弦 **a** 和 **b** 。我们的任务是打印任何大于 **a** (按字典顺序)但小于 **b** (按字典顺序)的字符串。如果不可能得到这样的字符串，打印-1；

**示例:**

```
Input : a = "abg", b = "abj"
Output : abh
The string "abh" is lexicographically 
greater than "abg" and smaller than
"abj"        

Input : a = "abc", b = "abd"
Output :-1
There is no string which is lexicographically
greater than a but smaller than b/
```

因为可以有多个满足上述条件的字符串，所以我们将字符串“a”转换为一个字符串，该字符串在字典序上是 [**然后**](https://www.geeksforgeeks.org/lexicographically-next-string/) 转换为“a”。

接下来，我们开始从后向遍历字符串，并将所有字母“z”转换为字母“a”。如果我们遇到任何不是“z”的字母，那么我们将它增加 1，并且不会执行进一步的遍历。如果这个字符串不小于“b”，那么我们将打印-1，因为没有字符串能够满足上述条件。

例如，字符串 a="ddzzz "和字符串 b="deaao "。因此，从向后开始，我们将把所有字母“z”转换成字母“a”，直到我们到达字母“d”(在这种情况下)。将“d”增加 1(到“e”)，并脱离循环。所以，字符串 **a** 会变成“deaaa”，在词典上比“ddzzz”大，比“deaao”小。

## C++

```
// C++ program to implement above approach
#include <iostream>
using namespace std;

// function to find lexicographically mid
// string.
void lexMiddle(string a, string b)
{
    // converting string "a" into its
    // lexicographically next string
    for (int i = a.length() - 1; i >= 0; i--) {

        // converting all letter "z" to letter "a"
        if (a[i] == 'z')
            a[i] = 'a';
        else {

            // if letter other than "z" is
            // encountered, increment it by one
            // and break
            a[i]++;
            break;
        }
    }

    // if this new string "a" is lexicographically
    // smaller than b
    if (a < b)
        cout << a;
    else
        cout << -1;
}

// Driver function
int main()
{
    string a = "geeks", b = "heeks";
    lexMiddle(a, b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// above approach
class GFG
{

// function to find lexicographically
// mid String.
static void lexMiddle(String a, String b)
{
    String new_String = "";

    // converting String "a" into its
    // lexicographically next String
    for (int i = a.length() - 1; i >= 0; i--)
    {

        // converting all letter
        // "z" to letter "a"
        if (a.charAt(i) == 'z')
            new_String = 'a' + new_String;
        else
        {

            // if letter other than "z" is
            // encountered, increment it by
            // one and break
            new_String = (char)(a.charAt(i) + 1) +
                                       new_String;

            //compose the remaining string
            for(int j = i - 1; j >= 0; j--)
            new_String = a.charAt(j) + new_String;

            break;
        }
    }

    // if this new String new_String is
    // lexicographically smaller than b
    if (new_String.compareTo(b) < 0)
    System.out.println(new_String);
    else
        System.out.println(-1);
}

// Driver Code
public static void main(String args[])
{
    String a = "geeks", b = "heeks";
    lexMiddle(a, b);
}
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to implement above approach

# function to find lexicographically mid
# string.
def lexMiddle( a, b):

    # converting string "a" into its
    # lexicographically next string
    for i in range(len(a)-1,-1,-1):

        ans=[]
        # converting all letter "z" to letter "a"
        if (a[i] == 'z'):
            a[i] = 'a'
        else:

            # if letter other than "z" is
            # encountered, increment it by one
            # and break
            a[i]=chr(ord(a[i])+1)
            break

    # if this new string "a" is lexicographically
    # smaller than b
    if (a < b):
        return a
    else:
        return -1

# Driver function
if __name__=='__main__':
    a = list("geeks")
    b = list("heeks")
    ans=lexMiddle(a, b)
    ans = ''.join(map(str, ans))
    print(ans)

# this code is contributed by ash264
```

## C#

```
// C# program to implement above approach
using System;

class GFG
{

// function to find lexicographically
// mid String.
static void lexMiddle(string a, string b)
{
    string new_String = "";

    // converting String "a" into its
    // lexicographically next String
    for (int i = a.Length - 1; i >= 0; i--)
    {

        // converting all letter
        // "z" to letter "a"
        if (a[i] == 'z')
            new_String = 'a' + new_String;
        else
        {

            // if letter other than "z" is
            // encountered, increment it by
            // one and break
            new_String = (char)(a[i] + 1) +
                                new_String;

            //compose the remaining string
            for(int j = i - 1; j >= 0; j--)
                new_String = a[j] + new_String;

            break;
        }
    }

    // if this new String new_String is
    // lexicographically smaller than b
    if (new_String.CompareTo(b) < 0)
    Console.Write(new_String);
    else
        Console.Write(-1);
}

// Driver Code
public static void Main()
{
    string a = "geeks", b = "heeks";
    lexMiddle(a, b);
}
}

// This code is contributed by ita_c
```

## java 描述语言

```
<script>

// Javascript program to implement
// above approach

// Function to find lexicographically
// mid String.
function lexMiddle(a, b)
{
    let new_String = "";

    // Converting String "a" into its
    // lexicographically next String
    for(let i = a.length - 1; i >= 0; i--)
    {

        // Converting all letter
        // "z" to letter "a"
        if (a[i] == 'z')
            new_String = 'a' + new_String;
        else
        {

            // If letter other than "z" is
            // encountered, increment it by
            // one and break
            new_String = String.fromCharCode(
                a[i].charCodeAt(0) + 1) + new_String;

            // Compose the remaining string
            for(let j = i - 1; j >= 0; j--)
                new_String = a[j] + new_String;

            break;
        }
    }

    // If this new String new_String is
    // lexicographically smaller than b
    if (new_String < (b))
        document.write(new_String);
    else
        document.write(-1);
}

// Driver Code
let a = "geeks", b = "heeks";

lexMiddle(a, b);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
geekt
```

**时间复杂度:** O(n)，其中 n 是字符串‘a’的长度