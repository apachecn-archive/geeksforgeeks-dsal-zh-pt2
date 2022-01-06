# 字典上最小的字符串，其与给定字符串的汉明距离正好为 K

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列-最小-字符串-其-汉明距离-给定-字符串-精确-k/](https://www.geeksforgeeks.org/lexicographically-smallest-string-whose-hamming-distance-given-string-exactly-k/)

给定一个长度为 **N** 的小写字符串 **A** 和一个整数 **K** ，找到与 A 长度相同的字典最小字符串 B，使得 A 和 B 之间的[汉明距离](https://www.geeksforgeeks.org/hamming-distance-two-strings/)正好为 K。
**示例:**

```
Input : A = "pqrs", k = 1.
Output : aqrs
We can differ by at most one
character. So we put 'a' in the
beginning to make the result 
lexicographically smallest.

Input : A = "pqrs", k = 2.
Output : aars
```

我们从左到右开始，如果字符串 A 当前位置的字符是‘A’，那么我们把字符串 B 的当前位置赋给字符‘A’。这个位置不会增加汉明距离。如果 A 中这个位置的字符不等于‘A’，那么我们也将分配字符串 B 的当前位置字符‘A’，现在这将有助于汉明距离，并且这最多可以做 K 次，因为汉明距离必须等于 K，如果这已经做了 K 次，我们将分配 B 的这个位置与 A 相同的字符。
如果在前一步之后，A 和 B 之间的汉明距离是 K， 我们完成了，否则我们必须对 B 进行更多的更改。现在我们将在 B 中从右向左开始，如果当前位置的字符等于 A 的相应字符，则将 B 的字符更改为“B”，从而将汉明距离增加一，我们将一直这样做，直到汉明距离等于 k。
下面是这种方法的实现:

## C++

```
// CPP program to find Lexicographically
// smallest string whose hamming distance
// from given string is exactly K
#include <bits/stdc++.h>
using namespace std;

// function to find Lexicographically
// smallest string with hamming distance k
void findString(string str, int n, int k)
{
    // If k is 0, output input string
    if (k == 0) {
        cout << str << endl;
        return;
    }

    // Copying input string into output
    // string
    string str2 = str;
    int p = 0;

    // Traverse all the character of the
    // string
    for (int i = 0; i < n; i++) {

        // If current character is not 'a'
        if (str2[i] != 'a') {

            // copy character 'a' to
            // output string
            str2[i] = 'a';
            p++;

            // If hamming distance became k,
            // break;
            if (p == k)
                break;
        }
    }

    // If k is less than p
    if (p < k) {

        // Traversing string in reverse
        // order
        for (int i = n - 1; i >= 0; i--)
            if (str[i] == 'a') {
                str2[i] = 'b';
                p++;

                if (p == k)
                    break;
            }
    }

    cout << str2 << endl;
}

// Driven Program
int main()
{
    string str = "pqrs";
    int n = str.length();
    int k = 2;

    findString(str, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Lexicographically
// smallest string whose hamming distance
// from given string is exactly K 

class GFG {

// function to find Lexicographically
// smallest string with hamming distance k
static void findString(String str, int n, int k)
{
    // If k is 0, output input string
    if (k == 0) {
                  System.out.println(str);;
        return;
    }

    // Copying input string into output
    // string
    String str2 = str;
    int p = 0;

    // Traverse all the character of the
    // string
    for (int i = 0; i < n; i++) {

        // If current character is not 'a'
        if (str2.charAt(i) != 'a') {

            // copy character 'a' to
            // output string
                        str2 = str2.substring(0,i)+'a'+str2.substring(i+1);
            //str2[i] = 'a';
            p++;

            // If hamming distance became k,
            // break;
            if (p == k)
                break;
        }
    }

    // If k is less than p
    if (p < k) {

        // Traversing string in reverse
        // order
        for (int i = n - 1; i >= 0; i--)
            if (str.charAt(i) == 'a') {
                                str2 = str2.substring(0,i)+'b'+str2.substring(i+1);
                p++;
                if (p == k)
                    break;
            }
    }

       System.out.println(str2);
}

// Driven Program
 public static void main(String[] args) {

        String str = "pqrs";
    int n = str.length();
    int k = 2;

    findString(str, n, k);

    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to find Lexicographically
# smallest string whose hamming distance
# from the given string is exactly K

# function to find Lexicographically
# smallest string with hamming distance k
def findString(str, n, k):

    # If k is 0, output input string
    if (k == 0):
        print(str)
        return

    # Copying input string into output
    # string
    str2 = str
    p = 0

    # Traverse all the character of the
    # string
    for i in range(0, n, 1):

        # If current character is not 'a'
        if (str2[i] != 'a'):

            # copy character 'a' to
            # output string
            str2 = str2.replace(str2[i], 'a')
            p += 1

            # If hamming distance became k,
            # break;
            if (p == k):
                break

    # If k is less than p
    if (p < k):

        # Traversing string in reverse
        # order
        i = n - 1
        while(i >= 0):
            if (str[i] == 'a'):
                str2 = str2.replace(str2[i], 'b')
                p += 1

            if (p == k):
                break
            i -= 1

    print(str2)

# Driver Code
if __name__ == '__main__':
    str = "pqrs"
    n = len(str)
    k = 2

    findString(str, n, k)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find Lexicographically
// smallest string whose hamming distance
// from given string is exactly K
using System;

class GFG
{

// function to find Lexicographically
// smallest string with hamming distance k
static void findString(String str,
                       int n, int k)
{
    // If k is 0, output input string
    if (k == 0)
    {
        Console.Write(str);;
        return;
    }

    // Copying input string into 
    // output string
    String str2 = str;
    int p = 0;

    // Traverse all the character 
    // of the string
    for (int i = 0; i < n; i++)
    {

        // If current character is not 'a'
        if (str2[i] != 'a')
        {

            // copy character 'a' to
            // output string
            str2 = str2.Substring(0, i) + 'a' +
                   str2.Substring(i + 1);
            //str2[i] = 'a';
            p++;

            // If hamming distance became k,
            // break;
            if (p == k)
                break;
        }
    }

    // If k is less than p
    if (p < k)
    {

        // Traversing string in reverse
        // order
        for (int i = n - 1; i >= 0; i--)
            if (str[i] == 'a')
            {
                str2 = str2.Substring(0, i) + 'b' +
                       str2.Substring(i + 1);
                p++;
                if (p == k)
                break;
            }
        }

    Console.Write(str2);
}

// Driver Code
public static void Main()
{
    String str = "pqrs";
    int n = str.Length;
    int k = 2;

    findString(str, n, k);
}
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find Lexicographically
// smallest string whose hamming distance
// from given string is exactly K

// function to find Lexicographically
// smallest string with hamming distance k
function findString($str, $n, $k)
{
    // If k is 0, output input string
    if ($k == 0)
    {
        echo $str . "\n";
        return;
    }

    // Copying input string into
    // output string
    $str2 = $str;
    $p = 0;

    // Traverse all the character
    // of the string
    for ($i = 0; $i < $n; $i++)
    {

        // If current character is not 'a'
        if ($str2[$i] != 'a')
        {

            // copy character 'a' to
            // output string
            $str2[$i] = 'a';
            $p++;

            // If hamming distance became k,
            // break;
            if ($p == $k)
                break;
        }
    }

    // If k is less than p
    if ($p < $k)
    {

        // Traversing string in reverse
        // order
        for ($i = $n - 1; $i >= 0; $i--)
            if ($str[$i] == 'a')
            {
                $str2[$i] = 'b';
                $p++;

                if ($p == $k)
                    break;
            }
    }

    echo $str2 . "\n";
}

// Driver Code
$str = "pqrs";
$n = strlen($str);
$k = 2;

findString($str, $n, $k);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// javascript program to find Lexicographically
// smallest string whose hamming distance
// from given string is exactly K 
// function to find Lexicographically
// smallest string with hamming distance k
function findString(str , n , k)
{
    // If k is 0, output input string
    if (k == 0) {
                  document.write(str);;
        return;
    }

    // Copying input string into output
    // string
    var str2 = str;
    var p = 0;

    // Traverse all the character of the
    // string
    for (i = 0; i < n; i++) {

        // If current character is not 'a'
        if (str2.charAt(i) != 'a') {

            // copy character 'a' to
            // output string
                        str2 = str2.substring(0,i)+'a'+str2.substring(i+1);
            //str2[i] = 'a';
            p++;

            // If hamming distance became k,
            // break;
            if (p == k)
                break;
        }
    }

    // If k is less than p
    if (p < k) {

        // Traversing string in reverse
        // order
        for (i = n - 1; i >= 0; i--)
            if (str.charAt(i) == 'a') {
                                str2 = str2.substring(0,i)+'b'+str2.substring(i+1);
                p++;
                if (p == k)
                    break;
            }
    }

       document.write(str2);
}

// Driven Program

var str = "pqrs";
var n = str.length;
var k = 2;

findString(str, n, k);

// This code is contributed by 29AjayKumar
</script>
```

**输出:**

```
aars
```

本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。