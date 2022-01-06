# 允许排列的最长公共子序列

> 原文:[https://www . geesforgeks . org/最长-公共-子序列-带排列-允许/](https://www.geeksforgeeks.org/longest-common-subsequence-with-permutations-allowed/)

给定两个小写字符串，找到最长的字符串，它的排列是给定两个字符串的子序列。必须对输出的最长字符串进行排序。
**例:**

```
Input  :  str1 = "pink", str2 = "kite"
Output : "ik" 
The string "ik" is the longest sorted string 
whose one permutation "ik" is subsequence of
"pink" and another permutation "ki" is 
subsequence of "kite". 

Input  : str1 = "working", str2 = "women"
Output : "now"

Input  : str1 = "geeks" , str2 = "cake"
Output : "ek"

Input  : str1 = "aaaa" , str2 = "baba"
Output : "aa"
```

这个想法是计算两个字符串中的字符数。

1.  计算每个字符串的字符频率，并将它们存储在各自的计数数组中，比如 str1 的 count1[]和 str2 的 count2[]。
2.  现在我们有了 26 个字符的计数数组。因此遍历 count1[]并对任何索引“I”在结果字符串“result”中追加字符(‘a’+I)最小(count1[i]，count2[i])次。
3.  因为我们以升序遍历计数数组，所以最后的字符串将按排序顺序排列。

## C++

```
// C++ program to find LCS with permutations allowed
#include<bits/stdc++.h>
using namespace std;

// Function to calculate longest string
// str1     --> first string
// str2     --> second string
// count1[] --> hash array to calculate frequency
//             of characters in str1
// count[2] --> hash array to calculate frequency
//             of characters in str2
// result --> resultant longest string whose
// permutations are sub-sequence of given two strings
void longestString(string str1, string str2)
{
    int count1[26] = {0}, count2[26]= {0};

    // calculate frequency of characters
    for (int i=0; i<str1.length(); i++)
        count1[str1[i]-'a']++;
    for (int i=0; i<str2.length(); i++)
        count2[str2[i]-'a']++;

    // Now traverse hash array
    string result;
    for (int i=0; i<26; i++)

        // append character ('a'+i) in resultant
        // string 'result' by min(count1[i],count2i])
        // times
        for (int j=1; j<=min(count1[i],count2[i]); j++)
            result.push_back('a' + i);

    cout << result;
}

// Driver program to run the case
int main()
{
    string str1 = "geeks", str2 = "cake";
    longestString(str1, str2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program to find LCS with permutations allowed

class GFG {

// Function to calculate longest String
// str1     --> first String
// str2     --> second String
// count1[] --> hash array to calculate frequency
//             of characters in str1
// count[2] --> hash array to calculate frequency
//             of characters in str2
// result --> resultant longest String whose
// permutations are sub-sequence of given two strings
    static void longestString(String str1, String str2) {
        int count1[] = new int[26], count2[] = new int[26];

        // calculate frequency of characters
        for (int i = 0; i < str1.length(); i++) {
            count1[str1.charAt(i) - 'a']++;
        }
        for (int i = 0; i < str2.length(); i++) {
            count2[str2.charAt(i) - 'a']++;
        }

        // Now traverse hash array
        String result = "";
        for (int i = 0; i < 26; i++) // append character ('a'+i) in resultant
        // String 'result' by min(count1[i],count2i])
        // times
        {
            for (int j = 1; j <= Math.min(count1[i], count2[i]); j++) {
                result += (char)('a' + i);
            }
        }

        System.out.println(result);
    }

// Driver program to run the case
    public static void main(String[] args) {
        String str1 = "geeks", str2 = "cake";
        longestString(str1, str2);

    }
}
/* This java code is contributed by 29AjayKumar*/
```

## 蟒蛇 3

```
# Python 3 program to find LCS
# with permutations allowed

# Function to calculate longest string
# str1     --> first string
# str2     --> second string
# count1[] --> hash array to calculate frequency
#             of characters in str1
# count[2] --> hash array to calculate frequency
#             of characters in str2
# result --> resultant longest string whose
# permutations are sub-sequence
# of given two strings
def longestString(str1, str2):

    count1 = [0] * 26
    count2 = [0] * 26

    # calculate frequency of characters
    for i in range( len(str1)):
        count1[ord(str1[i]) - ord('a')] += 1
    for i in range(len(str2)):
        count2[ord(str2[i]) - ord('a')] += 1

    # Now traverse hash array
    result = ""
    for i in range(26):

        # append character ('a'+i) in
        # resultant string 'result' by
        # min(count1[i],count2i]) times
        for j in range(1, min(count1[i],
                            count2[i]) + 1):
            result = result + chr(ord('a') + i)

    print(result)

# Driver Code
if __name__ == "__main__":

    str1 = "geeks"
    str2 = "cake"
    longestString(str1, str2)

# This code is contributed by ita_c
```

## C#

```
// C# program to find LCS with
// permutations allowed
using System;

class GFG
{

// Function to calculate longest String
// str1 --> first String
// str2 --> second String
// count1[] --> hash array to calculate
//     frequency of characters in str1
// count[2] --> hash array to calculate
//         frequency of characters in str2
// result --> resultant longest String whose
// permutations are sub-sequence of
// given two strings
static void longestString(String str1,
                        String str2)
{
    int []count1 = new int[26];
    int []count2 = new int[26];

    // calculate frequency of characters
    for (int i = 0; i < str1.Length; i++)
    {
        count1[str1[i] - 'a']++;
    }
    for (int i = 0; i < str2.Length; i++)
    {
        count2[str2[i] - 'a']++;
    }

    // Now traverse hash array
    String result = "";
    for (int i = 0; i < 26; i++)

    // append character ('a'+i) in resultant
    // String 'result' by min(count1[i],count2i])
    // times
    {
        for (int j = 1;
                j <= Math.Min(count1[i],
                            count2[i]); j++)
        {
            result += (char)('a' + i);
        }
    }

Console.Write(result);
}

// Driver Code
public static void Main()
{
    String str1 = "geeks", str2 = "cake";
    longestString(str1, str2);
}
}

// This code is contributed
// by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find LCS with
// permutations allowed

// Function to calculate longest string
// str1     --> first string
// str2     --> second string
// count1[] --> hash array to calculate frequency
//             of characters in str1
// count[2] --> hash array to calculate frequency
//             of characters in str2
// result --> resultant longest string whose
// permutations are sub-sequence of given two strings
function longestString($str1, $str2)
{
    $count1 = array_fill(0, 26, NULL);
    $count2 = array_fill(0, 26, NULL);

    // calculate frequency of characters
    for ($i = 0; $i < strlen($str1); $i++)
        $count1[ord($str1[$i]) - ord('a')]++;
    for ($i = 0; $i < strlen($str2); $i++)
        $count2[ord($str2[$i]) - ord('a')]++;

    // Now traverse hash array
    $result = "";
    for ($i = 0; $i < 26; $i++)

        // append character ('a'+i) in resultant
        // string 'result' by min(count1[$i],
        // count2[$i]) times
        for ($j = 1; $j <= min($count1[$i],
                            $count2[$i]); $j++)
            $result = $result.chr(ord('a') + $i);

    echo $result;
}

// Driver Code
$str1 = "geeks";
$str2 = "cake";
longestString($str1, $str2);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript program to find LCS with permutations allowed
function min(a, b)
{
    if(a < b)
        return a;
       else
       return b;
}

// Function to calculate longest String
// str1     --> first String
// str2     --> second String
// count1[] --> hash array to calculate frequency
//             of characters in str1
// count[2] --> hash array to calculate frequency
//             of characters in str2
// result --> resultant longest String whose
// permutations are sub-sequence of given two strings
function longestString( str1,  str2)
{
        var count1 = new Array(26);
        var count2 = new Array(26);
        count1.fill(0);
         count2.fill(0);

        // calculate frequency of characters
        for (var i = 0; i < str1.length; i++) {
            count1[str1.charCodeAt(i) -97]++;
        }
        for (var i = 0; i < str2.length; i++) {
            count2[str2.charCodeAt(i) - 97]++;
        }

        // Now traverse hash array
        var result = "";
        for (var i = 0; i < 26; i++)

        // append character ('a'+i) in resultant
        // String 'result' by min(count1[i],count2i])
        // times
        {
            for (var j = 1; j <= min(count1[i], count2[i]); j++) {
                result += String.fromCharCode(97 + i);
            }
        }

        document.write(result);
    }
        var str1 = "geeks";
        var str2 = "cake";
        longestString(str1, str2);

// This code is contributed by akshitsaxenaa09.
</script>
```

**Output**

```
ek
```