# 给定两个字符串中常见的最长前缀字谜长度

> 原文:[https://www . geesforgeks . org/最长前缀长度-给定两个字符串中常见的字谜/](https://www.geeksforgeeks.org/length-of-longest-prefix-anagram-which-are-common-in-given-two-strings/)

给定两个长度分别为 **N** 和 **M** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **str1** 和 **str2** ，任务是找出这两个字符串中前缀为[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)的最长[字谜](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/)字符串的长度。

**示例:**

> **输入:**str1 =“abaabcdezwer”，str2 =“caaabbttyh”
> **输出:** 6
> **解释:**
> 字符串 str 1 和 str 2 的长度 1 的前缀是“a”和“c”。
> 字符串 str1 和 str2 的长度 2 的前缀是“ab”和“ca”。
> 字符串 str1 和 str2 的长度 3 的前缀是“aba”和“caa”。
> 字符串 str1 和 str2 长度为 4 的前缀为“abaa”和“caaa”。
> 字符串 str1 和 str2 长度为 5 的前缀为“abaab”和“caaab”。
> 字符串 str1 和 str2 长度为 6 的前缀为“abaabc”和“caaabb”。
> 字符串 str1 和 str2 长度为 7 的前缀为“abaabcd”和“caaabbt”。
> 字符串 str1 和 str2 长度为 8 的前缀为“abaabcde”和“caaabbtt”。
> 字符串 str1 和 str2 长度为 9 的前缀为“abaabcdez”和“caaabbtty”。
> 字符串 str1 和 str2 长度为 10 的前缀为“abaabcdezz”和“caaabbttyh”。
> 长度为 6 的前缀只是相互之间的字谜。
> 
> **输入:**str 1 =“abcdef”，str 2 =“tuvwxyz”
> T3】输出: 0

**方法:**思路是用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)来解决上述问题。按照以下步骤解决问题:

*   初始化两个整数数组 **freq1[]** 和 **freq2[]** ，每个数组大小为 **26** ，分别存储字符串 **str1** 和 **str2** 中的字符数。
*   初始化一个变量，比如**和**，来存储结果。
*   [迭代出现在索引**【0，最小值(N-1，M-1)】**中的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)的字符，并执行以下操作:
    *   将**频率 Q1【】**阵列中 **str1[i]** 的计数和**频率 Q2【】**阵列中**str 2[I]**的计数增加 **1** 。
    *   检查频率数组 **freq1[]** 是否与频率数组 **freq2[]，**赋值 **ans = i + 1** 。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
#define SIZE 26

// Function to check if two arrays
// are identical or not
bool longHelper(int freq1[], int freq2[])
{
    // Iterate over the range [0, SIZE]
    for (int i = 0; i < SIZE; ++i) {

        // If frequency any character is
        // not same in both the strings
        if (freq1[i] != freq2[i]) {
            return false;
        }
    }

    // Otherwise
    return true;
}

// Function to find the maximum
// length of the required string
int longCommomPrefixAnagram(
    string s1, string s2, int n1, int n2)
{
    // Store the count of
    // characters in string str1
    int freq1[26] = { 0 };

    // Store the count of
    // characters in string str2
    int freq2[26] = { 0 };

    // Stores the maximum length
    int ans = 0;

    // Minimum length of str1 and str2
    int mini_len = min(n1, n2);

    for (int i = 0; i < mini_len; ++i) {

        // Increment the count of
        // characters of str1[i] in
        // freq1[] by one
        freq1[s1[i] - 'a']++;

        // Increment the count of
        // characters of str2[i] in
        // freq2[] by one
        freq2[s2[i] - 'a']++;

        // Checks if prefixes are
        // anagram or not
        if (longHelper(freq1, freq2)) {
            ans = i + 1;
        }
    }

    // Finally print the ans
    cout << ans;
}

// Driver Code
int main()
{
    string str1 = "abaabcdezzwer";
    string str2 = "caaabbttyh";
    int N = str1.length();
    int M = str2.length();

    // Function Call
    longCommomPrefixAnagram(str1, str2,
                            N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class Main
{
  static int SIZE = 26;

  // Function to check if two arrays
  // are identical or not
  static boolean longHelper(int[] freq1, int[] freq2)
  {

    // Iterate over the range [0, SIZE]
    for (int i = 0; i < SIZE; ++i)
    {

      // If frequency any character is
      // not same in both the strings
      if (freq1[i] != freq2[i])
      {
        return false;
      }
    }

    // Otherwise
    return true;
  }

  // Function to find the maximum
  // length of the required string
  static void longCommomPrefixAnagram(
    String s1, String s2, int n1, int n2)
  {
    // Store the count of
    // characters in string str1
    int[] freq1 = new int[26];

    // Store the count of
    // characters in string str2
    int[] freq2 = new int[26];

    // Stores the maximum length
    int ans = 0;

    // Minimum length of str1 and str2
    int mini_len = Math.min(n1, n2);

    for (int i = 0; i < mini_len; ++i) {

      // Increment the count of
      // characters of str1[i] in
      // freq1[] by one
      freq1[s1.charAt(i) - 'a']++;

      // Increment the count of
      // characters of str2[i] in
      // freq2[] by one
      freq2[s2.charAt(i) - 'a']++;

      // Checks if prefixes are
      // anagram or not
      if (longHelper(freq1, freq2)) {
        ans = i + 1;
      }
    }

    // Finally print the ans
    System.out.print(ans);
  }

  // Driver code
  public static void main(String[] args)
  {
    String str1 = "abaabcdezzwer";
    String str2 = "caaabbttyh";
    int N = str1.length();
    int M = str2.length();

    // Function Call
    longCommomPrefixAnagram(str1, str2, N, M);
  }
}

// This code is contributed by divyeshrrabadiya07.
```

## 蟒蛇 3

```
# Python3 program for the above approach
SIZE = 26

# Function to check if two arrays
# are identical or not
def longHelper(freq1, freq2):

    # Iterate over the range [0, SIZE]
    for i in range(26):

        # If frequency any character is
        # not same in both the strings
        if (freq1[i] != freq2[i]):
            return False

    # Otherwise
    return True

# Function to find the maximum
# length of the required string
def longCommomPrefixAnagram(s1, s2, n1, n2):

    # Store the count of
    # characters in str1
    freq1 = [0]*26

    # Store the count of
    # characters in str2
    freq2 = [0]*26

    # Stores the maximum length
    ans = 0

    # Minimum length of str1 and str2
    mini_len = min(n1, n2)
    for i in range(mini_len):

        # Increment the count of
        # characters of str1[i] in
        # freq1[] by one
        freq1[ord(s1[i]) - ord('a')] += 1

        # Increment the count of
        # characters of stord(r2[i]) in
        # freq2[] by one
        freq2[ord(s2[i]) - ord('a')] += 1

        # Checks if prefixes are
        # anagram or not
        if (longHelper(freq1, freq2)):
            ans = i + 1

    # Finally print the ans
    print (ans)

# Driver Code
if __name__ == '__main__':
    str1 = "abaabcdezzwer"
    str2 = "caaabbttyh"
    N = len(str1)
    M = len(str2)

    # Function Call
    longCommomPrefixAnagram(str1, str2, N, M)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{   
    static int SIZE = 26;

    // Function to check if two arrays
    // are identical or not
    static bool longHelper(int[] freq1, int[] freq2)
    {

        // Iterate over the range [0, SIZE]
        for (int i = 0; i < SIZE; ++i)
        {

            // If frequency any character is
            // not same in both the strings
            if (freq1[i] != freq2[i])
            {
                return false;
            }
        }

        // Otherwise
        return true;
    }

    // Function to find the maximum
    // length of the required string
    static void longCommomPrefixAnagram(
        string s1, string s2, int n1, int n2)
    {
        // Store the count of
        // characters in string str1
        int[] freq1 = new int[26];

        // Store the count of
        // characters in string str2
        int[] freq2 = new int[26];

        // Stores the maximum length
        int ans = 0;

        // Minimum length of str1 and str2
        int mini_len = Math.Min(n1, n2);

        for (int i = 0; i < mini_len; ++i) {

            // Increment the count of
            // characters of str1[i] in
            // freq1[] by one
            freq1[s1[i] - 'a']++;

            // Increment the count of
            // characters of str2[i] in
            // freq2[] by one
            freq2[s2[i] - 'a']++;

            // Checks if prefixes are
            // anagram or not
            if (longHelper(freq1, freq2)) {
                ans = i + 1;
            }
        }

        // Finally print the ans
        Console.Write(ans);
    }

  // Driver code
  static void Main() {
    string str1 = "abaabcdezzwer";
    string str2 = "caaabbttyh";
    int N = str1.Length;
    int M = str2.Length;

    // Function Call
    longCommomPrefixAnagram(str1, str2, N, M);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

let SIZE = 26;

// Function to check if two arrays
// are identical or not
function longHelper(freq1, freq2)
{

    // Iterate over the range [0, SIZE]
    for(let i = 0; i < SIZE; ++i)
    {

        // If frequency any character is
        // not same in both the strings
        if (freq1[i] != freq2[i])
        {
            return false;
        }
    }

    // Otherwise
    return true;
}

// Function to find the maximum
// length of the required string
function longCommomPrefixAnagram(s1, s2, n1, n2)
{

    // Store the count of
    // characters in string str1
    let freq1 = new Array(26);
    freq1.fill(0);

    // Store the count of
    // characters in string str2
    let freq2 = new Array(26);
    freq2.fill(0);

    // Stores the maximum length
    let ans = 0;

    // Minimum length of str1 and str2
    let mini_len = Math.min(n1, n2);

    for(let i = 0; i < mini_len; ++i)
    {

        // Increment the count of
        // characters of str1[i] in
        // freq1[] by one
        freq1[s1[i].charCodeAt() -
                'a'.charCodeAt()]++;

        // Increment the count of
        // characters of str2[i] in
        // freq2[] by one
        freq2[s2[i].charCodeAt() -
                'a'.charCodeAt()]++;

        // Checks if prefixes are
        // anagram or not
        if (longHelper(freq1, freq2))
        {
            ans = i + 1;
        }
    }

    // Finally print the ans
    document.write(ans);
}

// Driver code
let str1 = "abaabcdezzwer";
let str2 = "caaabbttyh";
let N = str1.length;
let M = str2.length;

// Function Call
longCommomPrefixAnagram(str1, str2, N, M);

// This code is contributed by rameshtravel07

</script>
```

**Output:** 

```
6
```

***时间复杂度:** O(N*26)*
***辅助空间:** O(26)*