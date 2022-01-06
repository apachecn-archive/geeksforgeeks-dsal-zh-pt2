# 字符串中最大连续重复字符数

> 原文:[https://www . geesforgeks . org/最大连续重复字符串/](https://www.geeksforgeeks.org/maximum-consecutive-repeating-character-string/)

给定一个字符串，任务是找到一个字符串中最大的连续重复字符。
**注:**我们不需要考虑整体的计数，而是重复出现在一个地方的计数。
**示例:**

```
Input : str = "geeekk"
Output : e

Input : str = "aaaabbcbbb"
Output : a
```

这个问题的**简单解决方案**是使用两个 for 循环。外部循环考虑当前字符，内部循环计算当前字符的出现次数。如果计数超过当前最大计数，我们将更新结果。

## C++

```
// C++ program to find the maximum consecutive
// repeating character in given string
#include<bits/stdc++.h>
using namespace std;

// function to find out the maximum repeating
// character in given string
char maxRepeating(string str)
{
    int len = str.length();
    int count = 0;

    // Find the maximum repeating character
    // starting from str[i]
    char res = str[0];
    for (int i=0; i<len; i++)
    {
        int cur_count = 1;
        for (int j=i+1; j<len; j++)
        {
            if (str[i] != str[j])
                break;
            cur_count++;
        }

        // Update result if required
        if (cur_count > count)
        {
            count = cur_count;
            res = str[i];
        }
    }
    return res;
}

// Driver code
int main()
{

    string str = "aaaabbaaccde";
    cout << maxRepeating(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum consecutive
// repeating character in given string
public class GFG {

    // function to find out the maximum repeating
    // character in given string
    static char maxRepeating(String str)
    {
        int len = str.length();
        int count = 0;

        // Find the maximum repeating character
        // starting from str[i]
        char res = str.charAt(0);
        for (int i=0; i<len; i++)
        {
            int cur_count = 1;
            for (int j=i+1; j<len; j++)
            {
                if (str.charAt(i) != str.charAt(j))
                    break;
                cur_count++;
            }

            // Update result if required
            if (cur_count > count)
            {
                count = cur_count;
                res = str.charAt(i);
            }
        }
        return res;
    }

    // Driver code
    public static void main(String args[])
    {

        String str = "aaaabbaaccde";
        System.out.println(maxRepeating(str));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python 3 program to find the
# maximum consecutive repeating
# character in given string

# function to find out the maximum
# repeating character in given string
def maxRepeating(str):

    l = len(str)
    count = 0

    # Find the maximum repeating
    # character starting from str[i]
    res = str[0]
    for i in range(l):

        cur_count = 1
        for j in range(i + 1, l):

            if (str[i] != str[j]):
                break
            cur_count += 1

        # Update result if required
        if cur_count > count :
            count = cur_count
            res = str[i]
    return res

# Driver code
if __name__ == "__main__":

    str = "aaaabbaaccde"
    print(maxRepeating(str))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find the maximum
// consecutive repeating character
// in given string
using System;

class GFG
{

// function to find out the maximum
// repeating character in given string
static char maxRepeating(string str)
{
    int len = str.Length;
    int count = 0;
    char res = str[0];

    // Find the maximum repeating
    // character starting from str[i]
    for (int i = 0; i < len; i++)
    {
        int cur_count = 1;
        for (int j = i + 1; j < len; j++)
        {
            if (str[i] != str[j])
                break;
            cur_count++;
        }

        // Update result if required
        if (cur_count > count)
        {
            count = cur_count;
            res = str[i];
        }
    }
    return res;
}

// Driver code
public static void Main()
{
    string str = "aaaabbaaccde";
    Console.Write(maxRepeating(str));
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP program to find the maximum consecutive
// repeating character in given string

// function to find out the maximum repeating
// character in given string
function  maxRepeating( $str)
{
     $len = strlen($str);
    $count = 0;

    // Find the maximum repeating character
    // starting from str[i]
     $res = $str[0];
    for ($i = 0; $i < $len; $i++)
    {
         $cur_count = 1;
        for ($j = $i+1; $j < $len; $j++)
        {
            if ($str[$i] != $str[$j])
                break;
            $cur_count++;
        }

        // Update result if required
        if ($cur_count > $count)
        {
            $count = $cur_count;
            $res = $str[$i];
        }
    }
    return $res;
}

// Driver code
    $str = "aaaabbaaccde";
    echo  maxRepeating($str);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to find the maximum consecutive
// repeating character in given string

    // function to find out the maximum repeating
    // character in given string
    function maxRepeating(str)
    {
        let len = str.length;
        let count = 0;

        // Find the maximum repeating character
        // starting from str[i]
        let res = str[0];
        for (let i=0; i<len; i++)
        {
            let cur_count = 1;
            for (let j=i+1; j<len; j++)
            {
                if (str[i] != str[j])
                    break;
                cur_count++;
            }

            // Update result if required
            if (cur_count > count)
            {
                count = cur_count;
                res = str[i];
            }
        }
        return res;
    }

    // Driver code
    let str = "aaaabbaaccde";
    document.write(maxRepeating(str));

    // This code is contributed by rag2127

</script>
```

**输出:**

```
a
```

**时间复杂度:**o(n^2)
T3】空间复杂度: O(1)
一个**高效的解决方案**是只运行一个循环。这个想法是，一旦我们发现一个字符与前一个不匹配，就将计数重置为 1。

## C++

```
// C++ program to find the maximum consecutive
// repeating character in given string
#include<bits/stdc++.h>
using namespace std;

// Returns the maximum repeating character in a
// given string
char maxRepeating(string str)
{
    int n = str.length();
    int count = 0;
    char res = str[0];
    int cur_count = 1;

    // Traverse string except last character
    for (int i=0; i<n; i++)
    {
        // If current character matches with next
        if (i < n-1 && str[i] == str[i+1])
            cur_count++;

        // If doesn't match, update result
        // (if required) and reset count
        else
        {
            if (cur_count > count)
            {
                count = cur_count;
                res = str[i];
            }
            cur_count = 1;
        }
    }

    return res;
}

// Driver code
int main()
{
    string str = "aaaabbaaccde";
    cout << maxRepeating(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum consecutive
// repeating character in given string
class GFG {

    // function to find out the maximum repeating
    // character in given string
    static char maxRepeating(String str)
    {
        int n = str.length();
        int count = 0;
        char res = str.charAt(0);
        int cur_count = 1;

        // Traverse string except last character
        for (int i = 0; i < n; i++)
        {
            // If current character matches with next
            if (i < n - 1 && str.charAt(i) == str.charAt(i + 1))
                cur_count++;

            // If doesn't match, update result
            // (if required) and reset count
            else
            {
                if (cur_count > count)
                {
                    count = cur_count;
                    res = str.charAt(i);
                }
                cur_count = 1;
            }
        }
        return res;
    }

    // Driver code
    public static void main(String args[])
    {
        String str = "aaaabbaaccde";
        System.out.println(maxRepeating(str));
    }
}

// This code is contributed by Sudeep Mukherjee
```

## 蟒蛇 3

```
# Python 3 program to find the
# maximum consecutive repeating
# character in given string

# Returns the maximum repeating
# character in a given string
def maxRepeating(str):

    n = len(str)
    count = 0
    res = str[0]
    cur_count = 1

    # Traverse string except
    # last character
    for i in range(n):

        # If current character
        # matches with next
        if (i < n - 1 and
            str[i] == str[i + 1]):
            cur_count += 1

        # If doesn't match, update result
        # (if required) and reset count
        else:
            if cur_count > count:
                count = cur_count
                res = str[i]
            cur_count = 1
    return res

# Driver code
if __name__ == "__main__":
    str = "aaaabbaaccde"
    print(maxRepeating(str))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find the maximum
// consecutive repeating character
// in given string
using System;

class GFG
{

// function to find out the
// maximum repeating character
// in given string
static char maxRepeating(string str)
{
    int n = str.Length;
    int count = 0;
    char res = str[0];
    int cur_count = 1;

    // Traverse string except
    // last character
    for (int i = 0; i < n; i++)
    {
        // If current character
        // matches with next
        if (i < n - 1 &&
            str[i] == str[i + 1])
            cur_count++;

        // If doesn't match, update result
        // (if required) and reset count
        else
        {
            if (cur_count > count)
            {
                count = cur_count;
                res = str[i];
            }
            cur_count = 1;
        }
    }
    return res;
}

// Driver code
public static void Main()
{
    string str = "aaaabbaaccde";
    Console.Write(maxRepeating(str));
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the maximum
// consecutive repeating character
// in given string

// Returns the maximum repeating
// character in a given string
function maxRepeating($str)
{
    $n = strlen($str);
    $count = 0;
    $res = $str[0];
    $cur_count = 1;

    // Traverse string except
    // last character
    for ($i = 0; $i < $n; $i++)
    {
        // If current character
        // matches with next
        if ($i < $n - 1 &&
            $str[$i] == $str[$i + 1])
            $cur_count++;

        // If doesn't match, update result
        // (if required) and reset count
        else
        {
            if ($cur_count > $count)
            {
                $count = $cur_count;
                $res = $str[$i];
            }
            $cur_count = 1;
        }
    }

    return $res;
}

// Driver code
$str = "aaaabbaaccde";
echo maxRepeating($str);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// JavaScript program to find the maximum consecutive
// repeating character in given string

  // function to find out the maximum repeating
  // character in given string
function maxRepeating( str)
{
    var n = str.length;
    var count = 0;
    var res = str[0];
    var cur_count = 1;

    // Traverse string except last character
    for (var i=0; i<n; i++)
    {
        // If current character matches with next
        if (i < n-1 && str[i] == str[i+1])
            cur_count++;

        // If doesn't match, update result
        // (if required) and reset count
        else
        {
            if (cur_count > count)
            {
                count = cur_count;
                res = str[i];
            }
            cur_count = 1;
        }
    }

    return res;
}

var str = "aaaabbaaccde";
    document.write( maxRepeating(str));

</script>
```

**输出:**

```
a
```

**时间复杂度:**O(n)
T3】空间复杂度: O(1)
本文由 [**丹麦语 _RAZA**](https://www.facebook.com/danish.raza.98096721) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。