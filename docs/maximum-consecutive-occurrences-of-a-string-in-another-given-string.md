# 一个字符串在另一个给定字符串中的最大连续出现次数

> 原文:[https://www . geeksforgeeks . org/给定字符串中一个字符串的最大连续出现次数/](https://www.geeksforgeeks.org/maximum-consecutive-occurrences-of-a-string-in-another-given-string/)

给定两个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **str1** 和 **str2** ，任务是计算字符串 **str2** 在字符串 **str1** 中的最大连续出现次数。

**示例:**

> **输入:**str 1 =“abababcba”，str2 =“ba”
> **输出** : 2
> **说明:**字符串 str 2 在子字符串{ str[1]，…，str[4] }中连续出现。因此，获得的最大计数是 2
> 
> **输入:**str1 =“ababc”，str2 =“AC”
> **输出:** 0
> **说明:**
> 由于 str 2 在 str 1 中不是作为子串出现的，所以需要的输出为 0。

**方法:**按照以下步骤解决问题:

*   初始化一个变量，比如 **cntOcc** ，来存储字符串 **str1** 中 **str2** 的[出现次数。](https://www.geeksforgeeks.org/python-string-count/.)
*   迭代范围**【CntOcc，1】**。对于迭代中的每个 i <sup>第</sup>个值，[将字符串**str 2**](https://www.geeksforgeeks.org/c-program-concatenate-string-given-number-times/)I**次连接，并检查连接的字符串是否是字符串 **str1** 的子字符串。第一个 **i** <sup>第一个</sup>值被发现为真，将其打印为所需答案。**

下面是实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
#include <string.h>
using namespace std;

int countFreq(string& pat, string& txt)
{
    int M = pat.length();
    int N = txt.length();
    int res = 0;

    // A loop to slide pat[] one by one
    for(int i = 0; i <= N - M; i++)
    {

        // For current index i, check
        // for pattern match
        int j;
        for(j = 0; j < M; j++)
            if (txt[i + j] != pat[j])
                break;

        // If pat[0...M-1] = txt[i, i+1, ...i+M-1]
        if (j == M)
        {
            res++;
            j = 0;
        }
    }
    return res;
}

// Function to count the maximum
// consecutive occurrence of the
// string str2 in in the string str1
int maxRepeating(string str1, string str2)
{

    // Stores the count of consecutive
    // occurrences of str2 in str1
    int cntOcc = countFreq(str2, str1);

    // Concatenate str2 cntOcc times
    string Contstr = "";

    for(int i = 0; i < cntOcc; i++)
        Contstr += str2;

    // Iterate over the string str1
    // while Contstr is not present in str1
    size_t found = str1.find(Contstr);

    while (found == string::npos)
    {
        found = str1.find(Contstr);

        // Update cntOcc
        cntOcc -= 1;

        // Update Contstr
        Contstr = "";

        for(int i = 0; i < cntOcc; i++)
            Contstr += str2;
    }
    return cntOcc;
}

// Driver Code
int main()
{
    string str1 = "abababc";
    string str2 = "ba";

    cout << maxRepeating(str1, str2);

    return 0;
}

// This code is contributed by grand_master
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

import java.util.*;
class GFG
{
static int countFreq(String pat, String txt)
{
    int M = pat.length();
    int N = txt.length();
    int res = 0;

    // A loop to slide pat[] one by one
    for(int i = 0; i <= N - M; i++)
    {

        // For current index i, check
        // for pattern match
        int j;
        for(j = 0; j < M; j++)
            if (txt.charAt(i + j) != pat.charAt(j))
                break;

        // If pat[0...M-1] = txt[i, i+1, ...i+M-1]
        if (j == M)
        {
            res++;
            j = 0;
        }
    }
    return res;
}

// Function to count the maximum
// consecutive occurrence of the
// String str2 in in the String str1
static int maxRepeating(String str1, String str2)
{

    // Stores the count of consecutive
    // occurrences of str2 in str1
    int cntOcc = countFreq(str2, str1);

    // Concatenate str2 cntOcc times
    String Contstr = "";

    for(int i = 0; i < cntOcc; i++)
        Contstr += str2;

    // Iterate over the String str1
    // while Contstr is not present in str1
    boolean found = str1.contains(Contstr);

    while (!found)
    {
        found = str1.contains(Contstr);

        // Update cntOcc
        cntOcc -= 1;

        // Update Contstr
        Contstr = "";

        for(int i = 0; i < cntOcc; i++)
            Contstr += str2;
    }
    return cntOcc;
}

// Driver Code
public static void main(String[] args)
{
    String str1 = "abababc";
    String str2 = "ba"; 
    System.out.print(maxRepeating(str1, str2));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count the maximum
# consecutive occurrence of the
# string str2 in in the string str1
def maxRepeating(str1, str2):

    # Stores the count of consecutive
    # occurrences of str2 in str1
    cntOcc = str1.count(str2)

    # Concatenate str2 cntOcc times
    Contstr = str2 * cntOcc

    # Iterate over the string str1
    # while Contstr is not present in str1
    while(Contstr not in str1):

        # Update cntOcc
        cntOcc -= 1

       # Update Contstr
        Contstr = str2 * cntOcc

    return cntOcc

# Driver Code
if __name__ =="__main__":
  str1 = "abababc"
  str2 = "ba"
  print(maxRepeating(str1, str2))

```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG
{
static int countFreq(String pat, String txt)
{
    int M = pat.Length;
    int N = txt.Length;
    int res = 0;

    // A loop to slide pat[] one by one
    for(int i = 0; i <= N - M; i++)
    {

        // For current index i, check
        // for pattern match
        int j;
        for(j = 0; j < M; j++)
            if (txt[i + j] != pat[j])
                break;

        // If pat[0...M-1] = txt[i, i+1, ...i+M-1]
        if (j == M)
        {
            res++;
            j = 0;
        }
    }
    return res;
}

// Function to count the maximum
// consecutive occurrence of the
// String str2 in in the String str1
static int maxRepeating(String str1, String str2)
{

    // Stores the count of consecutive
    // occurrences of str2 in str1
    int cntOcc = countFreq(str2, str1);

    // Concatenate str2 cntOcc times
    String Contstr = "";

    for(int i = 0; i < cntOcc; i++)
        Contstr += str2;

    // Iterate over the String str1
    // while Contstr is not present in str1
    bool found = str1.Contains(Contstr);   
    while (!found)
    {
        found = str1.Contains(Contstr);

        // Update cntOcc
        cntOcc -= 1;

        // Update Contstr
        Contstr = "";

        for(int i = 0; i < cntOcc; i++)
            Contstr += str2;
    }
    return cntOcc;
}

// Driver Code
public static void Main(String[] args)
{
    String str1 = "abababc";
    String str2 = "ba"; 
    Console.Write(maxRepeating(str1, str2));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
      // JavaScript program to implement
      // the above approach
      function countFreq(pat, txt) {
        var M = pat.length;
        var N = txt.length;
        var res = 0;

        // A loop to slide pat[] one by one
        for (var i = 0; i <= N - M; i++) {
          // For current index i, check
          // for pattern match
          var j;
          for (j = 0; j < M; j++)
              if (txt[i + j] !== pat[j])
                break;

          // If pat[0...M-1] = txt[i, i+1, ...i+M-1]
          if (j === M) {
            res++;
            j = 0;
          }
        }
        return res;
      }

      // Function to count the maximum
      // consecutive occurrence of the
      // String str2 in in the String str1
      function maxRepeating(str1, str2) {
        // Stores the count of consecutive
        // occurrences of str2 in str1
        var cntOcc = countFreq(str2, str1);

        // Concatenate str2 cntOcc times
        var Contstr = "";

        for (var i = 0; i < cntOcc; i++)
            Contstr += str2;

        // Iterate over the String str1
        // while Contstr is not present in str1
        var found = str1.includes(Contstr);
        while (!found) {
          found = str1.includes(Contstr);

          // Update cntOcc
          cntOcc -= 1;

          // Update Contstr
          Contstr = "";

          for (var i = 0; i < cntOcc; i++)
              Contstr += str2;
        }
        return cntOcc;
      }

      // Driver Code
      var str1 = "abababc";
      var str2 = "ba";
      document.write(maxRepeating(str1, str2));
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*