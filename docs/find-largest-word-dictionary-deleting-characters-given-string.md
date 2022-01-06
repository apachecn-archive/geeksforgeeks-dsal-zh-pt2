# 通过删除给定字符串的某些字符找到字典中最大的单词

> 原文:[https://www . geesforgeks . org/find-最大单词-词典-删除-字符-给定-字符串/](https://www.geeksforgeeks.org/find-largest-word-dictionary-deleting-characters-given-string/)

给定一个字典和一个字符串“str”，找到字典中最长的字符串，该字符串可以通过删除给定“str”的某些字符而形成。
示例:

```
Input : dict = {"ale", "apple", "monkey", "plea"}   
        str = "abpcplea"  
Output : apple 

Input  : dict = {"pintu", "geeksfor", "geeksgeeks", 
                                        " forgeek"} 
         str = "geeksforgeeks"
Output : geeksgeeks
```

问于:**谷歌面试**

这个问题简化为[判断一个字符串是否是另一个字符串的子序列](https://www.geeksforgeeks.org/dynamic-programming-set-4-longest-common-subsequence/)。我们遍历所有字典单词，对于每个单词，我们检查它是否是给定字符串的子序列，并且是所有这些单词中最大的。我们最终以给定的字符串作为子序列返回最长的单词。
以下是上述想法的实现

## C++

```
// C++ program to find largest word in Dictionary
// by deleting some characters of given string
#include <bits/stdc++.h>
using namespace std;

// Returns true if str1[] is a subsequence of str2[].
// m is length of str1 and n is length of str2
bool isSubSequence(string str1, string str2)
{
    int m = str1.length(), n = str2.length();

    int j = 0; // For index of str1 (or subsequence

    // Traverse str2 and str1, and compare current
    // character of str2 with first unmatched char
    // of str1, if matched then move ahead in str1
    for (int i = 0; i < n && j < m; i++)
        if (str1[j] == str2[i])
            j++;

    // If all characters of str1 were found in str2
    return (j == m);
}

// Returns the longest string in dictionary which is a
// subsequence of str.
string findLongestString(vector<string> dict, string str)
{
    string result = "";
    int length = 0;

    // Traverse through all words of dictionary
    for (string word : dict) {
        // If current word is subsequence of str and is
        // largest such word so far.
        if (length < word.length()
            && isSubSequence(word, str)) {
            result = word;
            length = word.length();
        }
    }

    // Return longest string
    return result;
}

// Driver program to test above function
int main()
{
    vector<string> dict
        = { "ale", "apple", "monkey", "plea" };
    string str = "abpcplea";
    cout << findLongestString(dict, str) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find largest
// word in Dictionary by deleting
// some characters of given String

import java.util.*;

class GFG
{

    // Returns true if str1[] is a
    // subsequence of str2[]. m is
    // length of str1 and n is length of str2
    static boolean isSubSequence(String str1,
                                String str2)
    {
        int m = str1.length(), n = str2.length();

        int j = 0; // For index of str1 (or subsequence)

        // Traverse str2 and str1, and compare current
        // character of str2 with first unmatched char
        // of str1, if matched then move ahead in str1
        for (int i = 0; i < n && j < m; i++)
        {
            if (str1.charAt(j) == str2.charAt(i))
            {
                j++;
            }
        }

        // If all characters of str1
        // were found in str2
        return (j == m);
    }

// Returns the longest String
// in dictionary which is a
// subsequence of str.
    static String findLongestString(Vector<String> dict,
                                            String str)
    {
        String result = "";
        int length = 0;

        // Traverse through all words of dictionary
        for (String word : dict)
        {

            // If current word is subsequence of str
            // and is largest such word so far.
            if (length < word.length() &&
                isSubSequence(word, str))
            {
                result = word;
                length = word.length();
            }
        }

        // Return longest String
        return result;
    }

    // Driver code
    public static void main(String[] args)
    {
        String[] arr = {"ale", "apple", "monkey", "plea"};
        Vector dict = new Vector(Arrays.asList(arr));
        String str = "abpcplea";
        System.out.println(findLongestString(dict, str));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find largest word in Dictionary
# by deleting some characters of given string

# Returns true if str1[] is a subsequence of str2[].
# m is length of str1 and n is length of str2
def isSubSequence(str1, str2):

    m = len(str1);
    n = len(str2);

    j = 0; # For index of str1 (or subsequence

    # Traverse str2 and str1, and compare current
    # character of str2 with first unmatched char
    # of str1, if matched then move ahead in str1
    i = 0;
    while (i < n and j < m):
        if (str1[j] == str2[i]):
            j += 1;
        i += 1;

    # If all characters of str1 were found in str2
    return (j == m);

# Returns the longest string in dictionary which is a
# subsequence of str.
def findLongestString(dict1, str1):
    result = "";
    length = 0;

    # Traverse through all words of dictionary
    for word in dict1:

        # If current word is subsequence of str and is largest
        # such word so far.
        if (length < len(word) and isSubSequence(word, str1)):
            result = word;
            length = len(word);

    # Return longest string
    return result;

# Driver program to test above function

dict1 = ["ale", "apple", "monkey", "plea"];
str1 = "abpcplea" ;
print(findLongestString(dict1, str1));

# This code is conribued by mits
```

## C#

```
// C# program to find largest
// word in Dictionary by deleting
// some characters of given String
using System;
using System.Collections.Generic;

class GFG
{

    // Returns true if str1[] is a
    // subsequence of str2[]. m is
    // length of str1 and n is length of str2
    static bool isSubSequence(String str1,
                                String str2)
    {
        int m = str1.Length, n = str2.Length;

        int j = 0; // For index of str1 (or subsequence)

        // Traverse str2 and str1, and compare current
        // character of str2 with first unmatched char
        // of str1, if matched then move ahead in str1
        for (int i = 0; i < n && j < m; i++)
        {
            if (str1[j] == str2[i])
            {
                j++;
            }
        }

        // If all characters of str1
        // were found in str2
        return (j == m);
    }

    // Returns the longest String
    // in dictionary which is a
    // subsequence of str.
    static String findLongestString(List<String> dict,
                                            String str)
    {
        String result = "";
        int length = 0;

        // Traverse through all words of dictionary
        foreach (String word in dict)
        {

            // If current word is subsequence of str
            // and is largest such word so far.
            if (length < word.Length &&
                isSubSequence(word, str))
            {
                result = word;
                length = word.Length;
            }
        }

        // Return longest String
        return result;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String[] arr = {"ale", "apple", "monkey", "plea"};
        List<String> dict = new List<String>(arr);
        String str = "abpcplea";
        Console.WriteLine(findLongestString(dict, str));
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find largest word in Dictionary
// by deleting some characters of given string

// Returns true if str1[] is a subsequence of str2[].
// m is length of str1 and n is length of str2
function isSubSequence($str1, $str2)
{
    $m = strlen($str1);
    $n = strlen($str2);

    $j = 0; // For index of str1 (or subsequence

    // Traverse str2 and str1, and compare current
    // character of str2 with first unmatched char
    // of str1, if matched then move ahead in str1
    for ($i = 0; $i < $n && $j < $m; $i++)
        if ($str1[$j] == $str2[$i])
            $j++;

    // If all characters of str1 were found in str2
    return ($j == $m);
}

// Returns the longest string in dictionary which is a
// subsequence of str.
function findLongestString($dict, $str)
{
    $result = "";
    $length = 0;

    // Traverse through all words of dictionary
    foreach ($dict as $word)
    {

        // If current word is subsequence
        // of str and is largest
        // such word so far.
        if ($length < strlen($word) &&
             isSubSequence($word, $str))
        {
            $result = $word;
            $length = strlen($word);
        }
    }

    // Return longest string
    return $result;
}

// Driver code
$dict = array("ale", "apple", "monkey", "plea");
$str = "abpcplea" ;
echo findLongestString($dict, $str);

// This code is conribued by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to find largest word in Dictionary
// by deleting some characters of given string

// Returns true if str1[] is a subsequence of str2[].
// m is length of str1 and n is length of str2
function isSubSequence(str1, str2)
{
    var m = str1.length, n = str2.length;

    var j = 0; // For index of str1 (or subsequence

    // Traverse str2 and str1, and compare current
    // character of str2 with first unmatched char
    // of str1, if matched then move ahead in str1
    for (var i = 0; i < n && j < m; i++)
        if (str1[j] == str2[i])
            j++;

    // If all characters of str1 were found in str2
    return (j == m);
}

// Returns the longest string in dictionary which is a
// subsequence of str.
function findLongestString(dict, str)
{
    var result = "";
    var length = 0;

    // Traverse through all words of dictionary

    dict.forEach(word => {

        // If current word is subsequence of str and is
        // largest such word so far.
        if (length < word.length
            && isSubSequence(word, str)) {
            result = word;
            length = word.length;
        }
    });

    // Return longest string
    return result;
}

// Driver program to test above function
var dict
    = ["ale", "apple", "monkey", "plea"];
var str = "abpcplea";
document.write( findLongestString(dict, str));

</script>
```

**输出:**

```
apple
```

**时间复杂度:** O(N*(K+n))这里 N 是字典的长度，N 是给定字符串‘str’的长度，K–字典中单词的最大长度。
**辅助空间:** O(1)

一个**高效的**解决方案是我们**整理**这个字典单词。我们遍历所有字典单词，对于每个单词，我们检查它是否是给定字符串的子序列，最后我们检查这个子序列是否是所有这样的子序列中最大的..我们最终以给定的字符串作为子序列返回最长的单词。

## C++

```
// C++ program to find largest word in Dictionary
// by deleting some characters of given string
#include <bits/stdc++.h>
using namespace std;
    string res="";
    void check(string d,string s)
    {
        int i=0;
        int j=0;
        while(i<d.size() && j<s.size())
        {
            if(d[i]==s[j])
            {
                i++;
                j++;
            }
            else
             j++;
        }
        if(i==d.size() && res.size()<d.size())
        {
            res=d;
        }
    }
   string LongestWord(vector<string> d,string S) {
     //sort the dictionary word
     // for smallest lexicographical order

     sort(d.begin(),d.end());
     for(string c:d)
     {
         check(c,S);
     }
     return res;
    }
// Driver program
int main()
{
    vector<string> dict
        = { "ale", "apple", "monkey", "plea" };
    string str = "abpcplea";
    cout << LongestWord(dict, str) << endl;
    return 0;
}
```

本文由 [**尼尚·辛格**](https://practice.geeksforgeeks.org/user-profile.php?user=_code) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。