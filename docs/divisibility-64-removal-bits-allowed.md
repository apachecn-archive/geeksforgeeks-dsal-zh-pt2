# 64 分频，允许移除位

> 原文:[https://www . geeksforgeeks . org/divisionity-64-remove-bits-allowed/](https://www.geeksforgeeks.org/divisibility-64-removal-bits-allowed/)

给定一个二进制字符串，我们需要在去掉一些位后检查这个数是否能被 64 整除。如果是，则打印“可能”，否则打印“不可能”。我们不能让数字 0 被整除。
**例:**

```
Input: 100010001 
Output: Possible
Explanation: We can get string 1 000 000 
after removing two ones which is a 
representation of number 64 in the binary 
numerical system.

Input: 100
Output: Not possible
Explanation : The number is 4 which is not 
divisible by 64 or cannot be made possible 
my removing some digits.
```

如果我们在任何一个之后有 6 个零，那么我们可以去掉其他的位，把它表示为 64 的倍数。所以我们只需要检查六个零之前是否有 1。

## C++

```
// CPP program to find if given binary string can
// become divisible by 64 after removing some bits.
#include <iostream>
using namespace std;

// function to check if it is possible
// to make it a multiple of 64.
bool checking(string s)
{
    int c = 0; // counter to count 0's
    int n = s.length(); // length of the string

    // loop which traverses right to left and
    // calculates the number of zeros before 1.
    for (int i = n - 1; i >= 0; i--) {
        if (s[i] == '0')
            c++;

        if (c >= 6 and s[i] == '1')
            return true;
    }

    return false;
}

// driver code
int main()
{
    string s = "100010001";
    if (checking(s))
        cout << "Possible";
    else
        cout << "Not possible";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if
// given binary string can
// become divisible by
// 64 after removing some bits
import java.io.*;

class GFG
{
    // function to check if it is possible
    // to make it a multiple of 64.
    static boolean checking(String s)
    {
        // counter to count 0's
        int c = 0;

        // length of the string
        int n = s.length();

        // loop which traverses right to left and
        // calculates the number of zeros before 1.
        for (int i = n - 1; i >= 0; i--)
        {
            if (s.charAt(i) == '0')
                c++;

            if (c >= 6 && s.charAt(i) == '1')
                return true;
        }

        return false;
    }

    // Driver code
    public static void main (String[] args)
    {
        String s = "100010001";
        if (checking(s))
            System.out.println ( "Possible");
        else
            System.out.println ( "Not possible");

    }
}

// This code  is contributed by vt_m
```

## 蟒蛇 3

```
# Python 3 program to find if given binary
# string can become divisible by 64 after
# removing some bits.

# function to check if it is possible
# to make it a multiple of 64.
def checking(s):
    c = 0

    # counter to count 0's
    n = len(s)

    # length of the string

    # loop which traverses right to left and
    # calculates the number of zeros before 1.
    i = n - 1
    while(i >= 0):
        if (s[i] == '0'):
            c += 1

        if (c >= 6 and s[i] == '1'):
            return True

        i -= 1

    return False

# Driver code
if __name__ == '__main__':
    s = "100010001"
    if (checking(s)):
        print("Possible")
    else:
        print("Not possible")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find if given binary
// string can become divisible by 64
// after removing some bits
using System;

class GFG {

    // function to check if it is possible
    // to make it a multiple of 64.
    static bool checking(string s)
    {

        // counter to count 0's
        int c = 0;

        // length of the string
        int n = s.Length;

        // loop which traverses right to
        // left and calculates the number
        // of zeros before 1.
        for (int i = n - 1; i >= 0; i--)
        {
            if (s[i] == '0')
                c++;

            if (c >= 6 && s[i] == '1')
                return true;
        }

        return false;
    }

    // Driver code
    public static void Main ()
    {
        String s = "100010001";

        if (checking(s))
            Console.WriteLine (
                          "Possible");
        else
            Console.WriteLine(
                     "Not possible");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if
// given binary string can
// become divisible by 64
// after removing some bits.

// function to check if
// it is possible
// to make it a multiple of 64.

function checking($s)
{
    // counter to count 0's
    $c = 0;

    // length of the string
    $n = strlen($s);

    // loop which traverses right
    // to left and calculates the
    // number of zeros before 1.
    for ($i = $n - 1; $i >= 0; $i--)
    {
        if ($s[$i] == '0')
            $c++;

        if ($c >= 6 and $s[$i] == '1')
            return true;
    }

    return false;
}

// Driver Code
$s = "100010001";
if (checking($s))
    echo "Possible";
else
    echo "Not possible";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to find if given binary
// string can become divisible by 64
// after removing some bits

    // function to check if it is possible
    // to make it a multiple of 64.
    function checking(s)
    {

        // counter to count 0's
        let c = 0;

        // length of the string
        let n = s.length;

        // loop which traverses right to
        // left and calculates the number
        // of zeros before 1.
        for (let i = n - 1; i >= 0; i--)
        {
            if (s[i] == '0')
                c++;

            if (c >= 6 && s[i] == '1')
                return true;
        }

        return false;
    }

// Driver code
        let s = "100010001";

        if (checking(s))
            document.write(
                          "Possible");
        else
            document.write(
                     "Not possible");

   // This code is contributed by code_hunt.
</script>
```

**输出:**

```
Possible
```

**时间复杂度:** O(字符串长度)

本文由 [**钿巴贾杰**](https://auth.geeksforgeeks.org/profile.php?user=Twinkl Bajaj) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。