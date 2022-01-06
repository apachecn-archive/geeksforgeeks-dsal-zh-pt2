# 德姆洛数(11…1 的平方)

> 原文:[https://www.geeksforgeeks.org/demlo-number-square-11-1/](https://www.geeksforgeeks.org/demlo-number-square-11-1/)

给定表格 11 的数量..1，这样其中的位数小于 10，求该数的平方。
**例:**

```
Input : 111111
Output : 12345654321

Input : 1111
Output : 1234321
```

11…1 的平方(长度小于 10)称为德姆洛数。德姆洛数是由 1，2，3…组成的数。n，n-1，n-2，…..1.
德姆洛编号为:

```
1 = 1
11 * 11 = 121
111 * 111 = 12321
1111 * 1111 = 1234321
```

要找到德姆洛数，首先我们要找到增加的 n 个数字，然后再找到减少的数字。

## C++

```
// CPP program to print DemloNumber
#include <bits/stdc++.h>
using namespace std;

// To return demlo number. This function assumes
// that the length of str is smaller than 10.
string printDemlo(string str)
{
    int len = str.length();
    string res = "";

    // Add numbers to res upto size
    // of str and then add number
    // reverse to it
    for (int i = 1; i <= len; i++)
        res += char(i + '0');

    for (int i = len - 1; i >= 1; i--)
        res += char(i + '0');

    return res;
}

// Driver program to test printDemlo()
int main()
{
    string str = "111111";
    cout << printDemlo(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print DemloNumber
public class Main {

    // To return demlo number. This function assumes
    // that the length of str is smaller than 10.
    static String printDemlo(String str)
    {
        int len = str.length();
        String res = "";

        // Add numbers to res upto size
        // of str and then add number
        // reverse to it
        for (int i = 1; i <= len; i++)
            res += Integer.toString(i);

        for (int i = len - 1; i >= 1; i--)
            res += Integer.toString(i);

        return res;
    }

    // Driver program to test printDemlo()
    public static void main(String[] args)
    {
        String str = "111111";
        System.out.println(printDemlo(str));
    }
}
```

## 计算机编程语言

```
# Python program to print Demlo Number

# To return demlo number
# Length of s is smaller than 10
def printDemlo(s):
    l = len(s)
    res = ""

    # Add numbers to res upto size
    # of s then add in reverse

    for i in range(1,l+1):
        res = res + str(i)

    for i in range(l-1,0,-1):
        res = res + str(i)

    return res

# Driver Code
s = "111111"   
print printDemlo(s)

# Contributed by Harshit Agrawal
```

## C#

```
// C# program to print DemloNumber
using System;
public class GFG {

    // To return demlo number. This function assumes
    // that the length of str is smaller than 10.
    static String printDemlo(String str)
    {
        int len = str.Length;
        String res = "";

        // Add numbers to res upto size
        // of str and then add number
        // reverse to it
        for (int i = 1; i <= len; i++)
            res += i.ToString();

        for (int i = len - 1; i >= 1; i--)
            res += i.ToString();

        return res;
    }

    // Driver program to test printDemlo()
    public static void Main()
    {
        String str = "111111";
        Console.WriteLine(printDemlo(str));
    }
}
// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print DemloNumber

// To return demlo number. This function
// assumes that the length of str is
// smaller than 10.
function printDemlo($str)
{
    $len = strlen($str);
    $res = "";

    // Add numbers to res upto size
    // of str and then add number
    // reverse to it
    for ($i = 1; $i <= $len; $i++)
        $res .= chr($i + 48);

    for ($i = $len - 1; $i >= 1; $i--)
        $res .= chr($i + 48);

    return $res;
}

// Driver Code
$str = "111111";
echo printDemlo($str);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to print DemloNumber

    // To return demlo number. This function assumes
    // that the length of str is smaller than 10.
    function printDemlo(str)
    {
        let len = str.length;
        let res = "";

        // Add numbers to res upto size
        // of str and then add number
        // reverse to it
        for (let i = 1; i <= len; i++)
            res += i.toString();

        for (let i = len - 1; i >= 1; i--)
            res += i.toString();

        return res;
    }

// driver program
        let str = "111111";
        document.write(printDemlo(str));

  // This code is contributed by susmitakundugoaldanga.
</script>
```

**输出:**

```
12345654321
```

本文由 [**核素**](https://www.facebook.com/nuclode) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。