# 元字符串(检查在一个字符串中交换后两个字符串是否可以相同)

> 原文:[https://www . geesforgeks . org/meta-strings-check-two-strings-can-swap-one-string/](https://www.geeksforgeeks.org/meta-strings-check-two-strings-can-become-swap-one-string/)

给定两个字符串，任务是检查这些字符串是否是元字符串。元字符串是可以通过任意字符串中的一次交换而相等的字符串。这里不将相等字符串视为元字符串。
示例:

```
Input : str1 = "geeks" 
        str2 = "keegs"
Output : Yes
By just swapping 'k' and 'g' in any of string, 
both will become same.

Input : str1 = "rsting"
        str2 = "string
Output : No

Input :  str1 = "Converse"
         str2 = "Conserve"
```

问于:谷歌

以下是算法中使用的步骤。

1.  检查两个字符串的长度是否相等，如果不相等，则返回 false。
2.  否则，开始比较字符串并计算不匹配字符的数量，同时存储不匹配字符的索引。
3.  如果不匹配的字符超过 2，则返回 false。
4.  否则，检查在任何字符串中交换这两个字符是否会使字符串相等。
5.  如果是，则返回真。否则返回 false。

## C++

```
// C++ program to check if two strings are meta strings
#include <bits/stdc++.h>
using namespace std;

// Returns true if str1 and str2 are meta strings
bool areMetaStrings(string str1, string str2)
{
    int len1 = str1.length();
    int len2 = str2.length();

    // Return false if both are not of equal length
    if (len1 != len2)
        return false;

    //If strings are equal
    if(str1 == str2){
       set<char>se(str1.begin(), str1.end());

       //If there is a character,which occur more than
       //once, we can swap, so that resultant string
       //remains same
       if(se.size() < str1.length()){
           return true;
       }
       return false;   

    }
    // To store indexes of previously mismatched
    // characters
    int prev = -1, curr = -1;

    int count = 0;
    for (int i=0; i<len1; i++)
    {
        // If current character doesn't match
        if (str1[i] != str2[i])
        {
            // Count number of unmatched character
            count++;

            // If unmatched are greater than 2,
            // then return false
            if (count > 2)
                return false;

            // Store both unmatched characters of
            // both strings
            prev = curr;
            curr = i;
        }
    }

    // Check if previous unmatched of string1
    // is equal to curr unmatched of string2
    // and also check for curr unmatched character,
    // if both are same, then return true
    return (count == 2 &&
            str1[prev] == str2[curr] &&
            str1[curr] == str2[prev]);
}

// Driver code
int main()
{
    string str1 = "converse";
    string str2 = "converse";

    areMetaStrings(str1,str2) ? cout << "Yes"
                            : cout << "No";
    return 0;
}
```

## C#

```
// C# program to check if two strings
// are meta strings
using System;
using System.Collections.Generic;

class GFG {

    // Returns true if str1 and str2
    // are meta strings
    static bool areMetaStrings(String str1,
                                String str2)
    {
        int len1 = str1.Length;
        int len2 = str2.Length;

        // Return false if both are not of
        // equal length
        if (len1 != len2)
            return false;

        if(str1==str2){
            var c = (new HashSet<char>(str1)).Count;
            if (c<len1){
                return true;
            }
            return false;

        }
        // To store indexes of previously
        // mismatched characters
        int prev = -1, curr = -1;

        int count = 0;
        for (int i = 0; i < len1; i++)
        {

            // If current character
            // doesn't match
            if (str1[i] != str2[i])
            {

                // Count number of unmatched
                // character
                count++;

                // If unmatched are greater
                // than 2, then return false
                if (count > 2)
                    return false;

                // Store both unmatched
                // characters of both strings
                prev = curr;
                curr = i;
            }
        }

        // Check if previous unmatched of
        // string1 is equal to curr unmatched
        // of string2 and also check for curr
        // unmatched character, if both are
        // same, then return true
        return (count == 2 &&
                 str1[prev] == str2[curr] &&
                   str1[curr] == str2[prev]);
    }

    // Driver method
    public static void Main()
    {
        String str1 = "converse";
        String str2 = "conserve";

        Console.WriteLine(
            areMetaStrings(str1,str2)
                       ? "Yes" :"No");
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php program to check if two strings
// are meta strings

// Returns true if str1 and str2 are
// meta strings
function areMetaStrings($str1, $str2)
{
    $len1 = strlen($str1);
    $len2 = strlen($str1);

    // Return false if both are not
    // of equal length
    if ($len1 != $len2)
        return false;

    if($str1 == $str2){

        $result = (count_chars($str1, len1));
        if(strlen($result) < $len1){
            return true;
        }
        return false;
    }
    // To store indexes of previously
    // mismatched characters
    $prev = -1; $curr = -1;

    $count = 0;
    for ($i = 0; $i < $len1; $i++)
    {

        // If current character
        // doesn't match
        if ($str1[$i] != $str2[$i])
        {

            // Count number of unmatched
            // character
            $count++;

            // If unmatched are greater
            // than 2, then return false
            if ($count > 2)
                return false;

            // Store both unmatched
            // characters of both
            // strings
            $prev = $curr;
            $curr = $i;
        }
    }

    // Check if previous unmatched of
    // string1 is equal to curr unmatched
    // of string2 and also check for curr
    // unmatched character, if both are
    // same, then return true
    return ($count == 2 &&
            $str1[$prev] == $str2[$curr] &&
            $str1[$curr] == $str2[$prev]);
}

// Driver code
    $str1 = "converse";
    $str2 = "conserve";

    if(areMetaStrings($str1, $str2))
        echo "Yes";
    else
        echo "No";

// This code is contributed by nitin mittal.
?>
```

## 蟒蛇 3

```
# Python program to check if two strings
# are meta strings

# Returns true if str1 and str2 are meta strings
def areMetaStrings( str1, str2) :
    len1 = len(str1)
    len2 = len(str2)

    # Return false if both are not of equal length
    if (len1 != len2) :
        return False

    if str1 == str2:
        char_seen = []
        for char in str1:
            if char not in char_seen:
                char_seen.append(char)
        if len(char_seen) < len(str1):
            return True
        return False       

    # To store indexes of previously mismatched
    # characters
    prev = -1
    curr = -1

    count = 0
    i = 0
    while i < len1 :

        # If current character doesn't match
        if (str1[i] != str2[i] ) :

        # Count number of unmatched character
            count = count + 1

            # If unmatched are greater than 2,
            # then return false
            if (count > 2) :
                return False

            # Store both unmatched characters of
            # both strings
            prev = curr
            curr = i

        i = i + 1

    # Check if previous unmatched of string1
    # is equal to curr unmatched of string2
    # and also check for curr unmatched character,
    # if both are same, then return true
    return (count == 2 and str1[prev] == str2[curr]
               and str1[curr] == str2[prev])

# Driver method
str1 = "converse"
str2 = "converse"
if ( areMetaStrings(str1,str2) ) :
    print("Yes")
else:
    print("No")

# This code is contributed by Koulick Sadhu.
```

## java 描述语言

```
<script>

      // JavaScript program to check if two strings
      // are meta strings
      // Returns true if str1 and str2
      // are meta strings
      function areMetaStrings(str1, str2) {
        var len1 = str1.length;
        var len2 = str2.length;

        // Return false if both are not of
        // equal length
        if (len1 !== len2) return false;

        if (str1 === str2) {
          var c = new Set(str1.split(""));
          if (c < len1) {
            return true;
          }
          return false;
        }
        // To store indexes of previously
        // mismatched characters
        var prev = -1,
          curr = -1;

        var count = 0;
        for (var i = 0; i < len1; i++) {
          // If current character
          // doesn't match
          if (str1[i] !== str2[i]) {
            // Count number of unmatched
            // character
            count++;

            // If unmatched are greater
            // than 2, then return false
            if (count > 2) return false;

            // Store both unmatched
            // characters of both strings
            prev = curr;
            curr = i;
          }
        }

        // Check if previous unmatched of
        // string1 is equal to curr unmatched
        // of string2 and also check for curr
        // unmatched character, if both are
        // same, then return true
        return (
          count === 2 && str1[prev] === str2[curr] &&
          str1[curr] === str2[prev]
        );
      }

      // Driver method
      var str1 = "converse";
      var str2 = "conserve";

      document.write(areMetaStrings(str1, str2) ? "Yes" : "No");

 </script>
```

**输出:**

```
Yes
```

**参考:**
[【https://www.careercup.com/question?id=6247626241474560】](https://www.careercup.com/question?id=6247626241474560)
本文由[**Sahil Chhabra(akku)**](https://www.facebook.com/sahil.chhabra.965)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。