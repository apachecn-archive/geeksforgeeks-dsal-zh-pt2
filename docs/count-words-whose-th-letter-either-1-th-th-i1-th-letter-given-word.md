# 给定单词的第 I 个字母为第(i-1)个、第 i-个或第(i+1)个字母的单词数

> 原文:[https://www . geesforgeks . org/count-words-what-th-字母-or-1-th-i1-th-字母-给定-word/](https://www.geeksforgeeks.org/count-words-whose-th-letter-either-1-th-th-i1-th-letter-given-word/)

给定一根弦**弦**。任务是统计与 str 长度相同的单词，第 I 个位置的每个字母要么是 str 的第(i-1)个，要么是 str 的第(i+1)个位置的字母。
注:第一个字母考虑 w 的第 I 和(i+1)个位置字母，最后一个字母考虑 str 的第 I 和第 I 个位置字母。
示例:

```
Input : str[] = "ab"
Output : 4
Words that can be formed: aa, ab, ba, bb.

Input : str[] = "x"
Output : 1
```

对于索引 I 中的任何字母，除了第一个和最后一个字母，给定单词有三个可能的字母，即第(i-1)个、第(I)个或第(i+1)个字母。所以，如果其中三个是不同的，我们有三种可能性。如果其中两个相同，我们有两种可能。如果都一样，我们只有一种可能。
所以，遍历给定的单词，找出每个字母的可能性，并将其相乘。
同样，对于第一个字母，检查第一个和第二个位置的不同字母。最后一个位置检查最后一个和第二个最后一个位置的不同字母。
以下是本办法的实施情况:

## C++

```
// C++ program to count words  whose ith letter
// is either (i-1)th, ith, or (i+1)th letter
// of given word.
#include<bits/stdc++.h>
using namespace std;

// Return the count of words.
int countWords(char str[], int len)
{
    int count = 1;

    // If word contain single letter, return 1.
    if (len == 1)
        return count;

    // Checking for first letter.
    if (str[0] == str[1])
        count *= 1;
    else
        count *= 2;

    // Traversing the string and multiplying
    // for combinations.
    for (int j=1; j<len-1; j++)
    {
        // If all three letters are same.
        if (str[j] == str[j-1] && str[j] == str[j+1])
            count *= 1;

        // If two letter are distinct.
        else if (str[j] == str[j-1] ||
                 str[j] == str[j+1] ||
                 str[j-1] == str[j+1])
            count *= 2;

        // If all three letter are distinct.
        else
            count *= 3;
    }

    // Checking for last letter.
    if (str[len - 1] == str[len - 2])
        count *= 1;
    else
        count *= 2;

    return count;
}

// Driven Program
int main()
{
    char str[] = "abc";
    int len = strlen(str);

    cout << countWords(str, len) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count words  whose ith letter
// is either (i-1)th, ith, or (i+1)th letter
// of given word.
public class GFG {

    // Return the count of words.
    static int countWords(String str, int len)
    {
        int count = 1;

        // If word contain single letter, return 1.
        if (len == 1)
            return count;

        // Checking for first letter.
        if (str.charAt(0) == str.charAt(1))
            count *= 1;
        else
            count *= 2;

        // Traversing the string and multiplying
        // for combinations.
        for (int j = 1; j < len - 1; j++)
        {
            // If all three letters are same.
            if (str.charAt(j) == str.charAt(j - 1) &&
                    str.charAt(j) == str.charAt(j + 1))
                count *= 1;

            // If two letter are distinct.
            else if (str.charAt(j) == str.charAt(j - 1)||
                    str.charAt(j) == str.charAt(j + 1) ||
                   str.charAt(j - 1) == str.charAt(j + 1))
                count *= 2;

            // If all three letter are distinct.
            else
                count *= 3;
        }

        // Checking for last letter.
        if (str.charAt(len - 1) == str.charAt(len - 2))
            count *= 1;
        else
            count *= 2;

        return count;
    }

    // Driven Program
    public static void main(String args[])
    {
        String str = "abc";
        int len = str.length();

        System.out.println(countWords(str, len));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python 3 program to count words  whose ith letter
# is either (i-1)th, ith, or (i+1)th letter
# of given word.

# Return the count of words.
def countWords( str,  l):

    count = 1;

    # If word contain single letter, return 1.
    if (l == 1):
        return count

    # Checking for first letter.
    if (str[0] == str[1]):
        count *= 1
    else:
        count *= 2

    # Traversing the string and multiplying
    # for combinations.
    for j in range(1,l-1):
        # If all three letters are same.
        if (str[j] == str[j-1] and str[j] == str[j+1]):
            count *= 1

        # If two letter are distinct.
        elif (str[j] == str[j-1] or
                 str[j] == str[j+1] or
                 str[j-1] == str[j+1]):
            count *= 2

        # If all three letter are distinct.
        else:
            count *= 3

    # Checking for last letter.
    if (str[l - 1] == str[l - 2]):
        count *= 1
    else:
        count *= 2

    return count

# Driven Program
if __name__ == "__main__":

    str = "abc"
    l = len(str)

    print(countWords(str, l))
```

## C#

```
// C# program to count words whose
// ith letter is either (i-1)th,
// ith, or (i+1)th letter of the
// given word
using System;

public class GFG {

    // Return the count of words.
    static int countWords(string str, int len)
    {
        int count = 1;

        // If word contain single letter,
        // return 1.
        if (len == 1)
            return count;

        // Checking for first letter.
        if (str[0] == str[1])
            count *= 1;
        else
            count *= 2;

        // Traversing the string and
        // multiplying for combinations.
        for (int j = 1; j < len - 1; j++) {

            // If all three letters are same.
            if (str[j] == str[j - 1] &&
                  str[j] == str[j + 1])
                count *= 1;

            // If two letter are distinct.
            else if (str[j] == str[j - 1] ||
                     str[j] == str[j + 1] ||
                    str[j - 1] == str[j + 1])
                count *= 2;

            // If all three letter are distinct.
            else
                count *= 3;
        }

        // Checking for last letter.
        if (str[len - 1] == str[len - 2])
            count *= 1;
        else
            count *= 2;

        return count;
    }

    // Driver Program
    public static void Main()
    {
        string str = "abc";
        int len = str.Length;

        Console.WriteLine(countWords(str, len));
    }
}

// This code is contributed by Anant Agarwal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count
// words whose ith letter
// is either (i-1)th, ith,
// or (i+1)th letter of
// given word.

// Return the count of words.
function countWords($str, $len)
{
    $count = 1;

    // If word contain single
    // letter, return 1.
    if ($len == 1)
        return $count;

    // Checking for first letter.
    if ($str[0] == $str[1])
        $count *= 1;
    else
        $count *= 2;

    // Traversing the string
    // and multiplying for
    // combinations.
    for($j = 1; $j < $len - 1; $j++)
    {

        // If all three letters are same.
        if ($str[$j] == $str[$j - 1] &&
              $str[$j] == $str[$j + 1])
            $count *= 1;

        // If two letter are distinct.
        else if ($str[$j] == $str[$j - 1] ||
                 $str[$j] == $str[$j + 1] ||
                 $str[$j - 1] == $str[$j + 1])
            $count *= 2;

        // If all three letter
        // are distinct.
        else
            $count *= 3;
    }

    // Checking for last letter.
    if ($str[$len - 1] == $str[$len - 2])
        $count *= 1;
    else
        $count *= 2;

    return $count;
}

    // Driver Code
    $str = "abc";
    $len = strlen($str);

    echo countWords($str, $len) ;

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
// Javascript program to count words  whose ith letter
// is either (i-1)th, ith, or (i+1)th letter
// of given word.

    // Return the count of words.
    function countWords(str,len)
    {
        let count = 1;

        // If word contain single letter, return 1.
        if (len == 1)
            return count;

        // Checking for first letter.
        if (str[0] == str[1])
            count *= 1;
        else
            count *= 2;

        // Traversing the string and multiplying
        // for combinations.
        for (let j = 1; j < len - 1; j++)
        {
            // If all three letters are same.
            if (str[j] == str[j-1] &&
                    str[j] == str[j+1])
                count *= 1;

            // If two letter are distinct.
            else if (str[j] == str[j-1]||
                    str[j] == str[j+1] ||
                   str[j-1] == str[j+1])
                count *= 2;

            // If all three letter are distinct.
            else
                count *= 3;
        }

        // Checking for last letter.
        if (str[len-1] == str[len-2])
            count *= 1;
        else
            count *= 2;

        return count;
    }
     // Driven Program
    let str = "abc";
    let len= str.length;
    document.write(countWords(str, len));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
12
```

**时间复杂度:** O(字符串长度)。

本文由 [**Anuj Chauhan**](https://www.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。