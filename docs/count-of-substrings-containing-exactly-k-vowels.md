# 精确包含 K 个元音的子串计数

> 原文:[https://www . geeksforgeeks . org/count-of-substrings-包含确切的-k-元音/](https://www.geeksforgeeks.org/count-of-substrings-containing-exactly-k-vowels/)

给定包含大小写字母的字符串**和一个整数 **K** 。任务是找到包含**的子串的数量，正好是 K 个元音**(可能是重复的)。**

**示例:**

> **输入:** str = "aeiou "，K = 2
> 输出:4
> 说明:子串为“ae”、“ei”、“io”、“ou”。
> 
> **输入:** str = "TrueGeek "，K = 3
> **输出:** 5
> **解释:**所有这些可能的子串都是:
> “TrueGee”、“rueGe”、“ueGe”、“eGee”、“eGek”。

**进场:**解决这个问题是基于[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)。生成所有子字符串，并检查每个子字符串的元音计数。遵循下面提到的步骤。

*   生成所有 [**子串**](https://www.geeksforgeeks.org/substring-in-cpp/) 。对于每个子字符串，请执行以下操作
    *   存储**元音**出现的**次数**。
    *   检查子串中的新字符是否是元音。
    *   如果是元音，增加找到的元音计数
    *   现在对于每个子串，如果元音的**计数为 K** ，则增加最终计数。
*   在最后返回最终计数作为所需答案。

下面是上面代码的实现。

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
    return (x == 'a' || x == 'e' || 
            x == 'i' || x == 'o' || x == 'u' 
            || x == 'A' || x == 'E' || 
            x == 'I' || x == 'O' || x == 'U');
}

// Function to find the count of
// substring with k vowels
int get(string str, int k)
{

    int n = str.length();

    // Stores the count of
    // substring with K vowels
    int ans = 0;

    // Consider all substrings 
    // beginning with str[i]
    for (int i = 0; i < n; i++) {
        int count = 0;

        // Consider all substrings 
        // between [i, j]
        for (int j = i; j < n; j++) {

            // If this is a vowel, for this
            // substring, increment count.
            if (isVowel(str[j])) {
                count++;
            }

            // If vowel count becomes k,
            // then increment final count.
            if (count == k) {
                ans++;
            }

            if (count > k)
                break;
        }
    }
    return ans;
}

// Driver code
int main(void)
{
    string s = "aeiou";
    int K = 2;
    cout << get(s, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement above approach
class GFG
{

  static final int MAX = 128;

  // Function to check whether
  // a character is vowel or not
  static boolean isVowel(char x)
  {
    return (x == 'a' || x == 'e' || 
            x == 'i' || x == 'o' || x == 'u' 
            || x == 'A' || x == 'E' || 
            x == 'I' || x == 'O' || x == 'U');
  }

  // Function to find the count of
  // subString with k vowels
  static int get(String str, int k)
  {

    int n = str.length();

    // Stores the count of
    // subString with K vowels
    int ans = 0;

    // Consider all subStrings 
    // beginning with str[i]
    for (int i = 0; i < n; i++) {
      int count = 0;

      // Consider all subStrings 
      // between [i, j]
      for (int j = i; j < n; j++) {

        // If this is a vowel, for this
        // subString, increment count.
        if (isVowel(str.charAt(j))) {
          count++;
        }

        // If vowel count becomes k,
        // then increment final count.
        if (count == k) {
          ans++;
        }

        if (count > k)
          break;
      }
    }
    return ans;
  }

  // Driver code
  public static void main(String[] args)
  {
    String s = "aeiou";
    int K = 2;
    System.out.print(get(s, K));
  }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# python code to implement above approach
MAX = 128

# Function to check whether
# a character is vowel or not
def isVowel(x):

    return (x == 'a' or x == 'e' or
            x == 'i' or x == 'o' or x == 'u'
            or x == 'A' or x == 'E' or
            x == 'I' or x == 'O' or x == 'U')

# Function to find the count of
# substring with k vowels
def get(str, k):

    n = len(str)

    # Stores the count of
    # substring with K vowels
    ans = 0

    # Consider all substrings
    # beginning with str[i]
    for i in range(0, n):
        count = 0

        # Consider all substrings
        # between [i, j]
        for j in range(i, n):

            # If this is a vowel, for this
            # substring, increment count.
            if (isVowel(str[j])):
                count += 1

            # If vowel count becomes k,
            # then increment final count.
            if (count == k):
                ans += 1

            if (count > k):
                break

    return ans

# Driver code
if __name__ == "__main__":

    s = "aeiou"
    K = 2
    print(get(s, K))

# This code is contributed by rakeshsahni
```

## C#

```
// C# code to implement above approach
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

  // Function to find the count of
  // substring with k vowels
  static int get(string str, int k)
  {

    int n = str.Length;

    // Stores the count of
    // substring with K vowels
    int ans = 0;

    // Consider all substrings
    // beginning with str[i]
    for (int i = 0; i < n; i++) {
      int count = 0;

      // Consider all substrings
      // between [i, j]
      for (int j = i; j < n; j++) {

        // If this is a vowel, for this
        // substring, increment count.
        if (isVowel(str[j])) {
          count++;
        }

        // If vowel count becomes k,
        // then increment final count.
        if (count == k) {
          ans++;
        }

        if (count > k)
          break;
      }
    }
    return ans;
  }

  // Driver code
  public static void Main()
  {
    string s = "aeiou";
    int K = 2;
    Console.WriteLine(get(s, K));
  }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
   // JavaScript code for the above approach

   let MAX = 128

   // Function to check whether
   // a character is vowel or not
   function isVowel(x) {
     return (x == 'a' || x == 'e' ||
       x == 'i' || x == 'o' || x == 'u'
       || x == 'A' || x == 'E' ||
       x == 'I' || x == 'O' || x == 'U');
   }

   // Function to find the count of
   // substring with k vowels
   function get(str, k) {

     let n = str.length;

     // Stores the count of
     // substring with K vowels
     let ans = 0;

     // Consider all substrings 
     // beginning with str[i]
     for (let i = 0; i < n; i++) {
       let count = 0;

       // Consider all substrings 
       // between [i, j]
       for (let j = i; j < n; j++) {

         // If this is a vowel, for this
         // substring, increment count.
         if (isVowel(str[j])) {
           count++;
         }

         // If vowel count becomes k,
         // then increment final count.
         if (count == k) {
           ans++;
         }

         if (count > k)
           break;
       }
     }
     return ans;
   }

   // Driver code
   let s = "aeiou";
   let K = 2;
   document.write(get(s, K));

 // This code is contributed by Potta Lokesh
 </script>
```

**Output**

```
4
```

***时间复杂度:*** O(N <sup>2</sup> )其中 N 为弦的长度。
***辅助空间:*** O(1)