# 在不删除字符的情况下制作两个字符串字谜所需的最小操作次数

> 原文:[https://www . geeksforgeeks . org/最小操作次数-需要生成两个字符串-不删除字符的字谜/](https://www.geeksforgeeks.org/minimum-number-of-manipulations-required-to-make-two-strings-anagram-without-deletion-of-character/)

给定两个字符串 **s1** 和 **s2** ，我们需要找到在不删除任何字符的情况下制作两个字符串字谜所需的最小操作次数。

**注意:-** 字谜串有相同的字符集，字符顺序可以不同。
如果允许删除字符并给出成本，请参考[使两个字符串相同的最小成本](https://www.geeksforgeeks.org/minimum-cost-make-two-strings-identical/)T5】问题来源:[Yatra.com 面试经验|第 7 集](https://www.geeksforgeeks.org/yatra-com-interview-experience-set-7/)

**示例:**

```
Input : 
       s1 = "aba"
       s2 = "baa"
Output : 0
Explanation: Both String contains identical characters

Input :
       s1 = "ddcf"
       s2 = "cedk"
Output : 2
Explanation : Here, we need to change two characters
in either of the strings to make them identical. We 
can change 'd' and 'f' in s1 or 'e' and 'k' in s2.
```

**假设:**两个字符串的长度被认为是相似的

## C++

```
// C++ Program to find minimum number
// of manipulations required to make
// two strings identical
#include <bits/stdc++.h>
using namespace std;

    // Counts the no of manipulations
    // required
    int countManipulations(string s1, string s2)
    {

        int count = 0;

        // store the count of character
        int char_count[26];

        for (int i = 0; i < 26; i++)
        {
            char_count[i] = 0;
        }

        // iterate though the first String
        // and update count
        for (int i = 0; i < s1.length(); i++)
            char_count[s1[i] - 'a']++;

        // iterate through the second string
        // update char_count.
        // if character is not found in
        // char_count then increase count
        for (int i = 0; i < s2.length(); i++)
        {
            char_count[s2[i] - 'a']--;      
        }

        for(int i = 0; i < 26; ++i)
        {
          if(char_count[i] != 0)
          {
            count+=abs(char_count[i]);
          }
        }
        return count / 2;
    }

    // Driver code
    int main()
    {

        string s1 = "ddcf";
        string s2 = "cedk";

        cout<<countManipulations(s1, s2);
    }

// This code is contributed by vt_m.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find minimum number of manipulations
// required to make two strings identical
public class Similar_strings {

    // Counts the no of manipulations required
    static int countManipulations(String s1, String s2)
    {
        int count = 0;

        // store the count of character
        int char_count[] = new int[26];

        // iterate though the first String and update
        // count
        for (int i = 0; i < s1.length(); i++)
            char_count[s1.charAt(i) - 'a']++;       

        // iterate through the second string
        // update char_count.
        // if character is not found in char_count
        // then increase count
        for (int i = 0; i < s2.length(); i++)
        {
            char_count[s2.charAt(i) - 'a']--;
        }

        for(int i = 0; i < 26; ++i)
        {
          if(char_count[i] != 0)
          {
            count+= Math.abs(char_count[i]);
          }
        }

        return count / 2;
    }

    // Driver code
    public static void main(String[] args)
    {

        String s1 = "ddcf";
        String s2 = "cedk";
        System.out.println(countManipulations(s1, s2));
    }
}
```

## 蟒蛇 3

```
# Python3 Program to find minimum number
# of manipulations required to make
# two strings identical

# Counts the no of manipulations
# required
def countManipulations(s1, s2):

    count = 0

    # store the count of character
    char_count = [0] * 26

    for i in range(26):
        char_count[i] = 0

    # iterate though the first String
    # and update count
    for i in range(len( s1)):
        char_count[ord(s1[i]) -
                   ord('a')] += 1

    # iterate through the second string
    # update char_count.
    # if character is not found in
    # char_count then increase count
    for i in range(len(s2)):
        char_count[ord(s2[i]) - ord('a')] -= 1

    for i in range(26):
        if char_count[i] != 0:
            count += abs(char_count[i])

    return count / 2

# Driver code
if __name__ == "__main__":

    s1 = "ddcf"
    s2 = "cedk"

    print(countManipulations(s1, s2))

# This code is contributed by ita_c
```

## C#

```
// C# Program to find minimum number
// of manipulations required to make
// two strings identical
using System;

public class GFG {

    // Counts the no of manipulations
    // required
    static int countManipulations(string s1,
                                  string s2)
    {
        int count = 0;

        // store the count of character
        int []char_count = new int[26];

        // iterate though the first String
        // and update count
        for (int i = 0; i < s1.Length; i++)
            char_count[s1[i] - 'a']++;

        // iterate through the second string
        // update char_count.
        // if character is not found in
        // char_count then increase count
        for (int i = 0; i < s2.Length; i++)
            char_count[s2[i] - 'a']--;

        for(int i = 0; i < 26; ++i)
        {
            if(char_count[i] != 0)
            {
              count+= Math.Abs(char_count[i]);
            }
        }

        return count / 2;
    }

    // Driver code
    public static void Main()
    {

        string s1 = "ddcf";
        string s2 = "cedk";

        Console.WriteLine(
            countManipulations(s1, s2));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find minimum number
// of manipulations required to make
// two strings identical

// Counts the no of manipulations
// required
function countManipulations($s1, $s2)
{
    $count = 0;

    // store the count of character
    $char_count = array_fill(0, 26, 0);

    // iterate though the first String
    // and update count
    for ($i = 0; $i < strlen($s1); $i++)
        $char_count[ord($s1[$i]) -
                    ord('a')] += 1;

    // iterate through the second string
    // update char_count.
    // if character is not found in
    // char_count then increase count
    for ($i = 0; $i < strlen($s2); $i++)
    {
        $char_count[ord($s2[$i]) -
                    ord('a')] -= 1;

    }

    for ($i = 0; $i < 26; $i++)
    {
      if($char_count[i]!=0)
      {
        $count+=abs($char_count[i]);
      }
    }
    return ($count) / 2;
}

// Driver code
$s1 = "ddcf";
$s2 = "cedk";

echo countManipulations($s1, $s2);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript program to find minimum number
// of manipulations required to make
// two strings identical

// Counts the no of manipulations
// required
function countManipulations(s1, s2)
{
    let count = 0;

    // Store the count of character
    let char_count = new Array(26);
    for(let i = 0; i < char_count.length; i++)
    {
        char_count[i] = 0;
    }

    // Iterate though the first String and
    // update count
    for(let i = 0; i < s1.length; i++)
        char_count[s1[i].charCodeAt(0) -
                     'a'.charCodeAt(0)]++;      

    // Iterate through the second string
    // update char_count.
    // If character is not found in char_count
    // then increase count
    for(let i = 0; i < s2.length; i++)
    {
        char_count[s2[i].charCodeAt(0) -
                     'a'.charCodeAt(0)]--;
    }

    for(let i = 0; i < 26; ++i)
    {
        if (char_count[i] != 0)
        {
            count += Math.abs(char_count[i]);
        }
    }
    return count / 2;
}

// Driver code
let s1 = "ddcf";
let s2 = "cedk";

document.write(countManipulations(s1, s2));

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
2
```

**时间复杂度:O(n)** ，其中 **n** 为弦的长度。

本文由**苏米特·戈什**供稿，由**医学博士伊斯塔哈尔·安萨里**改进。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。