# 通过为每个字符分配范围[1，26]内的值来最大化字符串值

> 原文:[https://www . geesforgeks . org/通过为每个字符分配 1-26 范围内的值来最大化字符串值/](https://www.geeksforgeeks.org/maximize-the-string-value-by-assigning-values-in-range-1-26-to-each-character/)

给定一个大小为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是找到分配给字符串 **S** 所有字母的最大值和。分配给所有字符的值都超出了范围**【1，26】**，分配给相同小写和大写字符的值是相同的。

**示例:**

> **输入:**S = " pQrqQPR "
> T3】输出: 176
> **说明:**
> 字母‘P’的值取 25，‘Q’取 26，‘R’取 24。现在，分配给字符串字符的值的总和是 25 + 26 + 24 + 26 + 26 + 25 + 24 = 176，这是所有可能的赋值组合中的最大值。
> 
> **输入:**S =“# AaaA { content }”x201；
> T3【输出: 104

**方法:**给定的问题可以通过[将字母](https://www.geeksforgeeks.org/print-the-frequency-of-each-character-in-alphabetical-order/)的频率存储在[频率数组](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)中[并按降序](https://www.geeksforgeeks.org/sort-in-python/)排序来解决。思路是最高频率乘以 **26** ，2 <sup>nd</sup> 最高频率乘以 **25** 以此类推。按照以下步骤解决给定的问题:

*   初始化一个辅助数组，比如说**频率[]** ，存储字符串 **S** 中不同字符[频率](https://www.geeksforgeeks.org/count-distinct-elements-from-a-range-of-a-sorted-sequence-from-a-given-frequency-array/)。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-the-characters-of-a-string-in-java/)，在每次迭代中，如果字符 **ch** ，则使用以下情况增加频率:
    *   **大写:**以**频率【ch–‘A’】**递增数值。
    *   **小写:**在**频率【ch –' a '】**下增加数值。
    *   **特殊字符:** [继续循环](https://www.geeksforgeeks.org/continue-statement-cpp/)。
*   [按递增顺序排列阵列](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/) **频率[]** 。
*   初始化一个变量，说**将**求和为 **0** 来存储字符串的值。
*   [使用变量 **i** 从索引 **25** 到 **0** 以相反的顺序遍历数组](https://www.geeksforgeeks.org/iterate-list-in-reverse-order-in-java/)，并在每次迭代时执行以下步骤:
    *   如果**频率【I】**的值为 **0** ，则[断开回路](https://www.geeksforgeeks.org/break-statement-cc/)。
    *   否则，将**频率【I】**的值与 **i** 相乘，并将其添加到变量**和**中。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find max possible sum
// of values assigned to each characters
// of the given string
int maxStrength(string s)
{
    // Initialize a frequency array of
    // size 26 with all elements as 0
    vector<int> frequency(26, 0);

    for (char ch : s) {

        // Lowercase character
        if (ch >= 'a' && ch <= 'z') {
            frequency[ch - 'a']++;
        }

        // Uppercase character
        else if (ch >= 'A' && ch <= 'Z') {
            frequency[ch - 'A']++;
        }
    }

    // Sort the frequency array
    sort(frequency.begin(),
         frequency.end());

    // Stores the maximum sum of value
    int ans = 0;

    for (int i = 25; i >= 0; i--) {

        // If the frequency of the
        // current character is > 0
        if (frequency[i] > 0) {
            ans = ans + frequency[i] * (i + 1);
        }

        // Otherwise
        else
            break;
    }

    // Return the maximum sum obtained
    return ans;
}

// Driver Code
int main()
{
    string S = "pQrqQPR";
    cout << maxStrength(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach

import java.util.*;

public class GFG {

    // Function to find max possible sum
    // of values assigned to each characters
    // of the given string
    static int maxStrength(String s)
    {
        // Initialize a frequency array of
        // size 26 with all elements as 0
        int []frequency = new int[26];
        int len = s.length();

        for (int i = 0; i < len; i++){

            char ch = s.charAt(i);

            // Lowercase character
            if (ch >= 'a' && ch <= 'z') {
                frequency[ch - 'a']++;
            }

            // Uppercase character
            else if (ch >= 'A' && ch <= 'Z') {
                frequency[ch - 'A']++;
            }
        }

        // Sort the frequency array
        Arrays.sort(frequency);

        // Stores the maximum sum of value
        int ans = 0;

        for (int i = 25; i >= 0; i--) {

            // If the frequency of the
            // current character is > 0
            if (frequency[i] > 0) {
                ans = ans + frequency[i] * (i + 1);
            }

            // Otherwise
            else
                break;
        }

        // Return the maximum sum obtained
        return ans;
    }

    // Driver Code
    public static void main (String[] args) {
        String S = "pQrqQPR";
        System.out.println(maxStrength(S));
    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
#  python program for the above approach

# Function to find max possible sum
#  of values assigned to each characters
#  of the given string
def maxStrength(s):

    # Initialize a frequency array of
    # size 26 with all elements as 0
    frequency = [0 for x in range(26)]
    for ch in s:

        # Lowercase character
        if (ch >= 'a' and ch <= 'z'):
            frequency[ord(ch)-97] += 1

        # Uppercase character
        elif (ch >= 'A' and ch <= 'Z'):
            frequency[ord(ch)-65] += 1

    # Sort the frequency array
    frequency.sort()

    # Stores the maximum sum of value
    ans = 0
    for i in range(25, 0, -1):

        # If the frequency of the
        # current character is > 0
        if (frequency[i] > 0):
            ans = ans + frequency[i] * (i + 1)

        # Otherwise
        else:
            break

    # Return the maximum sum obtained
    return ans

# Driver Code
S = "pQrqQPR"
print(maxStrength(S))

# This code is contributed by amrshkumar3.
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

    // Function to find max possible sum
    // of values assigned to each characters
    // of the given string
    static int maxStrength(string s)
    {

        // Initialize a frequency array of
        // size 26 with all elements as 0
        int []frequency = new int[26];
        int len = s.Length;

        for (int i = 0; i < len; i++){

            char ch = s[i];

            // Lowercase character
            if (ch >= 'a' && ch <= 'z') {
                frequency[ch - 'a']++;
            }

            // Uppercase character
            else if (ch >= 'A' && ch <= 'Z') {
                frequency[ch - 'A']++;
            }
        }

        // Sort the frequency array
        Array.Sort(frequency);

        // Stores the maximum sum of value
        int ans = 0;

        for (int i = 25; i >= 0; i--) {

            // If the frequency of the
            // current character is > 0
            if (frequency[i] > 0) {
                ans = ans + frequency[i] * (i + 1);
            }

            // Otherwise
            else
                break;
        }

        // Return the maximum sum obtained
        return ans;
    }

// Driver Code
public static void Main(String[] args)
{
    string S = "pQrqQPR";
    Console.Write(maxStrength(S));
}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>
      // JavaScript Program to implement
      // the above approach

      // Function to find max possible sum
      // of values assigned to each characters
      // of the given string
      function maxStrength(s)
      {

          // Initialize a frequency array of
          // size 26 with all elements as 0
          let frequency = new Array(26).fill(0);

          for (let ch of s) {

              // Lowercase character
              if (ch.charCodeAt(0) >= 'a'.charCodeAt(0) && ch.charCodeAt(0) <= 'z'.charCodeAt(0)) {
                  frequency[ch.charCodeAt(0) - 'a'.charCodeAt(0)]++;
              }

              // Uppercase character
              else if (ch.charCodeAt(0) >= 'A'.charCodeAt(0) && ch.charCodeAt(0) <= 'Z'.charCodeAt(0)) {
                  frequency[ch.charCodeAt(0) - 'A'.charCodeAt(0)]++;
              }
          }

          // Sort the frequency array
          frequency.sort(function (a, b) { return a - b })

          // Stores the maximum sum of value
          let ans = 0;

          for (let i = 25; i >= 0; i--) {

              // If the frequency of the
              // current character is > 0
              if (frequency[i] > 0) {
                  ans = ans + frequency[i] * (i + 1);
              }

              // Otherwise
              else
                  break;
          }

          // Return the maximum sum obtained
          return ans;
      }

      // Driver Code
      let S = "pQrqQPR";
      document.write(maxStrength(S));

  // This code is contributed by Potta Lokesh
  </script>
```

**Output:** 

```
176
```

***时间复杂度:** O(N* log N)*
***辅助空间:** O(26)*