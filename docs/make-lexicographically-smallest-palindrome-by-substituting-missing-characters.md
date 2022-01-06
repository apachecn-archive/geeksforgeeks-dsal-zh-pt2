# 通过替换缺失的字符

制作词典上最小的回文

> 原文:[https://www . geeksforgeeks . org/make-按字典顺序排列-最小-通过替换-缺少回文字符/](https://www.geeksforgeeks.org/make-lexicographically-smallest-palindrome-by-substituting-missing-characters/)

给定一个字符串 **str** ，其中一些字符缺失，用一个**' ***表示。任务是替换丢失的字符，使其成为字典上最小的回文。如果不可能使字符串回文，那么打印 **-1** 。
**举例:**

> **输入:** str = "ab*a"
> **输出:** abba
> **输入:** a*b
> **输出:** -1
> 我们不能让它回文所以输出为-1。

**进场:**

1.  将**‘I’**标记放在绳子的起点，将**‘j’**标记放在绳子的终点。
2.  如果两个位置的字符都丢失了，那么用**‘a’**替换这两个字符，使其成为字典上最小的回文。
3.  如果只有**I<sub>th</sub>T3】或**j<sub>th</sub>T7】位置的字符缺失，则分别将其替换为**j<sub>th</sub>T11】或**I<sub>th</sub>T15】字符。********
4.  如果在**I<sub>th</sub>T3】和**j<sub>th</sub>T7】位置的字符**不相等**，则该字符串不能被制成回文并打印 **-1** 。****

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the lexicographically
// smallest palindrome that can be made from
// the given string after replacing
// the required characters
string makePalindrome(string str)
{
    int i = 0, j = str.length() - 1;

    while (i <= j) {

        // If characters are missing at both the positions
        // then substitute it with 'a'
        if (str[i] == '*' && str[j] == '*') {
            str[i] = 'a';
            str[j] = 'a';
        }

        // If only str[j] = '*' then update it
        // with the value at str[i]
        else if (str[j] == '*')
            str[j] = str[i];

        // If only str[i] = '*' then update it
        // with the value at str[j]
        else if (str[i] == '*')
            str[i] = str[j];

        // If characters at both positions
        // are not equal and != '*' then the string
        // cannot be made palindrome
        else if (str[i] != str[j])
            return "-1";

        i++;
        j--;
    }

    // Return the required palindrome
    return str;
}

// Driver code
int main()
{
    string str = "na*an";

    cout << makePalindrome(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the lexicographically
// smallest palindrome that can be made from
// the given string after replacing
// the required characters
static String makePalindrome(char[] str)
{
    int i = 0, j = str.length - 1;

    while (i <= j)
    {

        // If characters are missing at both the positions
        // then substitute it with 'a'
        if (str[i] == '*' && str[j] == '*')
        {
            str[i] = 'a';
            str[j] = 'a';
        }

        // If only str[j] = '*' then update it
        // with the value at str[i]
        else if (str[j] == '*')
            str[j] = str[i];

        // If only str[i] = '*' then update it
        // with the value at str[j]
        else if (str[i] == '*')
            str[i] = str[j];

        // If characters at both positions
        // are not equal and != '*' then the string
        // cannot be made palindrome
        else if (str[i] != str[j])
            return "-1";

        i++;
        j--;
    }

    // Return the required palindrome
    return String.valueOf(str);
}

// Driver code
public static void main(String[] args)
{
    char[] str = "na*an".toCharArray();

    System.out.println(makePalindrome(str));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the lexicographically
# smallest palindrome that can be made from
# the given string after replacing
# the required characters
def makePalindrome(str1):
    i = 0
    j = len(str1) - 1
    str1 = list(str1)
    while (i <= j):

        # If characters are missing
        # at both the positions
        # then substitute it with 'a'
        if (str1[i] == '*' and str1[j] == '*'):
            str1[i] = 'a'
            str1[j] = 'a'

        # If only str1[j] = '*' then update it
        # with the value at str1[i]
        elif (str1[j] == '*'):
            str1[j] = str1[i]

        # If only str1[i] = '*' then update it
        # with the value at str1[j]
        elif (str1[i] == '*'):
            str1[i] = str1[j]

        # If characters at both positions
        # are not equal and != '*' then the string
        # cannot be made palindrome
        elif (str1[i] != str1[j]):
            str1 = '' . join(str1)
            return "-1"

        i += 1
        j -= 1

    # Return the required palindrome
    str1 = '' . join(str1)
    return str1

# Driver code
if __name__ == '__main__':
    str1 = "na*an"

    print(makePalindrome(str1))

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
// smallest palindrome that can be made from
// the given string after replacing
// the required characters
static String makePalindrome(char[] str)
{
    int i = 0, j = str.Length - 1;

    while (i <= j)
    {

        // If characters are missing at both the positions
        // then substitute it with 'a'
        if (str[i] == '*' && str[j] == '*')
        {
            str[i] = 'a';
            str[j] = 'a';
        }

        // If only str[j] = '*' then update it
        // with the value at str[i]
        else if (str[j] == '*')
            str[j] = str[i];

        // If only str[i] = '*' then update it
        // with the value at str[j]
        else if (str[i] == '*')
            str[i] = str[j];

        // If characters at both positions
        // are not equal and != '*' then the string
        // cannot be made palindrome
        else if (str[i] != str[j])
            return "-1";

        i++;
        j--;
    }

    // Return the required palindrome
    return String.Join("",str);
}

// Driver code
public static void Main(String[] args)
{
    char[] str = "na*an".ToCharArray();

    Console.WriteLine(makePalindrome(str));
}
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the lexicographically
// smallest palindrome that can be made from
// the given string after replacing
// the required characters
function makePalindrome($str)
{
    $i = 0; $j = strlen($str) - 1;

    while ($i <= $j)
    {

        // If characters are missing at both the positions
        // then substitute it with 'a'
        if ($str[$i] == '*' && $str[$j] == '*')
        {
            $str[$i] = 'a';
            $str[$j] = 'a';
        }

        // If only str[j] = '*' then update it
        // with the value at str[i]
        else if ($str[$j] == '*')
            $str[$j] = $str[$i];

        // If only str[i] = '*' then update it
        // with the value at str[j]
        else if ($str[$i] == '*')
            $str[$i] = $str[$j];

        // If characters at both positions
        // are not equal and != '*' then the string
        // cannot be made palindrome
        else if ($str[$i] != $str[$j])
            return "-1";

        $i++;
        $j--;
    }

    // Return the required palindrome
    return $str;
}

    // Driver code
    $str = "na*an";

    echo makePalindrome($str);

    // This Code is contributed by AnkitRai01
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the lexicographically
// smallest palindrome that can be made from
// the given string after replacing
// the required characters
function makePalindrome(str)
{
    var i = 0, j = str.length - 1;

    while (i <= j) {

        // If characters are missing at both the positions
        // then substitute it with 'a'
        if (str[i] == '*' && str[j] == '*') {
            str[i] = 'a';
            str[j] = 'a';
        }

        // If only str[j] = '*' then update it
        // with the value at str[i]
        else if (str[j] == '*')
            str[j] = str[i];

        // If only str[i] = '*' then update it
        // with the value at str[j]
        else if (str[i] == '*')
            str[i] = str[j];

        // If characters at both positions
        // are not equal and != '*' then the string
        // cannot be made palindrome
        else if (str[i] != str[j])
            return "-1";

        i++;
        j--;
    }

    // Return the required palindrome
    return str.join("");
}

// Driver code
var str = "na*an".split('');

document.write(makePalindrome(str));

</script>
```

**Output:** 

```
naaan
```