# 连续字符的最小翻转，使字符串中的所有字符相同

> 原文:[https://www . geeksforgeeks . org/min-将连续字符翻转为字符串中的所有字符/](https://www.geeksforgeeks.org/min-flips-of-continuous-characters-to-make-all-characters-same-in-a-string/)

给定一个仅由 1 和 0 组成的字符串。在一次翻转中，我们可以改变该字符串的任何连续序列。找到这个最小翻转次数，这样字符串只包含相同的字符。
**例:**

```
Input : 00011110001110
Output : 2
We need to convert 1's sequence
so string consist of all 0's.

Input : 010101100011
Output : 4
```

我们需要找到字符串中的最小翻转，这样所有字符都是相等的。我们所要做的就是找出仅由 0 或 1 组成的数列。那么所需的翻转次数将是这个数字的一半，因为我们可以改变所有 0 或所有 1。

## C++

```
// CPP program to find min flips in binary
// string to make all characters equal
#include <bits/stdc++.h>
using namespace std;

// To find min number of flips in binary string
int findFlips(char str[], int n)
{
    char last = ' '; int res = 0;

    for (int i = 0; i < n; i++) {

        // If last character is not equal
        // to str[i] increase res
        if (last != str[i])
            res++;
        last = str[i];
    }

    // To return min flips
    return res / 2;
}

// Driver program to check findFlips()
int main()
{
    char str[] = "00011110001110";
    int n = strlen(str);

    cout << findFlips(str, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find min flips in binary
// string to make all characters equal
public class minFlips {

    // To find min number of flips in binary string
    static int findFlips(String str, int n)
    {
        char last = ' '; int res = 0;

        for (int i = 0; i < n; i++) {

            // If last character is not equal
            // to str[i] increase res
            if (last != str.charAt(i))
                res++;
            last = str.charAt(i);
        }

        // To return min flips
        return res / 2;
    }

    // Driver program to check findFlips()
    public static void main(String[] args)
    {
        String str = "00011110001110";
        int n = str.length();

        System.out.println(findFlips(str, n));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find min flips in
# binary string to make all characters equal

# To find min number of flips in
# binary string
def findFlips(str, n):

    last = ' '
    res = 0

    for i in range( n) :

        # If last character is not equal
        # to str[i] increase res
        if (last != str[i]):
            res += 1
        last = str[i]

    # To return min flips
    return res // 2

# Driver Code
if __name__ == "__main__":

    str = "00011110001110"
    n = len(str)

    print(findFlips(str, n))

# This code is contributed by ita_c
```

## C#

```
// C# program to find min flips in
// binary string to make all
// characters equal
using System;

public class GFG {

    // To find min number of flips
    // in binary string
    static int findFlips(String str, int n)
    {
        char last = ' '; int res = 0;

        for (int i = 0; i < n; i++) {

            // If last character is not
            // equal to str[i] increase
            // res
            if (last != str[i])
                res++;
            last = str[i];
        }

        // To return min flips
        return res / 2;
    }

    // Driver program to check findFlips()
    public static void Main()
    {
        String str = "00011110001110";
        int n = str.Length;

        Console.Write(findFlips(str, n));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find min flips in binary
// string to make all characters equal

// To find min number of
// flips in binary string
function findFlips($str, $n)
{
    $last = ' ';
    $res = 0;

    for ($i = 0; $i < $n; $i++)
    {

        // If last character is not equal
        // to str[i] increase res
        if ($last != $str[$i])
            $res++;
        $last = $str[$i];
    }

    // To return min flips
    return intval($res / 2);
}

    // Driver Code
    $str = "00011110001110";
    $n = strlen($str);

    echo findFlips($str, $n);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// JavaScript program to find min flips in binary
// string to make all characters equal

    // To find min number of flips in binary string
    function findFlips( str , n) {
        var last = ' ';
        var res = 0;

        for (i = 0; i < n; i++) {

            // If last character is not equal
            // to str[i] increase res
            if (last != str.charAt(i))
                res++;
            last = str.charAt(i);
        }

        // To return min flips
        return parseInt(res / 2);
    }

    // Driver program to check findFlips()

        var str = "00011110001110";
        var n = str.length;

        document.write(findFlips(str, n));

// This code contributed by aashish1995

</script>
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)

**输出:**

```
2
```

本文由 [**核素**](https://www.facebook.com/nuclode) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。