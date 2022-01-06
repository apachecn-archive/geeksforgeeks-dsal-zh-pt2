# 使二进制字符串交替的最小替换次数|集合 2

> 原文:[https://www . geeksforgeeks . org/二进制字符串替换最小次数-交替集-2/](https://www.geeksforgeeks.org/minimum-number-of-replacements-to-make-the-binary-string-alternating-set-2/)

给定一个二进制字符串 **str** ，任务是找到字符串中必须替换的最小字符数，以便使字符串交替出现(即形式为**0101010101……**或**10101010……**)。
**举例:**

> **输入:** str = "1100"
> **输出:** 2
> 将 2 <sup>nd</sup> 字符替换为“0”，将 3 <sup>rd</sup> 字符替换为“1”
> **输入:** str = "1010"
> **输出:** 0
> 字符串已经交替。

我们已经在[翻转次数中讨论了一种使二进制字符串交替出现的方法](https://www.geeksforgeeks.org/number-flips-make-binary-string-alternate/)。这篇文章讨论了一个更好的方法。
**方法:**对于字符串 **str** ，可以有两种可能的解决方案。生成的字符串可以是

1.  **010101……**或
2.  **101010…**

为了找到最少的替换，计算替换次数以转换类型 1 中的字符串，并将其存储在 **count** 中，然后最小替换将是 **min(count，len–count)**，其中 **len** 是字符串的长度。**len–count**是类型 2 中转换字符串的替换次数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum number of
// characters of the given binary string
// to be replaced to make the string alternating
int minReplacement(string s, int len)
{
    int ans = 0;
    for (int i = 0; i < len; i++) {

        // If there is 1 at even index positions
        if (i % 2 == 0 && s[i] == '1')
            ans++;

        // If there is 0 at odd index positions
        if (i % 2 == 1 && s[i] == '0')
            ans++;
    }
    return min(ans, len - ans);
}

// Driver code
int main()
{
    string s = "1100";
    int len = s.size();
    cout << minReplacement(s, len);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the minimum number of
    // characters of the given binary string
    // to be replaced to make the string alternating
    static int minReplacement(String s, int len)
    {
        int ans = 0;
        for (int i = 0; i < len; i++) {

            // If there is 1 at even index positions
            if (i % 2 == 0 && s.charAt(i) == '1')
                ans++;

            // If there is 0 at odd index positions
            if (i % 2 == 1 && s.charAt(i) == '0')
                ans++;
        }
        return Math.min(ans, len - ans);
    }

    // Driver code
    public static void main(String args[])
    {
        String s = "1100";
        int len = s.length();
        System.out.print(minReplacement(s, len));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach.

# Function to return the minimum number of
# characters of the given binary string
# to be replaced to make the string alternating
def minReplacement(s, length):

    ans = 0
    for i in range(0, length):

        # If there is 1 at even index positions
        if i % 2 == 0 and s[i] == '1':
            ans += 1

        # If there is 0 at odd index positions
        if i % 2 == 1 and s[i] == '0':
            ans += 1

    return min(ans, length - ans)

# Driver code
if __name__ == "__main__":

    s = "1100"
    length = len(s)
    print(minReplacement(s, length))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the minimum number of
    // characters of the given binary string
    // to be replaced to make the string alternating
    static int minReplacement(String s, int len)
    {
        int ans = 0;
        for (int i = 0; i < len; i++)
        {

            // If there is 1 at even index positions
            if (i % 2 == 0 && s[i] == '1')
                ans++;

            // If there is 0 at odd index positions
            if (i % 2 == 1 && s[i] == '0')
                ans++;
        }
        return Math.Min(ans, len - ans);
    }

    // Driver code
    public static void Main(String []args)
    {
        String s = "1100";
        int len = s.Length;
        Console.Write(minReplacement(s, len));
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the minimum number of
// characters of the given binary string
// to be replaced to make the string alternating
function minReplacement($s, $len)
{
    $ans = 0;
    for ($i = 0; $i < $len; $i++)
    {

        // If there is 1 at even index positions
        if ($i % 2 == 0 && $s[$i] == '1')
            $ans++;

        // If there is 0 at odd index positions
        if ($i % 2 == 1 && $s[$i] == '0')
            $ans++;
    }
    return min($ans, $len - $ans);
}

// Driver code
$s = "1100";
$len = strlen($s);
echo minReplacement($s, $len);

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the minimum number of
// characters of the given binary string
// to be replaced to make the string alternating
function minReplacement(s, len)
{
    var ans = 0;
    for (var i = 0; i < len; i++) {

        // If there is 1 at even index positions
        if (i % 2 == 0 && s[i] == '1')
            ans++;

        // If there is 0 at odd index positions
        if (i % 2 == 1 && s[i] == '0')
            ans++;
    }
    return Math.min(ans, len - ans);
}

// Driver code
var s = "1100";
var len = s.length;
document.write(minReplacement(s, len));

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(len)，其中 len 是给定字符串的长度。