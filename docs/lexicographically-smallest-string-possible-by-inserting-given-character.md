# 通过插入给定字符

可能的字典最小字符串

> 原文:[https://www . geeksforgeeks . org/按词典编纂-通过插入给定字符尽可能最小的字符串/](https://www.geeksforgeeks.org/lexicographically-smallest-string-possible-by-inserting-given-character/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 和一个字符 **C** ，任务是在字符串中放置一个字符，使得获得的字符串是字典上最小的字符串。

**示例:**

> **输入:**S =“ACD”，C =‘b’
> **输出:**“abcd”
> **解释:**将字符 C 放入不同索引的字符串中可能形成的字符串是[“bacd”、“abcd”、“acbd”、“acdb”]
> 得到的字典最小的字符串是“ABCD”。
> 
> **输入:** S = "abcd "，C='e'
> **输出:**【abcde "
> **解释:**将字符 C 放在字符串中不同的索引处可能形成的字符串有{“eabcd”、“aebcd”、“abecd”、“abcde”、“abcde”}。
> 字典上最小的字符串是“abcde”。

**方法:**想法是将字符放在字符串中第一个字符的前面，该字符在字典序上大于字符 **C** 。如果发现字符串中没有大于 **C** 的字符，则在末尾插入该字符。

下面是上述方法的实现:

## C++

```
// C++ Program to implement the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to obtain lexicographically
// smallest string possible by inserting
// character c in the string s
string SmallestString(string s, char c)
{

    // Traverse the string
    for (int i = 0; i < s.size(); i++) {

        // If the current character is greater
        // than the given character
        if (s[i] > c) {

            // Insert the character before
            // the greater character
            s.insert(i, 1, c);

            // Return the string
            return s;
        }
    }

    // Append the character at the end
    s += c;

    // Return the string
    return s;
}

// Driver Code
int main()
{
    string S = "acd";
    char C = 'b';

    cout << SmallestString(S, C) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the
// above approach
import java.util.*;

class GFG{

// Function to obtain lexicographically
// smallest String possible by inserting
// character c in the String s
static String SmallestString(String s, char c)
{

    // Traverse the String
    for(int i = 0; i < s.length(); i++)
    {

        // If the current character is greater
        // than the given character
        if (s.charAt(i) > c)
        {

            // Insert the character before
            // the greater character
            String temp = s;
            s = s.substring(0, i);
            s += c;
            s += temp.substring(i, temp.length());

            // Return the String
            return s;
        }
    }

    // Append the character at the end
    s += c;

    // Return the String
    return s;
}

// Driver Code
public static void main(String args[])
{
    String S = "acd";
    char C = 'b';

    System.out.println(SmallestString(S, C));
}
}

// This code is contributed by ipg2016107
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to obtain lexicographically
# smallest string possible by inserting
# character c in the string s
def SmallestString(s, c):

    i = 0

    # Traverse the string
    while(i < len(s)):

      # Check if current character is
      # greater than the given character
        if s[i] > c:

            # Insert the character before
            # the first greater character
            s = s[:i] + c + s[i:]

            # Return the string
            return s
        i = i + 1

    # Append the character at the end
    s = s + c

    # Return the string
    return s

S = 'abd'
C = 'c'

# Function call
print(SmallestString(S, C))
```

## C#

```
// C# program to implement the
// above approach
using System;

class GFG{

// Function to obtain lexicographically
// smallest String possible by inserting
// character c in the String s
static String SmallestString(String s, char c)
{

    // Traverse the String
    for(int i = 0; i < s.Length; i++)
    {

        // If the current character is greater
        // than the given character
        if (s[i] > c)
        {

            // Insert the character before
            // the greater character
            String temp = s;
            s = s.Substring(0, i);
            s += c;
            s += temp.Substring(i, temp.Length - 1);

            // Return the String
            return s;
        }
    }

    // Append the character at the end
    s += c;

    // Return the String
    return s;
}

// Driver Code
public static void Main(String []args)
{
    String S = "acd";
    char C = 'b';

    Console.WriteLine(SmallestString(S, C));
}
}

// This code is contributed by aashish1995
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach

// Function to obtain lexicographically
// smallest String possible by inserting
// character c in the String s
function SmallestString(s, c)
{

    // Traverse the String
    for(let i = 0; i < s.length; i++)
    {

        // If the current character is greater
        // than the given character
        if (s[i] > c)
        {

            // Insert the character before
            // the greater character
            let temp = s;
            s = s.substring(0, i);
            s += c;
            s += temp.substring(i, temp.length);

            // Return the String
            return s;
        }
    }

    // Append the character at the end
    s += c;

    // Return the String
    return s;
}

// Driver code
     let S = "acd";
    let C = 'b';
    document.write(SmallestString(S, C));

     // This code is contributed by splevel62.
</script>
```

**Output:** 

```
abcd
```

**时间复杂度:** O(len(str))
**辅助空间:** O(1)