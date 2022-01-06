# 最多包含 X 个不同元音的 K 长度子串的计数

> 原文:[https://www . geesforgeks . org/count-of-k-length-substring-最多包含-x-distinct-元音/](https://www.geeksforgeeks.org/count-of-k-length-substring-containing-at-most-x-distinct-vowels/)

给定大小为 **N** 的字符串**字符串**，包含大小写字母和两个整数 **K** 和 **X** 。任务是找出大小为 **K** 最多包含**X**个不同元音的子串的个数。

**示例:**

> **输入:** str = "TrueGoik "，K = 3，X = 2
> **输出:** 6
> **解释:**这五个这样的子串是“Tru”、“rue”、“ueG”、“eGo”、“Goi”和“oik”。
> 
> **输入:** str = "GeeksForGeeks "，K = 2，X = 2
> **输出:** 12
> **解释:**“Ge”、“ee”、“ek”、“ks”、“sf”、“fo”、“or”、“rG”、“Ge”、“ee”、“ek”和“ks”。

**方法:**要解决这个问题，首先要生成长度为 **K** 的所有子串。然后在每个子串中检查不同元音的数量是否小于 **X** 。遵循下面提到的步骤。

*   首先生成长度为 **K** 的所有子串，从**【0，N–K】中的每个索引 **i** 开始。**
*   然后对于长度为 **K** 的每个子串，执行以下操作:
    *   保留一个散列来存储唯一元音的出现。
    *   检查子串**中的新字符是否是元音**。
    *   如果它是一个元音，增加它在散列中的出现次数，并保留找到的不同元音的**计数**
    *   现在对于每个子串，如果元音的独特计数小于或等于 **X** ，则增加最终计数。
*   当考虑了所有子字符串后，打印最终计数。

下面是上述方法的实现:

## C++

```
// C++ code to implement above approach
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
    return (ch - 'A' > 26 ? ch - 'a' : 
            ch - 'A');
}

// Function to find the count of K length
// substring with at most x distinct vowels
int get(string str, int k, int x)
{
    int n = str.length();

    // Initialize result
    int res = 0;

    // Consider all substrings 
    // beginning with str[i]
    for (int i = 0; i <= n - k; i++) {
        int dist_count = 0;

        // To store count of characters 
        // from 'a' to 'z'
        vector<int> cnt(26, 0);

        // Consider all substrings 
        // between str[i..j]
        for (int j = i; j < i + k; j++) {

            // If this is a new vowels 
            // for this substring, 
            // increment dist_count.
            if (isVowel(str[j])
                && cnt[getIndex(str[j])] 
                == 0) {
                dist_count++;
            }

            // Increment count of 
            // current character
            cnt[getIndex(str[j])]++;
        }

        // If count of distinct vowels
        // in current substring
        // of length k is less than 
        // equal to x, then increment result.
        if (dist_count <= x)
            res++;
    }

    return res;
}

// Driver code
int main(void)
{
    string s = "TrueGoik";
    int K = 3, X = 2;
    cout << get(s, K, X);
    return 0;
}
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to check whether
# a character is vowel or not
def isVowel(x):
    return (x == 'a' or x == 'e' or x == 'i' or x == 'o'
            or x == 'u' or x == 'A' or x == 'E' or x == 'I'
            or x == 'O' or x == 'U')

def getIndex(ch):
    return (ord(ch) - ord('a')) if (ord(ch) - ord('A')) > 26 else (ord(ch) - ord('A'))

# Function to find the count of K length
# substring with at most x distinct vowels
def get(str, k, x):
    n = len(str)

    # Initialize result
    res = 0

    # Consider all substrings
    # beginning with str[i]
    for i in range(n - k + 1):
        dist_count = 0

        # To store count of characters
        # from 'a' to 'z'
        cnt = [0] * 26

        # Consider all substrings
        # between str[i..j]
        for j in range(i, i + k):

            # If this is a new vowels
            # for this substring,
            # increment dist_count.
            if (isVowel(str[j]) and cnt[getIndex(str[j])] == 0):
                dist_count += 1

            # Increment count of
            # current character
            cnt[getIndex(str[j])] += 1

        # If count of distinct vowels
        # in current substring
        # of length k is less than
        # equal to x, then increment result.
        if (dist_count <= x):
            res += 1

    return res

# Driver code

s = "TrueGoik"
K = 3
X = 2
print(get(s, K, X))

# This code is contributed by Saurabh Jaiswal
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

      // Function to find the count of K length
      // substring with at most x distinct vowels
      function get(str, k, x) {
          let n = str.length;

          // Initialize result
          let res = 0;

          // Consider all substrings 
          // beginning with str[i]
          for (let i = 0; i <= n - k; i++) {
              let dist_count = 0;

              // To store count of characters 
              // from 'a' to 'z'
              let cnt = new Array(26).fill(0);

              // Consider all substrings 
              // between str[i..j]
              for (let j = i; j < i + k; j++) {

                  // If this is a new vowels 
                  // for this substring, 
                  // increment dist_count.
                  if (isVowel(str[j])
                      && cnt[getIndex(str[j])]
                      == 0) {
                      dist_count++;
                  }

                  // Increment count of 
                  // current character
                  cnt[getIndex(str[j])]++;
              }

              // If count of distinct vowels
              // in current substring
              // of length k is less than 
              // equal to x, then increment result.
              if (dist_count <= x)
                  res++;
          }

          return res;
      }

      // Driver code

      let s = "TrueGoik";
      let K = 3, X = 2;
      document.write(get(s, K, X));

// This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
6
```

***时间复杂度:***O(N * K)
*T6】辅助空间:* O(N * K)