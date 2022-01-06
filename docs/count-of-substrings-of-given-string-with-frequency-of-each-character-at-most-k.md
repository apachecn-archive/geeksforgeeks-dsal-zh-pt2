# 给定字符串的子串计数，每个字符的频率最多为 K

> 原文:[https://www . geeksforgeeks . org/给定字符串的子字符串计数，每个字符最多出现 k 次/](https://www.geeksforgeeks.org/count-of-substrings-of-given-string-with-frequency-of-each-character-at-most-k/)

给定一个[串](https://www.geeksforgeeks.org/string-data-structure/) **串**，任务是计算给定串的[子串](https://www.geeksforgeeks.org/substring-in-cpp/)的数量，使得串的每个元素的频率几乎为 **K** 。

**示例:**

> **输入:** str = "abab "，K = 1
> **输出:** 7
> **解释:**每个字符的频率为 atmost 1 的子串是“a”、“b”、“a”、“b”、“ab”、“ba”和“ab”。
> 
> **输入:**str[]=“xxyyzxx”，K = 2
> T3】输出: 33

**方法:**给定的问题可以使用[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)来解决。遍历范围[0，N]中字符串的每个字符，并在一个[无序映射](http://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)中保持[每个字符的频率。创建变量 **ptr** ，存储当前窗口起点的索引。最初，ptr 的值为 **0** 。对于索引 **i** ，如果 **str[i]** 的频率小于或等于 **K** ，则将**(I–ptr+1)**加入到子串计数中，否则，递增 ptr 的值直到 **str[i] > K** 。](https://www.geeksforgeeks.org/frequency-of-each-character-in-a-string-using-unordered_map-in-c/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the count of
// substrings such that frequency
// of each character is atmost K
int cntSubstr(string str, int K)
{
    // Stores the size of string
    int N = str.size();

    // Stores the final count
    int ans = 0;

    // Stores the starting index
    int ptr = 0;

    // Stores the frequency of
    // characters of string
    unordered_map<char, int> m;

    // Loop to iterate through string
    for (int i = 0; i < N; i++) {

        // Increment the frequency of
        // the current character
        m[str[i]]++;

        // While the frequency of char is
        // greater than K, increment ptr
        while (m[str[i]] > K && ptr <= i) {
            m[str[ptr]]--;
            ptr++;
        }

        // Update count
        ans += (i - ptr + 1);
    }

    // Return Answer
    return ans;
}

// Driver Code
int main()
{
    string str = "abab";
    int K = 1;

    cout << cntSubstr(str, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the count of
// substrings such that frequency
// of each character is atmost K
static int cntSubstr(String str, int K)
{

    // Stores the size of string
    int N = str.length();

    // Stores the final count
    int ans = 0;

    // Stores the starting index
    int ptr = 0;

    // Stores the frequency of
    // characters of string
    HashMap<Character,
            Integer> m = new HashMap<Character,
                                     Integer>();

    // Loop to iterate through string
    for(int i = 0; i < N; i++)
    {

        // Increment the frequency of
        // the current character
        int count = 0;
        if (m.containsKey(str.charAt(i)))
        {
            count = m.get(str.charAt(i));
        }
        m.put(str.charAt(i), count + 1);

        // While the frequency of char is
        // greater than K, increment ptr
        while (m.get(str.charAt(i)) > K && ptr <= i)
        {
            m.put(str.charAt(ptr),
                  m.get(str.charAt(ptr)) - 1);
            ptr++;
        }

        // Update count
        ans += (i - ptr + 1);
    }

    // Return Answer
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    String str = "abab";
    int K = 1;

    System.out.println(cntSubstr(str, K));
}
}

// This code is contributed by ukasp
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to find the count of
# substrings such that frequency
# of each character is atmost K
def cntSubstr(str, K):

    # Stores the size of string
    N = len(str)

    # Stores the final count
    ans = 0

    # Stores the starting index
    ptr = 0

    # Stores the frequency of
    # characters of string
    m = {}

    # Loop to iterate through string
    for i in range(N) :

        # Increment the frequency of
        # the current character
        if (str[i] in m):
            m[str[i]] += 1
        else:
            m[str[i]] = 1

        # While the frequency of char is
        # greater than K, increment ptr
        while (m[str[i]] > K and ptr <= i):
            m[str[ptr]] -= 1
            ptr += 1

        # Update count
        ans += (i - ptr + 1)

    # Return Answer
    return ans

# Driver Code
str = "abab"
K = 1
print(cntSubstr(str, K))

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{

// Function to find the count of
// substrings such that frequency
// of each character is atmost K
static int cntSubstr(string str, int K)
{

    // Stores the size of string
    int N = str.Length;

    // Stores the final count
    int ans = 0;

    // Stores the starting index
    int ptr = 0;

    // Stores the frequency of
    // characters of string
    Dictionary<char, int> m =
          new Dictionary<char, int>();

    // Loop to iterate through string
    for (int i = 0; i < N; i++) {

        // Increment the frequency of
        // the current character
        int count = 0;
        if (m.ContainsKey(str[i])) {

            count = m[str[i]];
        }
        m[str[i]] = count + 1;

        // While the frequency of char is
        // greater than K, increment ptr
        while (m[str[i]] > K && ptr <= i) {
            m[str[ptr]]--;
            ptr++;
        }

        // Update count
        ans += (i - ptr + 1);
    }

    // Return Answer
    return ans;
}

// Driver Code
public static void Main()
{
    string str = "abab";
    int K = 1;

    Console.Write(cntSubstr(str, K));

}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>

       // JavaScript Program to implement
       // the above approach

       // Function to find the count of
       // substrings such that frequency
       // of each character is atmost K
       function cntSubstr(str, K) {
           // Stores the size of string
           let N = str.length;

           // Stores the final count
           let ans = 0;

           // Stores the starting index
           let ptr = 0;

           // Stores the frequency of
           // characters of string
           let m = new Map();

           // Loop to iterate through string
           for (let i = 0; i < N; i++) {

               // Increment the frequency of
               // the current character
               if (m.has(str.charAt(i)))
                   m.set(str[i], m.get(str[i]) + 1);
               else
                   m.set(str[i], 1);

               // While the frequency of char is
               // greater than K, increment ptr
               while (m.get(str[i]) > K && ptr <= i) {
                   m.set(str[ptr], m.get(str[ptr]) - 1);
                   ptr++;
               }

               // Update count
               ans += (i - ptr + 1);
           }

           // Return Answer
           return ans;
       }

       // Driver Code
       let str = "abab";
       let K = 1;

       document.write(cntSubstr(str, K));

   // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
7
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)