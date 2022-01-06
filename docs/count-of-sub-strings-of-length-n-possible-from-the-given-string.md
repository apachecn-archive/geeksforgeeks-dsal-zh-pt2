# 给定字符串中长度为 n 的子字符串的计数

> 原文:[https://www . geeksforgeeks . org/给定字符串中长度为 n 的子字符串的计数/](https://www.geeksforgeeks.org/count-of-sub-strings-of-length-n-possible-from-the-given-string/)

给定一个字符串 **str** 和一个整数 **N** ，任务是找到长度为 **N** 的可能子字符串的数量。
**举例:**

> **输入:** str = "geeksforgeeks "，n = 5
> **输出:** 9
> 长度为 5 的所有可能的子串都是“geeks”、“eeksf”、“eksfo”、
> “ksfor”、“sforg”、“forge”、“orgee”、“rgeek”和“geeks”。
> **输入:** str = "jgec "，N = 2
> **输出:** 3

**方法:**长度为 **n** 的子串的计数将始终为**len–n+1**，其中 **len** 是给定串的长度。例如，如果**str = " geeks forgeeks "****n = 5**，那么长度为 5 的子串的计数将为**【geeks】****【eeksf】****【eks fo】****【ksfor】****【sforg】****【forge】** **以下是上述方法的实施:** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// possible sub-strings of length n
int countSubStr(string str, int n)
{
    int len = str.length();
    return (len - n + 1);
}

// Driver code
int main()
{
    string str = "geeksforgeeks";
    int n = 5;

    cout << countSubStr(str, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the count of
// possible sub-strings of length n
static int countSubStr(String str, int n)
{
    int len = str.length();
    return (len - n + 1);
}

// Driver code
public static void main(String args[])
{
    String str = "geeksforgeeks";
    int n = 5;

    System.out.print(countSubStr(str, n));
}
}

// This code is contributed by mohit kumar 29
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# possible sub-strings of length n
def countSubStr(string, n) :

    length = len(string);
    return (length - n + 1);

# Driver code
if __name__ == "__main__" :

    string = "geeksforgeeks";
    n = 5;

    print(countSubStr(string, n));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of
// possible sub-strings of length n
static int countSubStr(string str, int n)
{
    int len = str.Length;
    return (len - n + 1);
}

// Driver code
public static void Main()
{
    string str = "geeksforgeeks";
    int n = 5;

    Console.WriteLine(countSubStr(str, n));
}
}

// This code is contributed by Code_Mech.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count of
// possible sub-strings of length n
function countSubStr($str, $n)
{
    $len = strlen($str);
    return ($len - $n + 1);
}

// Driver code
$str = "geeksforgeeks";
$n = 5;

echo(countSubStr($str, $n));

// This code is contributed by Code_Mech.
?>
```

## java 描述语言

```
<script>
  // JavaScript implementation of the approach
  // Function to return the count of
  // possible sub-strings of length n
  function countSubStr(str, n) {
    var len = str.length;
    return len - n + 1;
  }

  // Driver code
  var str = "geeksforgeeks";
  var n = 5;

  document.write(countSubStr(str, n));
</script>
```

**Output:** 

```
9
```