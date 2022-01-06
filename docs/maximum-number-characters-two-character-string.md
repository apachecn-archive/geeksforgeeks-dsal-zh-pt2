# 字符串中任意两个相同字符之间的最大字符数

> 原文:[https://www . geesforgeks . org/最大字符数-双字符串/](https://www.geeksforgeeks.org/maximum-number-characters-two-character-string/)

给定一个字符串，找出该字符串中任意两个字符之间的最大字符数。如果没有字符重复，打印-1。

**示例:**

```
Input : str = "abba"
Output : 2
The maximum number of characters are
between two occurrences of 'a'.

Input : str = "baaabcddc"
Output : 3
The maximum number of characters are
between two occurrences of 'b'.

Input : str = "abc"
Output : -1
```

**方法 1(简单):**使用两个嵌套循环。外部循环从左到右挑选字符，内部循环查找最远的匹配项并跟踪最大匹配项。

## C++

```
// Simple C++ program to find maximum number
// of characters between two occurrences of
// same character
#include <bits/stdc++.h>
using namespace std;

int maximumChars(string& str)
{
    int n = str.length();
    int res = -1;
    for (int i = 0; i < n - 1; i++)
        for (int j = i + 1; j < n; j++)
            if (str[i] == str[j])
                res = max(res, abs(j - i - 1));
    return res;
}

// Driver code
int main()
{
    string str = "abba";
    cout << maximumChars(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Simple Java program to find maximum
// number of characters between two
// occurrences of same character
class GFG {

    static int maximumChars(String str)
    {
        int n = str.length();
        int res = -1;

        for (int i = 0; i < n - 1; i++)
            for (int j = i + 1; j < n; j++)
                if (str.charAt(i) == str.charAt(j))
                    res = Math.max(res,
                         Math.abs(j - i - 1));

        return res;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "abba";

        System.out.println(maximumChars(str));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Simple Python3 program to find maximum number
# of characters between two occurrences of
# same character
def maximumChars(str):
    n = len(str)
    res = -1
    for i in range(0, n - 1):
        for j in range(i + 1, n):
            if (str[i] == str[j]):
                res = max(res, abs(j - i - 1))
    return res

# Driver code
if __name__ == '__main__':
    str = "abba"
    print(maximumChars(str))

# This code is contributed by PrinciRaj1992
```

## C#

```
// Simple C# program to find maximum
// number of characters between two
// occurrences of same character
using System;

public class GFG {

    static int maximumChars(string str)
    {
        int n = str.Length;
        int res = -1;

        for (int i = 0; i < n - 1; i++)
            for (int j = i + 1; j < n; j++)
                if (str[i] == str[j])
                    res = Math.Max(res,
                         Math.Abs(j - i - 1));

        return res;
    }

    // Driver code
    static public void Main ()
    {
        string str = "abba";

        Console.WriteLine(maximumChars(str));
    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>
    // Simple Javascript program to find maximum
    // number of characters between two
    // occurrences of same character

    function maximumChars(str)
    {
        let n = str.length;
        let res = -1;

        for (let i = 0; i < n - 1; i++)
            for (let j = i + 1; j < n; j++)
                if (str[i] == str[j])
                    res = Math.max(res,
                         Math.abs(j - i - 1));

        return res;
    }

    // Driver code
    let str = "abba";
    document.write(maximumChars(str));

// This code is contributed by unknown2108
</script>
```

**输出:**

```
2
```

**时间复杂度:** O(n^2)

**方法 2(高效):**初始化一个长度为 26 的数组“FIRST”，其中我们必须存储字符串中字母表的第一次出现，以及另一个长度为 26 的数组“LAST”，其中我们将存储字符串中字母表的最后一次出现。这里，索引 0 对应字母 a，1 对应字母 b，以此类推。之后，如果最后一个数组和第一个数组不在同一个位置，我们将取它们之间的差值，找出最大差值。

## C++

```
// Efficient C++ program to find maximum number
// of characters between two occurrences of
// same character
#include <bits/stdc++.h>
using namespace std;

const int MAX_CHAR = 256;

int maximumChars(string& str)
{
    int n = str.length();
    int res = -1;

    // Initialize all indexes as -1.
    int firstInd[MAX_CHAR];
    for (int i = 0; i < MAX_CHAR; i++)
        firstInd[i] = -1;

    for (int i = 0; i < n; i++) {
        int first_ind = firstInd[str[i]];

        // If this is first occurrence
        if (first_ind == -1)
            firstInd[str[i]] = i;

        // Else find distance from previous
        // occurrence and update result (if
        // required).
        else
            res = max(res, abs(i - first_ind - 1));
    }
    return res;
}

// Driver code
int main()
{
    string str = "abba";
    cout << maximumChars(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient java program to find maximum
// number of characters between two
// occurrences of same character
import java.io.*;

public class GFG {

    static int MAX_CHAR = 256;

    static int maximumChars(String str)
    {
        int n = str.length();
        int res = -1;

        // Initialize all indexes as -1.
        int []firstInd = new int[MAX_CHAR];

        for (int i = 0; i < MAX_CHAR; i++)
            firstInd[i] = -1;

        for (int i = 0; i < n; i++)
        {
            int first_ind = firstInd[str.charAt(i)];

            // If this is first occurrence
            if (first_ind == -1)
                firstInd[str.charAt(i)] = i;

            // Else find distance from previous
            // occurrence and update result (if
            // required).
            else
                res = Math.max(res, Math.abs(i
                                  - first_ind - 1));
        }

        return res;
    }

    // Driver code

    static public void main (String[] args)
    {
        String str = "abba";

        System.out.println(maximumChars(str));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Efficient Python3 program to find maximum
# number of characters between two occurrences
# of same character

MAX_CHAR = 256

def maximumChars(str1):

    n = len(str1)
    res = -1

    # Initialize all indexes as -1.
    firstInd = [-1 for i in range(MAX_CHAR)]

    for i in range(n):
        first_ind = firstInd[ord(str1[i])]

        # If this is first occurrence
        if (first_ind == -1):
            firstInd[ord(str1[i])] = i

        # Else find distance from previous
        # occurrence and update result (if
        # required).
        else:
            res = max(res, abs(i - first_ind - 1))

    return res

# Driver code
str1 = "abba"
print(maximumChars(str1))

# This code is contributed by Mohit kumar 29
```

## C#

```
// Efficient C# program to find maximum
// number of characters between two
// occurrences of same character
using System;

public class GFG {

    static int MAX_CHAR = 256;

    static int maximumChars(string str)
    {
        int n = str.Length;
        int res = -1;

        // Initialize all indexes as -1.
        int []firstInd = new int[MAX_CHAR];

        for (int i = 0; i < MAX_CHAR; i++)
            firstInd[i] = -1;

        for (int i = 0; i < n; i++)
        {
            int first_ind = firstInd[str[i]];

            // If this is first occurrence
            if (first_ind == -1)
                firstInd[str[i]] = i;

            // Else find distance from previous
            // occurrence and update result (if
            // required).
            else
                res = Math.Max(res, Math.Abs(i
                              - first_ind - 1));
        }

        return res;
    }

    // Driver code

    static public void Main ()
    {
        string str = "abba";

        Console.WriteLine(maximumChars(str));
    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>
    // Efficient javascript program to find maximum
    // number of characters between two
    // occurrences of same character

    let MAX_CHAR = 256;

    function maximumChars(str)
    {
        let n = str.length;
        let res = -1;

        // Initialize all indexes as -1.
        let firstInd = new Array(MAX_CHAR);

        for (let i = 0; i < MAX_CHAR; i++)
            firstInd[i] = -1;

        for (let i = 0; i < n; i++)
        {
           let first_ind = firstInd[str[i].charCodeAt(0)];

            // If this is first occurrence
            if (first_ind == -1)
                firstInd[str[i].charCodeAt(0)] = i;

            // Else find distance from previous
            // occurrence and update result (if
            // required).
            else
                res = Math.max(res, Math.abs(i
                                  - first_ind - 1));
        }

        return res;
    }

    // Driver code
    let str = "abba";
    document.write(maximumChars(str));

// This code is contributed by patel2127
</script>
```

**输出:**

```
2
```

**时间复杂度:** O(n)

本文由 [**UDIT UPADHYAY**](https://auth.geeksforgeeks.org/profile.php?user=UDIT UPADHYAY) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。