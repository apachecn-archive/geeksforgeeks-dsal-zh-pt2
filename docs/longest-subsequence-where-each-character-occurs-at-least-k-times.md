# 每个字符出现至少 k 次的最长子序列

> 原文:[https://www . geesforgeks . org/最长子序列-每个字符出现的位置-至少 k 次/](https://www.geeksforgeeks.org/longest-subsequence-where-each-character-occurs-at-least-k-times/)

给定一个字符串“s”和一个整数 k，找到另一个字符串“t ”,使得“t”是给定字符串“s”的最大子序列，并且“t”的每个字符必须在字符串 s 中出现至少 k 次。
**示例:**

```
Input : s = "geeksforgeeks"
        k = 2
Output : geeksgeeks

Input : s = "baaabaacba"
        k = 3
Output : baaabaaba
```

一个**简单的解决方案**是[生成所有子序列](https://www.geeksforgeeks.org/print-subsequences-string/)。对于每个子序列，检查它是否有至少 k 次的所有字符。找到最长的这样的子序列。这种方法的时间复杂度是指数级的。
**高效方法**我们可以取另一个数组来保存字符串 s 中每个字符的计数记录，如果有任何字符出现的次数大于或等于 k 次，那么我们就简单的打印出来。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP Program to find the subsequence
// with each character occurring at least
// k times in string s
#include <iostream>
using namespace std;

#define MAX_CHAR 26

// Function to find the subsequence
void findSubsequence(string str, int k)
{
    // Taking an extra array to keep
    // record for character count in s
    int a[MAX_CHAR] = { 0 };

    // Counting occurrences of all
    // characters in str[]
    for (int i = 0; i < str.size(); i++)
        a[str[i] - 'a']++;   

    // Printing characters with count
    // >= k in same order as they appear
    // in str.
    for (int i = 0; i < l; i++)
        if (a[str[i] - 'a'] >= k)
            cout << str[i];   
}

// Driver code
int main()
{
    int k = 2;
    findSubsequence("geeksforgeeks", k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the subsequence
// with each character occurring at least
// k times in string s
class GFG {

    static final int MAX_CHAR = 26;

    // Function to find the subsequence
    static void findSubsequence(String str, int k)
    {

        // Taking an extra array to keep
        // record for character count in s
        int a[] = new int[MAX_CHAR];

        // Counting occurrences of all
        // characters in str[]
        for (int i = 0; i < str.length(); i++)
            a[str.charAt(i) - 'a']++;

        // Printing characters with count
        // >= k in same order as they appear
        // in str.
        for (int i = 0; i < str.length(); i++)
            if (a[str.charAt(i) - 'a'] >= k)
                System.out.print(str.charAt(i));
    }

    // Driver code
    public static void main(String[] args) {

        int k = 2;
        findSubsequence("geeksforgeeks", k);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python Program to find the subsequence
# with each character occurring at least
# k times in string s

MAX_CHAR = 26

# Function to find the subsequence
def findSubsequence(stri, k):
    # Taking an extra array to keep
    # record for character count in s
    a = [0] * MAX_CHAR;

    # Counting occurrences of all
    # characters in str[]
    for i in range(len(stri)):
        a[ord(stri[i]) - ord('a')] += 1

    # Printing characters with count
    # >= k in same order as they appear
    # in str.
    for i in range(len(stri)):
        if a[ord(stri[i]) - ord('a')] >= k:
            print(stri[i],end='')

# Driver code
k = 2
findSubsequence("geeksforgeeks", k)

# This code is contributed by Shubham Rana
```

## C#

```
// C# Program to find the subsequence
// with each character occurring at
// least k times in string s
using System;

class GFG {

    static int MAX_CHAR = 26;

    // Function to find the subsequence
    static void findSubsequence(string str, int k)
    {

        // Taking an extra array to keep
        // record for character count in s
        int []a = new int[MAX_CHAR];

        // Counting occurrences of all
        // characters in str[]
        for (int i = 0; i < str.Length; i++)
            a[str[i] - 'a']++;

        // Printing characters with count
        // >= k in same order as they appear
        // in str.
        for (int i = 0; i < str.Length; i++)
            if (a[str[i] - 'a'] >= k)
                Console.Write(str[i]);
    }

    // Driver code
    public static void Main() {

        int k = 2;
        findSubsequence("geeksforgeeks", k);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the
// subsequence with each
// character occurring at
// least k times in string s

// Function to find the subsequence
function findSubsequence($str, $k)
{

    // Taking an extra array to keep
    // record for character count in s
    $a = array(1024);

    for($i = 0; $i < 26; $i++)
        $a[$i] = 0;

    // Counting occurrences of all
    // characters in str[]
    for ($i = 0; $i < strlen($str); $i++)
    {
        $temp = ord($str[$i]) - ord('a');
        $a[$temp] += 1;
    }

    // Printing characters with
    // count >= k in same order
    // as they appear in str.
    for ($i = 0; $i < strlen($str); $i++)
        if ($a[ord($str[$i]) - ord('a')] >= $k)
            echo $str[$i];
}

// Driver code
$k = 2;
findSubsequence("geeksforgeeks", $k);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// Javascript Program to find the subsequence
// with each character occurring at least
// k times in string s

var MAX_CHAR = 26;

// Function to find the subsequence
function findSubsequence(str, k)
{
    // Taking an extra array to keep
    // record for character count in s
    var a = Array(MAX_CHAR).fill(0);

    // Counting occurrences of all
    // characters in str[]
    for (var i = 0; i < str.length; i++)
        a[str[i].charCodeAt(0) -
        'a'.charCodeAt(0)]++;   

    // Printing characters with count
    // >= k in same order as they appear
    // in str.
    for (var i = 0; i < str.length; i++)
        if (a[str[i].charCodeAt(0) -
        'a'.charCodeAt(0)] >= k)
            document.write( str[i]);   
}

// Driver code
var k = 2;
findSubsequence("geeksforgeeks", k);

</script>
```

**输出:**

```
geeksgeeks
```