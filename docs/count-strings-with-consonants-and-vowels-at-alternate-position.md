# 计算辅音和元音交替出现的字符串

> 原文:[https://www . geeksforgeeks . org/count-带辅音和元音的交替位置字符串/](https://www.geeksforgeeks.org/count-strings-with-consonants-and-vowels-at-alternate-position/)

给定一根弦**弦**。任务是找到通过替换“{content}”可以获得的所有可能的字符串数量。给定字符串中有字母。
**注**:字母的摆放方式应该是:字符串总是元音和辅音交替出现，字符串必须总是以辅音开头。假设这样的字符串总是可能的，即不需要关心除了“{content}”以外的字符。。
**示例** :

```
Input: str = "y$s"
Output: 5
$ can be replaced with any of the 5 vowels.
So, there can be 5 strings.

Input: str = "s$e{content}quot;
Output: 2205
```

**做法:**给出字符串将以辅音开头。所以，如果{ content }；在偶数位置(考虑基于 0 的索引)，那么应该有一个辅音，否则应该有一个元音。此外，假设除了“{content}”之外，没有必要关心其他字符。，即“{content}”以外的字符；被正确地放置在保持辅音和元音交替的字符串中。让我们用一个例子来理解这个问题。

> **str = " s $ e { content } # x201；**
> 这里我们要找到在给定约束条件下形成字符串的方法数量。
> 
> *   $第一次出现在第二个位置，即第一个索引，所以我们可以使用 5 个元音。
> *   $的第二次出现在第三个位置，所以我们可以使用 21 个辅音。
> *   第三次出现$是在第五个位置，所以我们可以用 21 个辅音。
> 
> 所以，形成以上字符串的方式总数为 **= 5*21*21 = 2205**

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>

using namespace std;

// Function to find the count of strings
int countStrings(string s)
{
    // Variable to store the final result
    long sum = 1;

    // Loop iterating through string
    for (int i = 0; i < s.size(); i++) {

        // If '{content}apos; is present at the even
        // position in the string
        if (i % 2 == 0 && s[i] == '{content}apos;)

            //'sum' is multiplied by 21
            sum *= 21;

        // If '{content}apos; is present at the odd
        // position in the string
        else if (s[i] == '{content}apos;)

            //'sum' is multiplied by 5
            sum *= 5;
    }

    return sum;
}

// Driver code
int main()
{
    // Let the string 'str' be s$e$
    string str = "s$e{content}quot;;

    // Print result
    cout << countStrings(str) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{

// Function to find the count of strings
static int countStrings(String s)
{
    // Variable to store the final result
    int sum = 1;

    // Loop iterating through string
    for (int i = 0; i < s.length(); i++) {

        // If '{content}apos; is present at the even
        // position in the string
        if (i % 2 == 0 && s.charAt(i) == '{content}apos;)

            //'sum' is multiplied by 21
            sum *= 21;

        // If '{content}apos; is present at the odd
        // position in the string
        else if (s.charAt(i) == '{content}apos;)

            //'sum' is multiplied by 5
            sum *= 5;
    }

    return sum;
}

// Driver code
public static void main(String args[])
{
    // Let the string 'str' be s$e$
    String str = "s$e{content}quot;;

    // Print result
    System.out.println(countStrings(str));
}
}
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# Function to find the count of strings
def countStrings(s):

    # Variable to store the final result
    sum = 1

    # Loop iterating through string
    for i in range(len(s)):

        # If '{content}apos; is present at the even
        # position in the string
        if (i % 2 == 0 and s[i] == '{content}apos;):

            #'sum' is multiplied by 21
            sum *= 21

        # If '{content}apos; is present at the odd
        # position in the string
        elif(s[i] == '{content}apos;):

            # 'sum' is multiplied by 5
            sum *= 5

    return sum

# Driver code
if __name__ == "__main__":

    # Let the string 'str' be s$e$
    str = "s$e{content}quot;

    # Print result
    print(countStrings(str))

# this code is contributed by ChitraNayal
```

## C#

```
// C# implementation of above approach

using System;

class GFG{

// Function to find the count of strings
static int countStrings(String s)
{
    // Variable to store the final result
    int sum = 1;

    // Loop iterating through string
    for (int i = 0; i < s.Length; i++) {

        // If '{content}apos; is present at the even
        // position in the string
        if (i % 2 == 0 && s[i] == '{content}apos;)

            //'sum' is multiplied by 21
            sum *= 21;

        // If '{content}apos; is present at the odd
        // position in the string
        else if (s[i] == '{content}apos;)

            //'sum' is multiplied by 5
            sum *= 5;
    }

    return sum;
}

// Driver code
public static void Main()
{
    // Let the string 'str' be s$e$
    String str = "s$e{content}quot;;

    // Print result
    Console.WriteLine(countStrings(str));
}
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to find the count of strings
function countStrings($s)
{
    // Variable to store the
    // final result
    $sum = 1;

    // Loop iterating through string
    for ($i = 0; $i < strlen($s); $i++)
    {

        // If '{content}apos; is present at the even
        // position in the string
        if ($i % 2 == 0 && $s[$i] == '{content}apos;)

            //'sum' is multiplied by 21
            $sum *= 21;

        // If '{content}apos; is present at the odd
        // position in the string
        else if ($s[$i] == '{content}apos;)

            //'sum' is multiplied by 5
            $sum *= 5;
    }

    return $sum;
}

// Driver code

// Let the string 'str' be s$e$
$str = "s\$\$e\{content}quot;;

// Print result
echo countStrings($str);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// javascript implementation of above approach

// Function to find the count of strings
function countStrings( s)
{

    // Variable to store the final result
    let sum = 1;

    // Loop iterating through string
    for (let i = 0; i < s.length; i++)
    {

        // If '{content}apos; is present at the even
        // position in the string
        if (i % 2 == 0 && s[i] == '{content}apos;)

            //'sum' is multiplied by 21
            sum *= 21;

        // If '{content}apos; is present at the odd
        // position in the string
        else if (s[i] == '{content}apos;)

            //'sum' is multiplied by 5
            sum *= 5;
    }
    return sum;
}

// Driver code

    // Let the string 'str' be s$e$
    let str = "s$e{content}quot;;

    // Print result
    document.write(countStrings(str));

// This code is contributed by gauravrajput1
</script>
```

**Output:** 

```
2205
```