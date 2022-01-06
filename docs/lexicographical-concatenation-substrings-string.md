# 一个字符串的所有子串的字典式连接

> 原文:[https://www . geesforgeks . org/词典编纂-串联-子字符串-字符串/](https://www.geeksforgeeks.org/lexicographical-concatenation-substrings-string/)

给定一个字符串，按照字典顺序查找所有子字符串的串联。
示例:

> 输入:s =“abc”
> 输出:aababcbbcc
> s 的[子串](https://write.geeksforgeeks.org/c-program-to-print-all-substrings-of-a-given-string/)按照字典顺序为“a”、“b”、“c”、“ab”、“Abc”、“BC”。子串的串联是“a”+“ab”+“ABC”+“b”+“BC”+“c”=“aababcbbcc”。
> 输入:s =“CBA”
> 输出:阿巴 ccbcba

1.找到字符串的所有子字符串，并将其存储在字符串数组中。数组的大小为 n*(n+1)/2，其中 n 是输入字符串的长度。
2。对字符串数组进行排序，使它们都按照字典顺序排列。
3。将字符串数组的字符串连接到另一个空字符串中。

## C++

```
// CPP Program to create concatenation of all
// substrings in lexicographic order.
#include <bits/stdc++.h>
using namespace std;

string lexicographicSubConcat(string s)
{
    int n = s.length();

    // Creating an array to store substrings
    int sub_count = n*(n+1)/2;
    string arr[sub_count];    

    // finding all substrings of string
    int index = 0;
    for (int i = 0; i < n; i++)
        for (int len = 1; len <= n - i; len++)
            arr[index++] = s.substr(i, len);

    // Sort all substrings in lexicographic
    // order
    sort(arr, arr + sub_count);

    // Concatenating all substrings
    string res = "";
    for (int i = 0; i < sub_count; i++)
        res += arr[i];    

    return res;   
}

int main()
{
    string s = "abc";
    cout << lexicographicSubConcat(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to create concatenation of all
// substrings in lexicographic order.
import java.util.*;

class GFG
{

static String lexicographicSubConcat(String s)
{
    int n = s.length();

    // Creating an array to store substrings
    int sub_count = n*(n+1)/2;
    String []arr = new String[sub_count];    

    // finding all substrings of string
    int index = 0;
    for (int i = 0; i < n; i++)
        for (int len = 1; len <= n - i; len++)
        {
                arr[index++] = s.substring(i, i+len);
        }
    // Sort all substrings in lexicographic
    // order
    Arrays.sort(arr);

    // Concatenating all substrings
    String res = "";
    for (int i = 0; i < sub_count; i++)
        res += arr[i];    

    return res;
}

// Driver code
public static void main(String[] args)
{
    String s = "abc";
    System.out.println(lexicographicSubConcat(s));
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python Program to create concatenation of all
# substrings in lexicographic order.

def lexicographicSubConcat(s):
    n = len(s);

    # Creating an array to store substrings
    sub_count = (n * (n + 1))//2;
    arr = [0]*sub_count;    

    # finding all substrings of string
    index = 0;
    for i in range(n):
        for j in range(1,n - i + 1):
            arr[index] = s[i:i + j];
            index += 1;

    # Sort all substrings in lexicographic
    # order
    arr.sort();

    # Concatenating all substrings
    res = "";
    for i in range(sub_count):
        res += arr[i];    

    return res;

s = "abc";
print(lexicographicSubConcat(s));

# This code is contributed by Princi Singh
```

## C#

```
// C# Program to create concatenation of all
// substrings in lexicographic order.
using System;    

class GFG
{

static String lexicographicSubConcat(String s)
{
    int n = s.Length;

    // Creating an array to store substrings
    int sub_count = n*(n+1)/2;
    String []arr = new String[sub_count];    

    // finding all substrings of string
    int index = 0;
    for (int i = 0; i < n; i++)
        for (int len = 1; len <= n - i; len++)
        {
            arr[index++] = s.Substring(i, len);
        }

    // Sort all substrings in lexicographic
    // order
    Array.Sort(arr);

    // Concatenating all substrings
    String res = "";
    for (int i = 0; i < sub_count; i++)
        res += arr[i];    

    return res;
}

// Driver code
public static void Main(String[] args)
{
    String s = "abc";
    Console.WriteLine(lexicographicSubConcat(s));
}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript Program to create concatenation of all
// substrings in lexicographic order.

function lexicographicSubConcat(s)
{
    var n = s.length;

    // Creating an array to store substrings
    var sub_count = n*parseInt((n+1)/2);
    var arr = Array(sub_count);    

    // finding all substrings of string
    var index = 0;
    for (var i = 0; i < n; i++)
        for (var len = 1; len <= n - i; len++)
            arr[index++] = s.substring(i,i+ len);

    // Sort all substrings in lexicographic
    // order
    arr.sort();

    // Concatenating all substrings
    var res = "";
    for (var i = 0; i < sub_count; i++)
        res += arr[i];    

    return res;   
}

var s = "abc";
document.write( lexicographicSubConcat(s));

</script>
```

**输出:**

```
aababcbbcc
```