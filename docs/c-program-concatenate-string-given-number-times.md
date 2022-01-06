# C++程序给定次数连接一个字符串

> 原文:[https://www . geesforgeks . org/c-program-concatenate-string-给定-number-times/](https://www.geeksforgeeks.org/c-program-concatenate-string-given-number-times/)

编写一个函数，该函数返回一个新的字符串，该字符串由给定的字符串串联 n 次而成。
示例:

```
Input : str = "geeks"
         n  = 3
Output : str = "geeksgeeksgeeks"
We concatenate "geeks" 3 times

Input : str = "for"
         n  = 2
Output : str = "forfor"
We concatenate "for" 2 times
```

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to concatenate given string
// n number of times
#include <bits/stdc++.h>
#include <string>
using namespace std;

// Function which return string by concatenating it.
string repeat(string s, int n)
{
    // Copying given string to temporary string.
    string s1 = s;

    for (int i=1; i<n;i++)
        s += s1; // Concatenating strings

    return s;
}

// Driver code
int main()
{
    string s = "geeks";
    int n = 3;
    cout << repeat(s, n) << endl;;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to concatenate given
// string n number of times

class GFG {

    // Function which return string by
    // concatenating it.
    static String repeat(String s, int n)
    {

        // Copying given string to
        // temporary string.
        String s1 = s;

        for (int i = 1; i < n; i++)

            // Concatenating strings
            s += s1;

        return s;
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "geeks";
        int n = 3;
        System.out.println(repeat(s, n));
    }
}

// This code is contributed by Smitha
```

## 蟒蛇 3

```
# Python 3 program to concatenate
# given string n number of times

# Function which return string by
# concatenating it.
def repeat(s, n):

    # Copying given string to
    # temporary string.
    s1 = s

    for i in range(1, n):

        # Concatenating strings
        s += s1

    return s

# Driver code
s = "geeks"
n = 3
print(repeat(s, n))

# This code is contributed
# by Smitha
```

## C#

```
// C# program to concatenate given
// string n number of times
using System;

class GFG {

    // Function which return string
    // by concatenating it.
    static String repeat(String s, int n)
    {

        // Copying given string to
        // temporary string.
        String s1 = s;

        for (int i = 1; i < n; i++)

            // Concatenating strings
            s += s1;

        return s;
    }

    // Driver code
    public static void Main()
    {
        String s = "geeks";
        int n = 3;
        Console.Write(repeat(s, n));
    }
}

// This code is contributed by Smitha
```

## java 描述语言

```
<script>
// javascript program to concatenate given string
// n number of times

// Function which return string by concatenating it.
function repeat(s, n)
{

    // Copying given string to temporary string.
    let s1 = s;

    for (let i = 1; i < n; i++)
        s += s1; // Concatenating strings

    return s;
}

    let s = "geeks";
    let n = 3;
    document.write(repeat(s, n));

    // This code is contributed by vaibhavrabadiya117
</script>
```

输出:

```
geeksgeeksgeeks
```

本文由 [**萨赫勒拉吉普特**](https://www.linkedin.com/in/sahil-rajput-3ba2b3134/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。