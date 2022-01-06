# 小写到大写——一个有趣的事实

> 原文:[https://www . geesforgeks . org/小写-大写-有趣-事实/](https://www.geeksforgeeks.org/lower-case-upper-case-interesting-fact/)

问题:给定一个只包含小写字母的字符串，生成一个字母相同但大写的字符串。

```
Input : GeeksForGeeks
Output : GEEKSFORGEEKS 
```

我们想到的第一个方法是

## C++

```
// C++ program to convert a string to uppercase
#include <iostream>
using namespace std;

// Converts a string to uppercase
string to_upper(string &in)
{
    for (int i = 0; i < in.length(); i++)
          if ('a' <= in[i] <= 'z')
              in[i] = in[i] - 'a' + 'A';
    return in;
}

// Driver code
int main()
{
   string str = "geeksforgeeks";
   cout << to_upper(str);
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert a string to uppercase

class GFG
{

    // Converts a string to uppercase
    static String to_upper(char[] in)
    {
        for (int i = 0; i < in.length; i++)
        {
            if ('a' <= in[i] & in[i] <= 'z')
            {
                in[i] = (char) (in[i] - 'a' + 'A');
            }
        }
        return String.valueOf(in);
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "geeksforgeeks";
        System.out.println(to_upper(str.toCharArray()));
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to convert a string to uppercase

# Converts a string to uppercase
def to_upper(string):
    for i in range(len(string)):
        if ('a' <= string[i] <= 'z'):
            string = (string[0:i] + chr(ord(string[i]) -
                                        ord('a') + ord('A')) +
                                        string[i + 1:])
    return string;

# Driver code
if __name__ == '__main__':
    str = "geeksforgeeks";
    print(to_upper(str));

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program to convert a string to uppercase
using System;

class GFG
{
    // Converts a string to uppercase
    static String to_upper(char []In)
    {
        for (int i = 0; i < In.Length; i++)
        {
            if ('a' <= In[i] & In[i] <= 'z')
            {
                In[i] = (char) (In[i] - 'a' + 'A');
            }
        }
        return String.Join("", In);
    }

    // Driver code
    public static void Main()
    {
        String str = "geeksforgeeks";
        Console.WriteLine(to_upper(str.ToCharArray()));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
      // JavaScript program to convert a string to uppercase
      // Converts a string to uppercase
      function to_upper(input)
      {
        var result = new Array(input.length);
        for (var i = 0; i < input.length; i++)
          if ("a".charCodeAt(0) <= input[i].charCodeAt(0) <= "z".charCodeAt(0))
            result[i] = String.fromCharCode(
              input[i].charCodeAt(0) - "a".charCodeAt(0) + "A".charCodeAt(0)
          );

        return result.join("").toString();
      }

      // Driver code
      var str = "geeksforgeeks";
      document.write(to_upper(str));

      // This code is contributed by rdtank.
    </script>
```

**输出:**

```
GEEKSFORGEEKS
```

另一方面，更有趣的解决方案是:

## C++

```
// C++ program to convert a string to uppercase
#include <iostream>
using namespace std;

// Converts a string to uppercase
string to_upper(string &in)
{
    for (int i = 0; i < in.length(); i++)
          if ('a' <= in[i] <= 'z')
              in[i] &= ~(1 << 5);
    return in;
}

// Driver code
int main()
{
   string str = "geeksforgeeks";
   cout << to_upper(str);
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert a string to uppercase
class GFG
{

// Converts a string to uppercase
static String to_upper(char[] in)
{
    for (int i = 0; i < in.length; i++)
        if ('a' <= in[i] && in[i] <= 'z')
            in[i] &= ~(1 << 5);
    return String.valueOf(in);
}

// Driver code
public static void main(String[] args)
{
    String str = "geeksforgeeks";
    System.out.println(to_upper(str.toCharArray()));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to convert
# a string to uppercase

# Converts a string to uppercase
def to_upper(s):
    for i in range(len(s)):
        if ('a' <= s[i] <= 'z'):
            s = s[0:i] + chr(ord(s[i]) & \
                            (~(1 << 5))) + s[i + 1:];
    return s;

# Driver code
if __name__ == '__main__':
    string = "geeksforgeeks";
    print(to_upper(string));

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# program to convert a string to uppercase
using System;

class GFG
{

// Converts a string to uppercase
static String to_upper(char[] str)
{
    for (int i = 0; i < str.Length; i++)
        if ('a' <= str[i] && str[i] <= 'z')
            str[i] = (char)((int)str[i]&(~(1 << 5)));
    return String.Join("", str);
}

// Driver code
public static void Main(String[] args)
{
    String str = "geeksforgeeks";
    Console.WriteLine(to_upper(str.ToCharArray()));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to convert
// a string to uppercase

// Converts a string to uppercase
function to_upper(In)
{
    let n = In.length;
    for(let i = 0; i < In.length; i++)
        if ('a' <= In[i] && In[i] <= 'z')
            In[i] = String.fromCharCode(
                In[i].charCodeAt(0) & (~(1 << 5)));

    return (In).join("");
}

// Driver code
let str = "geeksforgeeks";

document.write(to_upper(str.split("")));

// This code is contributed by rag2127

</script>
```

**输出:**

```
GEEKSFORGEEKS
```

**说明:**[ASCII 表](http://www.asciitable.com/)的构造方式是小写字母的二进制表示与大写字母的二进制表示几乎相同。唯一的区别是第六位，只为小写字母设置。这个优雅的函数所做的是取消设置[i]中索引 5 的位，从而使该字符小写。

**缺点:**该策略仅适用于字母字符。如果输入包含数字或标点符号，我们将不得不使用天真的方式。

**例:**字符‘A’为整数 65 = (0100 0001)2，字符‘A’为整数= 97 = (0110 0001) <sub>2</sub> 。(请注意，97–65 = 32。你能猜到为什么吗？)

**练习:**

1.  编写一个函数，使字符串的所有字母都小写。例子:极客暴发户变成极客暴发户。
2.  写一个改变字符串大小写的函数。例子:极客暴发户变身极客暴发户。

本文由**伊戈尔·喀尔巴嫩**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息