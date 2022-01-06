# 最长回文子串|集合 2

> 原文:[https://www . geesforgeks . org/long-回文-substring-set-2/](https://www.geeksforgeeks.org/longest-palindromic-substring-set-2/)

给定一个字符串，找出最长的子字符串，即回文。
**例如:**

```
Input: Given string :"forgeeksskeegfor", 
Output: "geeksskeeg".

Input: Given string :"Geeks", 
Output: "ee".
```

**方法:**动态规划解决方案已经在[之前的帖子](https://www.geeksforgeeks.org/longest-palindrome-substring-set-1/)中讨论过了。基于动态规划的解决方案的时间复杂度是 O(n^2 ),并且它需要 O(n^2 的额外空间。我们可以在(n^2)时间内用 O(1)个额外的空间找到最长的回文子串。

1.  这个想法是生成所有偶数长度和奇数长度的回文，并跟踪到目前为止看到的最长的回文。
2.  为了生成奇数长度回文，固定一个中心，并在两个方向上展开较长的回文，即固定 i (index)为中心，两个 index 为 i1 = i+1 和 i2 = i-1
3.  比较 i1 和 i2，如果相等，则减少 i2，增加 i1，找到最大长度。
    用类似的技巧找到偶数长度的回文。
4.  取两个索引 i1 = i 和 i2 = i-1，比较 i1 和 i2 处的字符，找到最大长度，直到所有比较的字符对相等，并存储最大长度。
5.  打印最大长度。

## C++

```
// A O(n^2) time and O(1) space program to
// find the longest palindromic substring
#include <bits/stdc++.h>
using namespace std;

// A utility function to print
// a substring str[low..high]
// This function prints the
// longest palindrome substring (LPS)
// of str[]. It also returns the
// length of the longest palindrome
int longestPalSubstr(char* str)
{
    // The result (length of LPS)
    int maxLength = 1;

    int start = 0;
    int len = strlen(str);

    int low, high;

    // One by one consider every
    // character as center point of
    // even and length palindromes
    for (int i = 1; i < len; ++i) {
        // Find the longest even length palindrome
        // with center points as i-1 and i.
        low = i - 1;
        high = i;
        while (low >= 0 && high < len
               && str[low] == str[high]) {
            --low;
            ++high;
        }

          // Move back to the last possible valid palindrome substring
        // as that will anyway be the longest from above loop
        ++low; --high;
          if (str[low] == str[high] && high - low + 1 > maxLength) {
            start = low;
              maxLength = high - low + 1;
        }

        // Find the longest odd length
        // palindrome with center point as i
        low = i - 1;
        high = i + 1;
        while (low >= 0 && high < len
               && str[low] == str[high]) {
            --low;
            ++high;
        }

        // Move back to the last possible valid palindrome substring
          // as that will anyway be the longest from above loop
        ++low; --high;
          if (str[low] == str[high] && high - low + 1 > maxLength) {
            start = low;
              maxLength = high - low + 1;
        }
    }

    cout << "Longest palindrome substring is: ";
    int ans=maxlength; 
    while(ans--)
      cout<<str[start++];

      return maxLength;
}

// Driver program to test above functions
int main()
{
    char str[] = "forgeeksskeegfor";
    cout << "\nLength is: "
         << longestPalSubstr(str)
         << endl;
    return 0;
}

// This is code is contributed by rathbhupendra
```

## C

```
// A O(n^2) time and O(1) space
// program to find the longest
// palindromic substring
#include <stdio.h>
#include <string.h>

// A utility function to print
// a substring str[low..high]
void printSubStr(char* str, int low, int high)
{
    for (int i = low; i <= high; ++i)
        printf("%c", str[i]);
}

// This function prints the longest
// palindrome substring (LPS)
// of str[]. It also returns the
// length of the longest palindrome
int longestPalSubstr(char* str)
{

    // The result (length of LPS)
    int maxLength = 1;

    int start = 0;
    int len = strlen(str);

    int low, high;

    // One by one consider every
    // character as center point of
    // even and length palindromes
    for (int i = 1; i < len; ++i) {
        // Find the longest even length
        // palindrome with center points
        // as i-1 and i.
        low = i - 1;
        high = i;
        while (low >= 0 && high < len
               && str[low] == str[high]) {
            --low;
            ++high;
        }

          // Move back to the last possible valid palindrom substring
        // as that will anyway be the longest from above loop
        ++low; --high;
          if (str[low] == str[high] && high - low + 1 > maxLength) {
            start = low;
              maxLength = high - low + 1;
        }

        // Find the longest odd length
        // palindrome with center point as i
        low = i - 1;
        high = i + 1;
        while (low >= 0 && high < len
               && str[low] == str[high]) {
            --low;
            ++high;
        }

          // Move back to the last possible valid palindrom substring
        // as that will anyway be the longest from above loop
        ++low; --high;
          if (str[low] == str[high] && high - low + 1 > maxLength) {
            start = low;
              maxLength = high - low + 1;
        }
    }

    printf("Longest palindrome substring is: ");
    printSubStr(str, start, start + maxLength - 1);

    return maxLength;
}

// Driver program to test above functions
int main()
{
    char str[] = "forgeeksskeegfor";
    printf("\nLength is: %d", longestPalSubstr(str));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of O(n^2)
// time and O(1) space method
// to find the longest palindromic substring
public class LongestPalinSubstring {
    // A utility function to print
    // a substring str[low..high]
    static void printSubStr(String str,
                            int low, int high)
    {
        System.out.println(
            str.substring(
                low, high + 1));
    }

    // This function prints the
    // longest palindrome substring
    // (LPS) of str[]. It also
    // returns the length of the
    // longest palindrome
    static int longestPalSubstr(String str)
    {
        // The result (length of LPS)
        int maxLength = 1;

        int start = 0;
        int len = str.length();

        int low, high;

        // One by one consider every
        // character as center
        // point of even and length
        // palindromes
        for (int i = 1; i < len; ++i) {
            // Find the longest even
            // length palindrome with
            // center points as i-1 and i.
            low = i - 1;
            high = i;
            while (low >= 0 && high < len
                   && str.charAt(low)
                          == str.charAt(high)) {
                --low;
                ++high;
            }

              // Move back to the last possible valid palindrom substring
            // as that will anyway be the longest from above loop
            ++low; --high;
            if (str.charAt(low) == str.charAt(high) && high - low + 1 > maxLength) {
                start = low;
                maxLength = high - low + 1;
            }

            // Find the longest odd length
            // palindrome with center point as i
            low = i - 1;
            high = i + 1;
            while (low >= 0 && high < len
                   && str.charAt(low)
                          == str.charAt(high)) {
                --low;
                ++high;
            }

              // Move back to the last possible valid palindrom substring
            // as that will anyway be the longest from above loop
            ++low; --high;
            if (str.charAt(low) == str.charAt(high) && high - low + 1 > maxLength) {
                start = low;
                maxLength = high - low + 1;
            }
        }

        System.out.print("Longest palindrome substring is: ");
        printSubStr(str, start, start + maxLength - 1);

        return maxLength;
    }

    // Driver program to test above function
    public static void main(String[] args)
    {

        String str = "forgeeksskeegfor";
        System.out.println("Length is: " + longestPalSubstr(str));
    }
}
// This code is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# A O(n ^ 2) time and O(1) space program to find the
# longest palindromic substring

# This function prints the longest palindrome substring (LPS)
# of str[]. It also returns the length of the longest palindrome

def longestPalSubstr(string):
    maxLength = 1

    start = 0
    length = len(string)

    low = 0
    high = 0

    # One by one consider every character as center point of
    # even and length palindromes
    for i in xrange(1, length):
        # Find the longest even length palindrome with center
        # points as i-1 and i.
        low = i - 1
        high = i
        while low >= 0 and high < length and string[low] == string[high]:
            low -= 1
            high += 1

        # Move back to the last possible valid palindrom substring
        # as that will anyway be the longest from above loop
        low += 1
        high -= 1
        if string[low] == string[high] and high - low + 1 > maxLength:
          start = low
          maxLength = high - low + 1

        # Find the longest odd length palindrome with center
        # point as i
        low = i - 1
        high = i + 1
        while low >= 0 and high < length and string[low] == string[high]:
            low -= 1
            high += 1

        # Move back to the last possible valid palindrom substring
        # as that will anyway be the longest from above loop
        low += 1
        high -= 1
        if string[low] == string[high] and high - low + 1 > maxLength:
          start = low
          maxLength = high - low + 1

    print "Longest palindrome substring is:",
    print string[start:start + maxLength]

    return maxLength

# Driver program to test above functions
string = "forgeeksskeegfor"
print "Length is: " + str(longestPalSubstr(string))

# This code is contributed by BHAVYA JAIN
```

## C#

```
// C# implementation of O(n^2) time
// and O(1) space method to find the
// longest palindromic substring
using System;

class GFG {
    // A utility function to print
    // a substring str[low..high]
    public static void printSubStr(string str,
                                   int low, int high)
    {
        Console.WriteLine(str.Substring(low,
                                        (high + 1) - low));
    }

    // This function prints the longest
    // palindrome substring (LPS) of str[].
    // It also returns the length of the
    // longest palindrome
    public static int longestPalSubstr(string str)
    {
        int maxLength = 1; // The result (length of LPS)

        int start = 0;
        int len = str.Length;

        int low, high;

        // One by one consider every
        // character as center point
        // of even and length palindromes
        for (int i = 1; i < len; ++i) {
            // Find the longest even length
            // palindrome with center points
            // as i-1 and i.
            low = i - 1;
            high = i;
            while (low >= 0 && high < len && str[low] == str[high]) {
                --low;
                ++high;
            }

              // Move back to the last possible valid palindrom substring
            // as that will anyway be the longest from above loop
            ++low; --high;
            if (str[low] == str[high] && high - low + 1 > maxLength) {
                start = low;
                maxLength = high - low + 1;
            }

            // Find the longest odd length
            // palindrome with center point as i
            low = i - 1;
            high = i + 1;
            while (low >= 0 && high < len && str[low] == str[high]) {
                --low;
                ++high;
            }

              // Move back to the last possible valid palindrom substring
            // as that will anyway be the longest from above loop
            ++low; --high;
            if (str[low] == str[high] && high - low + 1 > maxLength) {
                start = low;
                maxLength = high - low + 1;
            }
        }

        Console.Write("Longest palindrome substring is: ");
        printSubStr(str, start, start + maxLength - 1);

        return maxLength;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        string str = "forgeeksskeegfor";
        Console.WriteLine("Length is: " + longestPalSubstr(str));
    }
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A O(n^2) time and O(1) space program to find the longest palindromic substring

// A utility function to print a substring str[low..high]
function printSubStr($str, $low, $high)
{
    for( $i = $low; $i <= $high; ++$i )
        echo $str[$i];
}

// This function prints the longest palindrome substring (LPS)
// of str[]. It also returns the length of the longest palindrome
function longestPalSubstr($str)
{
    $maxLength = 1;  // The result (length of LPS)

    $start = 0;
    $len = strlen($str);

    // One by one consider every character as center point of
    // even and length palindromes
    for ($i = 1; $i < $len; ++$i)
    {
        // Find the longest even length palindrome with center points
        // as i-1 and i. 
        $low = $i - 1;
        $high = $i;
        while ($low >= 0 && $high < $len && $str[$low] == $str[$high])
        {
            --$low;
            ++$high;
        }

        ++$low;
        --$high;
          if ($str[$low] == $str[$high] && $high - $low + 1 > $maxLength)
        {
            $start = $low;
            $maxLength = $high - $low + 1;
        }

        // Find the longest odd length palindrome with center
        // point as i
        $low = $i - 1;
        $high = $i + 1;
        while ($low >= 0 && $high < $len && $str[$low] == $str[$high])
        {
            --$low;
            ++$high;
        }

        ++$low;
        --$high;
          if ($str[$low] == $str[$high] && $high - $low + 1 > $maxLength)
        {
            $start = $low;
            $maxLength = $high - $low + 1;
        }
    }

    echo "Longest palindrome substring is: ";
    printSubStr($str, $start, $start + $maxLength - 1);

    return $maxLength;
}

// Driver program to test above functions

$str = "forgeeksskeegfor";
echo "\nLength is: ". longestPalSubstr( $str ) ;
return 0;
?>
```

## java 描述语言

```
<script>
// Javascript implementation of O(n^2)
// time and O(1) space method
// to find the longest palindromic substring

    // A utility function to print
    // a substring str[low..high]
    function printSubStr(str, low, high)
    {
        document.write(str.substring(low, high + 1)+"<br>");
    }

    // This function prints the
    // longest palindrome substring
    // (LPS) of str[]. It also
    // returns the length of the
    // longest palindrome
    function longestPalSubstr(str)
    {
        // The result (length of LPS)
        let maxLength = 1;
        let start = 0;
        let len = str.length;
        let low, high;

        // One by one consider every
        // character as center
        // point of even and length
        // palindromes
        for (let i = 1; i < len; ++i)
        {
            // Find the longest even
            // length palindrome with
            // center points as i-1 and i.
            low = i - 1;
            high = i;
            while (low >= 0 && high < len
                   && str[low] == str[high]) {
                --low;
                ++high;
            }

             ++low;
            --high;
             if (str[low] == str[high] && high - low + 1 > maxLength) {
                start = low;
                maxLength = high - low + 1;
            }

            // Find the longest odd length
            // palindrome with center point as i
            low = i - 1;
            high = i + 1;
            while (low >= 0 && high < len
                   && str[low] == str[high]) {
                --low;
                ++high;
            }

            ++low;
            --high;
             if (str[low] == str[high] && high - low + 1 > maxLength) {
                start = low;
                maxLength = high - low + 1;
            }
        }

        document.write("Longest palindrome substring is: ");
        printSubStr(str, start, start + maxLength - 1);
        return maxLength;
    }

    // Driver program to test above function
    let str = "forgeeksskeegfor";
    document.write("Length is: " + longestPalSubstr(str));

    // This code is contributed by rag2127
</script>
```

**输出:**

```
Longest palindrome substring is: geeksskeeg
Length is: 10
```

**复杂度分析:**

*   **时间复杂度:** O(n^2)，其中 n 是输入字符串的长度。
    需要字符串的嵌套遍历。所以时间复杂性就是 O(n^2).
*   **辅助空间:** O(1)。
    不需要额外的空间。

如果你发现任何不正确的地方，请写评论，或者对上面讨论的主题有更多的信息。