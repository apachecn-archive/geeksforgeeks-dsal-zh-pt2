# 用单个子序列的每个索引部分最大化 3 长度回文子序列的计数

> 原文:[https://www . geeksforgeeks . org/最大化长度为 3 的回文子序列的计数，每个子序列都是单个子序列的一部分/](https://www.geeksforgeeks.org/maximize-count-of-3-length-palindromic-subsequences-with-each-index-part-of-a-single-subsequence/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/)、 **S** ，任务是从给定的字符串中找到最大数量的长度为 3 的不同索引[回文子序列](https://www.geeksforgeeks.org/count-palindromic-subsequence-given-string/)。

**示例:**

> **输入** : str = "geekforg"
> **输出** : 2
> **说明:**满足条件的长度为 3 的可能回文子序列为“gkg”和“efe”。因此，所需的输出为 2。
> 
> **输入:** str = "geek"
> **输出:** 1
> **解释:**满足条件的长度为 3 的可能回文子序列为“ege”。

**方法:**思路是统计[串](https://www.geeksforgeeks.org/string-data-structure/) **S** 每个字符的[频率，统计频率对，使对具有相同的字符，通过将](https://www.geeksforgeeks.org/python-frequency-of-each-character-in-string/)[串](https://www.geeksforgeeks.org/string-data-structure/) **S** 除以 **3** 来统计长度为 **3** 的子序列数。最后，打印频率对的最小值作为子序列的数量。按照以下步骤解决问题:

*   初始化一个数组，比如说 **freq[]** ，来存储[串](https://www.geeksforgeeks.org/string-data-structure/)和 **S** 每个字符的频率。
*   初始化一个变量，比如**频率对**，来存储具有相同字符对的频率对。
*   初始化一个变量，比如 **len** ，来存储[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 的长度为 **3** 的子序列的数量。
*   迭代范围 **[0，str . length()–1]**。对于字符串**S**的每个 **i <sup>th</sup>** 索引，将字符**freq【S[I]–‘a’】**的计数增加 **1** 。
*   迭代范围**【0，26】**。对于数组的每一个**I<sup>th</sup>T5【索引】 **freq[]，**通过将数组元素除以 **2** 来计算频率对。**
*   最后，打印**频率对**和**透镜**的最小值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the maximum number
// oaf palindrome subsequences of length 3
// considering the same index only once
int maxNumPalindrome(string S)
{

    // Index of the string S
    int i = 0;

    // Stores the frequency of
    // every character
    int freq[26] = { 0 };

    // Stores the pair of frequency
    // containing same characters
    int freqPair = 0;

    // Number of subsequences
    // having length 3
    int len = S.length() / 3;

    // Counts the frequency
    while (i < S.length()) {

        freq[S[i] - 'a']++;
        i++;
    }

    // Counts the pair of frequency
    for (i = 0; i < 26; i++) {

        freqPair += (freq[i] / 2);
    }

    // Returns the minimum value
    return min(freqPair, len);
}

// Driver Code
int main()
{

    string S = "geeksforg";

    cout << maxNumPalindrome(S) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

import java.util.*;

class GFG {

    // Driver Code
    public static void main(String[] args)
    {

        String S = "geeksforg";

        System.out.println(maxNumPalindrome(S));
    }

    // Function to count the maximum number
    // of palindrome subsequences of length 3
    // considering the same index only once
    static int maxNumPalindrome(String S)
    {

        // Index of the string S
        int i = 0;

        // Stores the frequency of
        // every character
        int[] freq = new int[26];

        // Stores the pair of frequency
        // containing same characters
        int freqPair = 0;

        // Number of subsequences
        // having length 3
        int len = S.length() / 3;

        // Counts the frequency
        while (i < S.length()) {

            freq[S.charAt(i) - 'a']++;
            i++;
        }

        // Counts the pair of frequency
        for (i = 0; i < 26; i++) {

            freqPair += (freq[i] / 2);
        }

        // Returns the minimum value
        return Math.min(freqPair, len);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count the maximum number
# of palindrome subsequences of length 3
# considering the same index only once
def maxNumPalindrome(S):

    # Index of the S
    i = 0

    # Stores the frequency of
    # every character
    freq = [0] * 26

    # Stores the pair of frequency
    # containing same characters
    freqPair = 0

    # Number of subsequences
    # having length 3
    ln = len(S) // 3

    # Counts the frequency
    while (i < len(S)):
        freq[ord(S[i]) - ord('a')] += 1
        i += 1

    # Counts the pair of frequency
    for i in range(26):
        freqPair += (freq[i] // 2)

    # Returns the minimum value
    return min(freqPair, ln)

# Driver Code
if __name__ == '__main__':

    S = "geeksforg"

    print(maxNumPalindrome(S))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach 
using System;
class GFG
{

    // Driver Code
    public static void Main(String[] args)
    {
        string S = "geeksforg";
        Console.WriteLine(maxNumPalindrome(S));
    }

    // Function to count the maximum number
    // of palindrome subsequences of length 3
    // considering the same index only once
    static int maxNumPalindrome(string S)
    {

        // Index of the string S
        int i = 0;

        // Stores the frequency of
        // every character
        int[] freq = new int[26];

        // Stores the pair of frequency
        // containing same characters
        int freqPair = 0;

        // Number of subsequences
        // having length 3
        int len = S.Length / 3;

        // Counts the frequency
        while (i < S.Length)
        {
            freq[S[i] - 'a']++;
            i++;
        }

        // Counts the pair of frequency
        for (i = 0; i < 26; i++)
        {
            freqPair += (freq[i] / 2);
        }

        // Returns the minimum value
        return Math.Min(freqPair, len);
    }
}

// This code is contributed by susmitakundugoaldanga.
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to count the maximum number
// oaf palindrome subsequences of length 3
// considering the same index only once
function maxNumPalindrome(S)
{

    // Index of the string S
    let i = 0;

    // Stores the frequency of
    // every character
    let freq = new Array(26).fill(0);

    // Stores the pair of frequency
    // containing same characters
    let freqPair = 0;

    // Number of subsequences
    // having length 3
    let len = (S.length / 3);

    // Counts the frequency
    while (i < S.length)
    {
        freq[S[i].charCodeAt(0) -
              'a'.charCodeAt(0)]++;
        i++;
    }

    // Counts the pair of frequency
    for(i = 0; i < 26; i++)
    {
        freqPair += Math.floor(freq[i] / 2);
    }

    // Returns the minimum value
    return Math.min(freqPair, len);
}

// Driver Code
let S = "geeksforg";

document.write(maxNumPalindrome(S) + "<br>");

// This code is contributed by gfgking

</script>
```

**Output:** 

```
2
```

***时间复杂度:****O(| S |+26)*
***辅助空间:*** *O(26)*