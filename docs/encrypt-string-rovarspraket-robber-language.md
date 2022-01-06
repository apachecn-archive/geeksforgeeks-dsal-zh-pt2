# 将字符串加密到 Rovarspraket(强盗语言)

> 原文:[https://www . geeksforgeeks . org/encrypt-string-rovarspracket-rubber-language/](https://www.geeksforgeeks.org/encrypt-string-rovarspraket-robber-language/)

给定一个字符串，任务是编写一个函数 translate()，将文本翻译成“[rovarspracket](https://en.wikipedia.org/wiki/R%C3%B6varspr%C3%A5ket)”(瑞典语为“强盗的语言”)。也就是说，把每个辅音都加一倍，中间加一个“o”。
例子:

```
Input : this is fun
Output : tothohisos isos fofunon
t is consonant then double the consonant and place "o" in between, 
So it becomes "tot" and do this for full string

Input : geeks
Output : gogeekoksos

```

## C++

```
// C++ implementation to Encrypt a 
// string into the rovarspraket (Robber Language)
#include<iostream>
using namespace std;

// Function return translated string
string translate(string a)
{
    // Length of the string
    int len = a.length();
    string res="";

// Run till length of string
    for(int i=0; i<len ;i++)
    {
        // checking if character is vowel,
        // if yes then append it as it is
        if (a[i] == 'a' || a[i]== 'e' || a[i] == 'i' || a[i] == 'o' || a[i] == 'u')
        {
            res = res + a[i];
        }

        // if space then append as it is
        else if(a[i] == ' ')
        {
            res = res +a[i];
        }

        // else double the consonant and put o in between
        else
        {
            res =res+ a[i] + 'o' + a[i];
        }
    }

    // return translated string
    return res;
}

// Driver Code
int main()
{
    string str = "geeks for geeks";

    // Calling function
    cout << translate(str) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to Encrypt a 
// String into the rovarspraket (Robber Language)
import java.util.*;

class GFG 
{

// Function return translated String
static String translate(String a)
{
    // Length of the String
    int len = a.length();
    String res = "";

    // Run till length of String
    for(int i = 0; i < len; i++)
    {
        // checking if character is vowel,
        // if yes then append it as it is
        if (a.charAt(i) == 'a' || a.charAt(i)== 'e' || 
            a.charAt(i) == 'i' || a.charAt(i) == 'o' || 
            a.charAt(i) == 'u')
        {
            res = res + a.charAt(i);
        }

        // if space then append as it is
        else if(a.charAt(i) == ' ')
        {
            res = res +a.charAt(i);
        }

        // else double the consonant and 
        // put o in between
        else
        {
            res = res + a.charAt(i) + 'o' + a.charAt(i);
        }
    }

    // return translated String
    return res;
}

// Driver Code
public static void main(String[] args)
{
    String str = "geeks for geeks";

    // Calling function
    System.out.println(translate(str));
}
}

// This code is contributed by PrinciRaj1992
```

## 计算机编程语言

```
# Python implementation to Encrypt a 
# string into the rovarspraket (Robber Language)

def translate(a):
    c=0
    x = ""

    # Count length of string
    for i in a:
        c+=1
    for i in range (0, c):
        # If alphabet is vowel, do not change
        if a[i] == 'a' or a[i]== 'e' or a[i] == 'i' or a[i] == 'o' or a[i] == 'u':
            b = a[i]
            x += b

        # else double the consonant and put 'O' in between the alphabet
        elif a[i]!=" ":
            b = a[i] +'o' + a[i]
            x += b

        # if string has space than put space
        elif a[i] == " ":
            x +=a[i]

    # print string
    print(x)

s = "geeks for geeks"
translate(s)
```

## C#

```
// C# implementation to Encrypt a 
// String into the rovarspraket (Robber Language)
using System;

class GFG 
{

// Function return translated String
static String translate(String a)
{
    // Length of the String
    int len = a.Length;
    String res = "";

    // Run till length of String
    for(int i=0; i<len ;i++)
    {
        // checking if character is vowel,
        // if yes then append it as it is
        if (a[i] == 'a' || a[i]== 'e' || 
            a[i] == 'i' || a[i] == 'o' || a[i] == 'u')
        {
            res = res + a[i];
        }

        // if space then append as it is
        else if(a[i] == ' ')
        {
            res = res + a[i];
        }

        // else double the consonant and put o in between
        else
        {
            res = res + a[i] + 'o' + a[i];
        }
    }

    // return translated string
    return res;
}

// Driver Code
public static void Main(String[] args)
{
    String str = "geeks for geeks";

    // Calling function
    Console.WriteLine(translate(str));
}
}

// This code is contributed by PrinciRaj1992
```

**Output:**

```
gogeekoksos foforor gogeekoksos

```

本文由 **[萨赫勒拉吉普特](https://www.linkedin.com/in/sahil-rajput-3ba2b3134/)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。