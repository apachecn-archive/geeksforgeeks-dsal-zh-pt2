# 字符串的字典最大子串

> 原文:[https://www . geesforgeks . org/词典-最大值-子字符串-字符串/](https://www.geeksforgeeks.org/lexicographical-maximum-substring-string/)

给定一个字符串 s，我们必须找到一个字符串的字典最大子字符串

**示例:**

```
Input : s = "ababaa"
Output : babaa
Explanation : "babaa" is the maximum lexicographic substring formed from this string

Input : s = "asdfaa"
Output : sdfaa
```

想法很简单，我们遍历所有子字符串。对于每个子串，我们将其与当前结果进行比较，并在需要时更新结果。

下面是实现:

## C++

```
// CPP program to find the lexicographically
// maximum substring.
#include <bits/stdc++.h>
using namespace std;

string LexicographicalMaxString(string str)
{
    // loop to find the max leicographic
    // substring in the substring array
    string mx = "";
    for (int i = 0; i < str.length(); ++i)
        mx = max(mx, str.substr(i));

    return mx;
}

// Driver code
int main()
{
    string str = "ababaa";
    cout << LexicographicalMaxString(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the lexicographically
// maximum substring.

class GFG {

    static String LexicographicalMaxString(String str)
    {
        // loop to find the max leicographic
        // substring in the substring array
        String mx = "";
        for (int i = 0; i < str.length(); ++i) {
            if (mx.compareTo(str.substring(i)) <= 0) {
                mx = str.substring(i);
            }
        }

        return mx;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "ababaa";
        System.out.println(LexicographicalMaxString(str));
    }
}
// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to find the
# lexicographically maximum substring.
def LexicographicalMaxString(str):

    # loop to find the max leicographic 
    # substring in the substring array
    mx = ""
    for i in range(len(str)):
        mx = max(mx, str[i:])

    return mx

# Driver code
if __name__ == '__main__':
    str = "ababaa"
    print(LexicographicalMaxString(str))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to find the lexicographically
// maximum substring.

using System;
public class GFG {

    static String LexicographicalMaxString(String str)
    {
        // loop to find the max leicographic
        // substring in the substring array
        String mx = "";
        for (int i = 0; i < str.Length; ++i) {
            if (mx.CompareTo(str.Substring(i)) <= 0) {
                mx = str.Substring(i);
            }
        }

        return mx;
    }

    // Driver code
    public static void Main()
    {
        String str = "ababaa";
        Console.WriteLine(LexicographicalMaxString(str));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to find the lexicographically
// maximum substring.
   function LexicographicalMaxString(str)
    {
        // loop to find the max leicographic
    // substring in the substring array
    var mx = "";
    for (var i = 0; i < str.length; ++i) {
        if (mx.localeCompare(str.substring(i)) <= 0) {
            mx = str.substring(i);
        }
    }

    return mx;
}

// Driver code
   var str = "ababaa";
   document.write(LexicographicalMaxString(str));

// This code is contributed by 29AjayKumar 

</script>
```

**Output:** 

```
babaa
```

**优化:**
我们找到最大的人物及其所有指标。现在，我们只需遍历最大字符的所有实例，就可以找到字典上最大的子串。

这里我们遵循上述方法。

## C++

```
// C++ program to find the lexicographically
// maximum substring.
#include <bits/stdc++.h>
using namespace std;

string LexicographicalMaxString(string str)
{
    char maxchar = 'a';
    vector<int> index;

    // We store all the indexes of maximum
    // characters we have in the string
    for (int i = 0; i < str.length(); i++) {
        if (str[i] >= maxchar) {
            maxchar = str[i];
            index.push_back(i);
        }
    }
    string maxstring = "";

    // We form a substring from that maximum
    // character index till end and check if
    // its greater that maxstring
    for (int i = 0; i < index.size(); i++) {
        if (str.substr(index[i], str.length()) > maxstring) {
            maxstring = str.substr(index[i], str.length());
        }
    }
    return maxstring;
}

// Driver code
int main()
{
    string str = "acbacbc";
    cout << LexicographicalMaxString(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the lexicographically
// maximum substring.
import java.io.*;
import java.util.*;
class GFG
{    
  static String LexicographicalMaxString(String str)
  {
    char maxchar = 'a';
    ArrayList<Integer> index = new ArrayList<Integer>(); 

    // We store all the indexes of maximum
    // characters we have in the string
    for (int i = 0; i < str.length(); i++) 
    {
      if (str.charAt(i) >= maxchar)
      {
        maxchar = str.charAt(i);
        index.add(i);
      }
    }
    String maxstring = "";

    // We form a substring from that maximum
    // character index till end and check if
    // its greater that maxstring
    for (int i = 0; i < index.size(); i++) 
    {
      if (str.substring(index.get(i), 
                        str.length()).compareTo( maxstring) > 0)
      {
        maxstring = str.substring(index.get(i), 
                                  str.length());
      }
    }
    return maxstring;
  }

  // Driver code
  public static void main (String[] args) 
  {    
    String str = "acbacbc";   
    System.out.println(LexicographicalMaxString(str));
  }
}

// This code is contributed by rag2127.
```

## 蟒蛇 3

```
# Python 3 program to find 
# the lexicographically
# maximum substring.
def LexicographicalMaxString(st):

    maxchar = 'a'
    index = []

    # We store all the indexes 
    # of maximum characters we 
    # have in the string
    for i in range(len(st)):
        if (st[i] >= maxchar):
            maxchar = st[i]
            index.append(i)

    maxstring = ""

    # We form a substring from that 
    # maximum character index till 
    # end and check if its greater
    # that maxstring
    for i in range(len(index)):
        if (st[index[i]: len(st)] > 
            maxstring):
            maxstring = st[index[i]: 
                        len(st)]
    return maxstring

# Driver code
if __name__ == "__main__":

    st = "acbacbc"
    print(LexicographicalMaxString(st))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to find the lexicographically
// maximum substring.
using System;
using System.Collections.Generic;

class GFG{

static string LexicographicalMaxString(string str)
{
    char maxchar = 'a';
    List<int> index = new List<int>(); 

    // We store all the indexes of maximum
    // characters we have in the string
    for(int i = 0; i < str.Length; i++) 
    {
        if (str[i] >= maxchar)
        {
            maxchar = str[i];
            index.Add(i);
        }
    }
    string maxstring = "";

    // We form a substring from that maximum
    // character index till end and check if
    // its greater that maxstring
    for(int i = 0; i < index.Count; i++) 
    {
        if (str.Substring(index[i]).CompareTo(maxstring) > 0)
        {
            maxstring = str.Substring(index[i]);
        }
    }
    return maxstring;
}

// Driver code
static public void Main()
{
    string str = "acbacbc";

    Console.Write(LexicographicalMaxString(str));
}
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>
// Javascript program to find the lexicographically
// maximum substring.

function LexicographicalMaxString(str)
{
    let maxchar = 'a';
    let index = [];

    // We store all the indexes of maximum
    // characters we have in the string
    for (let i = 0; i < str.length; i++)
    {
      if (str[i] >= maxchar)
      {
        maxchar = str[i];
        index.push(i);
      }
    }
    let maxstring = "";

    // We form a substring from that maximum
    // character index till end and check if
    // its greater that maxstring
    for (let i = 0; i < index.length; i++)
    {
      if (str.substring(index[i],
                        str.length) > maxstring)
      {
        maxstring = str.substring(index[i],
                                  str.length);
      }
    }
    return maxstring;
}

// Driver code
let str = "acbacbc";  
document.write(LexicographicalMaxString(str));

// This code is contributed by ab2127
</script>
```

**Output:** 

```
cbc
```