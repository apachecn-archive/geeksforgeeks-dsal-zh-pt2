# 连续字符最长子串的长度

> 原文:[https://www . geeksforgeeks . org/带连续字符的最长子串长度/](https://www.geeksforgeeks.org/length-of-the-longest-substring-with-consecutive-characters/)

给定由小写字母组成的字符串 **str** ，任务是按字母顺序找出最长的字符子串的长度，即字符串“df **abc** k”将返回 3。**注意**这里的字母顺序被认为是循环的，即 **a、b、c、d、e、…、x、y、z、a、b、c、…** 。

**示例:**

> **输入:**str = " abc abcdefc "
> **输出:** 6
> 所有有效子串均为“ABC”、“abcdefb”和“ABC”
> 且其中最长的长度为 6
> 
> **输入:**str = " zabcd "
> T3】输出: 5

**进场:**

1.  初始化 **i = 0** 和 **len = 0** ，从 **i** 开始，找到最长有效子串的结束索引并保存，在**结束**中。
2.  现在，更新**len = max(end–I+1，len)** 和 **i = end + 1** (从索引 **end + 1** 开始获取下一个有效子串)，重复步骤 1，直到 **i < len(str)** 。
3.  最后打印 **len** 的值。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

    // Function to return the ending index for the
    // largest valid sub-string starting from index i
    int getEndingIndex(string str, int n, int i)
    {
        i++;
        while (i < n)
        {
            char curr = str[i];
            char prev = str[i-1];

            // If the current character appears after
            // the previous character according to
            // the given circular alphabetical order
            if ((curr == 'a' && prev == 'z') ||
                (curr - prev == 1))
                i++;
            else
                break;
        }

        return i - 1;
    }

    // Function to return the length of the longest
    // sub-string of consecutive characters from str
    int largestSubStr(string str, int n)
    {
        int len = 0;

        int i = 0;
        while (i < n)
        {

            // Valid sub-string exists from index
            // i to end
            int end = getEndingIndex(str, n, i);

            // Update the length
            len = max(end - i + 1, len);
            i = end + 1;
        }

        return len;
    }

    // Driver code
    int main()
    {
        string str = "abcabcdefabc";
        int n = str.length();
        cout << (largestSubStr(str, n));
    }

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the ending index for the
    // largest valid sub-string starting from index i
    static int getEndingIndex(String str, int n, int i)
    {
        i++;
        while (i < n) {
            char curr = str.charAt(i);
            char prev = str.charAt(i - 1);

            // If the current character appears after
            // the previous character  according to
            // the given circular alphabetical order
            if ((curr == 'a' && prev == 'z') ||
                (curr - prev == 1))
                i++;
            else
                break;
        }

        return i - 1;
    }

    // Function to return the length of the longest
    // sub-string of consecutive characters from str
    static int largestSubStr(String str, int n)
    {
        int len = 0;

        int i = 0;
        while (i < n) {

            // Valid sub-string exists from index
            // i to end
            int end = getEndingIndex(str, n, i);

            // Update the length
            len = Math.max(end - i + 1, len);
            i = end + 1;
        }

        return len;
    }

    // Driver code
    public static void main(String args[])
    {
        String str = "abcabcdefabc";
        int n = str.length();

        System.out.print(largestSubStr(str, n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the ending index for the
# largest valid sub-str1ing starting from index i
def getEndingIndex(str1, n, i):

    i += 1
    while (i < n):

        curr = str1[i]
        prev = str1[i - 1]

        # If the current character appears after
        # the previous character according to
        # the given circular alphabetical order
        if ((curr == 'a' and prev == 'z') or
            (ord(curr) - ord(prev) == 1)):
            i += 1
        else:
            break

    return i - 1

# Function to return the length of the
# longest sub-str1ing of consecutive
# characters from str1
def largestSubstr1(str1, n):

    Len = 0

    i = 0
    while (i < n):

        # Valid sub-str1ing exists from
        # index i to end
        end = getEndingIndex(str1, n, i)

        # Update the Length
        Len = max(end - i + 1, Len)
        i = end + 1

    return Len

# Driver code
str1 = "abcabcdefabc"
n = len(str1)
print(largestSubstr1(str1, n))

# This code is contributed by
# Mohit Kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the ending index for the
    // largest valid sub-string starting from index i
    static int getEndingIndex(string str, int n, int i)
    {
        i++;
        while (i < n)
        {
            char curr = str[i];
            char prev = str[i - 1];

            // If the current character appears after
            // the previous character according to
            // the given circular alphabetical order
            if ((curr == 'a' && prev == 'z') ||
                (curr - prev == 1))
                i++;
            else
                break;
        }
        return i - 1;
    }

    // Function to return the length of the longest
    // sub-string of consecutive characters from str
    static int largestSubStr(string str, int n)
    {
        int len = 0;

        int i = 0;
        while (i < n)
        {

            // Valid sub-string exists from index
            // i to end
            int end = getEndingIndex(str, n, i);

            // Update the length
            len = Math.Max(end - i + 1, len);
            i = end + 1;
        }
        return len;
    }

    // Driver code
    public static void Main()
    {
        string str = "abcabcdefabc";
        int n = str.Length;
        Console.Write(largestSubStr(str, n));
    }
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the ending index
// for the largest valid sub-string
/// starting from index i
function getEndingIndex($str, $n, $i)
{
    $i++;
    while ($i < $n)
    {
        $curr = $str[$i];
        $prev = $str[$i - 1];

        // If the current character appears after
        // the previous character according to
        // the given circular alphabetical order
        if (($curr == 'a' && $prev == 'z') ||
            (ord($curr) - ord($prev) == 1))
            $i++;
        else
            break;
    }

    return $i - 1;
}

// Function to return the length of the longest
// sub-string of consecutive characters from str
function largestSubStr($str, $n)
{
    $len = 0;

    $i = 0;
    while ($i < $n)
    {

        // Valid sub-string exists from index
        // i to end
        $end = getEndingIndex($str, $n, $i);

        // Update the length
        $len = max($end - $i + 1, $len);
        $i = $end + 1;
    }

    return $len;
}

// Driver code
$str = "abcabcdefabc";
$n = strlen($str);
echo largestSubStr($str, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the ending index for the
// largest valid sub-string starting from index i
function getEndingIndex(str,n,i)
{
        i++;
          while (i < n) {
            let curr = str[i];
            let prev = str[i - 1];

            // If the current character appears after
            // the previous character  according to
            // the given circular alphabetical order
            if ((curr == 'a' && prev == 'z') ||
                (curr.charCodeAt(0) - prev.charCodeAt(0) == 1))
                i++;
            else
                break;
        }

        return i - 1;
}

// Function to return the length of the longest
// sub-string of consecutive characters from str
function largestSubStr(str,n)
{
        let len = 0;

        let i = 0;
        while (i < n) {

            // Valid sub-string exists from index
            // i to end
            let end = getEndingIndex(str, n, i);

            // Update the length
            len = Math.max(end - i + 1, len);
            i = end + 1;
        }

        return len;
}

// Driver code
let str = "abcabcdefabc";
let n = str.length;

document.write(largestSubStr(str, n));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
6
```

**时间复杂度:** O(n)，其中 n 为输入字符串的长度。请注意，我们在最后增加了索引。