# 使用排序的最长公共前缀

> 原文:[https://www . geesforgeks . org/最长-常用-前缀-使用-排序/](https://www.geeksforgeeks.org/longest-common-prefix-using-sorting/)

**问题陈述:**给定一组字符串，找出最长的公共前缀。
**例:**

```
Input: {"geeksforgeeks", "geeks", "geek", "geezer"}
Output: "gee"

Input: {"apple", "ape", "april"}
Output: "ap"
```

字符串数组中最长的公共前缀是两个最不相似的字符串之间的公共前缀。例如，在给定的数组{“apple”、“ape”、“zebra”}中，没有公共前缀，因为数组“ape”和“zebra”的两个最不相似的字符串不共享任何起始字符。
我们已经在下面的帖子中讨论了五种不同的方法。

1.  [逐词匹配](https://www.geeksforgeeks.org/longest-common-prefix-set-1-word-by-word-matching/)
2.  [逐字符匹配](https://www.geeksforgeeks.org/longest-common-prefix-set-2-character-by-character-matching/)
3.  [分而治之](https://www.geeksforgeeks.org/longest-common-prefix-set-3-divide-and-conquer/)
4.  [二分搜索法](https://www.geeksforgeeks.org/longest-common-prefix-set-4-binary-search/)。
5.  [使用 Trie)](https://www.geeksforgeeks.org/longest-common-prefix-set-5-using-trie/)

本文讨论了一种基于排序的新方法。其思想是对字符串数组进行排序，并找到排序后的数组的第一个和最后一个字符串的公共前缀。

## C++

```
// C++ program to find longest common prefix
// of given array of words.
#include<iostream>
#include<algorithm>

using namespace std;

// Function to find the longest common prefix
string longestCommonPrefix(string ar[], int n)
{

    // If size is 0, return empty string
    if (n == 0)
        return "";

    if (n == 1)
        return ar[0];

    // Sort the given array
    sort(ar, ar + n);

    // Find the minimum length from
    // first and last string
    int en = min(ar[0].size(),
                 ar[n - 1].size());

    // Now the common prefix in first and
    // last string is the longest common prefix
    string first = ar[0], last = ar[n - 1];
    int i = 0;
    while (i < en && first[i] == last[i])
        i++;

    string pre = first.substr(0, i);
    return pre;
}

// Driver Code
int main()
{
    string ar[] = {"geeksforgeeks", "geeks",
                           "geek", "geezer"};
    int n = sizeof(ar) / sizeof(ar[0]);
    cout << "The longest common prefix is: "
         << longestCommonPrefix(ar, n);
    return 0;
}

// This code is contributed by jrolofmeister
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find longest common prefix of
// given array of words.
import java.util.*;

public class GFG
{
    public String longestCommonPrefix(String[] a)
    {
        int size = a.length;

        /* if size is 0, return empty string */
        if (size == 0)
            return "";

        if (size == 1)
            return a[0];

        /* sort the array of strings */
        Arrays.sort(a);

        /* find the minimum length from first and last string */
        int end = Math.min(a[0].length(), a[size-1].length());

        /* find the common prefix between the first and
           last string */
        int i = 0;
        while (i < end && a[0].charAt(i) == a[size-1].charAt(i) )
            i++;

        String pre = a[0].substring(0, i);
        return pre;
    }

    /* Driver Function to test other function */
    public static void main(String[] args)
    {
        GFG gfg = new GFG();
        String[] input = {"geeksforgeeks", "geeks", "geek", "geezer"};
        System.out.println( "The longest Common Prefix is : " +
                                   gfg.longestCommonPrefix(input));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find longest
# common prefix of given array of words.
def longestCommonPrefix( a):

    size = len(a)

    # if size is 0, return empty string
    if (size == 0):
        return ""

    if (size == 1):
        return a[0]

    # sort the array of strings
    a.sort()

    # find the minimum length from
    # first and last string
    end = min(len(a[0]), len(a[size - 1]))

    # find the common prefix between
    # the first and last string
    i = 0
    while (i < end and
           a[0][i] == a[size - 1][i]):
        i += 1

    pre = a[0][0: i]
    return pre

# Driver Code
if __name__ == "__main__":

    input = ["geeksforgeeks", "geeks",
                     "geek", "geezer"]
    print("The longest Common Prefix is :" ,
                 longestCommonPrefix(input))

# This code is contributed by ita_c
```

## C#

```
// C# program to find longest common prefix of
// given array of words.
using System;

public class GFG {

    static string longestCommonPrefix(String[] a)
    {
        int size = a.Length;

        /* if size is 0, return empty string */
        if (size == 0)
            return "";

        if (size == 1)
            return a[0];

        /* sort the array of strings */
        Array.Sort(a);

        /* find the minimum length from first
        and last string */
        int end = Math.Min(a[0].Length,
                            a[size-1].Length);

        /* find the common prefix between the
        first and last string */
        int i = 0;
        while (i < end && a[0][i] == a[size-1][i] )
            i++;

        string pre = a[0].Substring(0, i);
        return pre;
    }

    /* Driver Function to test other function */
    public static void Main()
    {

        string[] input = {"geeksforgeeks", "geeks",
                                 "geek", "geezer"};

        Console.WriteLine( "The longest Common"
                              + " Prefix is : "
                  + longestCommonPrefix(input));
    }
}

// This code is contributed by Sam007.
```

## java 描述语言

```
<script>
// Javascript program to find longest common prefix of
// given array of words.

    function longestCommonPrefix(a)
    {
        let size = a.length;

        /* if size is 0, return empty string */
        if (size == 0)
            return "";

        if (size == 1)
            return a[0];

        /* sort the array of strings */
        a.sort();

        /* find the minimum length from first and last string */
        let end = Math.min(a[0].length, a[size-1].length);

        /* find the common prefix between the first and
           last string */
        let i = 0;
        while (i < end && a[0][i] == a[size-1][i] )
            i++;

        let pre = a[0].substring(0, i);
        return pre;
    }

    /* Driver Function to test other function */
    let input=["geeksforgeeks", "geeks", "geek", "geezer"];
    document.write( "The longest Common Prefix is : " +
                                   longestCommonPrefix(input));

    // This code is contributed by rag2127
</script>
```

**输出:**

```
The longest common prefix is : gee
```

**时间复杂度:** O(MAX * n * log n)，其中 n 为数组中的字符串数，MAX 为任意字符串中的最大字符数。请注意，两个字符串的比较最多需要 O(最大值)时间，对于排序 n 个字符串，我们需要 O(最大值* n * log n)时间。
本文由**萨罗尼·巴韦贾**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。