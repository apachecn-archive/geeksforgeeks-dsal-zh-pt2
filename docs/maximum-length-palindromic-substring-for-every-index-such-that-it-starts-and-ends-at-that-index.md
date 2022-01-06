# 每个索引的最大长度回文子串，以使其在该索引处开始和结束

> 原文:[https://www . geesforgeks . org/最大长度-回文-每个索引的子串-以至于它在该索引处开始和结束/](https://www.geeksforgeeks.org/maximum-length-palindromic-substring-for-every-index-such-that-it-starts-and-ends-at-that-index/)

给定一个[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S** ，该字符串每个索引的任务是找到[最长回文子字符串](https://www.geeksforgeeks.org/longest-palindrome-substring-set-1/)的长度，该子字符串在该索引处开始**或结束**。****

****示例:****

> *****输入:*** S = "bababa"
> ***输出:***5 5 3 3 5
> ***解释:***
> 从索引 0 开始的最长回文子串为“babab”。因此，长度= 5
> 从索引 1 开始的最长回文子串为“亚的斯亚贝巴”。因此，长度= 5
> 以索引 2 结束的最长回文子串为“bab”。因此，长度= 3
> 以索引 3 结束的最长回文子串为“aba”。因此，长度= 3
> 以索引 4 结束的最长回文子串为“babab”。因此，长度= 5
> 以索引 5 结尾的最长回文子串为“亚的斯亚贝巴”。因此，长度= 5**
> 
> *****输入:**S*=“aaa”
> ***输出:*** 3 2 3
> ***解释:***
> 从索引 0 开始的最长回文子串为“AAA”。因此，长度= 3
> 从索引 1 开始的最长回文子串为“ab”。因此，长度= 2
> 以索引 3 结束的最长回文子串为:“aaa”。因此，长度= 3**

****方法:**解决这个问题的思路是[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)，对于每个索引，检查[最长的回文子串](https://www.geeksforgeeks.org/longest-palindrome-substring-set-1/)，该索引可以作为回文子串的**起始索引**和**结束索引**形成。按照以下步骤解决问题:**

*   **初始化一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **数组**来存储每个索引的最长回文子串的长度。**
*   **[使用变量 **i** 遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)，并执行以下操作:

    *   初始化一个变量，比如 **maxLength** ，为每个索引存储最长回文子串的长度。
    *   考虑 **i** 作为回文子串的结束索引，**在**【0，I–1】**的范围内从 **j** 找到第一个索引**，这样**S【j，I】就是回文**。更新**最大长度**。
    *   将 I 视为回文子串的**起始索引**，**在**【N–1，I+1】**范围内从 **j** 找到最后一个索引**，这样**S【I，j】就是回文**。更新**最大长度**。
    *   将**最大长度**的值存储在**数组【I】中，得到最大长度。**** 
*   **完成以上步骤后，[打印数组](https://www.geeksforgeeks.org/java-program-to-print-the-elements-of-an-array/) **palLength[]** 作为结果。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return true if
// S[i...j] is a palindrome
bool isPalindrome(string S, int i, int j)
{

  // Iterate until i < j
  while (i < j)
  {

    // If unequal character encountered
    if (S[i] != S[j])
      return false;
    i++;
    j--;
  }

  // Otherwise
  return true;
}

// Function to find for every index,
// longest palindromic substrings
// starting or ending at that index
void printLongestPalindrome(string S, int N)
{

  // Stores the maximum palindromic
  // substring length for each index
  int palLength[N];

  // Traverse the string
  for (int i = 0; i < N; i++)
  {

    // Stores the maximum length
    // of palindromic substring
    int maxlength = 1;

    // Consider that palindromic
    // substring ends at index i
    for (int j = 0; j < i; j++)
    {

      // If current character is
      // a valid starting index
      if (S[j] == S[i])
      {

        // If S[i, j] is palindrome,
        if (isPalindrome(S, j, i))
        {

          // Update the length of
          // the longest palindrome
          maxlength = i - j + 1;
          break;
        }
      }
    }

    // Consider that palindromic
    // substring starts at index i
    for (int j = N - 1; j > i; j--)
    {

      // If current character is
      // a valid ending index
      if (S[j] == S[i])
      {

        // If str[i, j] is palindrome
        if (isPalindrome(S, i, j))
        {

          // Update the length of
          // the longest palindrome
          maxlength = max(j - i + 1, maxlength);
          break;
        }
      }
    }

    // Update length of the longest
    // palindromic substring for index i
    palLength[i] = maxlength;
  }

  // Print the length of the
  // longest palindromic substring
  for (int i = 0; i < N; i++)
  {
    cout << palLength[i] << " ";
  }
}

// Driver Code
int main()
{
  string S = "bababa";
  int N = S.length();
  printLongestPalindrome(S, N);
  return 0;
}

// This code is contributed by Kingash.
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach

class GFG {

    // Function to find for every index,
    // longest palindromic substrings
    // starting or ending at that index
    public static void
    printLongestPalindrome(String S,
                           int N)
    {
        // Stores the maximum palindromic
        // substring length for each index
        int palLength[] = new int[N];

        // Traverse the string
        for (int i = 0; i < N; i++) {

            // Stores the maximum length
            // of palindromic substring
            int maxlength = 1;

            // Consider that palindromic
            // substring ends at index i
            for (int j = 0; j < i; j++) {

                // If current character is
                // a valid starting index
                if (S.charAt(j) == S.charAt(i)) {

                    // If S[i, j] is palindrome,
                    if (isPalindrome(S, j, i)) {

                        // Update the length of
                        // the longest palindrome
                        maxlength = i - j + 1;
                        break;
                    }
                }
            }

            // Consider that palindromic
            // substring starts at index i
            for (int j = N - 1; j > i; j--) {

                // If current character is
                // a valid ending index
                if (S.charAt(j) == S.charAt(i)) {

                    // If str[i, j] is palindrome
                    if (isPalindrome(S, i, j)) {

                        // Update the length of
                        // the longest palindrome
                        maxlength = Math.max(j - i + 1,
                                             maxlength);
                        break;
                    }
                }
            }

            // Update length of the longest
            // palindromic substring for index i
            palLength[i] = maxlength;
        }

        // Print the length of the
        // longest palindromic substring
        for (int i = 0; i < N; i++) {
            System.out.print(palLength[i] + " ");
        }
    }

    // Function to return true if
    // S[i...j] is a palindrome
    public static boolean isPalindrome(
        String S, int i, int j)
    {
        // Iterate until i < j
        while (i < j) {

            // If unequal character encountered
            if (S.charAt(i) != S.charAt(j))
                return false;
            i++;
            j--;
        }

        // Otherwise
        return true;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String S = "bababa";
        int N = S.length();
        printLongestPalindrome(S, N);
    }
}
```

## **蟒蛇 3**

```
# Python program for the above approach

# Function to return true if
# S[i...j] is a palindrome
def isPalindrome(S, i, j):
  # Iterate until i < j
  while (i < j):
    # If unequal character encountered
    if (S[i] != S[j]):
      return False
    i += 1
    j -= 1

  # Otherwise
  return True

# Function to find for every index,
# longest palindromic substrings
# starting or ending at that index
def printLongestPalindrome(S, N):
  # Stores the maximum palindromic
  # substring length for each index
  palLength = [0 for i in range(N)]

  # Traverse the string
  for i in range(N):
    # Stores the maximum length
    # of palindromic substring
    maxlength = 1

    # Consider that palindromic
    # substring ends at index i
    for j in range(i):
      # If current character is
      # a valid starting index
      if (S[j] == S[i]):
        # If S[i, j] is palindrome,
        if (isPalindrome(S, j, i)):
          # Update the length of
          # the longest palindrome
          maxlength = i - j + 1
          break

    # Consider that palindromic
    # substring starts at index i
    j = N-1
    while(j > i):
      # If current character is
      # a valid ending index
      if (S[j] == S[i]):
        # If str[i, j] is palindrome
        if (isPalindrome(S, i, j)):
          # Update the length of
          # the longest palindrome
          maxlength = max(j - i + 1, maxlength)
          break
      j -= 1

    # Update length of the longest
    # palindromic substring for index i
    palLength[i] = maxlength

  # Print the length of the
  # longest palindromic substring
  for i in range(N):
    print(palLength[i],end = " ")

# Driver Code
if __name__ == '__main__':
  S = "bababa"
  N = len(S)
  printLongestPalindrome(S, N)

  # This code is contributed by SURENDRA_GANGWAR.
```

## **C#**

```
// C# program for the above approach
using System;
class GFG
{

// Function to return true if
// S[i...j] is a palindrome
static bool isPalindrome(string S, int i, int j)
{

  // Iterate until i < j
  while (i < j)
  {

    // If unequal character encountered
    if (S[i] != S[j])
      return false;
    i++;
    j--;
  }

  // Otherwise
  return true;
}

// Function to find for every index,
// longest palindromic substrings
// starting or ending at that index
static void printLongestPalindrome(string S, int N)
{

  // Stores the maximum palindromic
  // substring length for each index
  int[] palLength = new int[N];

  // Traverse the string
  for (int i = 0; i < N; i++)
  {

    // Stores the maximum length
    // of palindromic substring
    int maxlength = 1;

    // Consider that palindromic
    // substring ends at index i
    for (int j = 0; j < i; j++)
    {

      // If current character is
      // a valid starting index
      if (S[j] == S[i])
      {

        // If S[i, j] is palindrome,
        if ((isPalindrome(S, j, i)) != false)
        {

          // Update the length of
          // the longest palindrome
          maxlength = i - j + 1;
          break;
        }
      }
    }

    // Consider that palindromic
    // substring starts at index i
    for (int j = N - 1; j > i; j--)
    {

      // If current character is
      // a valid ending index
      if (S[j] == S[i])
      {

        // If str[i, j] is palindrome
        if (isPalindrome(S, i, j))
        {

          // Update the length of
          // the longest palindrome
          maxlength = Math.Max(j - i + 1, maxlength);
          break;
        }
      }
    }

    // Update length of the longest
    // palindromic substring for index i
    palLength[i] = maxlength;
  }

  // Print the length of the
  // longest palindromic substring
  for (int i = 0; i < N; i++)
  {
    Console.Write(palLength[i] + " ");
  }
}

// Driver Code
static public void Main ()
{
    string S = "bababa";
  int N = S.Length;
  printLongestPalindrome(S, N);
}
}

// This code is contributed by code_hunt.
```

## **java 描述语言**

```
<script>
      // JavaScript program for the above approach

      // Function to return true if
      // S[i...j] is a palindrome
      function isPalindrome(S, i, j) {
        // Iterate until i < j
        while (i < j) {
          // If unequal character encountered
          if (S[i] !== S[j]) return false;
          i++;
          j--;
        }

        // Otherwise
        return true;
      }

      // Function to find for every index,
      // longest palindromic substrings
      // starting or ending at that index
      function printLongestPalindrome(S, N) {
        // Stores the maximum palindromic
        // substring length for each index
        var palLength = new Array(N);

        // Traverse the string
        for (var i = 0; i < N; i++) {
          // Stores the maximum length
          // of palindromic substring
          var maxlength = 1;

          // Consider that palindromic
          // substring ends at index i
          for (var j = 0; j < i; j++) {
            // If current character is
            // a valid starting index
            if (S[j] === S[i]) {
              // If S[i, j] is palindrome,
              if (isPalindrome(S, j, i) !== false) {
                // Update the length of
                // the longest palindrome
                maxlength = i - j + 1;
                break;
              }
            }
          }

          // Consider that palindromic
          // substring starts at index i
          for (var j = N - 1; j > i; j--) {
            // If current character is
            // a valid ending index
            if (S[j] === S[i]) {
              // If str[i, j] is palindrome
              if (isPalindrome(S, i, j)) {
                // Update the length of
                // the longest palindrome
                maxlength = Math.max(j - i + 1, maxlength);
                break;
              }
            }
          }

          // Update length of the longest
          // palindromic substring for index i
          palLength[i] = maxlength;
        }

        // Print the length of the
        // longest palindromic substring
        for (var i = 0; i < N; i++) {
          document.write(palLength[i] + "  ");
        }
      }

      // Driver Code
      var S = "bababa";
      var N = S.length;
      printLongestPalindrome(S, N);
    </script>
```

****Output:** 

```
5 5 3 3 5 5
```** 

*****时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)***