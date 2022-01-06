# 不包含给定字符的子字符串的计数

> 原文:[https://www . geesforgeks . org/不包含给定字符的子字符串计数/](https://www.geeksforgeeks.org/count-of-sub-strings-that-do-not-consist-of-the-given-character/)

给定一个字符串**字符串**和一个字符 **c** 。任务是找出不包含字符 **c** 的子字符串的数量。
**举例:**

> **输入:** str = "baa "，c = 'b'
> **输出:** 3
> 子串为“a”、“a”和“aa”
> **输入:** str = "ababaa "，C = 'b'
> **输出:** 5

**方法:**首先取一个连续计数字符数的计数器，没有字符 **c** 。迭代字符串并增加计数器直到 **str[i]！= c** 。一旦**串【I】= = c**，从相邻长度 **cnt** 开始的子串数量将为 **(cnt * (cnt + 1)) / 2** 。在字符串完全遍历后，在最后一次出现 **c** 后出现的一组字符的结果中也加上 **(cnt *(cnt + 1)) / 2** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number
// of sub-strings that do not contain
// the given character c
int countSubstrings(string s, char c)
{

    // Length of the string
    int n = s.length();

    int cnt = 0;
    int sum = 0;

    // Traverse in the string
    for (int i = 0; i < n; i++) {

        // If current character is different
        // from the given character
        if (s[i] != c)
            cnt++;
        else {

            // Update the number of sub-strings
            sum += (cnt * (cnt + 1)) / 2;

            // Reset count to 0
            cnt = 0;
        }
    }

    // For the characters appearing
    // after the last occurrence of c
    sum += (cnt * (cnt + 1)) / 2;
    return sum;
}

// Driver code
int main()
{
    string s = "baa";
    char c = 'b';
    cout << countSubstrings(s, c);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the number
// of sub-strings that do not contain
// the given character c
static int countSubstrings(String s, char c)
{

    // Length of the string
    int n = s.length();

    int cnt = 0;
    int sum = 0;

    // Traverse in the string
    for (int i = 0; i < n; i++)
    {

        // If current character is different
        // from the given character
        if (s.charAt(i) != c)
            cnt++;
        else
        {

            // Update the number of sub-strings
            sum += (cnt * (cnt + 1)) / 2;

            // Reset count to 0
            cnt = 0;
        }
    }

    // For the characters appearing
    // after the last occurrence of c
    sum += (cnt * (cnt + 1)) / 2;
    return sum;
}

// Driver code
public static void main(String[] args)
{
    String s = "baa";
    char c = 'b';
    System.out.println(countSubstrings(s, c));
}
}

// This code is contributed by Code_Mech.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the number
# of sub-strings that do not contain
# the given character c
def countSubstrings(s, c):

    # Length of the string
    n = len(s)

    cnt = 0
    Sum = 0

    # Traverse in the string
    for i in range(n):

        # If current character is different
        # from the given character
        if (s[i] != c):
            cnt += 1
        else:

            # Update the number of sub-strings
            Sum += (cnt * (cnt + 1)) // 2

            # Reset count to 0
            cnt = 0

    # For the characters appearing
    # after the last occurrence of c
    Sum += (cnt * (cnt + 1)) // 2
    return Sum

# Driver code
s = "baa"
c = 'b'
print(countSubstrings(s, c))

# This code is contributed
# by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the number
// of sub-strings that do not contain
// the given character c
static int countSubstrings(string s, char c)
{

    // Length of the string
    int n = s.Length;

    int cnt = 0;
    int sum = 0;

    // Traverse in the string
    for (int i = 0; i < n; i++)
    {

        // If current character is different
        // from the given character
        if (s[i] != c)
            cnt++;
        else
        {

            // Update the number of sub-strings
            sum += (cnt * (cnt + 1)) / 2;

            // Reset count to 0
            cnt = 0;
        }
    }

    // For the characters appearing
    // after the last occurrence of c
    sum += (cnt * (cnt + 1)) / 2;
    return sum;
}

// Driver code
public static void Main()
{
    string s = "baa";
    char c = 'b';
    Console.Write(countSubstrings(s, c));
}
}

// This code is contributed by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the number
// of sub-strings that do not contain
// the given character c
function countSubstrings($s, $c)
{

    // Length of the string
    $n = strlen($s);

    $cnt = 0;
    $sum = 0;

    // Traverse in the string
    for ($i = 0; $i < $n; $i++)
    {

        // If current character is different
        // from the given character
        if ($s[$i] != $c)
            $cnt++;
        else
        {

            // Update the number of sub-strings
            $sum += floor(($cnt * ($cnt + 1)) / 2);

            // Reset count to 0
            $cnt = 0;
        }
    }

    // For the characters appearing
    // after the last occurrence of c
    $sum += floor(($cnt * ($cnt + 1)) / 2);
    return $sum;
}

// Driver code
$s = "baa";
$c = 'b';

echo countSubstrings($s, $c);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// javascript implementation of the approach   
// Function to return the number
    // of sub-strings that do not contain
    // the given character c
    function countSubstrings( s,  c) {

        // Length of the string
        var n = s.length;

        var cnt = 0;
        var sum = 0;

        // Traverse in the string
        for (i = 0; i < n; i++) {

            // If current character is different
            // from the given character
            if (s.charAt(i) != c)
                cnt++;
            else {

                // Update the number of sub-strings
                sum += (cnt * (cnt + 1)) / 2;

                // Reset count to 0
                cnt = 0;
            }
        }

        // For the characters appearing
        // after the last occurrence of c
        sum += (cnt * (cnt + 1)) / 2;
        return sum;
    }

    // Driver code

        var s = "baa";
        var c = 'b';
        document.write(countSubstrings(s, c));

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
3
```