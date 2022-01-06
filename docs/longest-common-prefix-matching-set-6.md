# 最长公共前缀匹配| Set-6

> 原文:[https://www . geesforgeks . org/long-common-prefix-matching-set-6/](https://www.geeksforgeeks.org/longest-common-prefix-matching-set-6/)

给定一组字符串，找到最长的公共前缀。
**例:**

```
Input: str[] = {geeksforgeeks, geeks, geek, geezer}
Output: gee

Input: str[] = {apple, ape, april}
Output: ap
```

**之前的方法:**T2【set 1】|[set 2](https://www.geeksforgeeks.org/longest-common-prefix-set-2-character-by-character-matching/)|[set 3](https://www.geeksforgeeks.org/longest-common-prefix-set-3-divide-and-conquer/)|[set 4](https://www.geeksforgeeks.org/longest-common-prefix-set-4-binary-search/)|[set 5](https://www.geeksforgeeks.org/longest-common-prefix-set-5-using-trie/)
T13】方法:

*   对给定的一组 N 个字符串进行排序。
*   比较排序后的字符串数组中的第一个和最后一个字符串。
*   前缀字符在第一个和最后一个字符串中匹配的字符串将是答案。

以下是上述方法的实现:

## C++

```
// A C++ Program to find the longest common prefix
#include <bits/stdc++.h>
using namespace std;

// A Utility Function to find the common prefix between
// first and last strings
string commonPrefixUtil(string str1, string str2)
{
    string result;
    int n1 = str1.length(), n2 = str2.length();

    // Compare str1 and str2
    for (int i = 0, j = 0; i <= n1 - 1 && j <= n2 - 1; i++, j++) {
        if (str1[i] != str2[j])
            break;
        result.push_back(str1[i]);
    }

    return (result);
}

// A Function that returns the longest common prefix
// from the array of strings
void commonPrefix(string arr[], int n)
{
    // sorts the N set of strings
    sort(arr, arr + n);

    // prints the common prefix of the first and the
    // last string of the set of strings
    cout << commonPrefixUtil(arr[0], arr[n - 1]);
}

// Driver Code
int main()
{
    string arr[] = { "geeksforgeeks", "geeks",
                     "geek", "geezer" };
    int n = sizeof(arr) / sizeof(arr[0]);

    commonPrefix(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to find the longest common prefix

import java.util.Arrays;

class GFG {

// A Utility Function to find the common prefix between
// first and last strings
    static String commonPrefixUtil(String str1, String str2) {
        String result = "";
        int n1 = str1.length(), n2 = str2.length();

        // Compare str1 and str2
        for (int i = 0, j = 0; i <= n1 - 1 && j <= n2 - 1; i++, j++) {
            if (str1.charAt(i) != str2.charAt(j)) {
                break;
            }
            result += str1.charAt(i);
        }

        return (result);
    }

// A Function that returns the longest common prefix
// from the array of strings
    static void commonPrefix(String arr[], int n) {
        // sorts the N set of strings
        Arrays.sort(arr);

        // prints the common prefix of the first and the
        // last String of the set of strings
        System.out.println(commonPrefixUtil(arr[0], arr[n - 1]));
    }

// Driver Code
    public static void main(String[] args) {
        String arr[] = {"geeksforgeeks", "geeks",
            "geek", "geezer"};
        int n = arr.length;

        commonPrefix(arr, n);

    }
}
/* This JAVA code is contributed by 29AjayKumar*/
```

## 蟒蛇 3

```
# A Python 3 Program to find the
# longest common prefix

# A Utility Function to find the common
# prefix between first and last strings
def commonPrefixUtil(str1, str2):
    n1 = len(str1)
    n2 = len(str2)

    result = ""

    # Compare str1 and str2
    j = 0
    i = 0
    while(i <= n1 - 1 and j <= n2 - 1):
        if (str1[i] != str2[j]):
            break
        result += (str1[i])

        i += 1
        j += 1

    return (result)

# A Function that returns the longest
# common prefix from the array of strings
def commonPrefix(arr, n):

    # sorts the N set of strings
    arr.sort(reverse = False)

    # prints the common prefix of the first
    # and the last string of the set of strings
    print(commonPrefixUtil(arr[0], arr[n - 1]))

# Driver Code
if __name__ == '__main__':
    arr = ["geeksforgeeks", "geeks",
                    "geek", "geezer"]
    n = len(arr)

    commonPrefix(arr, n)

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# Program to find the longest
// common prefix
using System;

class GFG
{
// A Utility Function to find the common
// prefix between first and last strings
static String commonPrefixUtil(String str1,
                               String str2)
{
    string result = "";
    int n1 = str1.Length, n2 = str2.Length;

    // Compare str1 and str2
    for (int i = 0, j = 0;
             i <= n1 - 1 && j <= n2 - 1; i++, j++)
    {
        if (str1[i] != str2[j])
            break;
        result += (str1[i]);
    }

    return (result);
}

// A Function that returns the longest
// common prefix from the array of strings
static void commonPrefix(String []arr, int n)
{
    // sorts the N set of strings
    Array.Sort(arr);

    // prints the common prefix of the first
    // and the last String of the set of strings
    Console.Write(commonPrefixUtil(arr[0],
                                   arr[n - 1]));
}

// Driver Code
public static void Main()
{
    String []arr = {"geeksforgeeks", "geeks",
                    "geek", "geezer"};
    int n = arr.Length;
    commonPrefix(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A PHP Program to find the longest
// common prefix

// A Utility Function to find the common
// prefix between first and last strings
function commonPrefixUtil($str1, $str2)
{
    $result = "";
    $n1 = strlen($str1);
    $n2 = strlen($str2);

    // Compare str1 and str2
    for ($i = 0, $j = 0; $i <= $n1 - 1 &&
          $j <= $n2 - 1; $i++, $j++)
    {
        if ($str1[$i] != $str2[$j])
            break;
        $result = $result.$str1[$i];
    }

    return ($result);
}

// A Function that returns the longest
// common prefix from the array of strings
function commonPrefix(&$arr, $n)
{
    // sorts the N set of strings
    sort($arr);

    // prints the common prefix of the first
    // and the last string of the set of strings
    echo commonPrefixUtil($arr[0], $arr[$n - 1]);
}

// Driver Code
$arr = array("geeksforgeeks", "geeks",
             "geek", "geezer" );
$n = sizeof($arr);

commonPrefix($arr, $n);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// A Javascript program to find the longest common prefix

    // A Utility Function to find the common prefix between
// first and last strings
    function commonPrefixUtil(str1,str2)
    {
        let result = "";
        let n1 = str1.length, n2 = str2.length;

        // Compare str1 and str2
        for (let i = 0, j = 0; i <= n1 - 1 && j <= n2 - 1; i++, j++) {
            if (str1[i] != str2[j]) {
                break;
            }
            result += str1[i];
        }

        return (result);
    }

    // A Function that returns the longest common prefix
// from the array of strings
    function commonPrefix(arr,n)
    {
        // sorts the N set of strings
        arr.sort();

        // prints the common prefix of the first and the
        // last String of the set of strings
        document.write(commonPrefixUtil(arr[0], arr[n - 1])+"<br>");
    }

    // Driver Code

    let arr=["geeksforgeeks", "geeks",
            "geek", "geezer"];

    let n = arr.length;

    commonPrefix(arr, n);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
gee
```

**时间复杂度:** O(N * log N)