# 查找包含正好 K 个唯一元音的所有子串

> 原文:[https://www . geesforgeks . org/find-all-substrings-包含-精确-k-unique-元音/](https://www.geeksforgeeks.org/find-all-substrings-containing-exactly-k-unique-vowels/)

给定长度为 **N** 的字符串**和一个整数 **K** ，字符串**包含大小写字母。任务是找到所有包含精确的 **K** **不同元音**的子串。

**示例:**

> **输入:** str = "aeiou "，K = 2
> **输出:**【AE】【ei】【io】【ou】
> **解释:**这些是包含正好 2 个不同元音的子串。
> 
> **输入:** str = "TrueGeek "，K = 3
> **输出:**
> **说明:**虽然字符串有 3 个以上的元音但是没有三个唯一的元音。
> 所以答案是空的。
> 
> **输入:**str = " true goik "，K = 3
> **输出:**【true go】、【please】、【eGo】、【egio】、【egio】、【egio】

**进场:**这个问题可以通过[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决。生成子字符串并检查每个子字符串。按照下面提到的步骤解决问题:

*   首先从范围 **0** 到 **N** 的每个索引 **i** 开始生成所有子字符串。
*   然后对于每个子串:
    *   保留一个 [**哈希数组**](https://www.geeksforgeeks.org/hashing-set-1-introduction/) 来存储唯一元音的出现。
    *   检查子串中的新字符是否是元音。
    *   如果它是一个元音，**增加**它在散列中的出现，并记录找到的不同元音的计数
    *   现在对于每个子串，如果元音的**不同计数**是 **K** ，打印子串。
*   如果对于任何从 **i** 开始寻找子串的循环，不同元音的计数超过 **K** ，或者，子串长度已经达到字符串长度，则中断循环，从 **i+1** 开始寻找子串。

下面是上述方法的实现。

## C++

```
// C++ program to find all substrings with
// exactly k distinct vowels
#include <bits/stdc++.h>
using namespace std;

#define MAX 128

// Function to check whether
// a character is vowel or not
bool isVowel(char x)
{
    return (x == 'a' || x == 'e' || x == 'i' 
            || x == 'o' || x == 'u' || 
            x == 'A' || x == 'E' || x == 'I'
            || x == 'O' || x == 'U');
}

int getIndex(char ch)
{
    return (ch - 'A' > 26 ? 
            ch - 'a' : ch - 'A');
}

// Function to find all substrings
// with exactly k unique vowels
void countkDist(string str, int k)
{
    int n = str.length();

    // Consider all substrings 
    // beginning with str[i]
    for (int i = 0; i < n; i++) {
        int dist_count = 0;

        // To store count of characters 
        // from 'a' to 'z'
        vector<int> cnt(26, 0);

        // Consider all substrings 
        // between str[i..j]
        for (int j = i; j < n; j++) {

            // If this is a new vowel
            // for this substring, 
            // increment dist_count.
            if (isVowel(str[j])
                && cnt[getIndex(str[j])] == 0) {
                dist_count++;
            }

            // Increment count of 
            // current character
            cnt[getIndex(str[j])]++;

            // If distinct vowels count
            // becomes k, then print the 
            // substring.
            if (dist_count == k) {
                cout << str.substr(i, j - i + 1) << endl;
            }

            if (dist_count > k)
                break;
        }
    }
}

// Driver code
int main()
{
    string str = "TrueGoik";
    int K = 3;
    countkDist(str, K);
    return 0;
}
```

## 蟒蛇 3

```
# python3 program to find all substrings with
# exactly k distinct vowels
MAX = 128

# Function to check whether
# a character is vowel or not
def isVowel(x):

    return (x == 'a' or x == 'e' or x == 'i'
            or x == 'o' or x == 'u' or
            x == 'A' or x == 'E' or x == 'I'
            or x == 'O' or x == 'U')

def getIndex(ch):
    if ord(ch) - ord('A') > 26:
        return ord(ch) - ord('a')
    else:
        return ord(ch) - ord('A')

# Function to find all substrings
# with exactly k unique vowels
def countkDist(str, k):
    n = len(str)

    # Consider all substrings
    # beginning with str[i]
    for i in range(0, n):
        dist_count = 0

        # To store count of characters
        # from 'a' to 'z'
        cnt = [0 for _ in range(26)]

        # Consider all substrings
        # between str[i..j]
        for j in range(i, n):

            # If this is a new vowel
            # for this substring,
            # increment dist_count.
            if (isVowel(str[j])
                    and cnt[getIndex(str[j])] == 0):
                dist_count += 1

            # Increment count of
            # current character
            cnt[getIndex(str[j])] += 1

            # If distinct vowels count
            # becomes k, then print the
            # substring.
            if (dist_count == k):
                print(str[i:i+j - i + 1])

            if (dist_count > k):
                break

# Driver code
if __name__ == "__main__":

    str = "TrueGoik"
    K = 3
    countkDist(str, K)

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program to find all substrings with
// exactly k distinct vowels
using System;
class GFG {

  // Function to check whether
  // a character is vowel or not
  static bool isVowel(char x)
  {
    return (x == 'a' || x == 'e' || x == 'i' || x == 'o'
            || x == 'u' || x == 'A' || x == 'E'
            || x == 'I' || x == 'O' || x == 'U');
  }

  static int getIndex(char ch)
  {
    return (ch - 'A' > 26 ? ch - 'a' : ch - 'A');
  }

  // Function to find all substrings
  // with exactly k unique vowels
  static void countkDist(string str, int k)
  {
    int n = str.Length;

    // Consider all substrings
    // beginning with str[i]
    for (int i = 0; i < n; i++) {
      int dist_count = 0;

      // To store count of characters
      // from 'a' to 'z'
      int[] cnt = new int[26];

      // Consider all substrings
      // between str[i..j]
      for (int j = i; j < n; j++) {

        // If this is a new vowel
        // for this substring,
        // increment dist_count.
        if (isVowel(str[j])
            && cnt[getIndex(str[j])] == 0) {
          dist_count++;
        }

        // Increment count of
        // current character
        cnt[getIndex(str[j])]++;

        // If distinct vowels count
        // becomes k, then print the
        // substring.
        if (dist_count == k) {
          Console.WriteLine(
            str.Substring(i, j - i + 1));
        }

        if (dist_count > k)
          break;
      }
    }
  }

  // Driver code
  public static void Main()
  {
    string str = "TrueGoik";
    int K = 3;
    countkDist(str, K);
  }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
      // JavaScript code for the above approach

      // Function to check whether
      // a character is vowel or not
      function isVowel(x) {
          return (x == 'a' || x == 'e' || x == 'i' || x == 'o'
              || x == 'u' || x == 'A' || x == 'E' || x == 'I'
              || x == 'O' || x == 'U');
      }

      function getIndex(ch) {
          return ((ch.charCodeAt(0) - 'A'.charCodeAt(0)) > 26 ? (ch.charCodeAt(0) - 'a'.charCodeAt(0)) :
              (ch.charCodeAt(0) - 'A'.charCodeAt(0)));
      }

      // Function to find all substrings
      // with exactly k unique vowels
      function countkDist(str, k) {
          let n = str.length;

          // Consider all substrings 
          // beginning with str[i]
          for (let i = 0; i < n; i++) {
              let dist_count = 0;

              // To store count of characters 
              // from 'a' to 'z'
              let cnt = new Array(26).fill(0);

              // Consider all substrings 
              // between str[i..j]
              for (let j = i; j < n; j++) {

                  // If this is a new vowel
                  // for this substring, 
                  // increment dist_count.
                  if (isVowel(str[j])
                      && cnt[getIndex(str[j])] == 0) {
                      dist_count++;
                  }

                  // Increment count of 
                  // current character
                  cnt[getIndex(str[j])]++;

                  // If distinct vowels count
                  // becomes k, then print the 
                  // substring.
                  if (dist_count == k) {
                      document.write(str.slice(i, i + j - i + 1) + '<br>');
                  }

                  if (dist_count > k)
                      break;
              }
          }
      }

      // Driver code

      let s = "TrueGoik";
      let K = 3

      countkDist(s, K);

// This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
TrueGo
rueGo
ueGo
eGoi
eGoik
```

***时间复杂度:***O(N<sup>2</sup>)
***辅助空间:*** O(N <sup>2</sup> )存储结果子串