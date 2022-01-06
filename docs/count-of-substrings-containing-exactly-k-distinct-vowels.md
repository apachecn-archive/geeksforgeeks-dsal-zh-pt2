# 精确包含 K 个不同元音的子串计数

> 原文:[https://www . geeksforgeeks . org/count-of-substrings-包含-just-k-distinct-元音/](https://www.geeksforgeeks.org/count-of-substrings-containing-exactly-k-distinct-vowels/)

给定大小为 **N** 的字符串**和一个包含大小写字母的整数 **K** 。任务是找到精确包含 **K** 不同元音的子串的数量。**

**示例:**

> **输入:** str = "aeiou "，K = 2
> **输出:** 4
> **解释:**有两个不同元音的子串是“ae”、“ei”、“io”和“ou”。
> 
> **输入:** str = "TrueGoik "，K = 3
> **输出:** 5
> **说明:**子串为“TrueGo”“RueGo”“ueGo”“eGoi”“eGoik”。

**方法:**问题可以通过生成所有子串来解决。从生成的子串中计算出具有 K 个不同元音的子串。按照以下步骤实施该方法:

*   首先从范围**【0，N】**中的每个索引 **i** 开始生成所有子字符串
*   然后，对于每个子字符串，按照以下步骤操作:
    *   保留一个**散列数组**来存储唯一元音的出现。
    *   检查子串中的新字符是否是**元音**。
    *   如果它是一个元音，增加它在散列中的出现次数，并保留找到的不同元音的**计数**
    *   现在对于每个子串，如果元音的不同计数是 **K** ，**递增****最终计数**。
*   如果对于任何从 **i** 开始寻找子串的循环，不同元音的计数**超过了 K** ，或者，子串长度已经达到了字符串长度，则打破循环，从 **i+1** 开始寻找子串。
*   当考虑了所有子字符串后，打印最终计数。

下面是上述方法的实现。

## C++

```
// C++ program to count number of substrings
// with exactly k distinct vowels
#include <bits/stdc++.h>
using namespace std;

#define MAX 128

// Function to check whether
// a character is vowel or not
bool isVowel(char x)
{
    return (x == 'a' || x == 'e' || x == 'i' 
            || x == 'o' || x == 'u' || x == 'A' 
            || x == 'E' || x == 'I'
            || x == 'O' || x == 'U');
}

int getIndex(char ch)
{
    return (ch - 'A' > 26 ? ch - 'a' : 
            ch - 'A');
}

// Function to count number of substrings
// with exactly k unique vowels
int countkDist(string str, int k)
{
    int n = str.length();

    // Initialize result
    int res = 0;

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

            // If this is a new vowels
            // for this substring, 
            // increment dist_count.
            if (isVowel(str[j])
                && cnt[getIndex(str[j])] 
                == 0)
                dist_count++;

            // Increment count of 
            // current character
            cnt[getIndex(str[j])]++;

            // If distinct vowels count
            // becomes k then increment result
            if (dist_count == k) 
                res++;

            if (dist_count > k)
                break;
        }
    }
    return res;
}

// Driver code
int main()
{
    string str = "TrueGoik";
    int K = 3;
    cout << countkDist(str, K) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of substrings
// with exactly k distinct vowels
import java.util.*;
public class GFG
{

// Function to check whether
// a character is vowel or not
static boolean isVowel(char x)
{
    return (x == 'a' || x == 'e' || x == 'i' 
            || x == 'o' || x == 'u' || x == 'A' 
            || x == 'E' || x == 'I'
            || x == 'O' || x == 'U');
}

static int getIndex(char ch)
{
    return (ch - 'A' > 26 ? ch - 'a' : 
            ch - 'A');
}

// Function to count number of substrings
// with exactly k unique vowels
static int countkDist(String str, int k)
{
    int n = str.length();

    // Initialize result
    int res = 0;

    // Consider all substrings 
    // beginning with str[i]
    for (int i = 0; i < n; i++) {
        int dist_count = 0;

        // To store count of characters 
        // from 'a' to 'z'
        int cnt[] = new int[26];
        for(int t = 0; t < 26; t++) {
            cnt[t] = 0;
        }

        // Consider all substrings 
        // between str[i..j]
        for (int j = i; j < n; j++) {

            // If this is a new vowels
            // for this substring, 
            // increment dist_count.
            if (isVowel(str.charAt(j))
                && cnt[getIndex(str.charAt(j))] 
                == 0)
                dist_count++;

            // Increment count of 
            // current character
            cnt[getIndex(str.charAt(j))]++;

            // If distinct vowels count
            // becomes k then increment result
            if (dist_count == k) 
                res++;

            if (dist_count > k)
                break;
        }
    }
    return res;
}

// Driver code
public static void main(String args[])
{
    String str = "TrueGoik";
    int K = 3;
    System.out.println(countkDist(str, K));
}
}

// This code is contributed by Samim Hossain Mondal.
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

# Function to count number of substrings
# with exactly k unique vowels
def countkDist(str, k):
    n = len(str)

    # Initialize result
    res = 0

    # Consider all substrings
    # beginning with str[i]
    for i in range(n):
        dist_count = 0

        # To store count of characters
        # from 'a' to 'z'
        cnt = [0] * 26

        # Consider all substrings
        # between str[i..j]
        for j in range(i, n):

            # If this is a new vowels
            # for this substring,
            # increment dist_count.
            if (isVowel(str[j]) and cnt[getIndex(str[j])] == 0):
                dist_count += 1

            # Increment count of
            # current character
            cnt[getIndex(str[j])] += 1

            # If distinct vowels count
            # becomes k then increment result
            if (dist_count == k):
                res += 1

            if (dist_count > k):
                break
    return res

# Driver code
s = "TrueGoik"
K = 3

print(countkDist(s, K))

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# program to count number of substrings
// with exactly k distinct vowels
using System;
class GFG
{

  // Function to check whether
  // a character is vowel or not
  static bool isVowel(char x)
  {
    return (x == 'a' || x == 'e' || x == 'i' 
            || x == 'o' || x == 'u' || x == 'A' 
            || x == 'E' || x == 'I'
            || x == 'O' || x == 'U');
  }

  static int getIndex(char ch)
  {
    return (ch - 'A' > 26 ? ch - 'a' : 
            ch - 'A');
  }

  // Function to count number of substrings
  // with exactly k unique vowels
  static int countkDist(string str, int k)
  {
    int n = str.Length;

    // Initialize result
    int res = 0;

    // Consider all substrings 
    // beginning with str[i]
    for (int i = 0; i < n; i++) {
      int dist_count = 0;

      // To store count of characters 
      // from 'a' to 'z'
      int []cnt = new int[26];
      for(int t = 0; t < 26; t++) {
        cnt[t] = 0;
      }

      // Consider all substrings 
      // between str[i..j]
      for (int j = i; j < n; j++) {

        // If this is a new vowels
        // for this substring, 
        // increment dist_count.
        if (isVowel(str[j])
            && cnt[getIndex(str[j])] 
            == 0)
          dist_count++;

        // Increment count of 
        // current character
        cnt[getIndex(str[j])]++;

        // If distinct vowels count
        // becomes k then increment result
        if (dist_count == k) 
          res++;

        if (dist_count > k)
          break;
      }
    }
    return res;
  }

  // Driver code
  public static void Main()
  {
    string str = "TrueGoik";
    int K = 3;
    Console.Write(countkDist(str, K));
  }
}

// This code is contributed by Samim Hossain Mondal.
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

        // Function to count number of substrings
        // with exactly k unique vowels
        function countkDist(str, k)
        {
            let n = str.length;

            // Initialize result
            let res = 0;

            // Consider all substrings 
            // beginning with str[i]
            for (let i = 0; i < n; i++) {
                let dist_count = 0;

                // To store count of characters 
                // from 'a' to 'z'
                let cnt = new Array(26).fill(0)

                // Consider all substrings 
                // between str[i..j]
                for (let j = i; j < n; j++) {

                    // If this is a new vowels
                    // for this substring, 
                    // increment dist_count.
                    if (isVowel(str[j])
                        && cnt[getIndex(str[j])]
                        == 0)
                        dist_count++;

                    // Increment count of 
                    // current character
                    cnt[getIndex(str[j])]++;

                    // If distinct vowels count
                    // becomes k then increment result
                    if (dist_count == k)
                        res++;

                    if (dist_count > k)
                        break;
                }
            }
            return res;
        }

        // Driver code
        let s = "TrueGoik";
        let K = 3

        document.write(countkDist(s, K));

  // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
5
```

***时间复杂度:**T3】O(N<sup>2</sup>)
*T8】辅助空间:T10】O(N<sup>2</sup>**