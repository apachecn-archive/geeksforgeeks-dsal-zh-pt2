# 最少删除次数，以免两个连续的相同

> 原文:[https://www . geesforgeks . org/最小数量-删除-不-两个-连续/](https://www.geeksforgeeks.org/minimum-number-deletions-no-two-consecutive/)

给定一个字符串，找到所需的最小删除次数，这样字符串中就不会有两个连续的重复字符。
示例:

```
Input : AAABBB
Output : 4
Explanation : New string should be AB

Input : ABABABAB
Output : 0
Explanation : There are no consecutive repeating characters.
```

如果有 n 个连续的相同字符，从这 n 个字符中删除 n-1 个。

## C++

```
// CPP code to count minimum deletions required
// so that there are no consecutive characters left
#include <bits/stdc++.h>
using namespace std;

int countDeletions(string str)
{
    int ans = 0;
    for (int i = 0; i < str.length() - 1; i++)

        // If two consecutive characters are
        // the same, delete one of them.
        if (str[i] == str[i + 1])
            ans++;

   return ans;
}

// Driver code
int main()
{
    string str = "AAABBB";

    // Function call to print answer
    cout << countDeletions(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to count minimum deletions required
// so that there are no consecutive characters left
import java.util.*;

class GFG
{
  static int countDeletions(String s)
  {
    int ans = 0;
    char[] str = s.toCharArray();

    for (int i = 0; i < str.length - 1; i++)

        // If two consecutive characters are
        // the same, delete one of them.
        if (str[i] == str[i + 1])
            ans++;           

        return ans;
  }

    // Driver code
    public static void main(String[] args)
    {
      String str = "AAABBB";
      // Function call to print answer
     System.out.println(countDeletions(str));
    }
}
/* This code is contributed by Mr. Somesh Awasthi */
```

## 计算机编程语言

```
# Python code to count minimum deletions required
# so that there are no consecutive characters left\

def countDeletions(string):
    ans = 0
    for i in range(len(string) - 1):

        # If two consecutive characters are
        # the same, delete one of them.
        if (string[i] == string[i + 1]):
            ans += 1

    return ans

# Driver code
string = "AAABBB"

# Function call to print answer
print countDeletions(string)

# This code is contributed by Sachin Bisht
```

## C#

```
// C# Program to count minimum deletions
// required so that there are no
// consecutive characters left
using System;

class GFG
{

// Function for counting deletions   
static int countDeletions(String s)
{
    int ans = 0;
    char []str = s.ToCharArray();

    for (int i = 0; i < str.Length - 1; i++)

        // If two consecutive characters are
        // the same, delete one of them.
        if (str[i] == str[i + 1])
            ans++;        

        return ans;
}

    // Driver code
    public static void Main()
    {
        String str = "AAABBB";

        // Function call to print answer
        Console.Write(countDeletions(str));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to count minimum
// deletions required so that
// there are no consecutive
// characters left

function countDeletions($str)
{
    $ans = 0;
    for ($i = 0; $i < strlen($str) - 1; $i++)

        // If two consecutive characters are
        // the same, delete one of them.
        if ($str[$i] == $str[$i + 1])
            $ans++;

return $ans;
}

    // Driver Code
    $str = "AAABBB";

    // Function call to
    // print answer
    echo countDeletions($str);

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>
// javascript code to count minimum deletions required
// so that there are no consecutive characters left
    function countDeletions(s) {
        var ans = 0;
        var str = s;

        for (var i = 0; i < str.length - 1; i++)

            // If two consecutive characters are
            // the same, delete one of them.
            if (str[i] == str[i + 1])
                ans++;

        return ans;
    }

    // Driver code
        var str = "AAABBB";

        // Function call to print answer
        document.write(countDeletions(str));

// This code is contributed by gauravrajput1
</script>
```

输出:

```
4
```

本文由 **Rohit Thapliyal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。