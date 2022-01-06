# 字典最小字符串旋转|设置 1

> 原文:[https://www . geesforgeks . org/词典学-最小字符串-旋转/](https://www.geeksforgeeks.org/lexicographically-minimum-string-rotation/)

编写代码来查找循环数组中的字典序最小值，例如，对于 BCABDADAB 数组，字典序最小值是 ABBCABDAD。
来源:谷歌笔试
更多示例:

```
Input:  GEEKSQUIZ
Output: EEKSQUIZG

Input:  GFG
Output: FGG

Input:  GEEKSFORGEEKS
Output: EEKSFORGEEKSG
```

下面是一个简单的解决方案。让给定的字符串为“str”
1)将“str”与其自身连接起来，并存储在一个临时字符串中，比如“concat”。
2)创建一个字符串数组来存储“字符串”的所有旋转。让数组为“arr”。
3)通过在索引 0、1、2 处获取“concat”的子串，找到“str”的所有旋转..n-1。将这些旋转存储在 arr[]中
4)排序 arr[]并返回 arr[0]。

以下是上述解决方案的实现。

## C++

```
// A simple C++ program to find lexicographically minimum rotation
// of a given string
#include <iostream>
#include <algorithm>
using namespace std;

// This functionr return lexicographically minimum
// rotation of str
string minLexRotation(string str)
{
    // Find length of given string
    int n = str.length();

    // Create an array of strings to store all rotations
    string arr[n];

    // Create a concatenation of string with itself
    string concat = str + str;

    // One by one store all rotations of str in array.
    // A rotation is obtained by getting a substring of concat
    for (int i = 0; i < n; i++)
        arr[i] = concat.substr(i, n);

    // Sort all rotations
    sort(arr, arr+n);

    // Return the first rotation from the sorted array
    return arr[0];
}

// Driver program to test above function
int main()
{
    cout << minLexRotation("GEEKSFORGEEKS") << endl;
    cout << minLexRotation("GEEKSQUIZ") << endl;
    cout << minLexRotation("BCABDADAB") << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple Java program to find
// lexicographically minimum rotation
// of a given String
import java.util.*;

class GFG
{

    // This functionr return lexicographically
    // minimum rotation of str
    static String minLexRotation(String str)
    {
        // Find length of given String
        int n = str.length();

        // Create an array of strings
        // to store all rotations
        String arr[] = new String[n];

        // Create a concatenation of
        // String with itself
        String concat = str + str;

        // One by one store all rotations
        // of str in array. A rotation is
        // obtained by getting a substring of concat
        for (int i = 0; i < n; i++)
        {
            arr[i] = concat.substring(i, i + n);
        }

        // Sort all rotations
        Arrays.sort(arr);

        // Return the first rotation
        // from the sorted array
        return arr[0];
    }

    // Driver code
    public static void main(String[] args)
    {
        System.out.println(minLexRotation("GEEKSFORGEEKS"));
        System.out.println(minLexRotation("GEEKSQUIZ"));
        System.out.println(minLexRotation("BCABDADAB"));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# A simple Python3 program to find lexicographically
# minimum rotation of a given string

# This function return lexicographically minimum
# rotation of str
def minLexRotation(str_) :

    # Find length of given string
    n = len(str_)

    # Create an array of strings to store all rotations
    arr = [0] * n

    # Create a concatenation of string with itself
    concat = str_ + str_

    # One by one store all rotations of str in array.
    # A rotation is obtained by getting a substring of concat
    for i in range(n) :
        arr[i] = concat[i : n + i]

    # Sort all rotations
    arr.sort()

    # Return the first rotation from the sorted array
    return arr[0]

# Driver Code
print(minLexRotation("GEEKSFORGEEKS"))
print(minLexRotation("GEEKSQUIZ"))
print(minLexRotation("BCABDADAB"))

# This code is contributed by divyamohan123
```

## C#

```
// A simple C# program to find
// lexicographically minimum rotation
// of a given String
using System;

class GFG
{

    // This functionr return lexicographically
    // minimum rotation of str
    static String minLexRotation(String str)
    {
        // Find length of given String
        int n = str.Length;

        // Create an array of strings
        // to store all rotations
        String []arr = new String[n];

        // Create a concatenation of
        // String with itself
        String concat = str + str;

        // One by one store all rotations
        // of str in array. A rotation is
        // obtained by getting a substring of concat
        for (int i = 0; i < n; i++)
        {
            arr[i] = concat.Substring(i, n);
        }

        // Sort all rotations
        Array.Sort(arr);

        // Return the first rotation
        // from the sorted array
        return arr[0];
    }

    // Driver code
    public static void Main(String[] args)
    {
        Console.WriteLine(minLexRotation("GEEKSFORGEEKS"));
        Console.WriteLine(minLexRotation("GEEKSQUIZ"));
        Console.WriteLine(minLexRotation("BCABDADAB"));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// A simple Javascript program to find
// lexicographically minimum rotation
// of a given String

// This functionr return lexicographically
// minimum rotation of str
function minLexRotation(str)
{

    // Find length of given String
    let n = str.length;

    // Create an array of strings
    // to store all rotations
    let arr = new Array(n);

    // Create a concatenation of
    // String with itself
    let concat = str + str;

    // One by one store all rotations
    // of str in array. A rotation is
    // obtained by getting a substring of concat
    for(let i = 0; i < n; i++)
    {
        arr[i] = concat.substring(i, i + n);
    }

    // Sort all rotations
    arr.sort();

    // Return the first rotation
    // from the sorted array
    return arr[0];
}

// Driver code
document.write(minLexRotation("GEEKSFORGEEKS") + "</br>");
document.write(minLexRotation("GEEKSQUIZ") + "</br>");
document.write(minLexRotation("BCABDADAB") + "</br>");

// This code is contributed by divyeshrabadiya07

</script>
```

**输出:**

```
EEKSFORGEEKSG
EEKSQUIZG
ABBCABDAD
```

[字典序最小旋转序列|集合 2](https://www.geeksforgeeks.org/lexicographically-smallest-rotated-sequence-set-2/)
在假设我们已经使用了 O(nLogn)排序算法的情况下，上述解的时间复杂度为 O(n <sup>2</sup> Logn)。
这个问题可以使用更高效的方法来解决，比如[布斯算法](http://en.wikipedia.org/wiki/Lexicographically_minimal_string_rotation#Booth.27s_Algorithm)，它在 O(n)时间内解决了这个问题。我们很快将把这些方法作为单独的文章进行介绍。
本文由 Abhishek 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。