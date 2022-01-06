# 给定字典顺序的字典序最大字符串

> 原文:[https://www . geesforgeks . org/字典顺序最大字符串/](https://www.geeksforgeeks.org/lexicographically-largest-string-for-given-dictionary-order/)

给定一个由 **N** 根弦组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个表示弦的新字母顺序的弦**顺序**。任务是根据给定的顺序找到字典中最大的字符串。

**示例:**

> **输入:**a[]= {“abc”、“abd”、“abz”}，顺序=“abczdefghijklmnopqrstuvwxy”
> **输出:** abd
> **说明:**
> 比较两个字“ABC”、“abd”，顺序中第一个不匹配的字符是 c、d，c 排在 d 之前所以其中 abd 最大。
> 同样，比较 abd 和 abz。
> 
> **输入:**arr[]= {“ABC”、“abdz”、“Abd”}，订单=“abcdefghijklmnopqrstuvwxyz”
> **输出:** abdz
> **说明:**
> 在所有给定的字符串中，abdz 最大。

**天真方法:**想法是检查每个[字符串是否在给定字符串](https://www.geeksforgeeks.org/lexicographically-largest-string-formed-from-the-characters-in-range-l-and-r/)中按词典顺序最大。如果是，则打印该字符串，否则检查下一个字符串。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**思路是实现一个[比较器函数](https://www.geeksforgeeks.org/comparator-interface-java/)根据给定的字符串顺序找到字典上最大的字符串。以下是步骤:

1.  创建一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，以给定的字符串顺序存储字符的索引。
2.  将数组的第一个字符串视为字典中最大的字符串**和**。
3.  现在遍历范围**【1，N】**中的给定字符串，并使用存储在地图中的索引将每个字符串与字符串**和**进行比较。
4.  继续更新上面步骤中最大的字典式字符串，并打印该字符串。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h> 
using namespace std; 

int compare(string word1, string word2,
            int order[]);

// Find the lexicographically
// largest string
string largestString(string a[], int n,
                     string order)
{

    // Create a map of characters
    int map[26];

    // Value of each character is
    // string is given priority
    // according to their occurence
    // in the string
    for(int i = 0; i < order.length(); i++)
        map[order[i] - 'a'] = i;

    // Take first String as maximum
    string ans = a[0];

    for(int i = 1; i < n; i++)
    {

        // Compare two strings each time
        if (compare(ans, a[i], map) < 0)

            // Update answer
            ans = a[i];
    }
    return ans;
}

// Implement compare function
// to get the dictionary order
int compare(string word1, string word2,
            int order[])
{
    int i = 0, j = 0, charcompareval = 0;

    while (i < word1.length() &&
           j < word2.length())
    {

        // Compare each char
        // according to the order
        charcompareval = order[word1[i] - 'a'] -
                         order[word2[i] - 'a'];

        // Find the first non matching
        // character in the string
        if (charcompareval != 0)
            return charcompareval;

        i++;
        j++;
    }

    // If one word is prefix of
    // other return shortest word
    if (charcompareval == 0)
        return (word1.length() -
                word2.length());
    else
        return charcompareval;
}

// Driver Code
int main()
{
    int n = 3;

    // Given array of strings arr
    string arr[] = { "abc", "abd", "abz" };

    // Given order of string
    string order = "abczdefghijklmnopqrstuvwxy";

    // Function call
    string ans = largestString(arr, n, order);

    cout << ans;

    return 0;
}

// This code is contributed by rutvik_56
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;
public class Main {

    // Find the lexicographically
    // largest string
    public static String
    largestString(String[] a, int n,
                String order)
    {
        // Create a map of characters
        int map[] = new int[26];

        // Value of each character is
        // string is given priority
        // according to their occurence
        // in the string
        for (int i = 0; i < order.length(); i++)
            map[order.charAt(i) - 'a'] = i;

        // Take first String as maximum
        String ans = a[0];

        for (int i = 1; i < n; i++) {

            // Compare two strings each time
            if (compare(ans, a[i], map) < 0)

                // Update answer
                ans = a[i];
        }
        return ans;
    }

    // Implement compare function
    // to get the dictionary order
    public static int
    compare(String word1, String word2,
            int[] order)
    {
        int i = 0, j = 0, charcompareval = 0;

        while (i < word1.length()
            && j < word2.length()) {

            // Compare each char
            // according to the order
            charcompareval
                = order[word1.charAt(i) - 'a']
                - order[word2.charAt(i) - 'a'];

            // Find the first non matching
            // character in the string
            if (charcompareval != 0)

                return charcompareval;
            i++;
            j++;
        }

        // If one word is prefix of
        // other return shortest word
        if (charcompareval == 0)
            return (word1.length()
                    - word2.length());
        else
            return charcompareval;
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 3;

        // Given array of strings arr
        String arr[] = { "abc", "abd", "abz" };

        // Given order of string
        String order
            = "abczdefghijklmnopqrstuvwxy";

        // Function call
        String ans
            = largestString(arr, n, order);

        System.out.println(ans);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Find the lexicographically
# largest string
def largestString(a, n, order):

    # Create a map of characters
    map = [0] * 26

    # Value of each character is
    # string is given priority
    # according to their occurence
    # in the string
    for i in range(len(order)):
            map[ord(order[i]) - ord('a')] = i

    # Take first String as maximum
    ans = a[0]

    for i in range(1, n):

        # Compare two strings each time
        if (compare(ans, a[i], map) < 0):

            # Update answer
            ans = a[i]

    return ans

# Implement compare function
# to get the dictionary order
def compare(word1, word2, order):

    i = 0
    j = 0
    charcompareval = 0;

    while (i < len(word1) and
        j < len(word2)):

        # Compare each char
        # according to the order
        charcompareval = (order[ord(word1[i]) - ord('a')] -
                        order[ord(word2[i]) - ord('a')])

        # Find the first non matching
        # character in the string
        if (charcompareval != 0):
            return charcompareval

        i += 1
        j += 1

    # If one word is prefix of
    # other return shortest word
    if (charcompareval == 0):
        return (len(word1) - len(word2))
    else:
        return charcompareval

# Driver Code
if __name__ == "__main__":

    n = 3

    # Given array of strings arr
    arr = [ "abc", "abd", "abz" ]

    # Given order of string
    order = "abczdefghijklmnopqrstuvwxy"

    # Function call
    ans = largestString(arr, n, order)

    print(ans)

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Find the lexicographically
// largest string
public static String largestString(String[] a, int n,
                                    String order)
{
    // Create a map of characters
    int []map = new int[26];

    // Value of each character is
    // string is given priority
    // according to their occurence
    // in the string
    for (int i = 0; i < order.Length; i++)
    map[order[i] - 'a'] = i;

    // Take first String as maximum
    String ans = a[0];

    for (int i = 1; i < n; i++)
    {

    // Compare two strings each time
    if (compare(ans, a[i], map) < 0)

        // Update answer
        ans = a[i];
    }
    return ans;
}

// Implement compare function
// to get the dictionary order
public static int compare(String word1,
                            String word2,
                            int[] order)
{
    int i = 0, j = 0, charcompareval = 0;

    while (i < word1.Length &&
        j < word2.Length)
    {

    // Compare each char
    // according to the order
    charcompareval = order[word1[i] - 'a'] -
                    order[word2[i] - 'a'];

    // Find the first non matching
    // character in the string
    if (charcompareval != 0)

        return charcompareval;
    i++;
    j++;
    }

    // If one word is prefix of
    // other return shortest word
    if (charcompareval == 0)
    return (word1.Length -
            word2.Length);
    else
    return charcompareval;
}

// Driver Code
public static void Main(String []args)
{
    int n = 3;

    // Given array of strings arr
    String []arr = { "abc", "abd", "abz" };

    // Given order of string
    String order = "abczdefghijklmnopqrstuvwxy";

    // Function call
    String ans = largestString(arr, n, order);

    Console.WriteLine(ans);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascriptam for the above approach

// Find the lexicographically
// largest string
function largestString(a, n, order)
{

    // Create a map of characters
    let map = new Array(26);

    // Value of each character is
    // string is given priority
    // according to their occurence
    // in the string
    for(let i = 0; i < order.length; i++)
        map[order[i].charCodeAt(0) -
                 'a'.charCodeAt(0)] = i;

    // Take first String as maximum
    let ans = a[0];

    for(let i = 1; i < n; i++)
    {

        // Compare two strings each time
        if (compare(ans, a[i], map) < 0)

            // Update answer
            ans = a[i];
    }
    return ans;
}

// Implement compare function
// to get the dictionary order
function compare(word1, word2, order)
{
    let i = 0, j = 0, charcompareval = 0;

        while (i < word1.length &&
               j < word2.length)
        {

            // Compare each char
            // according to the order
            charcompareval = order[word1[i].charCodeAt(0) -
                                        'a'.charCodeAt(0)] -
                             order[word2[i].charCodeAt(0) -
                                        'a'.charCodeAt(0)];

            // Find the first non matching
            // character in the string
            if (charcompareval != 0)
                return charcompareval;

            i++;
            j++;
        }

        // If one word is prefix of
        // other return shortest word
        if (charcompareval == 0)
            return (word1.length - word2.length);
        else
            return charcompareval;
}

// Driver Code
let n = 3;
let arr = [ "abc", "abd", "abz" ];
let order = "abczdefghijklmnopqrstuvwxy";
let ans = largestString(arr, n, order);

document.write(ans);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
abd
```

***时间复杂度:**O(N * max _ word _ length)*
***辅助** **空间:** O(1)*