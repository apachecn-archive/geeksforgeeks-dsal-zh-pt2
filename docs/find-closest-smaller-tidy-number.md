# 找到最近且较小的整齐号

> 原文:[https://www . geesforgeks . org/find-最近-较小-整齐-数字/](https://www.geeksforgeeks.org/find-closest-smaller-tidy-number/)

[**【整齐号】**](https://www.geeksforgeeks.org/tidy-number-digits-non-decreasing-order/) 是那些数字按非递减顺序排列的数字。在这里，给我们一个数字，我们必须找到另一个更小但最接近给定数字的数字，并且这个数字应该是整齐的，即它们的数字应该是不递减的。

**示例:**

```
Input  : 91234
Output : 89999
Tidy property is violated by appearing 1 after 9\. 
So, we will reduce 9 by 1 and the number right
to it will be replaced by 9\. So, generated tidy
number is 89999.

Input  : 45000
Output : 44999
```

这个想法是从头到尾。每当违反整齐属性时，我们将数字减 1，并使所有后续数字都为 9。

## C++

```
// C++ program to find closest
// tidy number smaller than the
// given number
#include<bits/stdc++.h>
using namespace std;

char* tidyNum(char str[], int len)
{
    for (int i = len-2; i >= 0; i--)
    {
        // check whether string violates tidy property
        if (str[i] > str[i+1])
        {
            // if string violates tidy property, then
            // decrease the value stored at that index by 1
            // and replace all the value stored right to
            // that index by 9
            (char)str[i]--;
            for (int j=i+1; j<len; j++)
                str[j] = '9';
        }
    }
    return str;
}

// Driver code
int main()
{
    char str[] = "11333445538";
    int len = strlen(str);

    // num will store closest tidy number
    char *num = tidyNum(str, len);
    printf("%s\n", num);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find closest
// tidy number smaller than the
// given number
import java.io.*;
class GFG
{
static String tidyNum(String str1,
                      int len)
{
    char[] str = str1.toCharArray();
    for (int i = len - 2; i >= 0; i--)
    {
        // check whether string
        // violates tidy property
        if (str[i] > str[i + 1])
        {
            // if string violates tidy
            // property, then decrease the
            // value stored at that index
            // by 1 and replace all the value
            // stored right to that index by 9
            str[i]--;
            for (int j = i + 1; j < len; j++)
                str[j] = '9';
        }
    }
    return String.valueOf(str);
}

// Driver code
public static void main(String[] args)
{
    String str = "11333445538";
    int len = str.length();

    // num will store closest tidy number
    System.out.println(tidyNum(str, len));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python 3 program to find closest
# tidy number smaller than the
# given number

def tidyNum(str, len):

    for i in range(len-2, -1, -1):

        # check whether string
        # violates tidy property
        if (str[i] > str[i+1]):

            # if string violates tidy
            # property, then decrease the
            # value stored at that index by 1
            # and replace all the value
            # stored right to that index by 9
            str[i] -= 1
            for j in range(i+1, len):
                str[j] = 9

    return str

# Driver code
str = [1,1,3,3,3,4,4,5,5,3,8]
len = len(str)

# num will store closest tidy number
num = tidyNum(str, len)

for i in range(0,len):
    print(str[i], end = "")

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program to find closest
// tidy number smaller than the
// given number
using System;

class GFG
{
static String tidyNum(String str1, int len)
{
    char[] str = str1.ToCharArray();
    for (int i = len - 2; i >= 0; i--)
    {
        // check whether string
        // violates tidy property
        if (str[i] > str[i + 1])
        {
            // if string violates tidy
            // property, then decrease the
            // value stored at that index
            // by 1 and replace all the value
            // stored right to that index by 9
            str[i]--;
            for (int j = i + 1; j < len; j++)
                str[j] = '9';
        }
    }
    string s = new string(str);
    return s;
}

// Driver code
static void Main()
{
    String str = "11333445538";
    int len = str.Length;

    // num will store closest tidy number
    Console.WriteLine(tidyNum(str, len));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find closest
// tidy number smaller than the
// given number

function tidyNum($str, $len)
{
    for ($i = $len - 2; $i >= 0; $i--)
    {
        // check whether string
        // violates tidy property
        if ($str[$i] > $str[$i + 1])
        {
            // if string violates tidy
            // property, then decrease
            // the value stored at that
            // index by 1 and replace all
            // the value stored right to
            // that index by 9
            $x = ord($str[$i]);
            $x--;
            $str[$i] = chr($x);
            for ($j = $i + 1; $j < $len; $j++)
                $str[$j] = '9';
        }
    }
    return $str;
}

// Driver code
$str = "11333445538";
$len = strlen($str);

// num will store
// closest tidy number
$num = tidyNum($str, $len);
echo $num;

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find closest
// tidy number smaller than the
// given number
function tidyNum(str1, len)
{
    var str = str1.split('');
    for (i = len - 2; i >= 0; i--)
    {

        // Check whether string
        // violates tidy property
        if (str[i] > str[i + 1])
        {

            // If string violates tidy
            // property, then decrease the
            // value stored at that index
            // by 1 and replace all the value
            // stored right to that index by 9
            str[i]--;

            for(j = i + 1; j < len; j++)
                str[j] = '9';
        }
    }
    return str.join("");
}

// Driver code
var str = "11333445538";
var len = str.length;

// num will store closest tidy number
document.write(tidyNum(str, len));

// This code is contributed by Amit Katiyar

</script>
```

**输出:**

```
11333444999
```

**参考文献:**
这个问题是在 [Google Code Jam](https://code.google.com/codejam/contest/3264486/dashboard#s=p1) 2017 资格赛轮问的。

本文由 [**阿迪蒂亚·库马尔**](https://www.linkedin.com/in/aditya-kumar-837315100/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。