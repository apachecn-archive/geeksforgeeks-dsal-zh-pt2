# 恰好包含 K 个元音的最长子串

> 原文:[https://www . geesforgeks . org/最长子串-包含-精确-k-元音/](https://www.geeksforgeeks.org/longest-substring-containing-exactly-k-vowels/)

给定包含大小写字母的字符串**和一个整数 **K** 。任务是找到包含**的**最长的**子串，正好是** **K** **元音**(可能是重复的)。**

**示例:**

> **输入:** GeeksForGeeks，K = 2
> **输出:** 7、eksForG
> **说明:**正好有两个元音的最长子串是“eksForG”。
> 
> **输入:** TrueGeek，K = 3
> T3】输出: 6，TrueGe

**接近**:可以通过跟踪**当前**窗口中遇到的**元音数量**来解决任务。
按照以下步骤解决问题:

*   创建一个变量“**”来记录当前**窗口中**元音的数量******
*   ****开始增加窗户的尺寸，如果**发誓**变得**大于 **K** ，开始从前面缩小窗户。******
*   ****最大化**每一步窗口的大小**

**下面是上述方法的实现:**

## **C++14**

```
// C++ program to find the longest
// substring with exactly K vowels.
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

// Function to find the length of the longest
// substring with k vowels
void get(string s, int k)
{

    // Stores the length of longest
    // substring with K vowels
    int ans = -1;

    // Stores the number of vowels
    // in the current window
    int vow = 0;

    // Stores the resultant string
    string res;
    int l = 0, r = 0;

    while (r < s.length()) {
        if (isVowel(s[r]))
            vow++;
        if (vow == k) {
            if (ans < r - l + 1) {
                ans = max(ans, r - l + 1);
                res = s.substr(l, r - l + 1);
            }
        }
        if (vow > k) {
            while (vow > k) {
                if (isVowel(s[l]))
                    vow--;
                l++;
            }
            if (ans < r - l + 1) {
                ans = max(ans, r - l + 1);
                res = s.substr(l, r - l + 1);
            }
        }
        r++;
    }
    cout << ans << " " << res;
}

// Driver code
int main(void)
{
    string s = "TrueGeek";
    int K = 3;
    get(s, K);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java code to implement above approach
class GFG {

  // Function to check whether
  // a character is vowel or not
  static boolean isVowel(char x)
  {
    return (x == 'a' || x == 'e' || x == 'i' || x == 'o'
            || x == 'u' || x == 'A' || x == 'E'
            || x == 'I' || x == 'O' || x == 'U');
  }

  // Function to find the length of the longest
  // substring with k vowels
  static void get(String s, int k)
  {

    // Stores the length of longest
    // substring with K vowels
    int ans = -1;

    // Stores the number of vowels
    // in the current window
    int vow = 0;

    // Stores the resultant string
    String res = "";
    int l = 0, r = 0;

    while (r < s.length()) {
      if (isVowel(s.charAt(r)))
        vow++;
      if (vow == k) {
        if (ans < r - l + 1) {
          ans = Math.max(ans, r - l + 1);
          res = s.substring(l, r - l + 1);
        }
      }
      if (vow > k) {
        while (vow > k) {
          if (isVowel(s.charAt(l)))
            vow--;
          l++;
        }
        if (ans < r - l + 1) {
          ans = Math.max(ans, r - l + 1);
          res = s.substring(l, r - l + 1);
        }
      }
      r++;
    }
    System.out.print(ans + " " + res);
  }

  // Driver code
  public static void main(String[] args)
  {
    String s = "TrueGeek";
    int K = 3;
    get(s, K);
  }
}

// This code is contributed by ukasp.
```

## **蟒蛇 3**

```
# Python code for the above approach
MAX = 128

# Function to check whether
# a character is vowel or not
def isVowel(x):
    return (x == 'a' or x == 'e' or x == 'i' or x == 'o'
            or x == 'u' or x == 'A' or x == 'E' or x == 'I'
            or x == 'O' or x == 'U')

# Function to find the length of the longest
# substring with k vowels
def get(s, k):

    # Stores the length of longest
    # substring with K vowels
    ans = -1

    # Stores the number of vowels
    # in the current window
    vow = 0

    # Stores the resultant string
    res = None
    l = 0
    r = 0

    while (r < len(s)):
        if (isVowel(s[r])):
            vow += 1
        if (vow == k):
            if (ans < r - l + 1):
                ans = max(ans, r - l + 1)
                res = s[l:(r - l + 1)]
        if (vow > k):
            while (vow > k):
                if (isVowel(s[l])):
                    vow -= 1
                l += 1
            if (ans < r - l + 1):
                ans = max(ans, r - l + 1)
                res = s[l: (r - l + 1)]
        r += 1

    print(f"{ans} {res}")

# Driver code
s = "TrueGeek"
K = 3
get(s, K)

# This code is contributed by Saurabh Jaiswal
```

## **C#**

```
// C# code to implement above approach
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

// Function to find the length of the longest
// substring with k vowels
static void get(string s, int k)
{

    // Stores the length of longest
    // substring with K vowels
    int ans = -1;

    // Stores the number of vowels
    // in the current window
    int vow = 0;

    // Stores the resultant string
    string res = "";
    int l = 0, r = 0;

    while (r < s.Length) {
        if (isVowel(s[r]))
            vow++;
        if (vow == k) {
            if (ans < r - l + 1) {
                ans = Math.Max(ans, r - l + 1);
                res = s.Substring(l, r - l + 1);
            }
        }
        if (vow > k) {
            while (vow > k) {
                if (isVowel(s[l]))
                    vow--;
                l++;
            }
            if (ans < r - l + 1) {
                ans = Math.Max(ans, r - l + 1);
                res = s.Substring(l, r - l + 1);
            }
        }
        r++;
    }
    Console.Write(ans + " " + res);
}

// Driver code
public static void Main()
{
    string s = "TrueGeek";
    int K = 3;
    get(s, K);

}
}

// This code is contributed by Samim Hossain Mondal.
```

## **java 描述语言**

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

    // Function to find the length of the longest
    // substring with k vowels
    function get(s, k) {

      // Stores the length of longest
      // substring with K vowels
      let ans = -1;

      // Stores the number of vowels
      // in the current window
      let vow = 0;

      // Stores the resultant string
      let res;
      let l = 0, r = 0;

      while (r < s.length) {
        if (isVowel(s[r]))
          vow++;
        if (vow == k) {
          if (ans < r - l + 1) {
            ans = Math.max(ans, r - l + 1);
            res = s.slice(l, r - l + 1);
          }
        }
        if (vow > k) {
          while (vow > k) {
            if (isVowel(s[l]))
              vow--;
            l++;
          }
          if (ans < r - l + 1) {
            ans = Math.max(ans, r - l + 1);
            res = s.slice(l, r - l + 1);
          }
        }
        r++;
      }
      document.write(ans + " " + res);
    }

    // Driver code

    let s = "TrueGeek";
    let K = 3;
    get(s, K);

  // This code is contributed by Potta Lokesh
  </script>
```

****Output**

```
6 TrueGe
```** 

*****时间复杂度*****:**O(N)
***辅助空间*** **:** O(1)**