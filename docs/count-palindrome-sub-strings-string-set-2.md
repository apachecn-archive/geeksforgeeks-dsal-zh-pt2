# 统计一个字符串中所有回文子字符串|集合 2

> 原文:[https://www . geesforgeks . org/count-回文-子字符串-字符串-set-2/](https://www.geeksforgeeks.org/count-palindrome-sub-strings-string-set-2/)

给定一个字符串，任务是统计给定字符串中的所有回文子串。回文子串的长度大于或等于 2。

```
Examples:
Input : str = "abaab"
Output: 3
Explanation : 
All palindrome substring are :
 "aba", "aa", "baab" 

Input : str = "abbaeae"
Output: 4
Explanation : 
All palindrome substring are : 
"bb", "abba", "aea", "eae":
```

我们已经在下面的帖子中讨论了一个基于动态编程的解决方案。
[统计一个串中所有回文子串|集合 1](https://www.geeksforgeeks.org/count-palindrome-sub-strings-string/)
这里讨论的解决方案是[最长回文子串问题](https://www.geeksforgeeks.org/longest-palindrome-substring-set-1/)的扩展。这个想法是，对于给定输入字符串中的每个字符，我们将其视为回文的中点，并在两个方向上展开它，以找到所有偶数和奇数长度的回文。我们使用 hashmap 来跟踪所有长度大于 1 的不同回文，并返回包含所有可能的回文子串的映射大小。
c++实现如下。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to count all distinct palindromic
// substrings of a string.
#include <bits/stdc++.h>
using namespace std;

// Returns total number of palindrome substring of
// length greater than equal to 2
int countPalindromes(string s)
{
    unordered_map<string, int> m;
    for (int i = 0; i < s.length(); i++) {

        // check for odd length palindromes
        for (int j = 0; j <= i; j++) {

            if (!s[i + j])
                break;

            if (s[i - j] == s[i + j]) {

                // check for palindromes of length
                // greater than 1
                if ((i + j + 1) - (i - j) > 1)
                    m[s.substr(i - j,
                        (i + j + 1) - (i - j))]++;

            } else
                break;
        }

        // check for even length palindromes
        for (int j = 0; j <= i; j++) {
            if (!s[i + j + 1])
                break;
            if (s[i - j] == s[i + j + 1]) {

                // check for palindromes of length
                // greater than 1
                if ((i + j + 2) - (i - j) > 1)
                    m[s.substr(i - j,
                         (i + j + 2) - (i - j))]++;

            } else
                break;
        }
    }
    return m.size();
}

// Driver code
int main()
{
    string s = "abbaeae";
    cout << countPalindromes(s) << endl;
    return 0;
}
```

输出:

```
4
```

时间复杂度 O(n)<sup>2</sup>)
辅助空间 O(n)
我们可以轻松扩展这个解决方案，也可以打印所有回文子串。我们只需要遍历地图 m 并打印其内容。
**另一种方法是使用** [**Java 字符串类**](https://www.geeksforgeeks.org/string-class-in-java/) **，这样做，**

1.  子串循环两次，使用 [substring()](https://www.geeksforgeeks.org/substring-in-java/) 方法获取一个字符串的子串。
2.  使用 StringBuffer 类方法反向子字符串[反向()](https://www.geeksforgeeks.org/stringbuffer-reverse-method-in-java/)
3.  检查带有子串和反向子串的回文
4.  如果是回文，递增计数，最后返回计数

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to count palindrome substring
// in a string
public class PalindromeSubstring {

    // Method which return count palindrome substring
    static int countPS(String str){
        String temp = "";
        StringBuffer stf;
        int count = 0;
        // Iterate the loop twice
        for (int i = 0; i < str.length(); i++) {
            for (int j = i + 1; j <= str.length(); j++) {
                // Get each substring
                temp = str.substring(i, j);

                // If length is greater than or equal to two
                // Check for palindrome   
                if (temp.length() >= 2) {
                    // Use StringBuffer class to reverse the string
                    stf = new StringBuffer(temp);
                    stf.reverse();
                    // Compare substring with reverse of substring
                    if (stf.toString().compareTo(temp) == 0)
                        count++;
                }
            }
        }
        // return the count
        return count;
    }

    // Driver Code
    public static void main(String args[]) throws Exception {
        // Declare and initialize the string
        String str = "abbaeae";
        // Call the method
        System.out.println(countPS(str));
    }
} // This code is contributes by hungundji
```

## C#

```
// C# Program to count palindrome substring
// in a string
using System;

class GFG
{

    // Method which return count palindrome substring
    static int countPS(String str)
    {
        String temp = "";
        String stf;
        int count = 0;

        // Iterate the loop twice
        for (int i = 0; i < str.Length; i++)
        {
            for (int j = i + 1;
                     j <= str.Length; j++)
            {
                // Get each substring
                temp = str.Substring(i, j-i);

                // If length is greater than or equal to two
                // Check for palindrome
                if (temp.Length >= 2)
                {
                    // Use StringBuffer class to reverse
                    // the string
                    stf = temp;
                    stf = reverse(temp);

                    // Compare substring with reverse of substring
                    if (stf.ToString().CompareTo(temp) == 0)
                        count++;
                }
            }
        }

        // return the count
        return count;
    }

    static String reverse(String input)
    {
        char[] a = input.ToCharArray();
        int l, r = 0;
        r = a.Length - 1;

        for (l = 0; l < r; l++, r--)
        {
            // Swap values of l and r
            char temp = a[l];
            a[l] = a[r];
            a[r] = temp;
        }
        return String.Join("",a);
    }

    // Driver Code
    public static void Main(String []args)
    {
        // Declare and initialize the string
        String str = "abbaeae";

        // Call the method
        Console.WriteLine(countPS(str));
    }
}

// This code is contributed by Rajput-Ji
```

**Output:** 

```
4
```

时间复杂度 O(n)<sup>2</sup>)
辅助空间 O(n)
本文由**安库尔·辛格**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。