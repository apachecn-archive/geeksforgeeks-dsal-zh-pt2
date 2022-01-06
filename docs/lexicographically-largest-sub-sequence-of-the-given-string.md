# 给定字符串的字典上最大的子序列

> 原文:[https://www . geesforgeks . org/按字典顺序排列的给定字符串的最大子序列/](https://www.geeksforgeeks.org/lexicographically-largest-sub-sequence-of-the-given-string/)

给定一个包含小写字符的字符串 **str** ，任务是找到 **str** 的字典序最大的子序列。
**例:**

> **输入:** str = "abc"
> **输出:** c
> 所有可能的子序列都是“a”、“ab”、“ac”、“b”、“bc”和“c”
> 其中“c”是最大的(按字典顺序)
> **输入:**str = " geeksforgeeks "
> **输出:** ss

**方法:**让 **mx** 成为字符串中按字典顺序最大的字符。因为我们想要字典上最大的子序列，所以我们应该包括所有出现的 **mx** 。现在，在所有事件都被使用之后，可以对剩余的字符串(即在最后一次出现 **mx** 之后的子字符串)重复相同的过程，以此类推，直到没有剩余的字符。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the lexicographically
// largest sub-sequence of s
string getSubSeq(string s, int n)
{
    string res = "";
    int cr = 0;
    while (cr < n) {

        // Get the max character from the string
        char mx = s[cr];
        for (int i = cr + 1; i < n; i++)
            mx = max(mx, s[i]);
        int lst = cr;

        // Use all the occurrences of the
        // current maximum character
        for (int i = cr; i < n; i++)
            if (s[i] == mx) {
                res += s[i];
                lst = i;
            }

        // Repeat the steps for the remaining string
        cr = lst + 1;
    }
    return res;
}

// Driver code
int main()
{
    string s = "geeksforgeeks";
    int n = s.length();
    cout << getSubSeq(s, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the lexicographically
    // largest sub-sequence of s
    static String getSubSeq(String s, int n)
    {
        String res = "";
        int cr = 0;
        while (cr < n)
        {

            // Get the max character from the String
            char mx = s.charAt(cr);
            for (int i = cr + 1; i < n; i++)
            {
                mx = (char) Math.max(mx, s.charAt(i));
            }
            int lst = cr;

            // Use all the occurrences of the
            // current maximum character
            for (int i = cr; i < n; i++)
            {
                if (s.charAt(i) == mx)
                {
                    res += s.charAt(i);
                    lst = i;
                }
            }

            // Repeat the steps for
            // the remaining String
            cr = lst + 1;
        }
        return res;
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "geeksforgeeks";
        int n = s.length();
        System.out.println(getSubSeq(s, n));
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the lexicographically
# largest sub-sequence of s
def getSubSeq(s, n):
    res = ""
    cr = 0
    while (cr < n):

        # Get the max character from
        # the string
        mx = s[cr]
        for i in range(cr + 1, n):
            mx = max(mx, s[i])
        lst = cr

        # Use all the occurrences of the
        # current maximum character
        for i in range(cr,n):
            if (s[i] == mx):
                res += s[i]
                lst = i

        # Repeat the steps for the
        # remaining string
        cr = lst + 1

    return res

# Driver code
if __name__ == '__main__':
    s = "geeksforgeeks"
    n = len(s)
    print(getSubSeq(s, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the lexicographically
    // largest sub-sequence of s
    static String getSubSeq(String s, int n)
    {
        String res = "";
        int cr = 0;
        while (cr < n)
        {

            // Get the max character from
            // the String
            char mx = s[cr];
            for (int i = cr + 1; i < n; i++)
            {
                mx = (char) Math.Max(mx, s[i]);
            }
            int lst = cr;

            // Use all the occurrences of the
            // current maximum character
            for (int i = cr; i < n; i++)
            {
                if (s[i] == mx)
                {
                    res += s[i];
                    lst = i;
                }
            }

            // Repeat the steps for
            // the remaining String
            cr = lst + 1;
        }
        return res;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String s = "geeksforgeeks";
        int n = s.Length;
        Console.WriteLine(getSubSeq(s, n));
    }
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the lexicographically
// largest sub-sequence of s
function getSubSeq($s, $n)
{
    $res = "";
    $cr = 0;
    while ($cr < $n)
    {

        // Get the max character from the string
        $mx = $s[$cr];
        for ($i = $cr + 1; $i < $n; $i++)
            $mx = max($mx, $s[$i]);
        $lst = $cr;

        // Use all the occurrences of the
        // current maximum character
        for ($i = $cr; $i < $n; $i++)
            if ($s[$i] == $mx)
            {
                $res .= $s[$i];
                $lst = $i;
            }

        // Repeat the steps for the
        // remaining string
        $cr = $lst + 1;
    }
    return $res;
}

// Driver code
$s = "geeksforgeeks";
$n = strlen($s);
echo getSubSeq($s, $n);

// This code is contributed by
// Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the lexicographically
// largest sub-sequence of s
function getSubSeq(s, n)
{
    var res = "";
    var cr = 0;
    while (cr < n) {

        // Get the max character from the string
        var mx = s[cr].charCodeAt(0);
        for (var i = cr + 1; i < n; i++)
            mx = Math.max(mx, s[i].charCodeAt(0));
        var lst = cr;

        // Use all the occurrences of the
        // current maximum character
        for (var i = cr; i < n; i++)
            if (s[i].charCodeAt(0) == mx) {
                res += s[i];
                lst = i;
            }

        // Repeat the steps for the remaining string
        cr = lst + 1;
    }
    return res;
}

// Driver code
var s = "geeksforgeeks";
var n = s.length;
document.write( getSubSeq(s, n));

// This code is contributed by famously.
</script>
```

**Output:** 

```
ss
```

**时间复杂度:** O(N)，其中 N 是字符串的长度。
**辅助空间:** O(N)