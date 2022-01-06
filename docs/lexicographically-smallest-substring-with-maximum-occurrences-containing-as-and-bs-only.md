# 字典上最小的子串，最大出现次数只包含 a 和 b

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列-出现次数最多的最小子串-仅包含 as 和 bs/](https://www.geeksforgeeks.org/lexicographically-smallest-substring-with-maximum-occurrences-containing-as-and-bs-only/)

给定一个字符串![s  ](img/2f9e9564d9a0ab37fcfa0d3c7cda6a42.png "Rendered by QuickLaTeX.com")(包含从‘0’到‘9’的字符)和两个数字![a  ](img/c30e654d88f33e45c5463a428b007bce.png "Rendered by QuickLaTeX.com")和![b  ](img/5a3a9480cd4e66896d3cc12d182fefab.png "Rendered by QuickLaTeX.com")。任务是找到给定字符串中出现次数最多的子字符串，并且只包含 a 和 b。如果有两个或两个以上频率相同的子串，则打印字典序最小的子串。如果不存在这样的子串，那么打印-1。
T4【示例】T5:

```
Input : str = "47", a = 4, b = 7 
Output : 4

Input : str = "23", a = 4, b = 7
Output : -1
```

其思想是观察我们需要找到出现次数最多的子串。因此，如果我们考虑同时包含 a 和 b 的子字符串，那么出现的次数将少于我们单独考虑具有单个数字“a”和“b”的子字符串。
所以，思路是计算字符串中‘a’和‘b’的数字出现的频率，出现频率最高的那个就是答案。
**注**:如果两个数字的出现频率相同，那么在‘a’和‘b’中字典上较小的那个数字就是答案。
以下是上述方法的实施:

## C++

```
// CPP program to Find the lexicographically
// smallest substring in a given string with
// maximum frequency and contains a's and b's only

#include <bits/stdc++.h>
using namespace std;

// Function to Find the lexicographically
// smallest substring in a given string with
// maximum frequency and contains a's and b's only.
int maxFreq(string s, int a, int b)
{
    // To store frequency of digits
    int fre[10] = { 0 };

    // size of string
    int n = s.size();

    // Take lexicographically larger digit in b
    if (a > b)
        swap(a, b);

    // get frequency of each character
    for (int i = 0; i < n; i++)
        fre[s[i] - '0']++;

    // If no such string exits
    if (fre[a] == 0 and fre[b] == 0)
        return -1;

    // Maximum frequency
    else if (fre[a] >= fre[b])
        return a;
    else
        return b;
}

// Driver program
int main()
{
    int a = 4, b = 7;

    string s = "47744";

    cout << maxFreq(s, a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Find the lexicographically
// smallest substring in a given string with
// maximum frequency and contains a's and b's only

import java.io.*;

class GFG {

// Function to Find the lexicographically
// smallest substring in a given string with
// maximum frequency and contains a's and b's only.
static int maxFreq(String s, int a, int b)
{
    // To store frequency of digits
    int fre[] =  new int[10];

    // size of string
    int n = s.length();

    // Take lexicographically larger digit in b
    if (a > b)
    {
        int temp = a;
        a =b;
        b = temp;

    }

    // get frequency of each character
    for (int i = 0; i < n; i++)
        fre[s.charAt(i) - '0']++;

    // If no such string exits
    if (fre[a] == 0 && fre[b] == 0)
        return -1;

    // Maximum frequency
    else if (fre[a] >= fre[b])
        return a;
    else
        return b;
}

// Driver program

    public static void main (String[] args) {

    int a = 4, b = 7;

    String s = "47744";

    System.out.print(maxFreq(s, a, b));
    }
}
// This code is contributed by inder_verma
```

## 蟒蛇 3

```
# Python 3 program to Find the lexicographically
# smallest substring in a given string with
# maximum frequency and contains a's and b's only

# Function to Find the lexicographically
# smallest substring in a given string with
# maximum frequency and contains a's and b's only.
def maxFreq(s, a, b):
    # To store frequency of digits
    fre = [0 for i in range(10)]

    # size of string
    n = len(s)

    # Take lexicographically larger digit in b
    if (a > b):
        swap(a, b)

    # get frequency of each character
    for i in range(0,n,1):
        a = ord(s[i]) - ord('0')
        fre[a] += 1

    # If no such string exits
    if (fre[a] == 0 and fre[b] == 0):
        return -1

    # Maximum frequency
    elif (fre[a] >= fre[b]):
        return a
    else:
        return b

# Driver program
if __name__ == '__main__':
    a = 4
    b = 7

    s = "47744"

    print(maxFreq(s, a, b))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to Find the lexicographically
// smallest substring in a given string with
// maximum frequency and contains a's and b's only
using System;

class GFG {

// Function to Find the lexicographically
// smallest substring in a given string with
// maximum frequency and contains a's and b's only.
static int maxFreq(string s, int a, int b)
{
    // To store frequency of digits
    int []fre = new int[10];

    // size of string
    int n = s.Length;

    // Take lexicographically larger digit in b
    if (a > b)
    {
        int temp = a;
        a =b;
        b = temp;

    }

    // get frequency of each character
    for (int i = 0; i < n; i++)
        fre[s[i] - '0']++;

    // If no such string exits
    if (fre[a] == 0 && fre[b] == 0)
        return -1;

    // Maximum frequency
    else if (fre[a] >= fre[b])
        return a;
    else
        return b;
}

// Driver program

    public static void Main () {

    int a = 4, b = 7;

    string s = "47744";

     Console.WriteLine(maxFreq(s, a, b));
    }
}
// This code is contributed by inder_verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Find the lexicographically
// smallest substring in a given string with
// maximum frequency and contains a's and b's only

// Function to Find the lexicographically
// smallest substring in a given string with
// maximum frequency and contains a's and b's only.
function maxFreq($s, $a, $b)
{
    // To store frequency of digits
    $fre = array_fill(0, 10, 0);

    // size of string
    $n = strlen($s);

    // Take lexicographically larger digit in b
    if ($a > $b)
    {
        $xx = $a;
        $a = $b;
        $b = $xx;}

     // get frequency of each character
    for ($i = 0; $i < $n; $i++)
    {
        $a = ord($s[$i]) - ord('0');
        $fre[$a] += 1;
    }

    // If no such string exits
    if ($fre[$a] == 0 and $fre[$b] == 0)
        return -1;

    // Maximum frequency
    else if ($fre[$a] >= $fre[$b])
        return $a;
    else
        return $b;
}

// Driver Code
$a = 4;
$b = 7;

$s = "47744";

print(maxFreq($s, $a, $b));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
      // JavaScript program to Find the lexicographically
      // smallest substring in a given string with
      // maximum frequency and contains a's and b's only
      // Function to Find the lexicographically
      // smallest substring in a given string with
      // maximum frequency and contains a's and b's only.
      function maxFreq(s, a, b)
      {

        // To store frequency of digits
        var fre = new Array(10).fill(0);

        // size of string
        var n = s.length;

        // Take lexicographically larger digit in b
        if (a > b) {
          var temp = a;
          a = b;
          b = temp;
        }

        // get frequency of each character
        for (var i = 0; i < n; i++)
          fre[s[i].charCodeAt(0) - "0".charCodeAt(0)]++;

        // If no such string exits
        if (fre[a] === 0 && fre[b] === 0) return -1;

        // Maximum frequency
        else if (fre[a] >= fre[b]) return a;
        else return b;
      }

      // Driver program
      var a = 4,
        b = 7;
      var s = "47744";
      document.write(maxFreq(s, a, b));

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
4
```