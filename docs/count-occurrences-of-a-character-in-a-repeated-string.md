# 计算重复字符串中某个字符的出现次数

> 原文:[https://www . geesforgeks . org/count-重复字符串中出现的字符数/](https://www.geeksforgeeks.org/count-occurrences-of-a-character-in-a-repeated-string/)

给定一个整数 N 和一个小写字符串。字符串无限重复。任务是找出给定字符 x 在前 N 个字母中出现的次数。
**例:**

```
Input : N = 10 str = "abcac"
Output : 4
Explanation: "abcacabcac" is the substring from the infinitely repeated string. In first 10 letters 'a' occurs 4  times.

Input: N = 10, str = "aba"
Output : 7
```

**进场:**
1。查找给定字符串中出现的字符“a”。
2。找出找到“a”出现所需的重复次数。
3。将单个字符串的出现次数乘以重复次数。
4。如果给定的 n 不是给定字符串大小的倍数，那么我们将在剩余的子字符串中找到“a”的出现。
以下是上述方法的实施:

## C++

```
// CPP program to find the occurrences of
// character x in the infinite repeated string
// upto length n
#include <bits/stdc++.h>
using namespace std;

// Function to count the character 'a'
int countChar(string str, char x)
{
    int count = 0, n = 10;
    for (int i = 0; i < str.size(); i++)
        if (str[i] == x)
            count++;

    // atleast k repetition are required
    int repetitions = n / str.size();
    count = count * repetitions;

    // if n is not the multiple of the string size
    // check for the remaining repeating character.
    for (int i = 0; i < n % str.size(); i++) {
        if (str[i] == x)
            count++;
    }

    return count;
}

// Driver code
int main()
{
    string str = "abcac";
    cout << countChar(str, 'a');
    return 0;
}

// This code is contributed by Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the occurrences
// of character x in the infinite
// repeated string upto length n
import java.util.*;
import java.lang.*;

class GFG
{
// Function to count the character 'a'
static int countChar(String str, char x)
{
    int count = 0;
    int n = 10;
    for (int i = 0; i < str.length(); i++)
        if (str.charAt(i) == x)
            count++;

    // atleast k repetition are required
    int repetitions = n / str.length();
    count = count * repetitions;

    // if n is not the multiple of the
    // string size check for the remaining
    // repeating character.
    for (int i = 0;
            i < n % str.length(); i++)
    {
        if (str.charAt(i) == x)
            count++;
    }

    return count;
}

// Driver code
public static void main(String args[])
{
    String str = "abcac";
    System.out.println(countChar(str, 'a'));
}
}

// This code is contributed
// by Akanksha Rai
```

## 蟒蛇 3

```
# Python3 program to find the occurrences of
# character x in the infinite repeated string
# upto length n

# Function to count the character 'a'
def countChar(str, x):
    count = 0
    for i in range(len(str)):
        if (str[i] == x) :
            count += 1
    n = 10

    # atleast k repetition are required
    repetitions = n // len(str)
    count = count * repetitions

    # if n is not the multiple of the
    # string size check for the remaining
    # repeating character.
    l = n % len(str)
    for i in range(l):
        if (str[i] == x):
            count += 1
    return count

# Driver code
str = "abcac"
print(countChar(str, 'a'))

# This code is contributed
# by sahishelangia
```

## C#

```
// C# program to find the occurrences
// of character x in the infinite
// repeated string upto length n
using System;

class GFG
{
// Function to count the character 'a'
static int countChar(string str, char x)
{
    int count = 0;
    int n = 10;
    for (int i = 0; i < str.Length; i++)
        if (str[i] == x)
            count++;

    // atleast k repetition are required
    int repetitions = n / str.Length;
    count = count * repetitions;

    // if n is not the multiple of the
    // string size check for the remaining
    // repeating character.
    for (int i = 0;
             i < n % str.Length; i++)
    {
        if (str[i] == x)
            count++;
    }

    return count;
}

// Driver code
public static void Main()
{
    string str = "abcac";
    Console.WriteLine(countChar(str, 'a'));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the occurrences
// of character x in the infinite
// repeated string upto length n

// Function to count the character 'a'
function countChar($str, $x)
{
    $count = 0;
    $n = 10;
    for ($i = 0; $i < strlen($str); $i++)
        if ($str[$i] == $x)
            $count++;

    // atleast k repetition are required
    $repetitions = (int)($n / strlen($str));
    $count = $count * $repetitions;

    // if n is not the multiple of
    // the string size check for the
    // remaining repeating character.
    for ($i = 0; $i < $n % strlen($str); $i++)
    {
        if ($str[$i] == $x)
            $count++;
    }

    return $count;
}

// Driver code
$str = "abcac";
echo countChar($str, 'a');

// This code is contributed by Sachin
?>
```

## java 描述语言

```
<script>

    // JavaScript program to find the occurrences
    // of character x in the infinite
    // repeated string upto length n

    // Function to count the character 'a'
    function countChar(str, x)
    {
        let count = 0;
        let n = 10;
        for (let i = 0; i < str.length; i++)
            if (str[i] == x)
                count++;

        // atleast k repetition are required
        let repetitions = n / str.length;
        count = count * repetitions;

        // if n is not the multiple of the
        // string size check for the remaining
        // repeating character.
        for (let i = 0; i < n % str.length; i++)
        {
            if (str[i] == x)
                count++;
        }

        return count;
    }

    let str = "abcac";
    document.write(countChar(str, 'a'));

</script>
```

**输出:**

```
4
```