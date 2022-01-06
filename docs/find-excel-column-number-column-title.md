# 从列标题

找到 Excel 列号

> 原文:[https://www . geesforgeks . org/find-excel-column-number-column-title/](https://www.geeksforgeeks.org/find-excel-column-number-column-title/)

我们已经讨论了[从列号到 Excel 列名的转换](https://www.geeksforgeeks.org/find-excel-column-name-given-number/)。在这篇文章中，讨论了反向。
给定 Excel 表格中出现的列标题，返回其对应的列号。

```
column  column number
  A  ->  1
  B  ->  2
  C  ->  3
  ...
  Z  ->  26
  AA ->  27
  AB ->  28 
```

**例:**

```
Input: A
Output: 1
A is the first column so the output is 1.

Input: AA
Output: 27
The columns are in order A, B, ..., Y, Z, AA ..
So, there are 26 columns after which AA comes.
```

**方法:**过程类似于二进制到十进制的转换。
比如换算 AB，公式是 26 * 1 + 2。
又如，

```
To convert CDA,
3*26*26 + 4*26 + 1
= 26(3*26 + 4) + 1
= 26(0*26 + 3*26 + 4) + 1
```

所以这非常类似于将二进制转换为十进制，保持基数为 26。
将输入作为字符串，从左到右遍历输入字符串，计算结果如下:

```
result = 26*result + s[i] - 'A' + 1
```

。
结果将是
![Result &= \sum_{i=0}^{n} a[n-i-1]*(26^{(n-i-1)})    ](img/fa8502b756963d7dcadcc76bfd2fcfd9.png "Rendered by QuickLaTeX.com")的总和。

## C++

```
// C++ program to return title to result
// of excel sheet.
#include <bits/stdc++.h>

using namespace std;

// Returns result when we pass title.
int titleToNumber(string s)
{
    // This process is similar to
    // binary-to-decimal conversion
    int result = 0;
    for (const auto& c : s)
    {
        result *= 26;
        result += c  - 'A' + 1;
    }

    return result;
}

// Driver function
int main()
{
    cout << titleToNumber("CDA") << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to return title
// to result of excel sheet.
import java.util.*;
import java.lang.*;

class GFG
{

// Returns result when we pass title.
static int titleToNumber(String s)
{
    // This process is similar to
    // binary-to-decimal conversion
    int result = 0;
    for (int i = 0; i < s.length(); i++)
    {
        result *= 26;
        result += s.charAt(i) - 'A' + 1;
    }
    return result;
}

// Driver Code
public static void main (String[] args)
{
    System.out.print(titleToNumber("CDA"));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 蟒蛇 3

```
# Python program to return title to result
# of excel sheet.

# Returns result when we pass title.
def titleToNumber(s):
    # This process is similar to binary-to-
    # decimal conversion
    result = 0;
    for B in range(len(s)):
        result *= 26;
        result += ord(s[B]) - ord('A') + 1;

    return result;

# Driver function
print(titleToNumber("CDA"));

# This code contributed by Rajput-Ji
```

## C#

```
// C# program to return title
// to result of excel sheet.
using System;

class GFG
{

// Returns result when we pass title.
public static int titleToNumber(string s)
{
    // This process is similar to
    // binary-to-decimal conversion
    int result = 0;
    for (int i = 0; i < s.Length; i++)
    {
        result *= 26;
        result += s[i] - 'A' + 1;
    }
    return result;
}

// Driver Code
public static void Main(string[] args)
{
    Console.Write(titleToNumber("CDA"));
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// JavaScript program to return title
// to result of excel sheet.

// Returns result when we pass title
function titleToNumber(s)
{
    // This process is similar to
    // binary-to-decimal conversion
    let result = 0;
    for (let i = 0; i < s.length; i++)
    {
        result *= 26;
        result += s[i].charCodeAt(0) - 'A'.charCodeAt(0) + 1;
    }
    return result;
}
// Driver Code
document.write(titleToNumber("CDA"));

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
2133
```

**复杂度分析:**

*   **时间复杂度:** O(n)，其中 n 为输入字符串的长度。
*   **空间复杂度:** O(1)。
    因为不需要额外的空间。

本文由**萨赫勒拉杰普特**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。