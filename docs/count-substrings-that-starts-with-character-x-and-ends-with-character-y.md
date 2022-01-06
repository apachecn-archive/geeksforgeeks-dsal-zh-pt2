# 统计以字符 X 开始，以字符 Y 结束的子字符串

> 原文:[https://www . geesforgeks . org/count-substrings-以字符-x 开头，以字符-y 结尾/](https://www.geeksforgeeks.org/count-substrings-that-starts-with-character-x-and-ends-with-character-y/)

给定一个由 **n** 个小写字符组成的字符串 **str** ，任务是统计 **str** 从字符 X 开始到字符 y 结束的子字符串数量。
**示例:**

```
Input: str = "abbcaceghcak"
        x = 'a', y = 'c'
Output: 5
abbc, abbcac, ac, abbcaceghc, aceghc

Input: str = "geeksforgeeks"
        x = 'g', y = 'e'
Output: 6
```

**进场:**

*   初始化两个计数器，即 tot_count 以计数子字符串的总数，count_x 以计数以 x 开头的字符串数。
*   开始解开绳子。
*   如果当前字符是 X，则增加 count_x 的计数。
*   如果当前字符是 Y，这意味着一个字符串以 Y 结尾，因此增加 tot_count 的计数，即

```
tot_count = tot_count + count_x
```

*   这意味着，如果存在一个 Y，那么它将生成一个子串，其中所有的 X 出现在字符串中的 Y 之前。所以，把 X 的计数加到总计数上。
*   返回总计数。

以下是上述方法的实现:

## C++

```
// C++ implementation to count substrings
// starting with character X and ending
// with character Y
#include <bits/stdc++.h>
using namespace std;

// function to count substrings starting with
// character X and ending with character Y
int countSubstr(string str, int n,
                char x, char y)
{
    // to store total count of
    // required substrings
    int tot_count = 0;

    // to store count of character 'x'
    // up to the point the string 'str'
    // has been traversed so far
    int count_x = 0;

    // traverse 'str' form left to right
    for (int i = 0; i < n; i++) {

        // if true, increment 'count_x'
        if (str[i] == x)
            count_x++;

        // if true accumulate 'count_x'
        // to 'tot_count'
        if (str[i] == y)
            tot_count += count_x;
    }

    // required count
    return tot_count;
}

// Driver code
int main()
{
    string str = "abbcaceghcak";
    int n = str.size();
    char x = 'a', y = 'c';

    cout << "Count = "
         << countSubstr(str, n, x, y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count
// substrings starting with
// character X and ending
// with character Y
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{
// function to count substrings
// starting with character X and
// ending with character Y
static int countSubstr(String str, int n,
                       char x, char y)
{
    // to store total count of
    // required substrings
    int tot_count = 0;

    // to store count of character
    // 'x' up to the point the
    // string 'str' has been
    // traversed so far
    int count_x = 0;

    // traverse 'str' form
    // left to right
    for (int i = 0; i < n; i++)
    {

        // if true, increment 'count_x'
        if (str.charAt(i) == x)
            count_x++;

        // if true accumulate 'count_x'
        // to 'tot_count'
        if (str.charAt(i) == y)
            tot_count += count_x;
    }

    // required count
    return tot_count;
}

// Driver code
public static void main(String args[])
{
    String str = "abbcaceghcak";
    int n = str.length();
    char x = 'a', y = 'c';

    System.out.print ("Count = " +
       countSubstr(str, n, x, y));
}
}

// This code is contributed
// by Subhadeep
```

## 蟒蛇 3

```
# Python 3 implementation to count substrings
# starting with character X and ending
# with character Y

# function to count substrings starting with
# character X and ending with character Y
def countSubstr(str, n, x, y):

    # to store total count of
    # required substrings
    tot_count = 0

    # to store count of character 'x'
    # up to the point the string 'str'
    # has been traversed so far
    count_x = 0

    # traverse 'str' form left to right
    for i in range(n):

        # if true, increment 'count_x'
        if str[i] == x:
            count_x += 1

        # if true accumulate 'count_x'
        # to 'tot_count'
        if str[i] == y:
            tot_count += count_x

    # required count
    return tot_count

# Driver Code
str = 'abbcaceghcak'
n = len(str)
x, y = 'a', 'c'
print('Count =', countSubstr(str, n, x, y))

# This code is contributed SamyuktaSHegde
```

## C#

```
// C# implementation to count substrings
// starting with character X and ending
// with character Y
using System;

class GFG
{
// function to count substrings starting
// with character X and ending with character Y
static int countSubstr(string str, int n,
                       char x, char y)
{
    // to store total count of
    // required substrings
    int tot_count = 0;

    // to store count of character 'x' up
    // to the point the string 'str' has
    // been traversed so far
    int count_x = 0;

    // traverse 'str' form left to right
    for (int i = 0; i < n; i++)
    {

        // if true, increment 'count_x'
        if (str[i] == x)
            count_x++;

        // if true accumulate 'count_x'
        // to 'tot_count'
        if (str[i] == y)
            tot_count += count_x;
    }

    // required count
    return tot_count;
}

// Driver code
public static void Main()
{
    string str = "abbcaceghcak";
    int n = str.Length;
    char x = 'a', y = 'c';

    Console.Write("Count = " +
    countSubstr(str, n, x, y));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to count substrings
// starting with character X and ending
// with character Y

// function to count substrings starting with
// character X and ending with character Y
function countSubstr($str, $n, $x, $y)
{
    // to store total count of
    // required substrings
    $tot_count = 0;

    // to store count of character 'x'
    // up to the point the string 'str'
    // has been traversed so far
    $count_x = 0;

    // traverse 'str' form left to right
    for ($i = 0; $i < $n; $i++)
    {

        // if true, increment 'count_x'
        if ($str[$i] == $x)
            $count_x++;

        // if true accumulate 'count_x'
        // to 'tot_count'
        if ($str[$i] == $y)
            $tot_count += $count_x;
    }

    // required count
    return $tot_count;
}

// Driver code
$str = "abbcaceghcak";
$n = strlen($str);
$x = 'a'; $y = 'c';

echo "Count = ". countSubstr($str, $n, $x, $y);

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>
      // JavaScript implementation to count substrings
      // starting with character X and ending
      // with character Y

      // function to count substrings starting with
      // character X and ending with character Y
      function countSubstr(str, n, x, y) {
        // to store total count of
        // required substrings
        var tot_count = 0;

        // to store count of character 'x'
        // up to the point the string 'str'
        // has been traversed so far
        var count_x = 0;

        // traverse 'str' form left to right
        for (var i = 0; i < n; i++) {
          // if true, increment 'count_x'
          if (str[i] === x) count_x++;

          // if true accumulate 'count_x'
          // to 'tot_count'
          if (str[i] === y) tot_count += count_x;
        }

        // required count
        return tot_count;
      }

      // Driver code

      var str = "abbcaceghcak";
      var n = str.length;
      var x = "a",
        y = "c";

      document.write("Count = " + countSubstr(str, n, x, y));
    </script>
```

**Output:** 

```
Count = 5
```