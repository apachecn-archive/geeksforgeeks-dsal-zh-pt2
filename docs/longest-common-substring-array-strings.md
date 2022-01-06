# 字符串数组中最长的公共子串

> 原文:[https://www . geesforgeks . org/最长-公共-子串-数组-字符串/](https://www.geeksforgeeks.org/longest-common-substring-array-strings/)

我们得到了一个共有词干的单词列表，也就是说，这些单词源自同一个单词，例如:单词**悲伤，悲伤**和**悲伤**都源自词干**“悲伤”**。
我们的任务是找到并返回最长的公共子串，也就是那些单词的词干。如果有领带，我们按字母顺序选择最小的一条。

**示例:**

```
Input : grace graceful disgraceful gracefully
Output : grace

Input : sadness sad sadly
Output : sad

```

其思想是将列表中的任何单词作为引用，并形成其所有子字符串，然后遍历整个列表，检查生成的子字符串是否出现在所有子字符串中。

下面是上述想法的实现:

## C++

```
// C++ program to find the stem of given list of
// words
#include <bits/stdc++.h>
using namespace std;

// function to find the stem (longest common
// substring) from the string array
string findstem(vector<string> arr)
{
    // Determine size of the array
    int n = arr.size();

    // Take first word from array as reference
    string s = arr[0];
    int len = s.length();

    string res = "";

    for (int i = 0; i < len; i++) {
        for (int j = i + 1; j <= len; j++) {
            // generating all possible substrings
            // of our reference string arr[0] i.e s
            string stem = s.substr(i, j);
            int k = 1;
            for (k = 1; k < n; k++) {
                // Check if the generated stem is
                // common to all words
                if (arr[k].find(stem) == std::string::npos)
                    break;
            }

            // If current substring is present in
            // all strings and its length is greater
            // than current result
            if (k == n && res.length() < stem.length())
                res = stem;
        }
    }

    return res;
}

// Driver code
int main()
{
    vector<string> arr{ "grace", "graceful", "disgraceful",
                        "gracefully" };

    // Function call
    string stems = findstem(arr);
    cout << stems << endl;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the stem of given list of
// words
import java.io.*;
import java.util.*;

class stem {

    // function to find the stem (longest common
    // substring) from the string  array
    public static String findstem(String arr[])
    {
        // Determine size of the array
        int n = arr.length;

        // Take first word from array as reference
        String s = arr[0];
        int len = s.length();

        String res = "";

        for (int i = 0; i < len; i++) {
            for (int j = i + 1; j <= len; j++) {

                // generating all possible substrings
                // of our reference string arr[0] i.e s
                String stem = s.substring(i, j);
                int k = 1;
                for (k = 1; k < n; k++)

                    // Check if the generated stem is
                    // common to all words
                    if (!arr[k].contains(stem))
                        break;

                // If current substring is present in
                // all strings and its length is greater
                // than current result
                if (k == n && res.length() < stem.length())
                    res = stem;
            }
        }

        return res;
    }

    // Driver Code
    public static void main(String args[])
    {
        String arr[] = { "grace", "graceful",
                        "disgraceful","gracefully" };

        // Function call
        String stems = findstem(arr);
        System.out.println(stems);
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find the stem
# of given list of words

# function to find the stem (longest
# common substring) from the string array

def findstem(arr):

    # Determine size of the array
    n = len(arr)

    # Take first word from array
    # as reference
    s = arr[0]
    l = len(s)

    res = ""

    for i in range(l):
        for j in range(i + 1, l + 1):

            # generating all possible substrings
            # of our reference string arr[0] i.e s
            stem = s[i:j]
            k = 1
            for k in range(1, n):

                # Check if the generated stem is
                # common to all words
                if stem not in arr[k]:
                    break

            # If current substring is present in
            # all strings and its length is greater
            # than current result
            if (k + 1 == n and len(res) < len(stem)):
                res = stem

    return res

# Driver Code
if __name__ == "__main__":

    arr = ["grace", "graceful",
           "disgraceful", "gracefully"]

    # Function call
    stems = findstem(arr)
    print(stems)

# This code is contributed by ita_c
```

## C#

```
// C# program to find the stem of given list of
// words
using System;
using System.Collections.Generic;

class stem
{
    // function to find the stem (longest common
    // substring) from the string array
    public static String findstem(String []arr)
    {
        // Determine size of the array
        int n = arr.Length;

        // Take first word from array as reference
        String s = arr[0];
        int len = s.Length;

        String res = "";

        for (int i = 0; i < len; i++)
        {
            for (int j = i + 1; j <= len; j++)
            {

                // generating all possible substrings
                // of our reference string arr[0] i.e s
                String stem = s.Substring(i, j-i);
                int k = 1;
                for (k = 1; k < n; k++)

                    // Check if the generated stem is
                    // common to all words
                    if (!arr[k].Contains(stem))
                        break;

                // If current substring is present in
                // all strings and its length is greater
                // than current result
                if (k == n && res.Length < stem.Length)
                    res = stem;
            }
        }

        return res;
    }

    // Driver Code
    public static void Main(String []args)
    {
        String []arr = { "grace", "graceful", "disgraceful",
                                            "gracefully" };
        // Function call
        String stems = findstem(arr);
        Console.WriteLine(stems);
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the stem of given list of
// words

    // function to find the stem (longest common
    // substring) from the string array
    function findstem($arr)
    {
        // Determine size of the array
        $n = count($arr);

        // Take first word from array as reference
        $s = $arr[0];
        $len = strlen($s);

        $res = "";

        for ($i = 0; $i < $len; $i++)
        {
            for ($j = $i+1; $j <=$len; $j++)
            {

                // generating all possible substrings
                // of our reference string arr[0] i.e s
                $stem = substr($s,$i, $j-$i);

                $k = 1;
                for ($k = 1; $k < $n; $k++)

                    // Check if the generated stem is
                    // common to all words
                    if (!strpos($arr[$k],$stem))
                        break;

                // If current substring is present in
                // all strings and its length is greater
                // than current result
                if ($k <= $n && strlen($res) < strlen($stem))
                    $res = $stem;

            }
        }

        return $res;
    }

    // Driver Code
    $arr = array( "grace", "graceful",
                 "disgraceful", "gracefully" );

    // Function call
    $stems = findstem($arr);
    print($stems);

// This code is contributed by mits
?>
```

**Output**

```
grace

```

本文由 [**丹麦 KALEEM**](https://www.linkedin.com/in/mohdanishh/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。