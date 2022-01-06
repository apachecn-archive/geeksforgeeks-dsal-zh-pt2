# 在不使用任何额外数据结构的情况下，有效检查字符串是否具有所有唯一字符

> 原文:[https://www . geesforgeks . org/effective-check-string-replications-无需使用附加数据结构/](https://www.geeksforgeeks.org/efficiently-check-string-duplicates-without-using-additional-data-structure/)

实现一个节省空间的算法来确定一个字符串(从' a '到' z '的字符)是否具有所有唯一的字符。不允许使用额外的数据结构，如计数数组、散列等。
预计时间复杂度:O(n)
**示例:**

```
Input  : str = "aaabbccdaa"
Output : No

Input  : str = "abcd"
Output : Yes
```

其思想是使用一个整数变量，并在其二进制表示中使用位来存储字符是否存在。通常一个整数至少有 32 位，我们只需要存储 26 个字符的有无。
下面是想法的实现。

## C++

```
// A space efficient C++ program to check if
// all characters of string are unique.
#include<bits/stdc++.h>
using namespace std;

// Returns true if all characters of str are
// unique.
// Assumptions : (1) str contains only characters
//                   from 'a' to 'z'
//               (2) integers are stored using 32
//                   bits
bool areChractersUnique(string str)
{
    // An integer to store presence/absence
    // of 26 characters using its 32 bits.
    int checker = 0;

    for (int i = 0; i < str.length(); ++i)
    {
        int val = (str[i]-'a');

        // If bit corresponding to current
        // character is already set
        if ((checker & (1 << val)) > 0)
            return false;

        // set bit in checker
        checker |=  (1 << val);
    }

    return true;
}

// Driver code
int main()
{
    string s = "aaabbccdaa";
    if (areChractersUnique(s))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A space efficient Java program to check if
// all characters of string are unique.
class GFG {

    // Returns true if all characters of str are
    // unique.
    // Assumptions : (1) str contains only characters
    //                 from 'a' to 'z'
    //             (2) integers are stored using 32
    //                 bits
    static boolean areChractersUnique(String str)
    {

        // An integer to store presence/absence
        // of 26 characters using its 32 bits.
        int checker = 0;

        for (int i = 0; i < str.length(); ++i)
        {
            int val = (str.charAt(i)-'a');

            // If bit corresponding to current
            // character is already set
            if ((checker & (1 << val)) > 0)
                return false;

            // set bit in checker
            checker |= (1 << val);
        }

        return true;
    }

    //driver code
    public static void main (String[] args)
    {
        String s = "aaabbccdaa";

        if (areChractersUnique(s))
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# A space efficient c++ program to check if
# all characters of string are unique

# Returns true if all characters of str are
# unique.
# Assumptions : (1) str contains only characters
#                    from 'a' to 'z'
#                (2) integers are stored using 32
#                    bits

def areCharactersUnique(s):

    # An integer to store presence/absence
    # of 26 characters using its 32 bits
    checker = 0

    for i in range(len(s)):

        val = ord(s[i]) - ord('a')

        # If bit corresponding to current
        # character is already set
        if (checker & (1 << val)) > 0:
            return False

        # set bit in checker
        checker |= (1 << val)

    return True

# Driver code
s = "aaabbccdaa"
if areCharactersUnique(s):
    print("Yes")
else:
    print("No")

# This code is contributed
# by Mohit Kumar
```

## C#

```
// A space efficient program
// to check if all characters
// of string are unique.
using System;

class GFG {

    // Returns true if all characters
    // of str are unique. Assumptions:
    // (1)str contains only characters
    // from 'a' to 'z'.(2)integers are
    // stored using 32 bits
    static bool areChractersUnique(string str)
    {
        // An integer to store presence
        // or absence of 26 characters
        // using its 32 bits.
        int checker = 0;

        for (int i = 0; i < str.Length; ++i) {
            int val = (str[i] - 'a');

            // If bit corresponding to current
            // character is already set
            if ((checker & (1 << val)) > 0)
                return false;

            // set bit in checker
            checker |= (1 << val);
        }

        return true;
    }

    // Driver code
    public static void Main()
    {
        string s = "aaabbccdaa";

        if (areChractersUnique(s))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A space efficient PHP program
// to check if all characters of
// string are unique.

// Returns true if all characters
// of str are unique.
// Assumptions : (1) str contains
//                     only characters
//                   from 'a' to 'z'
//         (2) integers are stored
//             using 32 bits
function areChractersUnique($str)
{
    // An integer to store presence/absence
    // of 26 characters using its 32 bits.
    $checker = 0;

    for ($i = 0; $i < $len = strlen($str); ++$i)
    {
        $val = ($str[$i] - 'a');

        // If bit corresponding to current
        // character is already set
        if (($checker & (1 << $val)) > 0)
            return false;

        // set bit in checker
        $checker |= (1 << $val);
    }

    return true;
}

// Driver code
$s = "aaabbccdaa";
if (areChractersUnique($s))
    echo "Yes";
else
    echo "No";

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// Javascript program for the above approach

    // Returns true if all characters of str are
    // unique.
    // Assumptions : (1) str contains only characters
    //                   from 'a' to 'z'
    //               (2) integers are stored using 32
    //                 bits
    function areChractersUnique(str)
    {

        // An integer to store presence/absence
        // of 26 characters using its 32 bits.
        let checker = 0;

        for (let i = 0; i < str.length; ++i)
        {
            let val = (str[i]-'a');

            // If bit corresponding to current
            // character is already set
            if ((checker & (1 << val)) > 0)
                return false;

            // set bit in checker
            checker |= (1 << val);
        }

        return true;
    }

// Driver Code

    var s = "aaabbccdaa";

    if (areChractersUnique(s))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output**

```
No
```