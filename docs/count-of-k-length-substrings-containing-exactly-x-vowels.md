# 精确包含 X 个元音的 K 长度子串计数

> 原文:[https://www . geeksforgeeks . org/count-of-k-length-substrings-包含确切的-x-元音/](https://www.geeksforgeeks.org/count-of-k-length-substrings-containing-exactly-x-vowels/)

给定包含大写和小写英文字母的 **N** 字符的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，任务是找到大小为 **K** 的[子字符串](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的数量，这些子字符串恰好包含 **X** [元音](https://www.geeksforgeeks.org/program-find-character-vowel-consonant/)。

**示例:**

> **输入:** str = "GeeksForGeeks "，K = 2，X = 2
> **输出:** 2
> **解释:**给定的字符串只包含 2 个大小为 2 的子串，由 2 个元音组成。它们是“ee”和“ee”。
> 
> **输入:** str = "TrueGeek "，K = 3，X = 2
> **输出:** 5

**方法:**通过保持大小为 **K** 的窗口并跟踪当前窗口中遇到的[元音](https://www.geeksforgeeks.org/program-find-character-vowel-consonant/)的数量，可以使用[滑动窗口技术](http://www.geeksforgeeks.org/window-sliding-technique/)解决给定的问题。如果当前窗口中的元音计数等于 **X** ，则将最终所需计数增加 **1** 。

下面是上述方法的实现:

## C++

```
// C++ program of the above appraoch
#include <bits/stdc++.h>
using namespace std;

#define MAX 128

// Function to check whether
// a character is vowel or not
bool isVowel(char x)
{
    return (x == 'a' || x == 'e' || x == 'i' || x == 'o'
            || x == 'u' || x == 'A' || x == 'E' || x == 'I'
            || x == 'O' || x == 'U');
}

// Function to find the count of
// K-sized substring having X vowels
int cntSubstr(string str, int K, int X)
{
    // Stores the number of vowels
    // in the current window
    int vow = 0;

    for (int i = 0; i < K; i++)
        if (isVowel(str[i]))
            vow++;

    // Stores the count of K length
    // substring with X vowels
    int ans = vow == X ? 1 : 0;

    for (int i = 1; i < str.length(); i++) {

        // Remove (i - 1)th character
        // from the current window
        vow = isVowel(str[i - 1]) ? vow - 1 : vow;

        // Insert (i - 1 + K)th character
        // from the current window
        vow = isVowel(str[i - 1 + K]) ? vow + 1 : vow;

        if (vow == X)

            // Increment answer
            ans++;
    }

    // Return Answer
    return ans;
}

// Driver code
int main(void)
{
    string s = "TrueGeek";
    int K = 3, X = 2;

    cout << cntSubstr(s, K, X);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program of the above appraoch
MAX = 128

# Function to check whether
# a character is vowel or not
def isVowel(x):

    return(x == 'a' or x == 'e' or x == 'i' or
           x == 'o' or x == 'u' or x == 'A' or
           x == 'E' or x == 'I' or x == 'O' or
           x == 'U')

# Function to find the count of
# K-sized substring having X vowels
def cntSubstr(str, K, X):

    # Stores the number of vowels
    # in the current window
    vow = 0

    for i in range(0, K):
        if (isVowel(str[i])):
            vow += 1

    # Stores the count of K length
    # substring with X vowels
    ans = 1 if vow == X else 0

    for i in range(1, len(str) - K + 1):

        # Remove (i - 1)th character
        # from the current window
        vow = vow - 1 if isVowel(str[i - 1]) else vow

        # Insert (i - 1 + K)th character
        # from the current window
        vow = vow + 1 if isVowel(str[i - 1 + K]) else vow

        if (vow == X):

            # Increment answer
            ans += 1

    # Return Answer
    return ans

# Driver code
if __name__ == "__main__":

    s = "TrueGeek"
    K, X = 3, 2

    print(cntSubstr(s, K, X))

# This code is contributed by rakeshsahni
```

## C#

```
// C# code to implement the above approach
using System;
class GFG
{

  // Function to check whether
  // a character is vowel or not
  static bool isVowel(char x)
  {
    return (x == 'a' || x == 'e' || x == 'i' || x == 'o'
            || x == 'u' || x == 'A' || x == 'E' || x == 'I'
            || x == 'O' || x == 'U');
  }

  // Function to find the count of
  // K-sized substring having X vowels
  static int cntSubstr(string str, int K, int X)
  {
    // Stores the number of vowels
    // in the current window
    int vow = 0;

    for (int i = 0; i < K; i++)
      if (isVowel(str[i]))
        vow++;

    // Stores the count of K length
    // substring with X vowels
    int ans = vow == X ? 1 : 0;

    for (int i = 1; i < str.Length; i++) {

      // Remove (i - 1)th character
      // from the current window
      vow = isVowel(str[i - 1]) ? vow - 1 : vow;

      // Insert (i - 1 + K)th character
      // from the current window
      if(i - 1 +  K < str.Length)
        vow = isVowel(str[i - 1 + K]) ? vow + 1 : vow;

      if (vow == X)

        // Increment answer
        ans++;
    }

    // Return Answer
    return ans;
  }

  // Driver code
  public static void Main()
  {
    string s = "TrueGeek";
    int K = 3, X = 2;

    Console.Write(cntSubstr(s, K, X));
  }
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
        // JavaScript code for the above approach
        let MAX = 128

        // Function to check whether
        // a character is vowel or not
        function isVowel(x) {
            return (x == 'a' || x == 'e' || x == 'i' || x == 'o'
                || x == 'u' || x == 'A' || x == 'E' || x == 'I'
                || x == 'O' || x == 'U');
        }

        // Function to find the count of
        // K-sized substring having X vowels
        function cntSubstr(str, K, X)
        {

            // Stores the number of vowels
            // in the current window
            let vow = 0;

            for (let i = 0; i < K; i++)
                if (isVowel(str[i]))
                    vow++;

            // Stores the count of K length
            // substring with X vowels
            let ans = vow == X ? 1 : 0;
            for (let i = 1; i < str.length; i++) {

                // Remove (i - 1)th character
                // from the current window
                vow = isVowel(str[i - 1]) ? vow - 1 : vow;

                // Insert (i - 1 + K)th character
                // from the current window
                vow = isVowel(str[i - 1 + K]) ? vow + 1 : vow;

                if (vow == X)

                    // Increment answer
                    ans++;
            }

            // Return Answer
            return ans;
        }

        // Driver code
        let s = "TrueGeek";
        let K = 3, X = 2;

        document.write(cntSubstr(s, K, X));

  // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)